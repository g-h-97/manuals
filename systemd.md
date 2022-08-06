
```

    %n: Anywhere where this appears in a template file, the full resulting unit name will be inserted.
    %N: This is the same as the above, but any escaping, such as those present in file path patterns, will be reversed.
    %p: This references the unit name prefix. This is the portion of the unit name that comes before the @ symbol.
    %P: This is the same as above, but with any escaping reversed.
    %i: This references the instance name, which is the identifier following the @ in the instance unit. This is one of the most commonly used specifiers because it will be guaranteed to be dynamic. The use of this identifier encourages the use of configuration significant identifiers. For example, the port that the service will be run at can be used as the instance identifier and the template can use this specifier to set up the port specification.
    %I: This specifier is the same as the above, but with any escaping reversed.
    %f: This will be replaced with the unescaped instance name or the prefix name, prepended with a /.
    %c: This will indicate the control group of the unit, with the standard parent hierarchy of /sys/fs/cgroup/ssytemd/ removed.
    %u: The name of the user configured to run the unit.
    %U: The same as above, but as a numeric UID instead of name.
    %H: The host name of the system that is running the unit.
    %%: This is used to insert a literal percentage sign.
```

# Old

```
# this guide is from https://www.freedesktop.org/software/systemd/man/systemd.service.html#Examples
# and https://www.linux.com/training-tutorials/understanding-and-using-systemd/

# the units in directory '/etc/systemd/system' are symbolic links to units in '/usr/lib/systemd/system'

# ther are 12 types systemd units 

	.service 
	.socket 
	.device
	.target #group of units
	.automount #filesystem auto mount points
	.device #kernel device name, in sysfs and udev
	.mount
	.path
	.scope
	.slice
	.snapshot
	.socket #inter process communication "IPC" socket
	.swap #swap file
	.timer #systemd timer

# all units have [Unit] header and Description like soo

	[Unit]
	Description=This is My Unit

# after that the [Service] section

	[Service]
	Type=oneshot 	#if this is fast to execute unit and only once
	ExecStart=/path/to/program [args]
	ExecStart=/path/to/program0 [args] 	#only oneshot units support more than one 'ExecStart' field like this example

# at the end we can see [Install] section that tells systemd where to put this unit in '/usr/lib/systemd/system/' if it gest enables by 
	
	systemctl enable unit.type

# and the section is as follows
	[Install]
	WantedBy = multi-user.target

# there are three states which units can be in 
	enabled #means that the unit has a symlink in one of the '.wants' directories
	diabled #no symlink
	static	#it can't be enabled so it depends on other units to run

# the most usefull systemd commands

	systemctl start
	systemctl stop
	systemctl restart
	systemctl reload
	systemctl status
	systemctl is-active
	systemctl list-units --type [type] --all

# THIS IS AMAZING for system cleanup ; how to tell what unit is taking a fareshare in system loading time and the command is insane :p
		systemd-analyze blame
		systemd-analyze critical-chain
```	
