

# Scaling

Gns3 relays on the QT environment variable `export QT_SCALE_FACTOR=1.2 picard` in my `.zshenv` to scale properly.

# Dark Theme

I used a shell script from this github repo `https://github.com/n3oxmind/gns3theme`. I've also read the entire thing to ensure that it's safe since it requires root privileges to install gns3 ( Read it each time you wnat to run it ).

I've also added my custom theme to the `colorschemes` file

```
dwm-dark:         #0d0d0d #141414 #ffffff #0099d6 #181818 #000000 #BA4551 #161616 #b3b3b3 #6e6e6e 2   #303030   dark
```

The repo also contains `symbols` directory which I copied to `~/.cache/gns3/symbols` directory and used as custom symbols for my appliances.

There is also `Label Style` & `Note Style` which you can configure under `Edit -> Preferences -> General -> Topology View -> Default label style:` & `Edit -> Preferences -> General -> Topology View -> Default note style:` respectively.


# IOU Licensing

The script that came with the IOU images I downloaded is written in python2 which is a bit old, so I downloaded a python3 port from `http://www.ipvanquish.com/download/CiscoIOUKeygen3f.py` and ran it on the gns3 VM. This will generate a file called `iourc.txt` in the current directory copy the text in this file to `Edit -> Preferences -> IOS on UNIX` in the gns3-gui

## Script contents

Here are the script contents

```py
#! /usr/bin/python
print ("************************************************************************")
print ("Cisco IOU License Generator v2 - Kal 2011, python port of 2006 C version")
import os
import socket
import hashlib
import struct

# get the host id and host name to calculate the hostkey
hostid=os.popen("hostid").read().strip()
hostname = socket.gethostname()
ioukey=int(hostid,16)

for x in hostname:
	ioukey = ioukey + ord(x)

print "hostid=" + hostid +", hostname="+ hostname + ", ioukey=" + hex(ioukey)[2:]

# create the license using md5sum
iouPad1='\x4B\x58\x21\x81\x56\x7B\x0D\xF3\x21\x43\x9B\x7E\xAC\x1D\xE6\x8A'
iouPad2='\x80' + 39*'\0'

md5input=iouPad1 + iouPad2 + struct.pack('!Q', ioukey)[4:] + iouPad1
iouLicense=hashlib.md5(md5input).hexdigest()[:16]

print ("************************************************************************")
print ("Add the following text to ~/.iourc")
print ("[license]\n" + hostname + " = " + iouLicense + ";\n")

print ("************************************************************************")
print "You can disable the phone home feature with something like:"
print " echo '127.0.0.127 xml.cisco.com' >> /etc/hosts"
print "************************************************************************"
```

# Using ST & Tabbed

Navigate to `Edit -> Preferences -> General -> Console applications` and use this as the command, this will set up `st` as the terminal emulator with `tabbed` as window title to avoid confusion

```
tabbed -c -r 2 st -w '' -T %d -e telnet %h %p
```

If you don't want to use `tabbed` for what ever reason

```
st -T %d -e telnet %h %p
```

# Quick nat on edge router

Provided that everything else is configured, IPs, no shut, Default Routes...etc

```
int [Outside]
ip nat outside
int [Inside]
ip nat inside
exit
access-list 1 permit any
ip nat inside source list 1 interface [Outside] overload
```

If the overload command didn't take effect with error `%Dynamic mapping not found` just keep trying or shutdown the interface `Outside`:
> https://www.cisco.com/c/en/us/support/docs/ip/network-address-translation-nat/13779-clear-nat-comments.html

