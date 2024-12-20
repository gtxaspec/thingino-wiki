# Hardware Identification
The Wyze v3 camera has multiple "flavors" of hardware; each with its own image.  

The `FCC ID` on the label may be used to identify the correct image.  Full detail list here: 
https://github.com/themactep/thingino-firmware/wiki/Camera:-Hualai-(Wyze,-Atom,-Neos,-Personal)#device-info  )  

# General Tooling and Resources
* [wltechblog Automatic no-tools installer](https://youtu.be/3ajS7Xzlmis) (video walk through)
* [wltechblog Installation Guide](https://github.com/wltechblog/thingino-installers/tree/main/wyze-cam-3)
* [Non-Intrusive Installer](https://thingino.com/wyze-c3)
* [Sample camera breakdown](https://github.com/themactep/thingino-firmware/wiki/Hardware-Identification)
* [Ingenic USB Cloner](https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner)
  *  [Flashing with Cloner (video)](https://www.youtube.com/watch?v=SJgadXkdwzw)
* [Camera disassembly (video)](https://www.youtube.com/watch?v=VUTTJREU3mI)
* [WiFi Tips and Tricks](https://github.com/themactep/thingino-firmware/wiki/WiFi-Tips-and-Tricks#my-mac-address-has-changed)
* [Frigate Integration](https://github.com/themactep/thingino-firmware/wiki/Integration:-Frigate)

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

## USB NIC Disconnects:
The Wyze v3 supports USB OTG (On The Go), so hardwired NICs can offer better reliability than 2.4GhZ WiFi.
However, there have been some cases of USB NICs disconnecting.

An open discussion thread exists for this at: https://github.com/themactep/thingino-firmware/discussions/335

`dmesg` output for this issue will look something like this:
```
[49525.142850] hub 1-0:1.0: state 7 ports 1 chg 0000 evt 0002
[49525.142897] hub 1-0:1.0: port 1, status 0000, change 0003, 12 Mb/s
[49525.142912] usb 1-1: USB disconnect, device number 14
[49525.142922] usb 1-1: unregistering device
[49525.142933] usb 1-1: unregistering interface 1-1:1.0
[49525.143074] asix 1-1:1.0 eth0: unregister 'asix' usb-dwc2-1, ASIX AX88772B USB 2.0 Ethernet
[49525.178288] usb 1-1: usb_disable_device nuking all URBs
[49525.344404] hub 1-0:1.0: debounce: port 1: total 100ms stable 100ms status 0x101
[49525.534383] usb 1-1: new high-speed USB device number 15 using dwc2
[49525.750682] usb 1-1: default language 0x0409
[49525.756695] usb 1-1: device 0b95:772b detected via OTG
[49525.756716] usb 1-1: udev 15, busnum 1, minor = 14
[49525.756727] usb 1-1: New USB device found, idVendor=0b95, idProduct=772b
[49525.756737] usb 1-1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[49525.756746] usb 1-1: Product: AX88772C
[49525.756755] usb 1-1: Manufacturer: ASIX Elec. Corp.
[49525.756763] usb 1-1: SerialNumber: 078741
[49525.757257] usb 1-1: usb_probe_device
[49525.757283] usb 1-1: configuration #1 chosen from 1 choice
[49525.757849] usb 1-1: adding 1-1:1.0 (config #1, interface 0)
[49525.760838] asix 1-1:1.0: usb_probe_interface
[49525.760856] asix 1-1:1.0: usb_probe_interface - got id
[49526.078384] asix 1-1:1.0 eth0: register 'asix' at usb-dwc2-1, ASIX AX88772B USB 2.0 Ethernet, 00:0e:c6:07:87:41
[49526.078493] hub 1-0:1.0: state 7 ports 1 chg 0000 evt 0002
[49526.078519] hub 1-0:1.0: port 1 enable change, status 00000503
[49559.946117] IPv6: ADDRCONF(NETDEV_UP): eth0: link is not ready
[49560.965445] IPv6: ADDRCONF(NETDEV_UP): eth0: link is not ready
[49562.620497] IPv6: ADDRCONF(NETDEV_CHANGE): eth0: link becomes ready
[49562.623048] asix 1-1:1.0 eth0: link up, 100Mbps, full-duplex, lpa 0xD1E1
[50225.415976] hub 1-0:1.0: state 7 ports 1 chg 0000 evt 0002
```


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



