> Sources:
> https://serverfault.com/questions/929081/how-can-i-enable-packet-forwarding-on-windows


# windows command and shortcuts

1- Windows_key + R = Run
2- ctrl+shift+escap = task_manager
	in run :
	1- ncpa.cpl = interfaces
	2- appwiz.cpl = old windows uninstaller
	3- control = old control pannel
	4- compmgmt.msc = managment
	5- wf.msc = windows fire wall
	6- inetcpl.cpl = network configuration
	7- gpedit.msc = group policy editor
	8- regedit = registry editor
	9- services.msc = windows services
	10- mstsc = remote desktop
	11- systemproprtiesadvanced = domain window
	12- powershell
	13- winver = windows version

# ip forwarding in windows

```powershell
Get-NetIPInterface | select ifIndex,InterfaceAlias,AddressFamily,ConnectionState,Forwarding | Sort-Object -Property IfIndex | Format-Table

# Enable on specific interface
Set-NetIPInterface -ifindex <required interface index from table> -Forwarding Enabled

# Enable on all interfaces
Set-NetIPInterface -Forwarding Enabled

# Enable routing and remote access service
Set-Service RemoteAccess -StartupType Automatic; Start-Service RemoteAccess
```

# Super Administrator

```
Net user administrator [PASSWORD]
Net user administrator /active:yes
```
