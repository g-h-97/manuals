

# Block Sizes

> Source: `http://www.linuxintro.org/wiki/Blocks,_block_devices_and_block_size`

## Check

In order to check the block size of a device, do

```
fdisk -l /dev/sdXY
```

## Hardware

Typically the block size on the storage device it self `HDD, SSD, USB...` is `512`Bytes.

## Filesystem

File systems tend to use a block size of `4096`Bytes, meaning a single block in the file systems will take `8` Physical blocks.$ps=4096/512$ Then $ps=8$ blocks.

## Kernel

It seem that the Linux kernel uses a block size of `1024`Bytes, this information is from `man vmstat`.
