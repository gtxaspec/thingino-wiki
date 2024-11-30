Installation Methods
--------------------

There are lots of ways to install firmware on hardware devices, and different vendors and hardware designs have different approaches.
Below is a list of methods to replace the stock firmware on your camera, listed from the most reliable to the easiest:

### Programming with CH341A, off-board

![image](https://github.com/user-attachments/assets/5b0b5470-ec2c-4fe5-8b6d-f8205caf3be0)

This method requires desoldering the flash chip and reprogramming it in a programmer. 

Requirements:
- Soldering station
- CH341a programmer
- SOIC8 chip adapter
- Soldering skills

### Programming with CH341A, in-place

![image](https://github.com/user-attachments/assets/a693e83b-32e4-4d26-bcf6-75c1496ed923)

This method requires a programmer with a programming clip.

Requirements:
- CH341a programmer
- SOIC8 programming clip

### Programming via serial connection

![image](https://github.com/user-attachments/assets/655ce958-8113-4fdf-9a8a-fa14e81487d8)

This method requires a serial connection and access to U-Boot shell.
The firmware image can be read from an SD card, or downloaded from a TFTP server over an Ethernet connection, or uploaded over serial link using a modem protocol.

Requirements:
- UART adapter

### Programming over USB port with Cloner tool

![image](https://github.com/user-attachments/assets/72679ba5-ea0e-4a59-b5e9-20332cc280a0)

This method requires a USB OTG port on the camera and [Ingenic USB Cloner](https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner) tool.

Requirements:
- USB cable with data lines

![image](https://github.com/user-attachments/assets/87368bb1-34ea-407f-8f5c-02ae5b0e764b)

### Programming from an SD card with a magic filename

![image](https://github.com/user-attachments/assets/b38cf862-43da-43f5-b5bc-db5aef27df93)

Please check [No Tool Installation](https://github.com/themactep/thingino-firmware/wiki/No-Tool-Installation) method if that method exists for your camera. Check the list at [Thingino Installers](https://github.com/wltechblog/thingino-installers).

Requirements:
- SD card

### Programming from a sideloaded system

Try [wz_mini_hacks](https://github.com/gtxaspec/wz_mini_hacks) and get creative (requires SD card slot).

### Programming from within the stock system

Break the stock Linux password and get access to the shell (requires a UART connection)

... maybe something else

In Details
----------

This document outlines several methods of installation, each tailored to accommodate the unique characteristics of various devices. Some installation methods are straightforward and do not require the user to open the device, such as using USB recovery methods or SD card installations. However, other methods may necessitate physically opening the device to access interfaces like UART. The following sections provide detailed instructions for each method, ensuring you can successfully install the software on your device regardless of its design or vendor.

### Using the Ingenic USB Cloner tool

If your camera has a USB port, there is a good chance that you can install the firmware using [Ingenic USB Cloner](Ingenic-USB-Cloner).

### From the U-Boot Shell

1. Follow steps 1-4 from the previous chapter.
2. Create a [serial connection to the UART port](UART-Connection) of the camera.
3. While booting, press `Ctrl-c` to get into the bootloader shell.

Make sure the card is readable by the bootloader. 
Run `mmc rescan` followed by `mmcinfo` to verify the size of the card. 

```
ingenic_T31L# mmc rescan
ingenic_T31L# mmcinfo   
Device: msc
Manufacturer ID: 0
OEM: 3000
Name: APPSD 
Tran Speed: 50000000
Rd Block Len: 512
SD version 2.0
High Capacity: No
Capacity: 60 MiB
Bus Width: 4-bit
```

Run `fatls mmc 0` to check the contents of the card.

```
ingenic_T31L# fatls mmc 0
  8388608   autoupdate-full.bin 

1 file(s), 0 dir(s)
```

Execute the following commands line by line.

Use `setenv flashsize 0x800000;` for an 8MB flash chip,
`setenv flashsize 0x1000000;` for a 16MB flash chip.

```
setenv flashsize 0x800000;
setenv baseaddr 0x82000000;
mw.b ${baseaddr} 0xff ${flashsize};
fatload mmc 0:1 ${baseaddr} autoupdate-full.bin;
sf probe 0; sf erase 0x0 ${flashsize};
sf write ${baseaddr} 0x0 ${filesize};
reset
```

### From another firmware

Download the U-Boot image for your camera from https://github.com/gtxaspec/u-boot-ingenic/releases/, flash it to the first partition (mtd0), wipe the existing environment (mtd1) and reboot.

```
root@openipc-t31:~# curl -L -s -o /tmp/uboot.bin https://github.com/gtxaspec/u-boot-ingenic/releases/download/latest/u-boot-t31l.bin
root@openipc-t31:~# flashcp /tmp/uboot.bin /dev/mtd0
root@openipc-t31:~# flash_eraseall /dev/mtd1
root@openipc-t31:~# reboot
```

**If your camera has an SD card slot**, download the latest Thingino firmware for your camera from https://github.com/themactep/thingino-firmware/releases/tag/firmware and save it as `autoupdate-full.bin` to a FAT32 formatted SD card. Insert the card into the camera and reboot. The camera will reflash itself and reboot again to populate the environment. You should now have a Thingino camera.

**If your camera does not have an SD card slot**, update the boot arguments to replace the dynamic overlay size with a hard-coded value to overcome the limitations of the existing kernel, enable the updates, and reboot again.

```
root@openipc-t31:~# fw_setenv bootargs 'mem=${osmem} rmem=${rmem} console=${serialport},${baudrate}n8 panic=${panic_timeout} root=/dev/mtdblock3 rootfstype=squashfs init=/init mtdparts=jz_sfc:256k(boot),64k(env),${kern_size}(kernel),${rootfs_size}(rootfs),1024k(rootfs_data)${update}'
root@openipc-t31:~# fw_setenv enable_updates true
root@openipc-t31:~# reboot
```

Finally, download and flash the full thingino image for your camera. This will overwrite everything in the flash chip.

```
root@openipc-t31:~# curl -L -s -o /tmp/fw.bin https://github.com/themactep/thingino-firmware/releases/download/firmware/thingino-vanhua_l34.bin
root@openipc-t31:~# flashcp /tmp/fw.bin /dev/mtd6
root@openipc-t31:~# reboot
```


[1]: https://github.com/themactep/thingino-firmware/releases/tag/firmware
