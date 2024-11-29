### Save 8MB firmware image to SD card

```
watchdog 0;
setenv baseaddr 0x82000000;
mmc dev 0;
mmc erase 0x10 0x4000;
setenv flashsize 0x800000;
mw.b ${baseaddr} ff ${flashsize};
sf probe 0; sf read ${baseaddr} 0x0 ${flashsize};
mmc write ${baseaddr} 0x10 0x4000
```

Read the saved data on a desktop PC by running
`sudo dd bs=512 skip=16 count=16384 if=/dev/sdb of=./fulldump.bin`,
where `/dev/sdb` is the SD card device.

### Save 16MB firmware image to SD card

```
watchdog 0;
setenv baseaddr 0x82000000;
mmc dev 0;
mmc erase 0x10 0x8000;
setenv flashsize 0x1000000;
mw.b ${baseaddr} ff ${flashsize};
sf probe 0; sf read ${baseaddr} 0x0 ${flashsize};
mmc write ${baseaddr} 0x10 0x8000
```

Read the saved data on a desktop PC by running
`sudo dd bs=512 skip=16 count=32768 if=/dev/sdb of=./fulldump.bin`,
where `/dev/sdb` is the SD card device.

### Save 8MB firmware image to TFTP server

```
watchdog 0;
setenv ipaddr 192.168.1.10;
setenv netmask 255.255.255.0;
setenv gatewayip 192.168.1.1;
setenv serverip 192.168.1.254;
setenv baseaddr 0x82000000;
setenv flashsize 0x800000;
mw.b ${baseaddr} 0xff ${flashsize};
sf probe 0; sf read ${baseaddr} 0x0 ${flashsize};
tftpput ${baseaddr} ${flashsize} backup-${soc}-nor8m.bin
```

if there is no `tftpput` but `tftp` then run this instead

```
tftp ${baseaddr} backup-${soc}-nor8m.bin ${flashsize}
```

### Save 16MB firmware image to TFTP server

```
watchdog 0;
setenv ipaddr 192.168.1.10;
setenv netmask 255.255.255.0;
setenv gatewayip 192.168.1.1;
setenv serverip 192.168.1.254;
setenv baseaddr 0x82000000;
setenv flashsize 0x1000000;
mw.b ${baseaddr} 0xff ${flashsize};
sf probe 0; sf read ${baseaddr} 0x0 ${flashsize};
tftpput ${baseaddr} ${flashsize} backup-${soc}-nor16m.bin
```

if there is no `tftpput` but `tftp` then run this instead

```
tftp ${baseaddr} backup-${soc}-nor16m.bin ${flashsize}
```

### Save firmware image via hex dump

In the terminal program you use to connect to the UART port,
enable saving the session log files.

```
$ screen -L -Logfile fulldump.log /dev/ttyUSB0 115200
```

Set flash memory size. Use this command for an 8MB flash chip

```
setenv flashsize 0x800000
```

or this one for a 16MB flash chip

```
setenv flashsize 0x1000000
```

then dump the memory contents to the console

```
watchdog 0;
setenv baseaddr 0x82000000;
mw.b ${baseaddr} 0xff ${flashsize};
sf probe 0; sf read ${baseaddr} 0x0 ${flashsize};
md.b ${baseaddr} ${flashsize}
```

Since the reading process will take a considerable amount of time
(literally hours), you may want to disconnect from the terminal session
to prevent accidental keystrokes from contaminating the output.

Press `Ctrl-a` then `d` to disconnect the session from the active terminal.

Run `screen -r` when you need to reconnect it later, after the size of the log
file has stopped growing.

Reading of an 8 MB flash memory should result in about 40 MB log file,
and for a 16 MB chip the file should be twice that size.

Convert the hex dump into a binary firmware file.

```
cat fulldump.log | sed -E "s/^[0-9a-f]{8}\b: //i" | sed -E "s/ {4}.{16}\r?$//" > fulldump.hex
xxd -revert -plain fulldump.hex fulldump.bin
```

Use it for further investigation or to restore the camera to its original state.

