> https://www.rogerperkin.co.uk/cisco/software-upgrade-guides/upgrade-software-cisco-3850-switch/

# Firmware Upgrade

## TFTP

Copy the image from the TFTP server

```
3850-SW1#copy tftp flash
Address or name of remote host []? 10.1.1.250
Source filename []? cat3k_caa-universalk9.SPA.03.03.01.SE.150-1.EZ1.bin
Destination filename [cat3k_caa-universalk9.SPA.03.03.01.SE.150-1.EZ1.bin]?
Accessing tftp://10.1.1.250/cat3k_caa-universalk9.SPA.03.03.01.SE.150-1.EZ1.bin…
Loading cat3k_caa-universalk9.SPA.03.03.01.SE.150-1.EZ1.bin from 10.251.226.253 (via Port-channel1): !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
```

Check that the image is stored on `flash`

```
dir flash:
```

## USB

```
dir usbflash0:
copy usbflash0:cat3k_caa-universalk9.SPA.03.03.01.SE.150-1.EX3.bin flash:
software install file flash:cat3k_caa-universalk9.SPA.03.03.01.SE.150-1.EX3.bin switch 1-2
```

# Power over Ethernet PoE

- PoE enabled by default
- 7W, 15.4W (MAX), 30 (PoE+)(802.3at)
- Allocated maximum power when PoE device first connected
- Power redundancy
- Auto power when no power is sensed
- 802.3af
- 802.3at

## Configuration

### Modes

- auto: auto detect power requirements
- static: specify the amount of power to a high priority device
- never: disable the PoE capability on the port

```
interface [INT]
power inline {auto [max max-wattage] | never | static [max max-wattage]}

end

show power inline [INT]
```

### Budget to all Ports

```
conf t
no cdp run
power inline consumption default wattage [mWATs]

end

show power inline consumption default
```

mWATs: 4000mWA - 15400mWA(PoE) || 30000mWA(PoE+)

### Budget to one Port

```
conf t
no cdp run
interface [INT]
power inline consumption [mWATs]

end

show power inline consumption
```

mWATs: 4000mWA - 15400mWA(PoE) || 30000mWA(PoE+)

### Policing

```
conf t
interface [INT]
power inline police [action{log | errdisable}]
exit
errdisable detect cause inline-power
errdisable recovery cause inline-power
errdisable recovery interval [TIME]

end

show power inline police
show errdisable recovery
```

- Enable the detection error disabled state for PoE ports
- The auto recovery after a certain time interval (300 Seconds Default)
- Change the interval (Optional)



## Troubleshoot

### Auto mode

- If the switch detects a fault caused by an undervoltage, overvoltage, overtemperature, oscillator-fault, or short-circuit condition, it turns off power to the port, generates a syslog message, and updates the power budget and LEDs.

- If there is not enough available PoE, or if a device is disconnected and reconnected while other devices are waiting for power, it cannot be determined which devices are granted or are denied power.

- If granting power would exceed the system power budget, the switch denies power, ensures that power to the port is turned off, generates a syslog message.

- If the IEEE class maximum wattage of the powered device is greater than the configured maximum value, the switch does not provide power to the port.
