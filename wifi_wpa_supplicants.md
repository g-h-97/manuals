

```
wpa_passphrase [SSID] [PASSWORD] >> /etc/wpa_supplicant/wpa_supplicant-[IF].conf
wpa_supplicant -B -i [IF] -c /etc/wpa_supplicant/wpa_supplicant-[IF].conf
```
