Installation
------------

### Recommended method

Use programming clip on the flash chip on the board and re-program in place (requires a modified CH341A programmer and a clip). See videos below:

1. On linux, install https://github.com/Droid-MAX/SNANDer

2. Optional step: backup original firmware: `snander -r backup1 && snander -r backup2 && md5sum backup1 backup2`. If the checksums match, the firmware is probably saved correctly. If they don't, check your setup and repeat the process until you get two identical files.

3. Download firmware from thingino.com, Use `snander -e && snander -w <filename> -v` to erase the flash chip clean and write a new firmware to it with verification of the result.


[Programming Jooan A6M with a clip, pt.1](http://www.youtube.com/watch?v=lDzk7r3xyGE):

[![Programming Jooan A6M with a clip, pt.1](http://img.youtube.com/vi/lDzk7r3xyGE/0.jpg)](http://www.youtube.com/watch?v=lDzk7r3xyGE "Programming Jooan A6M with a clip, pt.1")


[Programming Jooan A6M with a clip, pt.2](http://www.youtube.com/watch?v=zWBrI0DF35U):

[![Programming Jooan A6M with a clip, pt.2](http://img.youtube.com/vi/zWBrI0DF35U/0.jpg)](http://www.youtube.com/watch?v=zWBrI0DF35U "Programming Jooan A6M with a clip, pt.2")


[CH341a programmer modification, pt. 1.5](http://www.youtube.com/watch?v=qXLmrmb0BJc):

For in-place programming, it is necessary to cut pin 8 of the programming adapter:

[![CH341a programmer](http://img.youtube.com/vi/qXLmrmb0BJc/0.jpg)](http://www.youtube.com/watch?v=qXLmrmb0BJc "CH341a programmer")


### Alternative methods

* Desolder the flash chip and reprogram it in a programmer.
* Use a [No Tool Installation](https://github.com/themactep/thingino-firmware/wiki/No-Tool-Installation) method. Doesn't exist for this camera
* Use SD cart and replace firmware from vendor U-Boot shell. Not possible, vendor uboot is password locked.
* Use [Ingenic USB Cloner](https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner) and reprogram via USB port. USB data lines not available for this camera.
* Get access to the linux shell from UART. Not possible: UART is disabled on vendor linux


Specifications
--------------

* Model: Jooan A6M-U
* Type: outdoor camera
* Weather resistance: IP65 (claimed)
* CPU: Ingenic T23, 1.2GHz
* RAM: 64MB
* Flash: 8MB, chip: Z 25V064CSJG
* Sensor: SmartSens SC1A4T, 1280H x 720V @ 15FPS, RGGB Bayer filter
* Sensor optical format: 1/4.6", active area: 3.392mm x 1.908mm, pixel: 2.65um x 2.65um
* Lens: 3.6mm, M12 mount, total length (sensor to lens edge): ~23mm
* Field of View: Horizontal ~51 degrees, Vertical ~30, Diagonal ~58 degrees
* Optical resolution: vertical 420 TVL, horizontal 550 TVL
* IR cut filter: Yes, mechanical shutter with solenoid, controlled by GPIO
* WIFI module, variant 1: SV6355
* WIFI module, variant 2: Altobeam ATBM6012BX, 802.11n 20MHz only, 2.4GHz only, BLE
* Microphone: Yes
* Speaker: Yes
* SD card slot: Yes
* reset button: Yes
* Illumination:
* White LEDs: Yes, 2x, controlled by GPIO/PWM
* IR 850nm LEDs: Yes, 2x, controlled by GPIO/PWM
* IR 940nm LEDs: No
* Power consumption: 5V 2A 7.5W (claimed on the box) or 5V 1.5A (supplied adapter in the box)
* FCC ID: 2BBQ4-A6M-U [fcc.report](https://fcc.report/FCC-ID/2BBQ4-A6M-U) (PDF manual, pictures, test report)
* Pan / Tilt / Zoom motors: No
* Ethernet interface: No
* USB: Yes, USB type C, Power only, no data lines
* Vendor app: [CAM720](https://play.google.com/store/apps/details?id=com.jooan.qiaoanzhilian.fmr.gp) (not compatible with thingino)

Pictures
--------

<img src="https://github.com/user-attachments/assets/fb1c4480-971f-4291-b4ff-86693097bb1c" width="400">

<img src="https://github.com/user-attachments/assets/ea2ee0a5-e593-4e12-8a36-23be3771bf13" width="400">

<img src="https://github.com/user-attachments/assets/5c1d651f-0398-40ca-8a3a-15adba113ee4" width="400">

<img src="https://github.com/user-attachments/assets/2d791426-e71d-4029-9106-1959756b1994" width="400">

<img src="https://github.com/user-attachments/assets/5e51bc3a-8cd7-4be3-b281-b354d7a31b0c" width="400">

**SV6355 Variant**

<img src="https://github.com/user-attachments/assets/68ef5fa4-dd7a-41e7-a948-2ba1c92269a4" width="400">

### Serial UART

115200 baud, 3.3V

<img src="https://github.com/user-attachments/assets/9a6e8be6-7fcd-47e5-9981-fa0878d46bcd" width="400">

### Jooan A6M TX-RX Pinout:

![jooan-a6m](https://github.com/user-attachments/assets/af52c554-9f64-491a-becc-11c9ddad78d1)

Logs
----

### Vendor uart log

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

Vendor kernel command line (extracted):
console=null mem=46080K@0x0 rmem=19456K@0x2d00000 init=/linuxrc rootfstype=squashfs root=/dev/mtdblock3 rw
 mtdparts=jz_sfc:256k(boot),32k(bootenv),1472k(kernel),2880k(rootfs),3136k(appfs),384k(config),32k(confbak)
 ja_version=01.23N.20231228.19 HWUbootGpioSet=60(0) CpuType=T23N HWKernelGpio=61(SdCd) SDKMem=19456
```
