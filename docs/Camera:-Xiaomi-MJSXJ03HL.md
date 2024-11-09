## Installation

Choose between:
1. Quick installation method, which doesn't require dismantling the camera, and doesn't backup the original firmware
2. Safe installation, which requires camera dismantling. Allows full backup of original firmware, and recovery from corrupted flash

### Quick method

See: https://github.com/Andrik45719/MJSXJ03HL

### Safe method

First, dismantle camera to access flash chip, then use either cloner or CH341 to backup and reprogram flash:
- [Ingenic USB Cloner](https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner) + flash pin short trick and reprogram via USB port (requires a USB OTG port on the camera, USB cable with data lines), or:
- [CH341 programming clip](https://github.com/themactep/thingino-firmware/wiki/CH341A-Programmer) on the chip on the board and re-program in place (requires a programmer and a clip).

## Specifications

* Model: Xiaomi MJSXJ03HL
* Type: indoor camera
* Weather resistance: no
* CPU: Ingenic
