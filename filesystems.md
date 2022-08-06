

# EXT

## EXT2

## EXT3

## EXT4

```
mkfs.ext4
```

# ZFS

# BTRFS

# NTFS

## Format a partition

In order to format a partition with the `NTFS` file system, use the following command (All Data Will Be Erased !!!). The `-f` flag or `--fast`, `-Q`, `--quick` can be used to skip zeroing & bad sector checking of the partition, otherways the process may take a long time depending on the partition size. Find out more at `man mkfs.ntfs`.

```
mkfs.ntfs -f /dev/sdXY

# equivalently
mkntfs -f /dev/sdXY
```

# FAT32

