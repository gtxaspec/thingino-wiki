### What is the default login?

The default login is _root_ with the password _root_. 

The default streaming user is _thingino_ with the password _thingino_. This can be changed in _/etc/prudynt.cfg_.


### How to reset the root password?

Turn off the camera's power. Press and hold the reset button, then turn the power back on. Keep holding the button for 5 seconds during boot. This should reset the camera to its default settings with _root_ as a password. **Your camera needs to have the `gpio_button` pin set!**


### How do I change the MAC address on an interface?

Change it in bootloader environment with `fw_setenv` command. Use `ethaddr` parameter for ethernet interface, `wlanmac` for wireless interface.

```
fw_setenv ethaddr 12:34:56:78:AB:CD
fw_setenv wlanmac 12:34:56:78:AB:EF
```

### Do you have a mobile app to view/control the camera?

We recommend to use [tinyCam Monitor Pro](https://tinycammonitor.com/).

![Screenshot_2024-06-01-00-50-52-704_com alexvas dvr pro](https://github.com/themactep/thingino-firmware/assets/37488/58b1a981-31b8-499a-b416-a7f885d947a3)

### Can Thingino run on this unsupported camera?

If the camera in question has an Ingenic SoC, there is a good chance that Thingino can run on it.
You can try to convert it using one of the prebuilt module firmware files or build a new one yourself.
Donate such a camera to the project to speed up the process!  

See our complete table of [Supported Hardware](https://github.com/themactep/thingino-firmware/wiki/Tech-Info-%E2%80%90-Supported-Hardware).

### Is Thingino a fork of OpenIPC?

Thingino was influenced by the ideas of the OpenIPC project, and core developers even collaborated
with OpenIPC for a while, but then the differences became too deep and thingino was born.

While there are some similarities, there are also significant differences between these two projects.

### Is My Data Safe? Do You Collect Data Metrics or Telemetry?

Thingino does not collect any data metrics or telemetry, ensuring your data remains solely on your device and entirely under your control. Being fully open source, Thingino allows you to audit the code and verify its operations, providing full transparency and peace of mind.  **_We Don't Want Your Data!_**
