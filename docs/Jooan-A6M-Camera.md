# Installation

## Recommended method
Use programming clip on the flash chip on the board and re-program in place (requires a programmer and a clip).

## Alternative methods

* Desolder the flash chip and reprogram it in a programmer.
* Use a [No Tool Installation](https://github.com/themactep/thingino-firmware/wiki/No-Tool-Installation) method. Doesn't exists for this camera
* Use SD cart and replace firmware from vendor U-Boot shell. Not possible, vendor uboot is password locked.
* Use [Ingenic USB Cloner](https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner) and reprogram via USB port. USB Port not available for this camera.
* Get access to the linux shell from UART. Not possible: UART is disabled on vendor linux

# Specifications

* Type: outdoor camera 
* CPU: Ingenic T23, 1188MHz
* RAM: 64MB
* Flash: 8MB, chip: Z 25V064CSJG
* Sensor: SmartSens SC1A4T, 1280 x 720p, 15FPS only, RGGB Bayer filter
* IR cut: Yes, switchable mechanical shutter with solenoid
* Optical resolution: vertical 420 TVL, horizontal 550 TVL
* WIFI module, variant 1: Altobeam ATBM6012BX, 802.11n 20MHz only, 2.4GHz only, BLE
* WIFI module, variant 2: SSV6355
* Microphone
* Speaker
* SD card slot
* reset button
* Illumination: 2x white LEDs + 2x IR 850nm LEDs
* Power consumption: 5V 2A 7.5W (claimed on the box) or 5V 1.5A (supplied adapter in the box)
* FCC ID: 2BBQ4-A6M-U
* Pan and Tilt motor: No
* Ethernet interface: No
* IR940 LED: No
* USB port: No

# Pictures

<img src="https://github.com/user-attachments/assets/fb1c4480-971f-4291-b4ff-86693097bb1c" width="400">

<img src="https://github.com/user-attachments/assets/ea2ee0a5-e593-4e12-8a36-23be3771bf13" width="400">

<img src="https://github.com/user-attachments/assets/5c1d651f-0398-40ca-8a3a-15adba113ee4" width="400">

<img src="https://github.com/user-attachments/assets/2d791426-e71d-4029-9106-1959756b1994" width="400">

<img src="https://github.com/user-attachments/assets/5e51bc3a-8cd7-4be3-b281-b354d7a31b0c" width="400">

# Serial UART

115200 baud, 3.3V

<img src="https://github.com/user-attachments/assets/9a6e8be6-7fcd-47e5-9981-fa0878d46bcd" width="400">
