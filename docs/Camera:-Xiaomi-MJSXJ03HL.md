## Installation

You can choose between:
1. Quick installation method, which doesn't require dismantling the camera, and doesn't backup the original firmware
2. Safe installation, which requires camera dismantling. Allows full backup of original firmware, and recovery from corrupted flash

### Quick method

See: https://github.com/Andrik45719/MJSXJ03HL

### Safe method

First, dismantle camera to access flash chip:
- Gently warm up the front of the camera (where the lens is). See pictures below.
- Using a utility knife or other pointed object, carefully pry off the front part. Remember, there are important wires under the front, don't damage them!
- After the front part is removed, unscrew 2 screws holding the two halves of the camera together

Then use either cloner or CH341 to backup and reprogram flash:
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

## Pictures

<img src="https://github.com/user-attachments/assets/a60d8dbf-feec-497a-a68e-96791b409b19" width="400">

<img src="https://github.com/user-attachments/assets/1f3e9eeb-0532-416f-8578-3aebc807c2b3" width="400">

<img src="https://github.com/user-attachments/assets/16f16504-a88d-496c-956b-b540f1ab79bd" width="400">

<img src="https://github.com/user-attachments/assets/83dae7df-befa-4327-b63d-d375b20bdeb1" width="400">


## Logs

### Vendor uboot log

