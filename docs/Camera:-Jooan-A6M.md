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
* Sensor: SmartSens SC1A4T, 1280H x 720V @ 15FPS, RGGB Bayer filter, related to [SC1346 Product Flyer](https://smartsens.oss-cn-beijing.aliyuncs.com/web/img/1642675887829478304.pdf)
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

### Vendor uboot log

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

### Vendor kernel log

Change console=null to console=ttyS1,115200n8

```
Initializing cgroup subsys cpu
Initializing cgroup subsys cpuacct
Linux version 3.10.14__isvp_pike_1.0__ (root@ubuntu) (gcc version 5.4.0 (Ingenic Ingenic r3.3.0-gcc540 Smaller Size 2023.05-22) ) #1 PREEMPT Tue May 28 15:34:13 CST 2024
CPU0 RESET ERROR PC:04002B2D
CPU0 revision is: 00d00100 (Ingenic Xburst)
FPU revision is: 00b70000
cgu_vpu clk should be opened!
CCLK:1400MHz L2CLK:700Mhz H0CLK:200MHz H2CLK:200Mhz PCLK:100Mhz
Determined physical RAM map:
 memory: 0040f000 @ 00010000 (usable)
 memory: 00031000 @ 0041f000 (usable after init)
User-defined physical RAM map:
 memory: 02d00000 @ 00000000 (usable)
Zone ranges:
  Normal   [mem 0x00000000-0x02cfffff]
Movable zone start for each node
Early memory node ranges
  node   0: [mem 0x00000000-0x02cfffff]
Primary instruction cache 16kB, 8-way, VIPT, linesize 32 bytes.
Primary data cache 16kB, 8-way, VIPT, no aliases, linesize 32 bytes
pls check processor_id[0x00d00100],sc_jz not support!
MIPS secondary cache 64kB, 8-way, linesize 32 bytes.
Built 1 zonelists in Zone order, mobility grouping off.  Total pages: 11430
Kernel command line: console=ttyS1,115200n8 mem=46080K@0x0 rmem=19456K@0x2d00000 init=/linuxrc rootfstype=squashfs root=/dev/mtdblock3 rw mtdparts=jz_sfc:256k(boot),32k(bootenv),1472k(kernel),2880k(rootfs),3136k(appfs),384k(config),32k(confbak) ja_version=01.23N.20231228.19 HWUbootGpioSet=60(0) CpuType=T23N HWKernelGpio=61(SdCd) SDKMem=19456
PID hash table entries: 256 (order: -2, 1024 bytes)
Dentry cache hash table entries: 8192 (order: 3, 32768 bytes)
Inode-cache hash table entries: 4096 (order: 2, 16384 bytes)
Memory: 40668k/46080k available (3522k kernel code, 5412k reserved, 631k data, 196k init, 0k highmem)
SLUB: HWalign=32, Order=0-3, MinObjects=0, CPUs=1, Nodes=1
Preemptible hierarchical RCU implementation.
NR_IRQS:351
clockevents_config_and_register success.
Calibrating delay loop... 1386.49 BogoMIPS (lpj=693248)
pid_max: default: 32768 minimum: 301
Mount-cache hash table entries: 512
Initializing cgroup subsys debug
Initializing cgroup subsys freezer
regulator-dummy: no parameters
NET: Registered protocol family 16
bio: create slab <bio-0> at 0
jz-dma jz-dma: JZ SoC DMA initialized
usbcore: registered new interface driver usbfs
usbcore: registered new interface driver hub
usbcore: registered new device driver usb
 (null): set:249  hold:250 dev=100000000 h=500 l=500
Switching to clocksource jz_clocksource
NET: Registered protocol family 2
TCP established hash table entries: 512 (order: 0, 4096 bytes)
TCP bind hash table entries: 512 (order: -1, 2048 bytes)
TCP: Hash tables configured (established 512 bind 512)
TCP: reno registered
UDP hash table entries: 256 (order: 0, 4096 bytes)
UDP-Lite hash table entries: 256 (order: 0, 4096 bytes)
NET: Registered protocol family 1
freq_udelay_jiffys[0].max_num = 10
cpufreq         udelay  loops_per_jiffy
12000    5942    5942
24000    11884   11884
60000    29710   29710
120000   59421   59421
200000   99035   99035
300000   148553  148553
600000   297106  297106
792000   392180  392180
1008000  499138  499138
1200000  594212  594212
cfg80211: Calling CRDA to update world regulatory domain
squashfs: version 4.0 (2009/01/31) Phillip Lougher
jffs2: version 2.2. © 2001-2006 Red Hat, Inc.
msgmni has been set to 79
io scheduler noop registered
io scheduler cfq registered (default)
wait stable.[290][cgu_vpu]
jz-uart.1: ttyS1 at MMIO 0x10031000 (irq = 58) is a uart1
console [ttyS1] enabled
brd: module loaded
loop: module loaded
zram: Created 2 device(s) ...
logger: created 256K log 'log_main'
jz SADC driver registeres over!
jz TCU driver register completed
the id code = 5e4017, the flash name is ZB25VQ64
jz-sfc jz-sfc: sfc use DMA mode
jz-sfc jz-sfc: nor flash now use standard mode!
JZ SFC Controller for SFC channel 0 driver register
7 cmdlinepart partitions found on MTD device jz_sfc
Creating 7 MTD partitions on "jz_sfc":
0x000000000000-0x000000040000 : "boot"
0x000000040000-0x000000048000 : "bootenv"
0x000000048000-0x0000001b8000 : "kernel"
0x0000001b8000-0x000000488000 : "rootfs"
0x000000488000-0x000000798000 : "appfs"
0x000000798000-0x0000007f8000 : "config"
0x0000007f8000-0x000000800000 : "confbak"
SPI NOR MTD LOAD OK
tun: Universal TUN/TAP device driver, 1.6
tun: (C) 1999-2004 Max Krasnyansky <maxk@qualcomm.com>
Bus Mode Reg after reset: 0x00020101, cnt=0
Bus Mode Reg after reset: 0x00020101, cnt=1
Bus Mode Reg after reset: 0x00020101, cnt=2
Bus Mode Reg after reset: 0x00020101, cnt=3
Bus Mode Reg after reset: 0x00020101, cnt=4
Bus Mode Reg after reset: 0x00020101, cnt=5
Bus Mode Reg after reset: 0x00020101, cnt=6
Bus Mode Reg after reset: 0x00020101, cnt=7
Bus Mode Reg after reset: 0x00020101, cnt=8
Bus Mode Reg after reset: 0x00020101, cnt=9
func:jz_mii_bus_probe, synopGMAC_reset failed
jz_mii_bus: probe of jz_mii_bus.0 failed with error -1
=======>gmacdev = 0x821b9680<================
=========>gmacdev->MacBase = 0xb34b0000 DmaBase = 0xb34b1000
Bus Mode Reg after reset: 0x00020101, cnt=0
Bus Mode Reg after reset: 0x00020101, cnt=1
Bus Mode Reg after reset: 0x00020101, cnt=2
Bus Mode Reg after reset: 0x00020101, cnt=3
Bus Mode Reg after reset: 0x00020101, cnt=4
Bus Mode Reg after reset: 0x00020101, cnt=5
Bus Mode Reg after reset: 0x00020101, cnt=6
Bus Mode Reg after reset: 0x00020101, cnt=7
Bus Mode Reg after reset: 0x00020101, cnt=8
Bus Mode Reg after reset: 0x00020101, cnt=9
func:jz_mac_probe, synopGMAC_reset failed
jz_mac: probe of jz_mac.0 failed with error -1
usbcore: registered new interface driver zd1201
DWC IN OTG MODE
dwc2 dwc2: Keep PHY ON
dwc2 dwc2: Using Buffer DMA mode
dwc2 dwc2: Core Release: 3.00a
dwc2 dwc2: DesignWare USB2.0 High-Speed Host Controller
dwc2 dwc2: new USB bus registered, assigned bus number 1
hub 1-0:1.0: USB hub found
hub 1-0:1.0: 1 port detected
dwc2 dwc2: DWC2 Host Initialized
jzmmc_v1.2 jzmmc_v1.2.0: vmmc regulator missing
jzmmc_v1.2 jzmmc_v1.2.0: register success!
TCP: cubic registered
NET: Registered protocol family 10
sit: IPv6 over IPv4 tunneling driver
NET: Registered protocol family 17
soc_vpu probe success,version:1.0.0-03203fd46d
input: gpio-keys as /devices/platform/gpio-keys/input/input0
drivers/rtc/hctosys.c: unable to open rtc device (rtc0)
VFS: Mounted root (squashfs filesystem) readonly on device 31:3.
Freeing unused kernel memory: 196K (8041f000 - 80450000)
dwc2 dwc2: ID PIN CHANGED!
usb 1-1: new high-speed USB device number 2 using dwc2
mdev is ok......
ifconfig: SIOCSIFADDR: No such device
XPathFind 260 not found: [1]/HardwareParam/wifiParam/ResetGpio

Usage: json_debug_rootfs -c command {-f Patten-File | [-n Num] -k Key [-v Value] [-t Val-Type]} Json-File

        options:
        -h, --help                 show help
        -i, --inner                writeback to Json-File instead of sdout
        -f, --file                 num-key-value pair records
        -c, --cmd {a|d|w|r}        add del write read
        -n, --num <num>            group number
        -k, --key <key>            node key-path of Json
        -v, --val <val>            node value
        -t, --val type<int|str>    node value tusb 1-1: USB disconnect, device number 2
ype
        _Error_@261
sh: bad number
Wi-Fi ResetGpio is not greater than 0. Exiting.
===wifi_gpio=6===wifi_level=1
wifi_IsConnect no
/etc/ssv6355-wifi-ble.cfg
usb 1-1: new high-speed USB device number 3 using dwc2
exist wifi driver, probe wifi UsbID=Bus 001 Device 003: ID 007a:888b
Bus 001 Device 001: ID 1d6b:0002 SdioID= ...
find usb atbm6012b-x OK
[atbm_log]:platform_init(252)
[atbm_log]:atbm_usb_probe : idVendor[7a] idProduct[888b]
[atbm_log]:AsmLite probe!
[atbm_log]:ble_spin_lock init
[atbm_log]: wait_event_interruptible from  send_prbresp_wq
[atbm_log]:Get 6012B-X UID Success!!support BLE
[atbm_log]:atbm_get_chiptype, chipver=0x4a, g_wifi_chip_type[12]
[atbm_log]:
======>>> load WIFI BLE COMB firmware <<<======

fwhdr->flags 34353678 sram_addr 9009000
[atbm_log]:flush rx[-145][0]
[atbm_log]:wsm_generic_confirm:status(2)
[atbm_log]:<WARNING> wsm_write_mib fail !!! mibId=4132
[atbm_log]:apollo wifi : can't open /data/.mac.info
[atbm_log]:[wlan0] has been disabled
[atbm_log]:[wlan1] has been disabled
[atbm_log]:ble_platform_probe(827e2780)
[atbm_log]:is registered as 'phy0'
[atbm_log]:apollo wifi : can't open /tmp/atbm_txpwer_dcxo_cfg.txt
[atbm_log]:apollo wifi : can't open /tmp/set_rate_power.txt
[atbm_log]:open_auto_cfo:ppm_buf:cfo 1 0 , buf_len:8
[atbm_log]:get chip id [834][10][0]
[atbm_log]:[atbm_wtd]:set wtd_probe = 1
usbcore: registered new interface driver atbm_wlan
/
goahead running ......
system_call_daemon running ......
==> startapp ok
/etc/init.d/rcS: line 252: system_call_daemon: not found
Thu Nov 11 00:00:00 UTC 2021


Jooan login: /mnt/mtd/jzstart.sh: line 59: keyinfo_utils: not found
file /tmp/keyinfo.json is not readable
rm: can't remove '/tmp/keyinfo.json': No such file or directory
Single camera isp.ko
insmod /lib/modules/tx-isp.ko direct_mode=0 isp_memopt=1
@@@@ tx-isp-probe ok(version H20240626a), compiler date=Jul  9 2024 @@@@@
name : i2c0 nr : 0
g_sinfo[i].name is sc1a4t,j is 0
 check_sc1a4t: i2c-w: 0x30-0x3004-0x64
i2c i2c-0: i2c_jz_irq 441, I2C transfer error, ABORT interrupt
i2c i2c-0: --I2C txabrt:
i2c i2c-0: --I2C TXABRT[0]=I2C_TXABRT_ABRT_7B_ADDR_NOACK
error: sensor_write,186 ret = -5
169 sensor_read: addr=0x3107 value = 0xda
g_sinfo[i].name is sc1a4t,j is 1
169 sensor_read: addr=0x3108 value = 0x4d
info: success sensor find : sc1a4t
name : i2c0 nr : 0
g_sinfo[i].name_sub is sc1a4t,j is 0
sub check_sc1a4t: i2c-w: 0x30-0x3004-0x64
i2c i2c-0: i2c_jz_irq 441, I2C transfer error, ABORT interrupt
i2c i2c-0: --I2C txabrt:
i2c i2c-0: --I2C TXABRT[0]=I2C_TXABRT_ABRT_7B_ADDR_NOACK
error: sensor_write,186 ret = -5
i2c i2c-0: i2c_jz_irq 441, I2C transfer error, ABORT interrupt
i2c i2c-0: --I2C txabrt:
i2c i2c-0: --I2C TXABRT[0]=I2C_TXABRT_ABRT_7B_ADDR_NOACK
error: sensor_read,157 ret = -5
169 sensor_read_sub: addr=0x3107 value = 0x0
err sensor_sub read addr = 0x3107, value = 0x0
g_sinfo[i].name_sub is sc2331,j is 0
i2c i2c-0: i2c_jz_irq 441, I2C transfer error, ABORT interrupt
i2c i2c-0: --I2C txabrt:
i2c i2c-0: --I2C TXABRT[0]=I2C_TXABRT_ABRT_7B_ADDR_NOACK
error: sensor_read,157 ret = -5
169 sensor_read_sub: addr=0x3107 value = 0x0
err sensor_sub read addr = 0x3107, value = 0x0
g_sinfo[i].name_sub is sc2336p,j is 0
i2c i2c-0: i2c_jz_irq 441, I2C transfer error, ABORT interrupt
i2c i2c-0: --I2C txabrt:
i2c i2c-0: --I2C TXABRT[0]=I2C_TXABRT_ABRT_7B_ADDR_NOACK
error: sensor_read,157 ret = -5
169 sensor_read_sub: addr=0x3107 value = 0x0
err sensor_sub read addr = 0x3107, value = 0x0
info: failed sensor find
sh: not: unknown operand
sensor2 ================
sensor not found
insmod /lib/modules/sensor_sc1a4t.ko shvflip=1
insmod /lib/modules/sensor_sensor not found.ko shvflip=1
insmod: can't open '/lib/modules/sensor_sensor': No such file or directory
hmaxstep=4100 vmaxstep=1200 vresetstep=600 hgpio1=53 hgpio2=52 hgpio3=54 hgpio4=14 vgpio1=53 vgpmotor_probe1084
io2=52 vgpio3=54 vgpio4=14
init MOTOR SWITCH GPIO,Get motorswitchgpio is 17, get_value is 1
spk_gpio=-1
insmod /lib/modules/audio.ko spk_gpio=-1
pipe_request_dma: paddr = 0x1c80000
dma dma0chan24: Channel 24 have been requested.(phy id 7,type 0x06 desc a1d3d000)
pipe_request_dma: paddr = 0x1cc0000
dma dma0chan25: Channel 25 have been requested.(phy id 6,type 0x06 desc a1c08000)
pipe_request_dma: paddr = 0x1f80000
dma dma0chan26: Channel 26 have been requested.(phy id 5,type 0x04 desc a1d30000)
@@@@@ inner codec power up@@@@@@
@@@@ audio driver ok(version H20230614a) @@@@@
cat: can't open '/tmp/eth_mac': No such file or directory
cat: can't open '/sys/class/net/eth0/address': No such file or directory
ifconfig: SIOCGIFFLAGS: No such device
will sleep 3 seconds
BusyBox v1.22.1 (2023-11-08 14:42:54 CST) multi-call binary.

Usage: ifconfig [-a] interface [address]

Configure a network interface

        [[-]broadcast [ADDRESS]] [[-]pointopoint [ADDRESS]]
        [netmask ADDRESS] [dstaddr ADDRESS]
        [outfill NN] [keepalive NN]
        [hw ether|infiniband ADDRESS] [metric NN] [mtu NN]
        [[-]trailers] [[-]arp] [[-]allmulti]
        [multicast] [[-]promisc] [txqueuelen NN] [[-]dynamic]
        [mem_start NN] [io_addr NN] [irq NN]
        [up|down] ...

ifconfig: SIOCSIFADDR: No such device
eth parter connected
 goahead run ok ======
 kernelinfo run ok ======
 syslogd run ok ======
 My_watch_dog run ok ======
 jooanipc run ok ======
```