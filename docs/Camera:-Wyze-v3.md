# Hardware Identification
The Wyze v3 camera has multiple "flavors" of hardware; each with its own image.  

The `FCC ID` on the label may be used to identify the correct image.  Full detail list here: 
https://github.com/themactep/thingino-firmware/wiki/Camera:-Hualai-(Wyze,-Atom,-Neos,-Personal)#device-info  )  

# General Tooling and Resources
* [Automatic no-tools installer](https://youtu.be/3ajS7Xzlmis) (video walk through)
* [Non-Intrusive Installer](https://thingino.com/wyze-c3)
* [Sample camera breakdown](https://github.com/themactep/thingino-firmware/wiki/Hardware-Identification)
* [Ingenic USB Cloner](https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner)
  *  [Flashing with Cloner (video)](https://www.youtube.com/watch?v=SJgadXkdwzw)
* [Camera disassembly (video)](https://www.youtube.com/watch?v=VUTTJREU3mI)
* [wltechblog Installation Guide](https://github.com/wltechblog/thingino-installers/tree/main/wyze-cam-3)

# LED states throughout boot process
##  Immediately after power
1. 4 visible IR LEDs illuminate dimly (very short blink)
2. all LEDs off

## Bootloader
Both the Wyze factory image and Thingino use `uBoot` as a bootloader; however, the Wyze factory version is locked-down. 
[uBoot Cheetsheet](https://github.com/themactep/thingino-firmware/wiki/U%E2%80%90Boot-Cheatsheet)

After initial power-on, the camera may be in one of these states:

### Entered Bootloader
1. 4 visible IR LEDs illuminate brighter (very short blink)
2. After blink, LEDs are off and control passes to thingino

### Failed to Enter bootloader
1. all LEDs off (in Cloner mode)

### Bootloader Errors
* Solid blue led 
  *  15 seconds - SD card inserted (with or without `autoupdate-full.bin`)
  *  22 seconds - No SD card inserted
* Off for ~0.5 second

## Thingino Booting
1. All LEDs off (about 5-10 seconds)
2. Blue LED fast blinking: failsafe mode (about 5-10 seconds)
3. Blue LED slow blinking: loading init scripts (about 20-30 seconds)

# Troubleshooting

## Scenario: "Camera is Dead"

### Unknown Case A: (TBD)
#### Symptoms:
* IR LEDs illuminate immediately at boot
* Blue LED remains illuminated solidly 

#### Resolution: (TBD)
* [Re-flash the camera with `autoupdate-full.bin`](https://github.com/themactep/thingino-firmware/wiki/Automation#upgrade-from-binary-images-on-sd-card)
  * Failed

## Remediation: Cloner:
You generally should not need to use Cloner with the Wyze v3, since a bootloader failure *should* force the camera into Cloner mode.

[Realtime video](https://www.youtube.com/watch?v=SJgadXkdwzw)

1. Identify these pins for shorting
![image](https://github.com/user-attachments/assets/9d027e16-2eaa-43d2-86e6-d2e50ab5e0bf)

2. Launch Cloner
  a. Follow the instructions at https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner#writing-firmware
  b. Should look like:
![image](https://github.com/user-attachments/assets/32c69808-49a9-4e59-a912-0cdbb238460c)