```
U-Boot SPL 2013.07-g8581847-dirty (Aug 09 2021 - 18:07:12)
Timer init
CLK stop
PLL init
pll_init:366
pll_cfg.pdiv = 10, pll_cfg.h2div = 5, pll_cfg.h0div = 5, pll_cfg.cdiv = 1, pll_cfg.l2div = 2
nf=84 nr = 1 od0 = 1 od1 = 2
cppcr is 05405100
CPM_CPAPCR 0540510d
nf=100 nr = 1 od0 = 1 od1 = 2
cppcr is 06405100
CPM_CPMPCR 0640510d
nf=100 nr = 1 od0 = 1 od1 = 2
cppcr is 06405100
CPM_CPVPCR 0640510d
cppcr 0x9a7b5510
apll_freq 1008000000 
mpll_freq 1200000000 
vpll_freq = 1200000000
ddr sel mpll, cpu sel apll
ddrfreq 600000000
cclk  1008000000
l2clk 504000000
h0clk 240000000
h2clk 240000000
pclk  120000000
CLK init
SDRAM init
sdram init start
ddr_inno_phy_init ..!
phy reg = 0x00000007, CL = 0x00000007
ddr_inno_phy_init ..! 11:  00000004
ddr_inno_phy_init ..! 22:  00000006
ddr_inno_phy_init ..! 33:  00000006
REG_DDR_LMR: 00000210
REG_DDR_LMR: 00000310
REG_DDR_LMR: 00000110
REG_DDR_LMR, MR0: 00f73011
T31_0x5: 00000007
T31_0x15: 0000000c
T31_0x4: 00000000
T31_0x14: 00000002
INNO_TRAINING_CTRL 1: 00000000
INNO_TRAINING_CTRL 2: 000000a1
T31_cc: 00000003
INNO_TRAINING_CTRL 3: 000000a0
T31_118: 0000003c
T31_158: 0000003c
T31_190: 0000001e
T31_194: 0000001c
jz-04 :  0x00000051 
jz-08 :  0x000000a0 
jz-28 :  0x00000024 
DDR PHY init OK
INNO_DQ_WIDTH   :00000003
INNO_PLL_FBDIV  :00000014
INNO_PLL_PDIV   :00000005
INNO_MEM_CFG    :00000051
INNO_PLL_CTRL   :00000018
INNO_CHANNEL_EN :0000000d
INNO_CWL        :00000006
INNO_CL         :00000007
DDR Controller init
DDRC_STATUS         0x80000001
DDRC_CFG            0x0a288a40
DDRC_CTRL           0x0000011c
DDRC_LMR            0x00400008
DDRC_DLP            0x00000000
DDRC_TIMING1        0x050f0a06
DDRC_TIMING2        0x021c0807
DDRC_TIMING3        0x20080723
DDRC_TIMING4        0x1f240031
DDRC_TIMING5        0xff060405
DDRC_TIMING6        0x321c0505
DDRC_REFCNT         0x00918403
DDRC_MMAP0          0x000020fc
DDRC_MMAP1          0x00002400
DDRC_REMAP1         0x03020d0c
DDRC_REMAP2         0x07060504
DDRC_REMAP3         0x0b0a0908
DDRC_REMAP4         0x0f0e0100
DDRC_REMAP5         0x13121110
DDRC_AUTOSR_EN      0x00000000
sdram init finished
SDRAM init ok
board_init_r
image entry point: 0x80100000


U-Boot 2013.07-g8581847-dirty (Aug 09 2021 - 18:07:12)

Board: ISVP (Ingenic XBurst T31 SoC)
DRAM:  64 MiB
Top of RAM usable for U-Boot at: 84000000
Reserving 436k for U-Boot at: 83f90000
Reserving 32772k for malloc() at: 81f8f000
Reserving 32 Bytes for Board Info at: 81f8efe0
Reserving 124 Bytes for Global Data at: 81f8ef64
Reserving 128k for boot params() at: 81f6ef64
Stack Pointer at: 81f6ef48
Now running in RAM - U-Boot at: 83f90000
MMC:   msc: 0
the manufacturer ef
SF: Detected W25Q128

*** Warning - bad CRC, using default environment

In:    serial
Out:   serial
Err:   serial
misc_init_r before change the wifi_enable_gpio
gpio_request lable = wifi_enable_gpio gpio = 58
misc_init_r after gpio_request the wifi_enable_gpio ret is 58
misc_init_r after change the wifi_enable_gpio ret is 0
misc_init_r before change the yellow_gpio
gpio_request lable = yellow_gpio gpio = 39
misc_init_r after gpio_request the yellow_gpio ret is 39
misc_init_r after change the yellow_gpio ret is 1
misc_init_r before change the blue_gpio
gpio_request lable = blue_gpio gpio = 38
misc_init_r after gpio_request the blue_gpio ret is 38
misc_init_r after change the blue_gpio ret is 0
gpio_request lable = night_gpio gpio = 60
misc_init_r after gpio_request the night_gpio ret is 60
misc_init_r after change the night_gpio ret is 0
gpio_request lable = SPK_able_gpio gpio = 63
misc_init_r after gpio_request the SPK_able_gpio ret is 63
misc_init_r after change the SPK_able_gpio ret is 0
gpio_request lable = TF_en_gpio gpio = 47
misc_init_r after gpio_request the TF_en_gpio ret is 47
misc_init_r after change the TF_en_gpio ret is 0
gpio_request lable = TF_cd_gpio gpio = 48
misc_init_r after gpio_request the TF_cd_gpio ret is 48
misc_init_r after change the TF_cd_gpio ret is 1
gpio_request lable = SD_able_gpio gpio = 54
misc_init_r after change the SD_able_gpio ret is 1
misc_init_r before change the wifi_enable_gpio
gpio_request lable = wifi_enable_gpio gpio = 58
misc_init_r after gpio_request the wifi_enable_gpio ret is 58
misc_init_r after change the wifi_enable_gpio ret is 1
Hit any key to stop autoboot:  0 
Card did not respond to voltage select!
SD card is not insert
gpio_request lable = sdupgrade gpio = 51
the manufacturer ef
SF: Detected W25Q128

The upgrade flag could not be found!
the manufacturer ef
SF: Detected W25Q128

--->probe spend 4 ms
SF: 2031616 bytes @ 0x40000 Read: OK
--->read spend 653 ms
## Booting kernel from Legacy Image at 80600000 ...
   Image Name:   Linux-3.10.14__isvp_swan_1.0__
   Image Type:   MIPS Linux Kernel Image (lzma compressed)
   Data Size:    1590203 Bytes = 1.5 MiB
   Load Address: 80010000
   Entry Point:  80367840
   Verifying Checksum ... OK
   Uncompressing Kernel Image ... OK

Starting kernel ...
```

### Vendor kernel log

