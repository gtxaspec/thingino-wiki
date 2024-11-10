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
* Product name: Mi Camera 2K (Magnetic Mount)
* Type: indoor camera
* Weather resistance: no IP rating
* CPU: Ingenic T31L or T31N
* RAM: 64MB
* Flash: 16MB
* Video encoding: H.264, H.265, MJPG
* Sensor: SOI (Silicon Optronics Inc) JX-Q03P, 2304 x 1296 @ 30FPS, RGGB Bayer filter
* Sensor optical format: 1/2.7", active area: 5.76 mm x 3.24 mm, pixel: 2.5 um x 2.5 um
* Lens: unk mm, unk mount, total length (sensor to lens edge): unk mm
* Field of View: Horizontal 125 degrees
* Optical resolution: unk TVL
* IR cut filter: Yes, mechanical shutter with solenoid, controlled by GPIO
* WIFI module: RTL8189FTV, 802.11n 20/40MHz, 2.4GHz only, 150Mbps
* Microphone: Yes
* Speaker: Yes
* SD card slot: Yes
* reset button: Yes
* Illumination:
* White LEDs: No
* IR 850nm LEDs: No
* IR 940nm LEDs: Yes, 6x, controlled by GPIO
* Power consumption: 5V 1A
* Operating temperature: -10 C to +50 C
* FCC ID: unk
* Pan / Tilt / Zoom motors: No
* Ethernet interface: No
* USB: Yes, USB type C, with data lines
* Vendor app: [Mi Home](https://play.google.com/store/apps/details?id=com.xiaomi.smarthome) (not compatible with thingino)