Thingino supports a variety of Wyze / Atom / Personal branded Hualai based ODM devices. 

## Supported Features

- **Spotlight Control**: Supported (Note: This is specifically for the spotlight, not the floodlight)
- **Doorbell Chime**: Supported
- **Garage Door Controller**: Not supported yet
- **Floodlight**: Not supported yet

> [!IMPORTANT]
> Beginning with the Wyze Cam Pan 3, Wyze has implemented secure boot on their SoC chips. For more details, please refer to the [Secure Boot](https://github.com/themactep/thingino-firmware/wiki/Supported-Cameras#secure-boot-and-camera-soc-security) section.  

### Installation
Thingino has great support for the Wyze Cam V2 and Wyze Cam V3.

> [!CAUTION]
> If you don't perform a full backup of your camera's flash storage, installation on Wyze devices is a one-way process. Without a backup, you won't be able to restore Wyze services on the device, ever. The flash storage holds your unique information needed to connect to the Wyze cloud.

1. Follow the steps in [Getting Started](https://github.com/themactep/thingino-firmware/wiki/Getting-Started) to install Thingino.
1. Configure the camera with the following settings to best mimic stock behavior by editing ``/etc/prudynt.conf`` and rebooting:
   * Motion Settings:
     * sensitivity: 8

Alternatively, we have personally tested the following devices and can confirm their functionality. The documentation provided below is for reference:

### Device Info

| MODEL     | FCC ID         | PCB VER                           |  SoC  | WIFI             |
|-----------|----------------|-----------------------------------|-------|------------------|
| WYZEC2    | 2ANJHWYZEC2    | 2019-06-38                        | T20X  | SDIO: RTL8189FTV |
| WYZECP1   | 2ANJHHWYZECP1  | DF3-IFPM01 V1.4                   | T20X  | SDIO: RTL8189ES  |
| WYZEC3    | 2AUIUWYZEC3    | WYZEV3_T31GC2053 V1.4_20201010    | T31ZX | SDIO: RTL8189FTV |
| WYZEC3    | 2AUIUWYZEC3A   | WYZEV3_T31GC2053 V1.2_20200715    | T31X  | SDIO: RTL8189FTV |
| WYZEC3    | 2AUIUWYZEC3A   | WYZEV3_T31GC2053 V2.02_20210523   | T31ZX | SDIO: ATBM6031   |
| WYZEC3    | 2AUIUWYZEC3A   | WYZEV3_T31GC2053 V2.03_20211206   | T31X  | SDIO: ATBM6031   |
| WYZEC3    | 2AUIUWYZEC3B   | WYZEV3_T31GC2053 V2.02_20210523   | T31ZX | SDIO: RTL8189FTV |
| WYZEC3    | 2AUIUWYZEC3B   | WYZEV3_T31GC2053 V2.03_20211206   | T31X  | SDIO: RTL8189FTV |
| WYZEC3    | 2AUIUWYZEC3F   | WYZEV3_T31AGC2053 V3.2_20210714   | T31A  | SDIO: ATBM6031   |
| WYZEC3    | 2AUIUWYZEC3F   | WYZEV3_T31AGC2053 V3.2_20210714   | T31A  | SDIO: ATBM6031   |
| WVDBV1    | 2AUIUWVDB1A    | WYZEDB3_MB_T31_2.2                | T31X  | SDIO: RTL8189FTV |
| WYZECP2   | 2AUIUWYZECP2   | DF3-MCU-S01-V2.2                  | T31X  | SDIO: ATBM6031   |
| WYZECPAN3 | 2AUIUWYZECPAN3 | WYZE PAN V3 MB V 1.3              | T31X  | SDIO: ATBM6031   |
| ATOMCAM2  |                | V3C_T31GC2063 V1.1_202001110      | T31ZX | SDIO: ATBM6031   |
| PERSONALCAM  |           |                                | T31X    | SDIO: ATBM6031   |

GPIO:

| MODEL     | IRCUT1 | IRCUT2 | IR LED1 | IR LED2 | WIFI   | LED1   | LED2   | SPEAKER | TF_EN  | TF_CD  | SD_ABLE | SD_PWR |BUTTON1 | BUTTON2 | SUB1G  | USB    |
|-----------|--------|--------|---------|---------|--------|--------|--------|---------|--------|--------|---------|--------|--------|---------|--------|--------|
| WYZEC2    | GPIO25 | GPIO26 | GPIO49  |         | GPIO62 | GPIO38 | GPIO39 | GPIO63  | GPIO54 | GPIO48 | GPIO47  |        | GPIO46 |         |        | GPIO47 |
| WYZECP1   | GPIO26 | GPIO25 | GPIO49  |         | GPIO62 | GPIO38 | GPIO39 | GPIO63  | GPIO54 | GPIO48 | GPIO47  |        | GPIO46 |         |        | GPIO47 |
| WYZEC3    | GPIO53 | GPIO52 | GPIO47  | GPIO49  | GPIO57 | GPIO38 | GPIO39 | GPIO63  | GPIO50 | GPIO62 | GPIO48  |        | GPIO51 |         |        |        |
| WYZEDBV1  | GPIO53 | GPIO52 | PWM2    |         | GPIO57 | GPIO38 | GPIO39 | GPIO58  |        |        | GPIO62  |        | GPIO06 | GPIO07  | GPIO61 |        |
| WYZECP2   | GPIO49 | GPIO50 | GPIO60  |         | GPIO58 | GPIO38 | GPIO39 | GPIO07  | GPIO47 | GPIO48 | GPIO54  |        | GPIO06 |         |        |        |
| WYZECPAN3 |        |        |         |         |        |        |        |         |        |        |         |        |        |         |        |        |
| WYZEC3PRO | GPIO118| GPIO119| GPIO66  | GPIO67  | GPIO57 | GPIO105| GPIO106| GPIO63  | GPIO58 | GPIO70 | GPIO71  | GPIO121| GPIO107|         |        |        |
| WVOD2     |        |        |         |         |        |        |        |         |        |        |         |        |        |         |        |        |
| ATOMCAM2  | GPIO53 | GPIO52 | GPIO26  |         | GPIO57 | GPIO38 | GPIO39 | GPIO63  | GPIO50 | GPIO59 | GPIO48  |        | GPIO51 |         |        | GPIO47 |
| PERSONALCAM  |        |        | GPIO14  |         | GPIO57 | GPIO47 | GPIO48 | GPIO63  | GPIO50 | GPIO59 | GPIO39  |        |        |         |        |        |

MOTORS: 
| MODEL     | HST1   | HST2   | HST3   | HST4   | VST1   | VST2   | VST3   | VST4   | HMAX | VMAX  | MAX SPEED |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|------|-------|-----------|
| WYZECP1   | GPIO54 | GPIO53 | GPIO52 | GPIO51 | GPIO75 | GPIO76 | GPIO79 | GPIO80 | 2590 | 720   | 900       |
| WYZECP2   | GPIO52 | GPIO53 | GPIO57 | GPIO51 | GPIO59 | GPIO61 | GPIO62 | GPIO63 | 2540 | 720   | 900       |
| WYZECPAN3 | GPIO52 | GPIO53 | GPIO57 | GPIO51 | GPIO59 | GPIO61 | GPIO62 | GPIO63 | 3050 | 1550   | 900       |
| PERSONALCAM | GPIO49 | GPIO57 | GPIO54 | GPIO51 | GPIO60 | GPIO61 | GPIO62 | GPIO63 | 2130 | 1600  | 900       |
