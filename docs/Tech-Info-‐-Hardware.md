Each camera has a unique set of gpio assignments.  These are stored as environment variables in a 64KB region of flash (offset 0x40000-0x50000) and they are read by UBoot, the Thingino Linux kernel, and Thingino user programs.  The `get` utility can retrieve the value of such a variable, and it can be set with `fw_setenv` and printed with `fw_printenv`.

# List of `gpio_` variables

- `gpio_button` - This GPIO pin is linked to the "reset" button on the device.  When it is pressed, Thingino will (do what exactly?)
- `gpio_ir940` - This GPIO pin turns on the 940nm infrared LED on the device
- `gpio_ir850` - This GPIO pin turns on the 850nm LED.  See [here](https://github.com/themactep/wiki/blob/master/hardware/components/ir-leds.md) for more info about the IR LEDs
- `gpio_ircut` - This is typically a pair of GPIOs that controls the solenoids for the [IRcut device](https://github.com/themactep/wiki/blob/master/hardware/components/ir-cut.md). Care is needed when determining those since activating them for even short periods of time may burn them out.
- `gpio_led_b` - This turns on the blue LED in the device (if it has one)
- `gpio_led_g` - This turns on the green LED if present
- `gpio_led_r` - This turns on the red LED if present
- `gpio_led_y` - This turns on the yellow LED if present
- `gpio_mmc_cd` - This input pin serves to detect whether an SD card is inserted into the SD/MMC device
- `gpio_mmc_power` - Some cameras require this GPIO pin to power up the MMC device
- `gpio_wlan` - Some cameras require this GPIO pin to provide power to the WiFi chip
- `gpio_motor_h` - 4 pins to drive the horizontal (pan) motor in a PTZ camera - order matters.  Reversing the order reverses the movement.
- `gpio_motor_v` - 4 pins to drive the vertical (tilt) motor in a PTZ camera
- `gpio_scl`/`gpio_sda` - these are the clock and data lines for an [I2C device](https://en.wikipedia.org/wiki/I%C2%B2C). Unclear what this is used for in Thingino
- `gpio_speaker` - an output pin that either directly drives the device's speaker, or drives an amplifier that enables the speaker
- `gpio_sub1g` - some cameras have a 925MHz [CC1101 or similar](https://www.ti.com/product/CC1101) transceiver, which is enabled with this pin.
- `gpio_usb_en` - ???
- `gpio_white` - ???
- `gpio_default` - (not shown below) - the UBoot loader will put the listed GPIOs in the listed state
- `gpio_default_net` - ???

# Thingino GPIO assignments as of 2024:07:20 11:00:13 EDT -0400

| Model | button|default_net|ir850|ir940|ircut|lds|led_b|led_g|led_r|led_w|led_y|mmc_cd|mmc_power|motor_h|motor_v|scl|sda|speaker|sub1g|usb_en|white|wlan
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| atom-cam-2 |51 | 48o | 26 |  | 53 52 |  |  |  |  |  |  | 59 | 48o |  |  |  |  | 63 |  |  |  | 57O|
| camsoy_okc01 | |  |  |  |  |  |  |  |  |  |  | 61 | 62 |  |  | 85 | 57 |  |  |  |  | |
| chinamobile-hdc51-t21n |59 |  |  |  |  |  | 52o |  | 53o |  |  | 51 |  |  |  |  |  | 63 |  |  |  | 62o|
| chinamobile-hdc51-t31l-jxf37 |54 |  |  |  | 49O | 7 | 53o |  | 52o |  |  | 51 |  |  |  |  |  | 63 |  |  |  | |
| chinamobile-hdc51-t31l-sc2332 |54 |  |  |  | 57 58 | 7 | 53o |  | 52o |  |  | 51 |  |  |  |  |  | 63 |  |  |  | |
| cinnado-d1-t23n |38 |  |  | 45 | 57 58 |  | 40 |  | 46 |  |  | 50 |  | 49 63 62 61 | 52 53 64 59 |  |  | 39o |  |  |  | 47o|
| cinnado-d1-t31l |14 |  |  | 11 | 57 58 |  | 9 |  | 8 |  |  | 50 |  | 49 63 62 61 | 52 53 64 59 |  |  | 7o |  |  |  | 47O|
| cinnado-d1-t31l.k4 |14 |  |  | 11 | 57 58 |  |  |  |  |  |  | 50 |  | 49 63 62 61 | 52 53 64 59 |  |  |  |  |  |  | 47O|
| dekco-dc5l | |  |  | 14 | 59 60 |  | 57 | 58 |  |  |  | 49 |  | 63 62 61 51 | 54 52 53 41 |  |  | 42 |  |  | 47 | 43o|
| eufy-e220 | |  | 9 |  | 57 58 |  |  |  |  |  |  | 49 |  | 61 62 63 51 | 64 53 52 54 |  |  |  |  |  |  | 8O|
| eufy-t8441 | | 72 | 60 |  | 49 50 |  |  |  |  |  |  | 58 |  |  |  |  |  |  |  |  | 59 | 48O|
| galayou-g2-t23n |14 |  |  | 50 | 16 17 |  | 35 |  |  |  |  | 49 |  | 54 52 53 64 | 61 62 63 51 | 58i | 57i | 7 |  |  |  | 6O|
| galayou-g2-t31lc | |  |  | 50 | 10 11 |  | 9o |  |  |  |  | 49 |  | 61 62 63 51 | 54 52 53 64 |  |  |  |  |  |  | |
| galayou-y4-t31l | |  |  | 11 | 57 58 |  |  |  |  |  |  | 50 |  | 49 63 62 61 | 52 53 64 59 |  |  |  |  |  |  | 17o|
| galayou-y4-t31n | |  |  | 11 | 57 58 |  |  |  |  |  |  | 50 |  | 49 63 62 61 | 52 53 64 59 |  |  |  |  |  |  | 17o|
| h3c-c2041 |50 |  |  |  | 57 58 |  | 16o |  | 17o |  |  | 49 |  |  |  |  |  |  |  |  |  | 10|
| litokam-c1 | |  | 50 |  | 10 11 |  |  | 8 | 9 |  |  | 49 |  |  |  |  |  |  |  |  |  | 6O|
| overtech_ov59wb |62 |  | 49 |  | 52 53 |  |  |  | 57 | 50 |  | 59 |  |  |  |  |  | 63O |  |  |  | 61o|
| personalcam |7 |  | 14 |  | 52 52 |  | 48 |  |  |  | 47 | 50 | 39o | 57 49 51 54 | 63 62 61 60 |  |  | 8 |  |  |  | |
| primecables-08360 |50 |  | 73o |  | 79 80 |  |  |  |  |  |  | 52 |  |  |  | 39i | 48i | 63O |  |  |  | |
| primecables-08361 |50 |  | 73o |  | 79 80 |  |  |  |  |  |  | 52 |  | 81 82 60 53 | 77 76 75 78 | 39i | 48i | 63O |  |  |  | |
| vanhua-ak54 | |  |  |  | 57 58 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | |
| vanhua-h33 | |  |  |  | 57 58 |  |  |  |  |  |  |  |  | 63 62 61 60 | 59 52 53 49 |  |  |  |  |  |  | |
| vanhua-h53 | |  |  |  | 57 58 |  |  |  |  |  |  |  |  | 63 62 61 60 | 59 52 53 49 |  |  |  |  |  |  | 14O|
| vanhua-l34 | |  |  |  | 57 58 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | |
| vanhua-z55i | |  |  |  | 57 58 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | |
| wansview-k5 | |  |  |  | 79 80 |  | 73 |  | 72 |  |  | 52 |  |  |  |  |  |  |  |  |  | |
| wansview-w7-t31l |14 |  |  | 11 | 57 58 |  |  |  |  |  |  | 50 |  | 49 61 62 63 | 52 59 64 53 |  |  |  |  |  |  | 17o|
| wuuk-y0510 |50IDU |  | 9 |  | 57 58 |  | 16 |  | 17 |  |  | 49 |  | 61 62 63 51 | 64 53 52 54 |  |  |  |  |  |  | 8O|
| wyze-c2 |46 | 48o | 49 |  | 26 25 |  |  |  |  |  |  | 43 | 48o |  |  |  |  | 63 |  |  |  | 62O|
| wyze-c3-t31al-atbm |51 | 48o | 47 | 49 | 52 53 |  | 39o |  | 38o |  |  | 59 | 48o |  |  |  |  | 63 |  |  |  | 57O|
| wyze-c3-t31x-atbm |51 | 48o | 47 | 49 | 52 53 |  |  |  |  |  |  | 59 | 48o |  |  |  |  | 63 |  |  |  | 57O|
| wyze-c3-t31x-rtl |51 | 48o | 47 | 49 | 52 53 |  |  |  |  |  |  | 59 | 48o |  |  |  |  | 63 |  |  |  | 57O|
| wyze-cp1 |46 | 48o |  | 49 | 26 25 |  | 39 |  |  |  | 38 | 43 | 48o | 54 53 52 51 | 80 79 76 75 |  |  | 63 |  | 47 |  | 62O|
| wyze-cp2 |6 |  | 60 |  | 50 49 |  |  |  |  |  |  | 48 | 47o 54o | 52 53 57 51 | 59 61 62 63 |  |  | 7 |  |  |  | 58O|
| wyze-cp3 |6 |  | 60 |  | 49 50 |  | 39o |  |  |  | 38o | 48 |  | 51 57 53 52 | 63 62 61 59 |  |  | 7 |  |  |  | |
| wyze-vdb1 |6 |  |  |  | 53 52 |  | 39 |  |  |  | 38 | 62 |  |  |  |  |  | 58 | 61 |  | 49 | 57O|
| xiaomi-hlcam04 |51 | 48o | 47 | 49 | 52 53 |  |  |  |  |  |  | 59 | 48o |  |  |  |  | 63 |  |  |  | 57O|
| xiaomi-mjsxj03hl-t31n |51 |  | 60 |  | 50 49 |  |  |  |  |  |  | 47 |  |  |  |  |  |  |  |  |  | 62O|
| xiaomi-xiaofang-t20l |46 | 48o |  | 49 | 26 25 |  | 39 |  |  |  | 38 | 43 | 48o | 51 52 53 54 | 75 76 79 80 |  |  | 63 |  | 47 |  | 62O|
