# Installation

## Recommended method
Use programming clip on the flash chip on the board and re-program in place (requires a programmer and a clip).

## Alternative methods

* Desolder the flash chip and reprogram it in a programmer.
* Use a [No Tool Installation](https://github.com/themactep/thingino-firmware/wiki/No-Tool-Installation) method. Doesn't exists for this camera
* Use SD cart and replace firmware from vendor U-Boot shell. Not possible, vendor uboot is password locked.
* Use [Ingenic USB Cloner](https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner) and reprogram via USB port. USB data lines not available for this camera.
* Get access to the linux shell from UART. Not possible: UART is disabled on vendor linux

# Specifications

* Type: outdoor camera
* Environment: IP65 (claimed)
* CPU: Ingenic T23, 1188MHz
* RAM: 64MB
* Flash: 8MB, chip: Z 25V064CSJG
* Sensor: SmartSens SC1A4T, 1280 x 720p, 15FPS only, RGGB Bayer filter
* IR cut: Yes, mechanical shutter with solenoid, connected to GPIO
* Optical resolution: vertical 420 TVL, horizontal 550 TVL
* WIFI module, variant 1: SV6355
* WIFI module, variant 2: Altobeam ATBM6012BX, 802.11n 20MHz only, 2.4GHz only, BLE
* Microphone: Yes
* Speaker: Yes
* SD card slot: Yes
* reset button: Yes
* Illumination: 2x white LEDs + 2x IR 850nm LEDs, connected to GPIO/PWM
* Power consumption: 5V 2A 7.5W (claimed on the box) or 5V 1.5A (supplied adapter in the box)
* FCC ID: 2BBQ4-A6M-U [fcc.report](https://fcc.report/FCC-ID/2BBQ4-A6M-U)
* Pan and Tilt motors: No
* Ethernet interface: No
* IR940 LED: No
* USB: Yes, USB-C, Power only, no data lines

# Pictures

<img src="https://github.com/user-attachments/assets/fb1c4480-971f-4291-b4ff-86693097bb1c" width="400">

<img src="https://github.com/user-attachments/assets/ea2ee0a5-e593-4e12-8a36-23be3771bf13" width="400">

<img src="https://github.com/user-attachments/assets/5c1d651f-0398-40ca-8a3a-15adba113ee4" width="400">

<img src="https://github.com/user-attachments/assets/2d791426-e71d-4029-9106-1959756b1994" width="400">

<img src="https://github.com/user-attachments/assets/5e51bc3a-8cd7-4be3-b281-b354d7a31b0c" width="400">

### SV6355 Variant
<img src="https://github.com/user-attachments/assets/68ef5fa4-dd7a-41e7-a948-2ba1c92269a4" width="400">

# Serial UART

115200 baud, 3.3V

<img src="https://github.com/user-attachments/assets/9a6e8be6-7fcd-47e5-9981-fa0878d46bcd" width="400">

# Logs

## Vendor uart log

```
U-Boot SPL 2013.07-svn4700 (Dec 28 2023 - 19:36:40)
Board info: T23N

apll_freq = 1400000000
mpll_freq = 1200000000
sdram init start
DDR clk rate 600000000
image entry point: 0x80100000


U-Boot 2013.07-svn4700 (Dec 28 2023 - 19:36:40)

Board: ISVP (Ingenic XBurst T23 SoC)
DRAM:  64 MiB
Top of RAM usable for U-Boot at: 84000000
Reserving 433k for U-Boot at: 83f90000
Reserving 32800k for malloc() at: 81f88000
Reserving 32 Bytes for Board Info at: 81f87fe0
Reserving 124 Bytes for Global Data at: 81f87f64
Reserving 128k for boot params() at: 81f67f64
Stack Pointer at: 81f67f48
Now running in RAM - U-Boot at: 83f90000
MMC:   msc: 0
the manufacturer 5e
SF: Detected ZB25VQ64

In:    serial
Out:   serial
Err:   serial
Net:   use default phy reset gpio is 64
use default phy reset gpio is 64
use default phy reset gpio is 64
====>PHY not found!Jz4775-9161
Card did not respond to voltage select!
** Bad device mmc 0 **
Card did not respond to voltage select!
** Bad device mmc 0 **
Hit any key to stop autoboot:  0
the manufacturer 5e
SF: Detected ZB25VQ64

--->probe spend 4 ms
SF: 1572864 bytes @ 0x48000 Read: OK
--->read spend 507 ms
## Booting kernel from Legacy Image at 80600000 ...
   Image Name:   Linux-3.10.14__isvp_pike_1.0__
   Image Type:   MIPS Linux Kernel Image (lzma compressed)
   Data Size:    1453839 Bytes = 1.4 MiB
   Load Address: 80010000
   Entry Point:  803782a0
   Verifying Checksum ... OK
   Uncompressing Kernel Image ... OK

Starting kernel ...
```
