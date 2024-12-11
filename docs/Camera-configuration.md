Getting the camera up and running requires initial setup of the bootloader environment. 
Most camera firmware images already have environment settings in them, and you only need to provide your wireless network credentials to get the camera online. However, if you are building firmware for a new camera, or if you are using a module firmware, you will need to provide the environment file yourself.

### Networking MAC Addressing

When the system is installed, it generates and assigns MAC addresses to the `ethaddr` and `wlanmac` environment variables. These MAC addresses are based on the SoC (System on Chip) serial number. They are unique to your device. If the serial number is not available, random MAC addresses are created instead. 

You can change or clear these variables if needed. It's important to note that some WiFi modules might not provide a consistent MAC address without these generated values.

### Configuring via the camera's access point

If your camera does not already have wireless credentials, it will launch an access point with a built-in portal that allows you to connect directly to the camera and enter credentials to connect to your wireless network. The portal will only stay up for 5 minutes, then it will shut down for security reasons and you will need to reboot the camera to restart it.

To access the portal, turn on the camera and scan available wireless networks for an SSID called THINGINO-XXXX, where XXXX is a unique part of the camera's MAC address. Connect to this network (it's open, so you don't need any credentials) and navigate to _http://thingino.local/_ or _http://172.16.0.1/_ in your web browser. On the page, enter your wireless network SSID and password to access the network and click the _Save Credentials_ button.
The camera will reboot and attempt to connect to your wireless network using the credentials provided.

### Configuration with an SD card

Find your camera model in [/environment/][envdir] directory, copy its configuration file and save it as `uEnv.txt`.
Replace the `wlanssid` and `wlanpass` values with your wireless network credentials.
Copy the file to an SD card, insert the card into your camera and reboot.

### Bootloader environment explained

#### Hardware Settings

- `gpio_default` - List of default GPIO states on boot. each position consists of the GPIO number followed by the desired state:
  - `O` - Output, High
  - `o` - Output, Low
  - `i` or `I` - Input
- `gpio_button` - GPIO pin for reset button
- `gpio_led_r` - GPIO pin for red LED
- `gpio_led_g` - GPIO pin for green LED
- `gpio_led_b` - GPIO pin for blue LED
- `gpio_led_y` - GPIO pin for yellow LED
- `gpio_mmc_cd` - GPIO pin for MMC card detection
- `gpio_mmc_power` - GPIO pin to control power to MMC
- `gpio_usb_en` - GPIO pin to control power to USB 
- `gpio_speaker` - GPIO pin to contol power to speaker

#### Night Mode

- `day_night_min` - Gain value to switch to day mode, defaults to `15000`
- `day_night_max` - Gain value to switch to night mode, defaults to `500`
- `day_night_color` - Whether to enable black & white colors on night mode and disable on day mode, defaults to `false`
- `day_night_ir850` - Whether to enable the 850nm IR LEDs on night mode and disable on day mode, defaults to `false`
- `day_night_ir940` - Whether to enable the 940nm IR LEDs on night mode and disable on day mode, defaults to `false`
- `day_night_ircut` - Whether to enable IRCUT on night mode and disable on day mode, defaults to `false`
- `day_night_white` - Whether to enable the white light LED on night mode and disable on day mode, defaults to `false`
- `gpio_ircut` - GPIO pins for IRCUT driver, can be one or two pins, depending on drive type
- `gpio_ir850` - GPIO pin for 850nm IR LEDs
- `gpio_ir940` - GPIO pin for 940nm IR LEDs
- `gpio_white` - GPIO pin for white light LEDs
- `pwm_ch_ir850` - PWM Channel of 850nm IR LED
- `pwm_ch_ir940` - PWM Channel of 940nm IR LED
- `pwm_ch_white` - PWM Channel of white light LED

#### Pan and tilt motors

- `gpio_motor_en` - GPIO pin for enabling the motor controller
- `gpio_motor_h` - GPIO pins for horizontal (pan) motors
- `gpio_motor_v` - GPIO pins for vertical motion (tilt) motors
- `motor_maxstep_h` - Maximum number of microsteps for pan motor
- `motor_maxstep_v` - Maximum number of microsteps for tilt motor
- `disable_homing` - Set to `true` to disable homing of motors on boot

#### Wireless networking

- `disable_wlan` - Disable WLAN
- `gpio_wlan` - GPIO pin to control power to wireless card
- `wlanbus` - Wireless card bus type, can be `usb` or `sdio`
- `wlandev` - Wireless card driver
- `wlandevopts` - Arguments to pass to wireless driver
- `wlanmac` - MAC address for wireless interface
- `wlanssid` - Wireless network name
- `wlanpass` - wireless network password

#### Ethernet networking

- `ethaddr` - MAC address for Ethernet interface
- `disable_eth` - Disable Ethernet networking for faster boot on Wi-Fi only cameras

#### Miscellaneous

- `disable_streamer` - Disable video streamer
- `disable_watchdog` - Disable system watchdog
- `enable_updates` - Enable virtual partitions used for firmware upgrades
- `hostname` - Host name to use when connecting to a network
- `timezone` - Timezone, set from Web UI so you don't need to edit it directly
- `sshkey_ed25519` - backup of ssh key
- `devip` - IP address of developer's workstation
- `debug` - Debug mode

### Configuring via SSH
If your camera is already connected to a wireless network, you can access an SSH shell using the same credentials as the WebUI (`root` / whatever password you've set).

Modifications to `/etc/prudent.cfg` should be made using the `/bin/prudyntcfg` script.

Example:
```
/bin/prudyntcfg set stream1.bitrate 900
/bin/prudyntcfg set stream2.fps 5
/bin/prudyntcfg set stream2.bitrate 900
```

The script will exit with code `0` if the modification was successful.

The "default" configuration for Prudynt is located at `/rom/etc/prudynt.cfg`, so you can revert easily by running:
```
rm /etc/prudynt.cfg && cp /rom/etc/prudynt.cfg /etc/prudynt.cfg
```
NOTE: Removing `/etc/prudynt.cfg` is only really necessary if you're using an idempotent configuration manager (like Ansible) to reset the configuration when no changes have been made since flashing the firmware due to the overlay filesystem.  Failure to remove a the stock file may result in the error: `cp: '/rom/etc/prudynt.cfg' and '/etc/prudynt.cfg' are the same file`


## DEPRECATED

### Configuration via wireless network

If your camera doesn't have an SD card slot and Wi-Fi is the only way to access it, you can use the default credentials that come with our firmware. Create a wireless network with a name _thingino_ and password _thingino_. Make sure it has a DHCP server to assign IP addresses to cameras. Boot the camera with the new firmware. Check the list of DHCP clients on the server. Find the client with hostname _thingino-<soc>_ where _<soc>_ is the SoC model of the camera. Check the assigned IP address and use it to connect to the camera via ssh. Once in shell, set your real wireless network credentials using the following commands:

```
fw_setenv wlanssid <ssid>
fw_setenv wlanpass <password>
reboot
```


[envdir]: https://github.com/themactep/thingino-firmware/tree/master/environment
