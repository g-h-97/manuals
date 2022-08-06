
# Connect to a new WiFi (Password Prompt)

To connect to wifi and be prompted for a password, you can hit tab few times to see all available wifi access points

```
nmcli -ask device wifi connect [AP_NAME]
```

# Scan & list available wifi networks

```
nmcli device wifi list --rescan yes
```

# Connect & Disconnect to/from known APs

To connect to a access point

```
nmcli connections up [AP_NAME]
```

To disconnect from a AP without shutting down the network interface

```
nmcli connections down [AP_NAME]
```

# Shutdown the network interface

```
nmcli device disconnect [INT]
```

# Turn off all radio devices

```
nmcli device radio off
nmcli device radio on
```

# Stop /etc/resolve.conf auto update

Add the following to `/etc/NetworkManager/NetworkManager.conf`, or (recomended) create a file in `/etc/NetworkManager/conf.d/` and call it something like `99-noautodns.conf`

```
[main]
dns=none
#or
rc-manager=unmanaged
```
