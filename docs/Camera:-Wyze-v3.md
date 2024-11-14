# Hardware Identification
The Wyze v3 camera has multiple "flavors" of hardware; each with its own image.  

The `FCC ID` on the label may be used to identify the correct image.  Full detail list here: https://github.com/OpenIPC/wiki/blob/master/en/device-wyze-integration.md#wyze-integration

# General Tooling and Resources
* [Sample camera breakdown](https://github.com/themactep/thingino-firmware/wiki/Hardware-Identification)
* [Ingenic USB Cloner](https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner)
  *  [Flashing with Cloner (video)](https://www.youtube.com/watch?v=SJgadXkdwzw)
* [Camera disassembly (video)](https://www.youtube.com/watch?v=VUTTJREU3mI)

# LED states throughout boot process
##  Immediately after power
1. 4 visible IR LEDs illuminate dimly (very short blink)
2. all LEDs off
3. 4 visible IR LEDs illuminate brighter (very short blink)
## After IR LED sequence
### Boot Failed
* Solid blue LED
- possibly corrupt bootloader or system image

### Thingino Booting
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



