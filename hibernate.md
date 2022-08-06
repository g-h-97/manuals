

Please Refer to `swap.md` before reading this file.

# Kernel Boot Parameters

The kernel must know how to find the swap file in order to perform hibernation correctly, this is done by editing the bootloader's file `/etc/default/grub` and adding the `resume=` and `resume_offset=` kernel startup parameters. Where `resume=` is the partition where the `swap` file is located and the `resume_offset=` is the physical offset on the (disk?/partition?).

We'll use the `findmnt` command to determine the partition UUID where `swap` is located, which is the root partition `/` in this case.

> Note: We can also use the partition block file path `/dev/sda2` instead of the UUID

```
findmnt -no UUID -T /swap
6bbedf14-9059-4c0a-afa8-e688d2c51203
```

And to find the physical offset we'll use the `filefrag` command, in this case the physical offset is `1458176`

```
filefrag -v /swap

# The output is

Filesystem type is: ef53
File size of /swap is 8589934592 (2097152 blocks of 4096 bytes)
 ext:     logical_offset:        physical_offset: length:   expected: flags:
   0:        0..    4095:    1458176..   1462271:   4096:
```

At the end the `GRUB_CMDLINE_LINUX=` variable in `/etc/default/grub` will look like this

```
GRUB_CMDLINE_LINUX="intel_iommu=on resume=UUID=6bbedf14-9059-4c0a-afa8-e688d2c51203 resume_offset=1458176"
```

Last but no least, we must regenerate the `/boot/grub.cfg` file

```
grub-mkconfig -o /boot/grub.cfg
```

# Regenerating RamFS

To do so the `mkinitcpio` bash script will be used, after editing the `/etc/mkinitcpio.conf` by adding the hook `resume` in the `HOOKS=` variable

```
HOOKS=(base udev autodetect modconf block filesystems keyboard resume fsck)
```
After that is done, let's regenerate the ramfs

```
doas mkinitcpio -p linux
```


# Enabling Hibernation on Lid Close

Edit `/etc/systemd/logind.conf` by uncommenting then changing the variables `HandleLidSwitch=`

```
HandleLidSwitch=hibernate

# Setting this will cause the device to hibernate automatically (Not Required)
# After the IdleActionSec time
IdleAction=hibernate
IdleActionSec=[TIME]
```

