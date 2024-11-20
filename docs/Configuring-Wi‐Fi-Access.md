## Captive Portal

After flashing a fresh Thingino firmware image on a supported camera with a wireless module, the camera will not have any information about your wireless network and will not be able to connect to it automatically.

> [!NOTE]
> Dual interface devices (those with both ethernet __and__ Wi-Fi) will not broadcast an Access Point.  Instead, connect to the IP or hostname to begin setup.

You can either provide your [wireless network credentials on an SD card](https://github.com/themactep/thingino-firmware/wiki/Configuring-Wi%E2%80%90Fi-Access#wifi-setup-via-sd-card) or use our versatile built-in portal.

After you turn on the camera without network credentials, it will set up a temporary access point and create a public network called THINGINO-XXXX, where XXXX is the last four characters of the camera's MAC address.

Connect to this network, either using a mobile device (smartphone or tablet) or from a PC, and navigate your browser to http://thingino.local/. You should see the form for entering initial settings for the camera:

![portal-1](https://github.com/user-attachments/assets/5adb3b2b-6ee4-4ac3-8478-b0e77f94c83d)

Fill in the form with the current information and click the "Save Credentials" button at the bottom.
Note that the SSID is case-sensitive, so you must type it exactly as it is.

![portal-2](https://github.com/user-attachments/assets/b81c4cea-5862-4039-a068-122f5b4875a1)

On the next page, review the information and correct it if you find an error. Otherwise, click the "Proceed with Reboot" button.

![portal-3](https://github.com/user-attachments/assets/75f389e4-b040-4d1f-a99b-c5da00285491)

The camera will reboot and register with your wireless network using the information provided.

![portal-4](https://github.com/user-attachments/assets/86047aaa-f570-43f6-ad38-183d1c6a2b3b)

Press RESET button or check the DHCP leases on your router to find the IP address assigned to the camera.

[Wyze Cam 2 telling its IP address](https://youtu.be/eOA8-_QJyAw):

[![Wyze Cam 2 telling its IP address](http://img.youtube.com/vi/eOA8-_QJyAw/0.jpg)](https://youtu.be/eOA8-_QJyAw "Wyze Cam 2 telling its IP address")

## WiFi setup from Linux shell

If you have access to Linux shell over UART or Ethernet, you can set up Wireless connection running `wlansetup`.
Follow the prompts and then reboot the camera afterwards.
 
![image](https://github.com/user-attachments/assets/6417820a-214f-4cec-bed4-1da9bf6af6b1)


## WiFi setup via SD card

Create an `uenv.txt` file on a blank FAT formatted SD card with the following content

```
wlanssid=nameofyournetwork
wlanpass=yourwirelessnetworkpass
```

Reboot the camera with the card inserted. The information provided will be added to the environment and reused to log on to the wireless network.


## Camera Reset

Hold down the reset button for 10 seconds while powering the camera up. This will reset the unit.
Repeat the configuration from the beginning using proper wireless network credentials.