## Self-Hosted Mode

Thingino supports a "self-hosted" mode, allowing the camera to function without an internet connection. In this mode, the camera creates its own wireless access point, enabling direct connection from a mobile device or computer. Once connected, users can open a web browser and go to `http://thingino.local` to access camera settings and features.

### How to Enable Self-Hosted Mode

**1. Using the WebUI on an Existing Setup**  
If the device is already configured, you can enable self-hosted mode via the WebUI under `Wireless Networking`.
![wlanap-webui](https://github.com/user-attachments/assets/d3d2110c-3917-49e2-b77e-6ff1dcfd7682)

**2. From the Setup Portal on a New Installation**  
For a fresh installation, you can configure and enable AP mode directly from the setup portal.  
![wlanap-portal](https://github.com/user-attachments/assets/1455454b-984e-4062-9228-da528f410dc9)

**3. Manually Enabling via Console**  
To enable self-hosted mode manually, first connect the device to your wireless network as usual. Then, run the following command in the console:
```
fw_setenv wlanap_enabled true
```
Reboot the device, and it will start broadcasting an access point. The default password for the access point is `thingino`.

### Accessing Thingino Services

You can use the `thingino.local` domain to access RTSP and other services, such as:
```
rtsp://thingino.local
```

Alternatively, you can connect using the device’s IP address. For example:
- Web access: `http://100.64.1.1`
- RTSP streaming: `rtsp://100.64.1.1/ch0`