```
[    0.000000] Initializing cgroup subsys cpu
[    0.000000] Initializing cgroup subsys cpuacct
[    0.000000] Linux version 3.10.14__isvp_swan_1.0__ (xuxuequan@ubuntu) (gcc version 4.7.2 (Ingenic r2.3.3 2016.12) ) #0 PREEMPT Mon Jul 12 02:36:24 CST 2021
[    0.000000] bootconsole [early0] enabled
[    0.000000] CPU0 RESET ERROR PC:00404E1C
[    0.000000] CPU0 revision is: 00d00100 (Ingenic Xburst)
[    0.000000] FPU revision is: 00b70000
[    0.000000] CCLK:1008MHz L2CLK:504Mhz H0CLK:200MHz H2CLK:200Mhz PCLK:100Mhz
[    0.000000] Determined physical RAM map:
[    0.000000]  memory: 00473000 @ 00010000 (usable)
[    0.000000]  memory: 0002d000 @ 00483000 (usable after init)
[    0.000000] User-defined physical RAM map:
[    0.000000]  memory: 02a00000 @ 00000000 (usable)
[    0.000000] Zone ranges:
[    0.000000]   Normal   [mem 0x00000000-0x029fffff]
[    0.000000] Movable zone start for each node
[    0.000000] Early memory node ranges
[    0.000000]   node   0: [mem 0x00000000-0x029fffff]
[    0.000000] Primary instruction cache 32kB, 8-way, VIPT, linesize 32 bytes.
[    0.000000] Primary data cache 32kB, 8-way, VIPT, no aliases, linesize 32 bytes
[    0.000000] pls check processor_id[0x00d00100],sc_jz not support!
[    0.000000] MIPS secondary cache 128kB, 8-way, linesize 32 bytes.
[    0.000000] Built 1 zonelists in Zone order, mobility grouping off.  Total pages: 10668
[    0.000000] Kernel command line: console=ttyS1,115200n8 mem=42M@0x0 rmem=22M@0x2A00000 init=/linuxrc rootfstype=squashfs root=/dev/mtdblock2 rw mtdparts=jz_sfc:256K(boot),1984K(kernel),3904K(rootfs),3904K(app),1984K(kback),3904K(aback),384K(cfg),64K(para)
[    0.000000] PID hash table entries: 256 (order: -2, 1024 bytes)
[    0.000000] Dentry cache hash table entries: 8192 (order: 3, 32768 bytes)
[    0.000000] Inode-cache hash table entries: 4096 (order: 2, 16384 bytes)
[    0.000000] Memory: 37216k/43008k available (3456k kernel code, 5792k reserved, 1098k data, 180k init, 0k highmem)
[    0.000000] SLUB: HWalign=32, Order=0-3, MinObjects=0, CPUs=1, Nodes=1
[    0.000000] Preemptible hierarchical RCU implementation.
[    0.000000] NR_IRQS:358
[    0.000000] clockevents_config_and_register success.
[    0.000018] Calibrating delay loop... 1001.88 BogoMIPS (lpj=5009408)
[    0.037791] pid_max: default: 32768 minimum: 301
[    0.042706] Mount-cache hash table entries: 512
[    0.047728] Initializing cgroup subsys debug
[    0.051986] Initializing cgroup subsys freezer
[    0.058588] regulator-dummy: no parameters
[    0.062808] NET: Registered protocol family 16
[    0.079039] bio: create slab <bio-0> at 0
[    0.084968] jz-dma jz-dma: JZ SoC DMA initialized
[    0.090040] usbcore: registered new interface driver usbfs
[    0.095590] usbcore: registered new interface driver hub
[    0.101020] usbcore: registered new device driver usb
[    0.106238]  (null): set:249  hold:250 dev=100000000 h=500 l=500
[    0.112344]  (null): set:61  hold:62 dev=100000000 h=125 l=125
[    0.118290] media: Linux media interface: v0.10
[    0.122841] Linux video capture interface: v2.00
[    0.129304] Switching to clocksource jz_clocksource
[    0.134758] jz-dwc2 jz-dwc2: cgu clk gate get error
[    0.139727] cfg80211: Calling CRDA to update world regulatory domain
[    0.146169] DWC IN OTG MODE
[    0.149576] dwc2 dwc2: Keep PHY ON
[    0.152944] dwc2 dwc2: Using Buffer DMA mode
[    0.157298] dwc2 dwc2: Core Release: 3.00a
[    0.161455] dwc2 dwc2: DesignWare USB2.0 High-Speed Host Controller
[    0.167807] dwc2 dwc2: new USB bus registered, assigned bus number 1
[    0.174803] usb usb1: New USB device found, idVendor=1d6b, idProduct=0002
[    0.181616] usb usb1: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    0.188980] usb usb1: Product: DesignWare USB2.0 High-Speed Host Controller
[    0.196020] usb usb1: Manufacturer: Linux 3.10.14__isvp_swan_1.0__ dwc2-hcd
[    0.203069] usb usb1: SerialNumber: dwc2
[    0.207390] hub 1-0:1.0: USB hub found
[    0.211120] hub 1-0:1.0: 1 port detected
[    0.215316] dwc2 dwc2: DWC2 Host Initialized
[    0.219767] NET: Registered protocol family 2
[    0.224677] TCP established hash table entries: 512 (order: 0, 4096 bytes)
[    0.231596] TCP bind hash table entries: 512 (order: -1, 2048 bytes)
[    0.238071] TCP: Hash tables configured (established 512 bind 512)
[    0.244358] TCP: reno registered
[    0.247565] UDP hash table entries: 256 (order: 0, 4096 bytes)
[    0.253490] UDP-Lite hash table entries: 256 (order: 0, 4096 bytes)
[    0.260094] NET: Registered protocol family 1
[    0.264472] dwc2 dwc2: ID PIN CHANGED!
[    0.268660] freq_udelay_jiffys[0].max_num = 10
[    0.273088] cpufreq  udelay  loops_per_jiffy
[    0.277546] 12000     59635   59635
[    0.280769] 24000     119271  119271
[    0.284224] 60000     298179  298179
[    0.287656] 120000    596358  596358
[    0.291188] 200000    993930  993930
[    0.294730] 300000    1490895         1490895
[    0.298428] 600000    2981790         2981790
[    0.302136] 792000    3935963         3935963
[    0.305854] 1008000   5009408         5009408
[    0.309640] 1200000   5963580         5963580
[    0.318433] squashfs: version 4.0 (2009/01/31) Phillip Lougher
[    0.324518] jffs2: version 2.2. © 2001-2006 Red Hat, Inc.
[    0.330336] msgmni has been set to 72
[    0.335016] io scheduler noop registered
[    0.338944] io scheduler cfq registered (default)
[    0.345247] jz-uart.1: ttyS1 at MMIO 0x10031000 (irq = 58) is a uart1
[    0.353182] console [ttyS1] enabled, bootconsole disabled
[    0.353182] console [ttyS1] enabled, bootconsole disabled
[    0.367841] brd: module loaded
[    0.372776] loop: module loaded
[    0.376802] zram: Created 2 device(s) ...
[    0.381016] logger: created 256K log 'log_main'
[    0.386318] jz TCU driver register completed
[    0.391089] the id code = ef4018, the flash name is WIN25Q128
[    0.397096] JZ SFC Controller for SFC channel 0 driver register
[    0.403234] 8 cmdlinepart partitions found on MTD device jz_sfc
[    0.409384] Creating 8 MTD partitions on "jz_sfc":
[    0.414377] 0x000000000000-0x000000040000 : "boot"
[    0.419846] 0x000000040000-0x000000230000 : "kernel"
[    0.425508] 0x000000230000-0x000000600000 : "rootfs"
[    0.431098] 0x000000600000-0x0000009d0000 : "app"
[    0.436488] 0x0000009d0000-0x000000bc0000 : "kback"
[    0.441977] 0x000000bc0000-0x000000f90000 : "aback"
[    0.447534] 0x000000f90000-0x000000ff0000 : "cfg"
[    0.452848] 0x000000ff0000-0x000001000000 : "para"
[    0.458311] SPI NOR MTD LOAD OK
[    0.461623] tun: Universal TUN/TAP device driver, 1.6
[    0.466880] tun: (C) 1999-2004 Max Krasnyansky <maxk@qualcomm.com>
[    0.473382] usbcore: registered new interface driver zd1201
[    0.479289] usbcore: registered new interface driver usbserial
[    0.485384] usbcore: registered new interface driver ch341
[    0.491090] usbserial: USB Serial support registered for ch341-uart
[    0.497618] usbcore: registered new interface driver usb_debug
[    0.503670] usbserial: USB Serial support registered for debug
[    0.509740] usbcore: registered new interface driver pl2303
[    0.515538] usbserial: USB Serial support registered for pl2303
[    0.521660] i2c /dev entries driver
[    0.525690] jzmmc_v1.2 jzmmc_v1.2.0: vmmc regulator missing
[    0.531794] jzmmc_v1.2 jzmmc_v1.2.0: register success!
[    0.537246] jzmmc_v1.2 jzmmc_v1.2.1: vmmc regulator missing
[    0.543164] jzmmc_v1.2 jzmmc_v1.2.1: register success!
[    0.548787] TCP: cubic registered
[    0.552219] NET: Registered protocol family 17
[    0.557618] input: gpio-keys as /devices/platform/gpio-keys/input/input0
[    0.564768] drivers/rtc/hctosys.c: unable to open rtc device (rtc0)
[    0.576456] VFS: Mounted root (squashfs filesystem) readonly on device 31:2.
[    0.584036] Freeing unused kernel memory: 180K (80483000 - 804b0000)
mdev is ok......
[    1.127731] jffs2: Node at 0x00007958 with length 0x00000bff would run over the end of the erase block
[    1.137481] jffs2: Perhaps the file system was created with the wrong erase size?
[    1.145257] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x0000795c: 0x0bff instead
[    1.155089] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x00007960: 0xdd67 instead
[    1.164913] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x00007964: 0x000d instead
[    1.174729] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x00007968: 0x0009 instead
[    1.184543] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x0000796c: 0x81fd instead
[    1.194355] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x00007970: 0x03e8 instead
[    1.204158] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x00007974: 0x6ff8 instead
[    1.213969] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x00007978: 0xd534 instead
[    1.223782] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x0000797c: 0xd534 instead
[    1.233595] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x00007980: 0xd534 instead
[    1.243403] jffs2: Further such events for this erase block will not be printed
[    1.251203] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x00008000: 0x22ae instead
[    1.261024] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x00008004: 0xe117 instead
[    1.270875] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x00008008: 0x7e11 instead
[    1.280694] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x0000800c: 0x7df0 instead
[    1.290508] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x00008010: 0xb423 instead
[    1.300321] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x00008014: 0x75cf instead
[    1.310133] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x00008018: 0x410d instead
[    1.319946] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x0000801c: 0xf0aa instead
[    1.329757] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x00008020: 0xce52 instead
[    1.339569] jffs2: jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x00008024: 0xc9ec instead
[    1.349377] jffs2: Further such events for this erase block will not be printed
[    1.440700] exFAT: Version 1.2.9
[    1.474782] jz_codec_register: probe() successful!
[    1.884463] dma dma0chan24: Channel 24 have been requested.(phy id 7,type 0x06 desc a1817000)
[    1.893634] dma dma0chan25: Channel 25 have been requested.(phy id 6,type 0x06 desc a27e0000)
[    1.902912] dma dma0chan26: Channel 26 have been requested.(phy id 5,type 0x04 desc a27ea000)
[    1.955109] jz_pwm_probe[212] d_name = tcu_chn0
[    1.961923] The version of PWM driver is H20180309a
[    1.974047] request pwm channel 0 successfully
[    1.981097] pwm-jz pwm-jz: jz_pwm_probe register ok !
[    2.312105] RTL871X: module init start
[    2.316083] RTL871X: rtl8189ftv v4.3.24.7_21113.20170208.nova.1.02
[    2.322480] RTL871X: build time: Aug 14 2020 13:46:20
[    2.327786] wlan power on
[    2.344641] RTL871X: module init ret=0
[    2.390089] mmc1: card claims to support voltages below the defined range. These will be ignored.
[    2.425035] mmc1: new SDIO card at address 0001
[    2.436291] RTL871X: ++++++++rtw_drv_init: vendor=0x024c device=0xf179 class=0x07
[    2.490306] RTL871X: HW EFUSE
[    2.493398] RTL871X: hal_com_config_channel_plan chplan:0x20
[    2.679364] RTL871X: rtw_regsty_chk_target_tx_power_valid return _FALSE for band:0, path:0, rs:0, t:-1
[    2.706802] RTL871X: rtw_ndev_init(wlan0) if1 mac_addr=c8:5c:cc:93:22:96
[    2.803476] @@@@ tx-isp-probe ok(version H20210112a), compiler date=Jan 12 2021 @@@@@
[    2.815241] zram0: detected capacity change from 0 to 16777216
Setting up swapspace version 1, size = 16773120 bytes
UUID=1903dcaa-6bab-48b3-996c-9[    2.828234] Adding 16380k swap on /dev/zram0.  Priority:-1 extents:1 across:16380k SS
ebe6ff470a3
[FC] step1 export sd power and en
[FC] step2 poweron sd card
[    3.164210] jzmmc_v1.2 jzmmc_v1.2.0: card inserted, state=0
[FC] step3 trigger cd pin
mount: mounting /dev/mmcblk0 on /media/mmc failed: No such file or directory

===========welcome to assis process=========
[Build date] Oct  4 2021 (09:08:09)
[exec-assis,0144]msgSndId:0
[exec-assis,0159]msgRcvId:32769
[SDK-DOG]dbg: turn on watchdog success!

===========welcome to iCamera_app===========
[Build date] Oct  4 2021 (09:08:10)
[msg:79]log: msg_queue_create() ok  MsgId:65538
[sdevice_not_work_set_callback]dbg: set ok! have 1 cb
[sdevice_can_work_set_callback]dbg: set ok! have 1 cb
init_log_module() ok
[sdevice_can_work_set_callback]dbg: set ok! have 2 cb
[exec-iCame,0144]msgSndId:0
[exec-iCame,0159]msgRcvId:32769
[timer,144]dbg: init complete.
open gpio direction: No such file or directory
[    9.420662] name : i2c0 nr : 0
[    9.504378] error: sensor_read,291 ret = -5
[    9.508733]  sensor_read: addr=0x3107 value = 0x0
[    9.513592] err sensor read addr = 0x3107, value = 0x0
[    9.604373] error: sensor_read,291 ret = -5
[    9.608700]  sensor_read: addr=0xf0 value = 0x0
[    9.613544] err sensor read addr = 0xf0, value = 0x0
[    9.618714] jzmmc_v1.2 jzmmc_v1.2.0: card removed, state=0
[    9.714704]  sensor_read: addr=0xa value = 0x8
[    9.804698]  sensor_read: addr=0xa value = 0x8
[    9.894696]  sensor_read: addr=0xa value = 0x8
[    9.899801]  sensor_read: addr=0xb value = 0x43
[    9.904532] info: success sensor find : jxq03p
[    9.909128] name : i2c1 nr : 1
[    9.912300] misc sinfo_release
[   10.054698] -----jxq03p_detect: 589 ret = 0, v = 0x08
[   10.060431] -----jxq03p_detect: 597 ret = 0, v = 0x43
[   10.065838] jxq03p chip found @ 0x40 (i2c0)
[   10.070206] sensor driver version H20200930b
[   10.277969] jxq03p stream on
---- FPGA board is ready ----
  Board UID : 30AB6E51
  Board HW ID : 72000460
  Board rev.  : 5DE5A975
  Board date  : 20190326
-----------------------------
[   10.874247] codec_set_device: set device: MIC...
[   11.194275] codec_set_device: set device: speaker...
[   11.200831] SPEAKER CTL MODE1 !
up
[   14.071537] SPEAKER CTL MODE1 !
[   18.105018] SPEAKER CTL MODE0 !
[   18.672243] SPEAKER CTL MODE1 !
killall: miio_client: no process killed
killall: miio_client_helper_nomqtt.sh: no process killed
killall: wifi_start.sh: no process killed
Jan  1 08:00:19 miio_client[272]: [W] miio_client: version: miio-client 4.1.6 (main,277)
Jan  1 08:00:19 miio_client[274]: [W] internal: handle_internal_hello, fd: 7, STATE: (0) (handle_internal_hello,2211)
Jan  1 08:00:19 miio_client[274]: [W] internal: cmd_internal_response_dinfo:1846 STATE: [STATE_DEVICE_INIT] -> [STATE_DIDKEY_DONE] (_set_conn_state,540)
Jan  1 08:00:19 miio_client[274]: [W] internal: handle_internal_hello, fd: 12, STATE: (3) (handle_internal_hello,2211)
Jan  1 08:00:19 miio_client[274]: [W] internal: ssid not string (cmd_internal_response_ot_config,1958)
Jan  1 08:00:19 miio_client[274]: [W] internal: password not string (cmd_internal_response_ot_config,1981)
Jan  1 08:00:19 miio_client[274]: [W] internal: country not string (cmd_internal_response_ot_config,2003)
Jan  1 08:00:19 miio_client[274]: [W] internal: uid not int (cmd_internal_response_ot_config,2026)
Jan  1 08:00:19 miio_client[274]: [W] internal: cmd_internal_response_ot_config:2035 STATE: [STATE_DIDKEY_DONE] -> [STATE_OT_CONFIG_DONE] (_set_conn_state,540)
Jan  1 08:00:19 miio_client[274]: [W] internal: handle_internal_hello, fd: 8, STATE: (4) (handle_internal_hello,2211)
Jan  1 08:00:19 miio_client[274]: [W] internal: cmd_internal_res_wifi_conf_status:644 STATE: [STATE_OT_CONFIG_DONE] -> [STATE_WIFI_AP_MODE] (_set_conn_state,540)
Jan  1 08:00:19 miio_client[274]: [W] internal: wifi enter AP mode (cmd_internal_res_wifi_conf_status,646)
Jan  1 08:00:19 miio_client[274]: [W] miio_client: miio_common init (main,336)
Jan  1 08:00:19 miio_client[274]: [W] internal: handle_internal_hello, fd: 8, STATE: (6) (handle_internal_hello,2211)
Jan  1 08:00:19 miio_client[274]: [W] internal: handle_internal_hello:2271 STATE: [STATE_WIFI_AP_MODE] -> [STATE_WIFI_MODE_MONITOR] (_set_conn_state,540)
killall: wpa_supplicant: no process killed
killall: udhcpc: no process killed
killall: udhcpd: no process killed
killall: hostapd: no process killed
killall: telnetd: no process killed
down
[   20.415078] SPEAKER CTL MODE0 !
up
Configuration file: /tmp/hostapd_wpa2.conf
rfkill: Cannot open RFKILL control device
nl80211: Could not re-add multicast membership for vendor events: -2 (No such file or directory)
Using interface wlan0 with hwaddr e4:aa:ec:9c:c2:00 and ssid "isa-camera-hlc7_miapC200"
[   21.605619] RTL871X: assoc success
wlan0: interface state UNINITIALIZED->ENABLED
wlan0: AP-ENABLED 
[   28.780798] SPEAKER CTL MODE1 !
[assis]WDG_CMD_FEED_DOG!!!!
[   30.525009] SPEAKER CTL MODE0 !
[   38.887856] SPEAKER CTL MODE1 !
[   40.625019] SPEAKER CTL MODE0 !
[   48.998751] SPEAKER CTL MODE1 !
[   50.735091] SPEAKER CTL MODE0 !
[   59.106661] SPEAKER CTL MODE1 !
[assis]WDG_CMD_FEED_DOG!!!!
[   60.855023] SPEAKER CTL MODE0 !
[   69.214791] SPEAKER CTL MODE1 !
[   70.965059] SPEAKER CTL MODE0 !
[   79.330846] SPEAKER CTL MODE1 !
[   81.075021] SPEAKER CTL MODE0 !
[   89.451911] SPEAKER CTL MODE1 !
[assis]WDG_CMD_FEED_DOG!!!!
[   91.195015] SPEAKER CTL MODE0 !
```
