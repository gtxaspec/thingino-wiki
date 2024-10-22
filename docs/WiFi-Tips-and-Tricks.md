## Tips for Improving Wi-Fi Signal

### Don't:
- Use 40 MHz channels on the 2.4 GHz band.

### Do:
- Stick to channels 1, 6, and 11 (or 13 if permitted in your region).
- Use a Wi-Fi scanner app on your mobile device to identify less congested channels.
- Opt for a wired connection whenever possible to improve stability and speed.

---

### How to Check Signal Strength on Altobeam Devices

To find the signal strength on devices with an Altobeam chipset, use the following command:

```
find /sys/module/ -name 'atbm_cmd' -exec sh -c 'echo ap_info > {}; cat {}' \;
```

#### Example Result:

```
ifname[wlan0] mac[e0:ff:ff:ff:be:ef] ssid[test] ssid_len[11] channel[11] channel_type[0] signal[-53] avg_signal[-53] rxbytes[102899858] txbytes[863243530] toprate[10406312]
ap_info[OK]
```

This will provide important details such as SSID, signal strength, and network activity.