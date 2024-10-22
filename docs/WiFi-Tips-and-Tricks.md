signal strength on altobeam:  
`find /sys/module/ -name 'atbm_cmd' -exec sh -c 'echo ap_info > {}; cat {}' \;`

result:  
`ifname[wlan0] mac[e0:ff:ff:ff:be:ef] ssid[test] ssid_len[11] channel[11] channel_type[0] signal[-53] avg_signal[-53] rxbytes[102899858] txbytes[863243530] toprate[10406312] 
ap_info[OK]`