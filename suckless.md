
# dwm

## multidisplay

Check that these lines are not commented in `config.mk`, then recompile dwm `rm config.h; make clean && make` then `doas make install`. Exit dwm with the shortcut `Alt+Shift+q` log back in.

```c
XINERAMALIBS  = -lXinerama
XINERAMAFLAGS = -DXINERAMA
```

### Mirror

Then use `xrandr` to setup external monitors or projectors

> Note : dwm will duplicate the output only if two prerequisites are met
- One of them is configured to show the same area as the other `xrandr` `--same-as` parameter
- They use the same resolution

```bash
# list avilable outputs and supported modes
xrandr

# to duplicate the out put
xrandr --output VGA1 --auto --same-as LVDS1 --mode 1024x768
xrandr --output LVDS1 --mode 1024x768
```

### Independent

> Note : the `--right-of` parameter can be replaced by the following parameters
- `--left-of`
- `--right-of`
- `--above`
- `--below`

```bash
xrandr --output HDMI-2 --auto [POSITION] eDP-1 --mode [RESOLUTION]
xrandr --output VGA1 --auto --right-of LVDS1
xrandr --output HDMI-2 --auto --right-of eDP-1
```

# dmenu


# st

This is about simple terminal (st) by suckless
Sources : https://st.suckless.org


This terminal emulator is so light wight that it doesn't even have a config file, to configure it you have to edit the source code which is (C) programing language.

However it's not as complicated as it soundes, the config file (config.h) & (config.def.h) is pretty much straight forward to edit. Keep in mind that :

    (config.def.h) : is the default config file incase there is no (config.h)
    (config.h) : is the user config file wich will be used instead of (config.def.h) remove if found

Before compiling or applying any patch be sure !!! To remove the (config.h) if it exists :

      mv config.h config.def.h

To add extra fuctionality such as mouse scrolling you need to download `patch` file form the suckless website and apply them, eg :

```bash
  # to apply mouse scrolling download the `.diff` patch file and copy it to source directory of (st) and apply it with the following command

      patch -i mouse-scrolling.diff

  # then make it with

      rm config.h ; make clean && make

  # this will make a binary file called (st) test it by running it :
      ./st

  # if it looks and behaves as you planed you can go ahead and install it :
  # of just copy the binary file to your `/usr/bin/` directory (not recommende for new users)
      sudo make clean install

```

# Void Linux Dependencies

```
st-terminfo
base-devel
libXft-devel
...
```

## Get Xorg Working

```
xorg-minimal
libXfontcache-1.0.5_2 
xfontsel-1.0.6_2 
libXfont2-2.0.4_1 
xorg-fonts-7.6_5 
dejavu-fonts-ttf-2.37_2 
font-mutt-misc-1.0.3_6 
font-misc-misc-1.1.2_7 
font-jis-misc-1.0.3_5 
font-isas-misc-1.0.3_6 
font-ibm-type1-1.0.3_6 
font-dec-misc-1.0.3_6 
font-daewoo-misc-1.0.3_6 
font-cursor-misc-1.0.3_6 
font-bitstream-type1-1.0.3_6 
font-bitstream-75dpi-1.0.3_6 
font-bitstream-100dpi-1.0.3_6 
font-bh-type1-1.0.3_6 
font-bh-ttf-1.0.3_6 
font-bh-lucidatypewriter-75dpi-1.0.3_6 
font-bh-lucidatypewriter-100dpi-1.0.3_6 
font-bh-75dpi-1.0.3_6 
font-bh-100dpi-1.0.3_6 
font-adobe-utopia-type1-1.0.4_7 
font-adobe-utopia-75dpi-1.0.4_7 
font-adobe-utopia-100dpi-1.0.4_7 
font-adobe-75dpi-1.0.3_7 
font-adobe-100dpi-1.0.3_7 
font-util-1.3.2_1 
mkfontscale-1.2.1_2 
libfontenc-1.1.4_1 
font-alias-1.0.4_2 
```
