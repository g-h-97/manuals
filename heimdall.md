# Flashing Stock S7 Edge ROM

Download The stock rom from `sammobile.com` then do the following

```bash
# create a new directory and copy it there
mkdir rom;cp ROM.zip rom/; cd rom/

# unzip the rom
unzip ROM.zip

# extract every .tar.md5 file using a for loop
for file in *.tar.md5; do tar -xvf $file; done

# decompress every .lz4 file
unlz4 -m *.lz4
```

Now you have all the files you need, put the phone in download mode by shutting it down then holding `vol down + power + home`, when the download mode screen shows up press the `vol up` button after of which run

```bash
# get the phones partion table
heimdall print-pit --no-reboot > s7edge_text.pit

# read the pit file in text editor
nvim s7edge_text.pit
```

After Opening the `pit` file construct the `heimdall` flash command according to it, just use the flags as you find the required files for them

```bash
heimdall flash --BOOTLOADER sboot.bin --CM cm.bin --PARAM param.bin --BOOT boot.img --RECOVERY recovery.img --RADIO modem.bin --SYSTEM system.img --CACHE cache.img --HIDDEN hidden.img --CP_DEBUG modem_debug.bin --USERDATA userdata.img
```

# Flashing TWRP

Download TWRP recovery from `twrp.me`, put the phone in download mode

```bash
heimdall flash --RECOVERY TWRP.img --no-reboot
```

> NOTE : the `--no-reboot` flag is really important since that if the phone booted past the recovery the process must be restarted all over again.

When the flash is complete, hold `vol down + power` and right after the screen turns black, switch your fingers to ` vol up + power + home` to go recovery right away if you fail in doing so and the boots to android repeat the flashing process all over else you are done flashing a custom recovery. Enjoy :)
