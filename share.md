

# Access Windows Share

> Source: https://www.cyberciti.biz/faq/access-windows-shares-from-linux/

## Mount

```
mkdir -p /mnt/win
mount -t smbfs -o username=[WIN_USER],password=[PASSWORD] //[WIN_SRV]/[SHARE_NAME] /mnt/win
ls /mnt/win
```

## Smbclient
