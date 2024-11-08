## Self-Hosted Mode

Thingino offers a "self-hosted" mode where the camera operates without needing an internet connection. In this mode, the camera broadcasts a dedicated wireless access point, allowing direct connection from a mobile device or computer. Once connected, users can open their web browser and navigate to `http://thingino.local` to access camera configuration and other features.

To enable this mode, first set up the device normally by connecting it to your wireless network. Then, run the command `fw_setenv wlanap_enabled true`, reboot the device, and it will broadcast an access point.  The default password for the access point is `thingino`.

The `thingino.local` domain can also be used to access RTSP and additional services, such as `rtsp://thingino.local`.

Alternatively, users can connect using the device’s IP address. For example, `http://100.64.1.1` provides web access, and `rtsp://100.64.1.1/ch0` can be used for RTSP streaming.
