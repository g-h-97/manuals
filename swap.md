

# Ext4

## Creating Swap File

First you need a SWAP partition or file, and it must be of the correct size which is better to be greater of equal than the size in `/sys/power/image_size`. In my case `6645452800` which is roughly `6.18 GB`.

```
cat /sys/power/image_size
6645452800
```

And since it's better if the swap file is larger than the actual suggested size, I opted for `8 GB`.

```
doas dd if=/dev/zero of=/swap BS=1M count=8192
```

## Making Swap Filesystem

- mkswap : make swap file system

```
doas mkswap /swap
```

- swapon : activate swap

```
doas swapon /swap
```

## Deleting Swap File

- swapoff : deactivate swap

```
doas swapoff /swap
```

Then Delete the file

```
rm -rf /swap
```

# Btrfs

Disable Copy-On-Write

```
chattr +C /swap
```
