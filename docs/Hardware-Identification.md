In order to install the correct firmware build, you need to determine what hardware components are used in your camera.
Here is a typical IP camera board. This particular one is a Wyze Cam V3.

![image](https://github.com/themactep/thingino-firmware/assets/37488/ccf35cd3-4b4d-45a7-8e2c-ac386fc88b0e)

### SoC

![image](https://github.com/themactep/thingino-firmware/assets/37488/c90d3fe1-f5bd-4d6e-9f7d-c09ef565f4a5)

The Ingenic SoC is usually the largest chip on the board, black and square in shape.

Ingenic chips usually have very clear labeling that uniquely identifies the SoC model.

The SoC family is written in larger type just below the Ingenic logo: T10, T20, T21, T23, T30, T31, etc.

The line below is mostly numbers, but also includes a literal code for the model: L, LC, N, X, ZX, A, etc.

### Flash Memory

![image](https://github.com/themactep/thingino-firmware/assets/37488/d67a37c2-949a-450c-8201-1ab34798bcd8)

The flash memory used on the camera can be either NOR type, which is well supported by thingino,
or NAND type, with very experimental preliminary support.

NOR chips are usually perfectly square in shape, with eight distinct legs, four on each opposite side. 

Leg number one is represented by an embossed or engraved depression.

NOR chips used in IP cameras are EEPROM type 25 and have `25` in their model names: `W25Q64`, `MX25L128`, and so on.

Numbers `64` and `128` refer to the size of the chip in megabits, which are converted to megabytes by dividing by eight: 64/8 = 8 megabytes, 128/8 = 16 megabytes.

### UART

![image](https://github.com/themactep/thingino-firmware/assets/37488/05b6d4a3-7002-41bf-b421-420cf7a7c6e5)

The [UART](https://en.wikipedia.org/wiki/Universal_asynchronous_receiver/transmitter) is a serial connection directly to the heart of the camera - its SoC.

Finding UART contacts and establishing a serial connection to the camera is crucial for any serious work with the hardware, and especially for firmware development.

Usually the UART has three contacts labeled G (GND), T (TX), R (RX). Sometimes there is another contact marked V (VCC), but we do not use it in our operations. The camera should be powered through its regular interface, which provides protection against overvoltage.

### Wi-Fi module

![image](https://github.com/themactep/thingino-firmware/assets/37488/33f838d8-b4f1-4a5d-9bef-c02ffa2f2853)

... to be continued