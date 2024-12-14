Thingino currently supports devices using Ingenic XBurst1-based System-on-Chips (SoCs). For a detailed list of supported chip models, please refer to the [Supported Hardware wiki article](https://github.com/themactep/thingino-firmware/wiki/Tech-Info-%E2%80%90-Supported-Hardware).

Even if your specific device is not listed, there is a high likelihood that Thingino can support it. This is because Thingino is designed to be highly adaptable. While a specific configuration profile for your device might not exist, the firmware can still be tailored to meet the requirements of your hardware. 

The reason your device may not be listed as supported is probably that we don't yet have the hardware on hand to test. If you have a device in mind that you would like to make work with Thingino but do not have the skills to do it yourself, please consider donating a copy of such a device to the project.

### Porting

Porting Thingino to a new camera is relatively easy.

In our repo, we have what we call **modules**, starter firmware files designed to support a certain set of core elements: SoC, image sensor, and either a wireless module or Ethernet for networking. Such a file is not a complete **camera firmware**, but it would allow you to start your project and boot into thingino linux for further investigation.

Open your camera and find out what kind of hardware you have. Take photos of all the boards from both sides, take close-up photos of all the components, pads, and connectors, along with their labels. Color code the connectors with markers to avoid mixing them up when reassembling the camera back.

ALL STEPS ARE VERY IMPORTANT!

### Firmware Backup

First things first. Make a backup of your existing firmware. Desolder the flash chip and read in a programmer, read it in-place using a programming clip, dump it with a patched [Ingenic USB Cloner](https://thingino.com/cloner/), copy it to an SD card from within U-Boot shell, or at least dump it via serial connection.

Verify the backup by doing at least two consecutive reads and comparing their checksums. They should match.

> [!IMPORTANT]  
> Analyzing the stock firmware is essential for effective device support. Without access to the stock firmware, identifying GPIOs can become a time-consuming task that requires the use of a multimeter, along with significant patience and effort.

### Boot Log Analysis

Connect to the UART port on your camera and read the boot log of the stock firmware. Save it to disk. Or better yet, set your terminal to automatically save full logs of your sessions. Check the boot log of stock Linux for notes on GPIO pins. 

### Stock Firmware Analysis

Unpack the stock firmware dump file using [binwalk](https://themactep.com/notes/how-to-install-binwalk-with-jffs-ubi-and-cramfs-support). Analyze its contents for clues about GPIO pin settings. You may need to use [Ghidra](https://github.com/NationalSecurityAgency/ghidra/) to read hardcoded values from appropriate drivers and applications.

Locate the password hash in the extracted files. Check the Internet to see if the hash has already been bruteforced to reveal the plaintext password.

Alternatively, you may need to gain access to the stock Linux firmware to read the GPIO from a live system.

### Stock Firmware Hijacking

Try to patch the stock firmware dump with our [Hijacker](https://github.com/themactep/thingino-firmware/blob/master/scripts/hijacker.sh) script to replace the unknown password hash with a known one or with a passwordless access, flash it on the camera and gain access to the system.

Once inside, run the following command and save the result.
```
mount -t debugfs none /sys/kernel/debug; cat /sys/kernel/debug/gpio
```
This is your GPIO map. You will need it.

> [!NOTE]  
> You may encounter a device where debugfs is disabled. As a result, viewing the GPIO map using `/sys/kernel/debug/gpio` won't be possible. In such cases, you'll need to identify GPIOs using alternative methods, such as decompiling and analyzing driver modules.

### New Firmware

[Download](https://github.com/themactep/thingino-firmware/releases/) or compile a firmware binary for your hardware set.

Install the firmware on the camera using one of the available techniques. Reboot the camera. If all went well, you should see a boot log and the following message: "Welcome to the Thingino firmware!

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

Finding GPIO
-------------

Sometimes it is impossible to gather information from the stock firmware, and we have to search for GPIO pins on an unknown hardware from withing a running barebone Thingino module image. In this case brute-force scanning is the easiest way to determine many of the pins. This simple one-liner will scan a sequence of pins from 1 to 10, print the pin number, then set the pin to High, and one second later to Low.

```
for x in $(seq 1 10); do echo $x; gpio set $x 1; sleep 1; gpio set $x 0; done
```

Using this script you can find IR cut filter, IR LEDs, indicator LEDs, maybe even speaker and Wi-Fi power pins.

> [!CAUTION]  
> Note that the IR cut filter is usually controlled by a pair of pins. Setting one high while leaving the other low will energize the solenoid that controls the filter movement and it will burn out if left energized for more than a few seconds.

IR LEDs are usually have faint violet glow and almost invisible to a naked human eye. You can utilize a smartphone camera to see the LED lit.
You can even use the IP camera itself pointing it to a reflective surface and monitoring the feed on the preview page in a web browser, or playing an rtsp stream in a video player.

**IR LEDs in a reflection with the IR cut filter engaged**  
![color-onircut-onirled-on](https://github.com/user-attachments/assets/8b1b6213-6a12-413b-8e20-e66019bd816c)

**IR LEDs in a reflection without the IR cut filter**  
![color-onircut-offirled-on](https://github.com/user-attachments/assets/2ec78c82-56ca-41e1-8b27-07b79a90a34b)


