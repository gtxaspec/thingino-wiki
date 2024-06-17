### Hardware

Porting thingino to a new camera is relatively easy.

In our repo, we have what we call **modules**, starter firmware files designed to support a certain set of core elements: SoC, image sensor, and either a wireless module or Ethernet for networking. Such a file is not a complete **camera firmware**, but it would allow you to start your project and boot into thingino linux for further investigation.

Open your camera and find out what kind of hardware you have. 

THE NEXT STEP IS VERY IMPORTANT!

Make a backup of your existing firmware. Verify the backup by taking at least two consecutive reads and comparing their checksums. They should match.

Download or compile a firmware binary for your hardware set.

Install the firmware on the camera using one of the available techniques. Reboot the camera. If all went well, you should see a boot log and the following message: "Welcome to the Thingino firmware!

### GPIO Map

Look in the boot log of the stock Linux for hints about GPIO pins.

Unpack the stock firmware dump file using `binwalk`. Analyze its contents for clues about GPIO pin settings. You may need to use [Ghidra](https://github.com/NationalSecurityAgency/ghidra/) to read hardcoded values from appropriate drivers and applications.

Alternatively, you may need to gain access to the stock Linux firmware to read the GPIO from a live system.

Locate the password hash in the extracted files. Check the Internet to see if the hash has already been bruteforced to reveal the plaintext password.
If not, try repacking the firmware to replace the unknown password hash with a known one or with a passwordless access.

Using the stock Linux firmware, run the following command to dump the GPIO map:
```
mount -t debugfs none /sys/kernel/debug; cat /sys/kernel/debug/gpio
```

The stock firmware console is usually cluttered with debug messages from various processes, so be quick to copy the response before it disappears from the screen.

### U-Boot Environment

Using the information from the stock Linux, create a boot loader environment to provision your camera on boot.

First, you need to convert the GPIO map of the stock Linux to the value for the gpio_default parameter. For example, this map

```
GPIOs 0-31, GPIO A:
 gpio-6   (irled)              ) out hi
 gpio-18  (sensor_reset        ) out hi

GPIOs 32-63, GPIO B:
 gpio-49  (ircut               ) out lo
 gpio-50  (ircut               ) out lo
 gpio-58  (mmc_detect          ) in  lo
 gpio-60  (850nm               ) out hi

GPIOs 64-95, GPIO C:
```

is changed to

```
gpio_default=6O 18O 49o 50o 58i 60O
```

where the letters following the pin numbers define the pin's direction and state:

- uppercase `O` means _output, high_
- lowercase `o` means _output, low_
- `i` means _input (both high and low)_

After that, you need to define individual pins and create a configuration file as described on the [Camera Configuration](Camera-configuration) page.