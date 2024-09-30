## Captive Portal

After flashing a fresh Thingino firmware image on a supported camera with a wireless module, the camera will not have any information about your wireless network and will not be able to connect to it automatically.

> [!NOTE]
> Dual interface devices (those with both ethernet __and__ Wi-Fi) will not broadcast an Access Point.  Instead, connect to the IP or hostname to begin setup.

You can either provide your [wireless network credentials on an SD card](https://github.com/themactep/thingino-firmware/wiki/Configuring-Wi%E2%80%90Fi-Access#wifi-setup-via-sd-card) or use our versatile built-in portal.

After you turn on the camera without network credentials, it will set up a temporary access point and create a public network called THINGINO-XXXX, where XXXX is the last four characters of the camera's MAC address.

Connect to this network, either using a mobile device (smartphone or tablet) or from a PC, and navigate your browser to http://thingino.local/. You should see the form for entering initial settings for the camera:

![portal1](https://github.com/user-attachments/assets/d0bcd753-c2e5-4694-8db8-bc086dfdc672)

Fill in the form with the current information and click the "Save Credentials" button at the bottom.

![portal2](https://github.com/user-attachments/assets/8ac87448-702e-4eb1-9ecc-08d62179bfa4)

On the next page, review the information and correct it if you find an error. Otherwise, click the "Proceed with Reboot" button.

![portal3](https://github.com/user-attachments/assets/15d0b12a-679d-45d2-a7d3-c71db9a159ab)

The camera will reboot and register with your wireless network using the information provided.

![portal4](https://github.com/user-attachments/assets/70dbeca8-f2e3-4c55-af06-d82148c61adf)

Check the DHCP leases on your router to find the IP address assigned to the camera.


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