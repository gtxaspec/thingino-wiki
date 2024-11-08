## Tips for Improving Wi-Fi Signal

### Don't:
- Use 40 MHz channels on the 2.4 GHz band.
- Use WPA2/WPA3 mixed mode. Stick to WPA2 only.

### Do:
- Stick to channels 1, 6, and 11 (or 13 if permitted in your region).
- Use a Wi-Fi scanner app on your mobile device to identify less congested channels.
- Opt for a wired connection whenever possible to improve stability and speed.

---

### How to Check Signal Strength on Altobeam Devices

To find the signal strength on devices with an Altobeam chipset, use the following command:

```
$ iwpriv wlan0 common get_rssi

wlan0     common:
rssi=-25
```

More info:

```
$ iwpriv wlan0 common get_ap_info

wlan0     common:
ssid=Home
rssi=-25
mac:00:11:22:aa:bb:cc
tx_pkt=38819
tx_suc_pkt=38383
rx_pkt=28000
tx_rate=650
rx_rate=650
idle=1001
throughput=8769635 Byte/s
```

This will provide important details such as SSID, signal strength, and network activity.

Another method:

```
$ find /sys/module/ -name 'atbm_cmd' -exec sh -c 'echo ap_info > {}; cat {}' \;

ifname[wlan0] mac[e0:ff:ff:ff:be:ef] ssid[test] ssid_len[11] channel[11] channel_type[0] signal[-53] avg_signal[-53] rxbytes[102899858] txbytes[863243530] toprate[10406312]
ap_info[OK]
```

This will provide important details such as SSID, signal strength, and network activity.