Use [binwalk](https://github.com/ReFirmLabs/binwalk) to unpack the binary file.


### Burn 8MB firmware image from SD card

```
watchdog 0;
setenv baseaddr 0x82000000;
setenv flashsize 0x800000;
mw.b ${baseaddr} 0xff ${flashsize};
fatload mmc 0:1 ${baseaddr} autoupdate-full.bin;
sf probe 0; sf erase 0x0 ${flashsize};
sf write ${baseaddr} 0x0 ${filesize}
```

### Burn 8MB firmware image from TFTP server

```
watchdog 0;
setenv ipaddr 192.168.1.10;
setenv netmask 255.255.255.0;
setenv gatewayip 192.168.1.1;
setenv serverip 192.168.1.254;
setenv baseaddr 0x82000000;
setenv flashsize 0x800000;
mw.b ${baseaddr} 0xff ${flashsize};
tftp ${baseaddr} autoupdate-full.bin;
sf probe 0; sf erase 0x0 ${flashsize};
sf write ${baseaddr} 0x0 ${filesize}
```

### Burn 8MB firmware image via serial upload

To upload a file over a serial connection by name only, the file should be
located in the user's home directory, or use the full path to the file instead.

```
watchdog 0;
setenv baseaddr 0x82000000;
setenv flashsize 0x800000;
mw.b ${baseaddr} 0xff ${flashsize}
loady
```

Press `Ctrl-a` followed by `:`, then type `exec !! sz --ymodem autoupdate-full.bin`
When the upload is complete, continue:

```
sf probe 0; sf erase 0x0 ${flashsize};
sf write ${baseaddr} 0x0 ${filesize}
```

### Burn 16MB firmware image from SD card

```
watchdog 0;
setenv baseaddr 0x82000000;
setenv flashsize 0x1000000;
mw.b ${baseaddr} 0xff ${flashsize};
fatload mmc 0:1 ${baseaddr} autoupdate-full.bin;
sf probe 0; sf erase 0x0 ${flashsize};
sf write ${baseaddr} 0x0 ${filesize}
```

### Burn 16MB firmware image from TFTP server

```
watchdog 0;
setenv ipaddr 192.168.1.10;
setenv netmask 255.255.255.0;
setenv gatewayip 192.168.1.1;
setenv serverip 192.168.1.254;
setenv baseaddr 0x82000000;
setenv flashsize 0x1000000;
mw.b ${baseaddr} 0xff ${flashsize};
tftp ${baseaddr} autoupdate-full.bin;
sf probe 0; sf erase 0x0 ${flashsize};
sf write ${baseaddr} 0x0 ${filesize}
```

### Burn 16MB firmware image via serial upload

To upload a file over a serial connection by name only, the file should be
located in the user's home directory, or use the full path to the file instead.

```
watchdog 0;
setenv baseaddr 0x82000000;
setenv flashsize 0x1000000;
mw.b ${baseaddr} 0xff ${flashsize}
loady
```

Press `Ctrl-a` followed by `:`, then type `exec !! sz --ymodem autoupdate-full.bin`
When the upload is complete, continue:

```
sf probe 0; sf erase 0x0 ${flashsize};
sf write ${baseaddr} 0x0 ${filesize}
```

### Burn only bootloader from SD card

```
watchdog 0;
setenv baseaddr 0x82000000;
setenv bootsize 0x50000;
mw.b ${baseaddr} 0xff ${bootsize};
fatload mmc 0:1 ${baseaddr} autoupdate-uboot.bin;
sf probe 0; sf erase 0x0 ${bootsize};
sf write ${baseaddr} 0x0 ${filesize}
```

### Burn only bootloader from TFTP server

```
watchdog 0;
setenv ipaddr 192.168.1.10;
setenv netmask 255.255.255.0;
setenv gatewayip 192.168.1.1;
setenv serverip 192.168.1.254;
setenv baseaddr 0x82000000;
setenv bootsize 0x50000;
mw.b ${baseaddr} 0xff ${bootsize};
tftp ${baseaddr} autoupdate-uboot.bin;
sf probe 0; sf erase 0x0 ${bootsize};
sf write ${baseaddr} 0x0 ${filesize}
```

### Burn only bootloader via serial upload

```
watchdog 0;
setenv baseaddr 0x82000000;
setenv bootsize 0x50000;
mw.b ${baseaddr} 0xff ${bootsize}
loady
```

Press `Ctrl-a` followed by `:`, then type `exec !! sz --ymodem autoupdate-uboot.bin`
When the upload is complete, continue:

```
sf probe 0; sf erase 0x0 ${bootsize};
sf write ${baseaddr} 0x0 ${filesize}
```

### Erase bootloader

```
sf probe; sf erase 0x0 0x40000
```

### Erase bootloader environment

```
sf probe; sf erase 0x40000 0x1000
```
