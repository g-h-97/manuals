

# Make Spoofed MAC Address Persistent

> Source : https://forums.kali.org/showthread.php?33405-SOLVED-NetworkManager-reverts-spoofed-MAC-to-permanent-one-or-randomizes-it

By default NetworkManager resets the wireless interface's MAC address to the factory one every time the interface is connected to a wireless network, obviously this is not the best thing when you want to spoof your address in public networks or just for privacy concerns by using tools such as `macchanger`. To get rid of this default behaviour add the following lines to `/etc/NetworkManager/NetworkManager.conf`

```
[device]
wifi.scan-rand-mac-address=no

[connection]
ethernet.cloned-mac-address=preserve
wifi.cloned-mac-address=preserve
```

Then restart NetworkManager with what ever init system you're using, in case of systemd

```
systemctl restart NetworkManager
```
