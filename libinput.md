

For CLI configuration

```
xinput
xinput list-props 
xinput set-porop
```

For permanent configuration edit config files `/etc/X11/xorg.conf.d/[XX]-libinput.conf`

```
Section "InputDevice"
  Identifier "devname"
  Driver "libinput"
  Option "Device"   "devpath"
  ...
EndSection
```

For a full list of `Option`s check `man 4 libinput`
