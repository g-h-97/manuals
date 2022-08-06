# trackpad/mouse

## xinput

```bash
# list input devices
xinput --list

# say the trackpad has id=11, run this to list available properties
xinput --list-props 11
```

Here is a sample of how the output should be for the trackpad

```bash
        libinput Tapping Enabled (312): 0
        libinput Tapping Enabled Default (313): 0
        libinput Tapping Drag Enabled (314):    1
        libinput Tapping Drag Enabled Default (315):    1
        libinput Tapping Drag Lock Enabled (316):       0
        libinput Tapping Drag Lock Enabled Default (317):       0
        libinput Tapping Button Mapping Enabled (318):  1, 0
        libinput Tapping Button Mapping Default (319):  1, 0
        libinput Natural Scrolling Enabled (320):       0
        libinput Natural Scrolling Enabled Default (321):       0
        libinput Disable While Typing Enabled (322):    1
        libinput Disable While Typing Enabled Default (323):    1
        libinput Scroll Methods Available (324):        1, 1, 0
        libinput Scroll Method Enabled (325):   1, 0, 0
        libinput Scroll Method Enabled Default (326):   1, 0, 0
        libinput Click Methods Available (327): 1, 1
        libinput Click Method Enabled (328):    1, 0
        libinput Click Method Enabled Default (329):    1, 0
        libinput Middle Emulation Enabled (330):        0
        libinput Middle Emulation Enabled Default (331):        0
        libinput Accel Speed (332):     0.000000
        libinput Accel Speed Default (333):     0.000000
        libinput Accel Profiles Available (334):        1, 1
        libinput Accel Profile Enabled (335):   1, 0
        libinput Accel Profile Enabled Default (336):   1, 0
        libinput Left Handed Enabled (337):     0
        libinput Left Handed Enabled Default (338):     0
        libinput Send Events Modes Available (295):     1, 1
        libinput Send Events Mode Enabled (296):        0, 0
        libinput Send Events Mode Enabled Default (297):        0, 0
        Device Node (298):      "/dev/input/event6"
        Device Product ID (299):        2, 7
        libinput Drag Lock Buttons (339):       <no items>
        libinput Horizontal Scroll Enabled (340):       1
```

To toggle any feature use the following command parameters, keep in mind that these changes are not persistent across reboots

```bash
xinput set-prop ['device_name'] [prop_number] [value]
```

```bash
# this is what I often like to enable under DWM
# to enable tapping
sudo xinput set-prop 'SynPS/2 Synaptics TouchPad' 312 1

# to enable natural scrolling
sudo xinput set-prop 'SynPS/2 Synaptics TouchPad' 320 1

# to change acceleration
sudo xinput set-prop 'SynPS/2 Synaptics TouchPad' 332 0.5

# enable edge & two finger scrolling respectively
sudo xinput set-prop 'SynPS/2 Synaptics TouchPad' 325 0 1 0
sudo xinput set-prop 'SynPS/2 Synaptics TouchPad' 325 1 0 0
```

## synaptics driver

```bash
# installing the driver
yay -S xf86-input-synaptics

# copy config & edit
cp /usr/share/X11/xorg.conf.d/70-synaptics.conf /etc/X11/xorg.conf.d/

# check the manual for full options list
man synaptics
```
