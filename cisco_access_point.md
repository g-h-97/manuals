
# Introduction

> https://community.cisco.com/t5/wireless-mobility-documents/understanding-access-point-os-images/ta-p/3123952

Introduction

All Cisco Aironet 802.11a/b/g/n and 11ac Wave 1 wireless access points and bridges run IOS, except for the OEAP602.

The newer 802.11ax and 11ac Wave 2 APs, including the C9100 and 1800, 2800 and 3800 series, run AP-COS.

Note: Some very old, no longer supported, Cisco access points ran VxWorks, such as the Aironet 342 and the 1010/1020 lightweight APs.

Access Point IOS is distributed as a tar file. These tar files can be downloaded from cisco.com SDS; lightweight IOS images (k9w8) are also bundled in the WLC software images (.aes.)

The AP image names include the following components:

platform-featureset-tar.version.tar

    platform- the access point hardware model or family supported by the image.
    Note: on an AireOS controller, the command show ap bundle shows the supported AP models and the corresponding platform names
        ap1g1 - 700 series (702w beginning with 15.2(4)JB5)

        ap1g2 - 1600 series

        ap1g3 - 1530 series, AP803 embedded in IR829 router

        ap1g4 - 1850/1830/1810 series (AP-COS)
        ap1g5 - 1800/1815/1540 series; AP1100AC embedded in C1000 series ISR (AP-COS)
        ap1g6 - C9117 (AP-COS)
        ap1g6a - C9130 (AP-COS)
        ap1g7 - C9115/9120 (AP-COS)
        ap1g8 - C9105 (AP-COS)
        ap3g1 - 3500/1260 series

        ap3g2 - 3700/3600/2700/2600/1700 series (aIOS, and lightweight up through 8.4/15.3(3)JE branch)
        ap3g3 - 2800/3800/4800/1560/IW6300/ESW6300 series (AP-COS)
        ap801 - AP embedded in 861W, CISCO88xW, CISCO891W, 1911W routers
        ap802 - AP embedded in 819, 812, 886VA-W/887VA-W, and C88x/C89x routers
        apw5100 - Rockwell Stratix 5100 WAPAK9, WAPCK9, WAPEK9, WAPZK9
        c3700 - 1700/2700/3700 series APs (lightweight, 8.5/15.3(3)JF and above)
        c1570 - 1570 series outdoor APs
        c1550 - 1550 (128MB model) series outdoor APs
        c1520 - 1520 and 1550 (64MB model) series mesh APs
        c1410 - BR1410
        c1310 - BR1310
        c1250 - 1250 series APs
        c1240 - 1240 series APs
        c1200 - 1200 series (1200/1210/1220/1230)
        c1140 - 1140 and 1040 series APs
        c1130 - 1130 series APs
        c1100 - 1100 series APs (i.e. the AP1121)
        c520 - 521 AP
        c350 - 350 series APs

    featureset- the set of software features supported by the image - one of:      
        k9w7 - autonomous (or "site survey") IOS (not available with AP-COS)
        k9w8 - full lightweight IOS/AP-COS (this is what is bundled in the WLC .aes image, and is factory installed on "mesh" APs)
        rcvk9w8 - lightweight recovery image - this is factory installed on lightweight APs, unless a "mesh" image is specified; it lacks radio firmware (not available with COS)
        boot - bootloader image (not IOS) - normally installed by manufacturing and not updated in the field
    version- the IOS version       
        There is a 1:1 mapping between the lightweight OS software version (such as 12.4(23c)JA) and the CUWN version (such as 7.0.98.0)  
            see the Wireless Solutions Software Compatibility Matrix on CCO

Example:

c1240-k9w7-tar.124-25d.JA1.tar

    Platform: c1240: 1240 series AP
    Featureset: k9w7: autonomous IOS
    Version: 124-25d.JA1: 12.4(25d)JA1


As AP IOS is always distributed as a tar file, the AP cannot directly execute such a file (thus, if you were to copy c1240-k9w7-tar.124-25d.JA1.tar directly onto AP flash, and then try to boot it, this could not work.)  The tar file contains, in addition to the IOS image proper, the radio firmware files, the HTML GUI files (if present), and various other files.

The AP IOS tar file must be unbundled into AP flash using the archive exec command (this is done in an automated fashion when a lightweight AP is upgraded after joining a WLC.)
Example:

AP1260#archive download-sw /overwrite tftp://10.95.42.136/ap3g1-k9w7-tar.124-25d.JA1

 

After unbundling, the IOS image itself be in a file called flash:/platform-featureset-mx.version/platform-featureset-mx.version - for example, flash:/c1240-k9w7-mx.124-25d.JA1/c1240-k9w7-mx.124-25d.JA1.  The AP is configured to boot this image if the bootloader BOOT environmental variable is set accordingly.

To see what IOS image the AP is configured to boot, examine the BOOT variable.
Example:

AP3502i#more flash:/env_vars | include BOOT

BOOT=flash:/ap3g1-k9w8-mx.152-2.JA/ap3g1-k9w8-mx.152-2.JA

 

To change the BOOT variable, use the IOS config mode boot system command.

 
Example:

 

AP3502i(config)#boot system flash:/ap3g1-k9w8-mx.124-25e.JA2/ap3g1-k9w8-mx.124-25e.JA2


# Standalone vs Lightweight

When IOS image contains `w7` it means it's a `Standalone` mode access point image, on the other hand if the image name contains `w8` this means that the image is a `Lightweight` image which will require a `Wireless Lan Controler` or `WLC` to work properly

w7 = Standalone
w8 = Lightweight

```
c1250-k9w7-mx.124-10b.tar
c1250-k9w8-mx.124-10b.tar
```

## Converting AP



Get IOS from a standalone AP
`archive upload-sw tftp://[IP]/[IMG].tar`

Boot the AP in `ap:` mode by holding the `MODE` button while plugging the Ethernet cable from a PoE capable switch (Or use power injector)

Configure networking interface in the AP, keep in mind that `DEFAULT_ROUTER` is required so if there is no gateway use the TFTP server's IP address instead

```
set IP_ADDR [IP]
set NETMASK [MASK]
set DEFAULT_ROUTER [IP]
```

Initialize 

```
ether_init
tftp_init
flash_init
```

> Note: Don't try to ping the AP since this will not work

Now tell the AP to download and extract the `tar` archive that you extracted earlier using the `archive` command from the TFTP server

> Note: make sure that the storage space is enough to hold the new IOS image, otherwise run `format flash:`

`tar -xtract tftp://[IP]/[IMG].tar flash:`

Use this command to make the AP boot from the newly extracted image, bellow the command is an example on how to do it

`set boot flash://[IMG_DIR]/[IMG]`

```
ap: dir flash:
Directory of flash:/

2    -rwx  283       <date>               info
3    -rwx  82        <date>               env_vars
4    drwx  512       <date>               c1250-k9w7-mx.124-10b.JDA3
156  -rwx  283       <date>               info.ver

25466880 bytes available (6402048 bytes used)

ap: set boot flash:c1250-k9w7-mx.124-10b.JDA3/c1250-k9w7-mx.124-10b.JDA3
```

After that boot the AP by writing `boot` and hitting Enter.
