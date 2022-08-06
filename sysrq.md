This is for rebooting in emergency situations
> Sources
> https://en.wikipedia.org/wiki/Magic_SysRq_key
>

# Sysrq

There are two ways to trigger the sysrq functions

## software

First `sysrq` must be enabled as follows

```bash
# to activate sysrq
echo 1 > /proc/sys/kernel/sysrq
```

Then echo the key that you would've have pressed if you are using the keyboard
> Note : that echoing the key will instantly engage the action

```bash
# echo the desired key
# `b` will force reboot
echo b > /proc/sysrq-trigger
```

However echoing `b` directly is never recommended since it may cause data lose instead echo the following sequence `reisub` each character individually like so

```bash
# take keyboard control from X server
echo r > /proc/sysrq-trigger

# Terminate `SIGTERM` all, excluding pid 1
echo e > /proc/sysrq-trigger

# Force terminate `SIGKILL` hung pids excluding 1
echo i > /proc/sysrq-trigger

# Sync to disk
echo s > /proc/sysrq-trigger

# Remount filesystems readonly
echo u > /proc/sysrq-trigger

# Force reboot
echo b > /proc/sysrq-trigger
```

## hardware

This is limited to my thinkpad X1 Yoga 1st Gen only since it's the only thing I tested it on, However it is possible that it might work on other systems.

Since there is no `Sysrq` key on my keyboard there is a shortcut for that which is

```
# press and hold
Fn + s + Alt

# release only
Fn + s

# press action key
b (force reboot "UNSAFE !!!")
```

> Note : in this case `Fn + s` equals a physical `Sysrq` key

Change `b` with what you want to do, in this case the computer will force reboot as if you pressed the reboot button on a desktop computer. The same applies here do not use `b` on it's own it's damaging; Use `reisub` instead, This requires you to repeat the sequence above for each key you input I.E pressing `Fn + s + Alt`, releasing `Fn + s` only, then pressing the key starting with `r`.

## keys

This is a list of all `sysrq` keys with their functions
> Note : use the fist key after the description (QWERTY), other keys are for other keyboard types
> QWERTY, DVORAK, AZERTY, COLEMAK

```
Set the console log level, which controls the types of kernel messages that are output to the console 	0 - 9 	0 - 9 	0 - 9
(without ⇧ Shift) 	0 - 9
Immediately reboot the system, without unmounting or syncing filesystems 	b 	x 	b 	b
Perform a system crash. A crashdump will be taken if it is configured. 	c 	j 	c 	c
Display all currently held Locks (CONFIG_LOCKDEP kernel option is required) 	d 	e 	d 	s
Send the SIGTERM signal to all processes except init (PID 1) 	e 	. 	e 	f
Call oom_kill, which kills a process to alleviate an OOM condition 	f 	u 	f 	t
When using Kernel Mode Setting, switch to the kernel's framebuffer console.[3]
If the in-kernel debugger kdb is present, enter the debugger. 	g 	i 	g 	d
Output a terse help document to the console
Any key which is not bound to a command should also perform this action 	h 	d 	h 	h
Send the SIGKILL signal to all processes except init 	i 	c 	i 	u
Forcibly "Just thaw it" – filesystems frozen by the FIFREEZE ioctl. 	j 	h 	j 	n
Kill all processes on the current virtual console (can kill X and SVGALib programs, see below)
This was originally designed to imitate a secure attention key 	k 	t 	k 	e
Shows a stack backtrace for all active CPUs. 	l 	n 	l 	i
Output current memory information to the console 	m 	m 	, 	m
Reset the nice level of all high-priority and real-time tasks 	n 	b 	n 	k
Shut off the system 	o 	r 	o 	y
Output the current registers and flags to the console 	p 	l 	p 	;
Display all active high-resolution timers and clock sources. 	q 	' 	a 	q
Switch the keyboard from raw mode, used by programs such as X11 and SVGALib, to XLATE mode 	r 	p 	r 	p
Sync all mounted filesystems 	s 	o 	s 	r
Output a list of current tasks and their information to the console 	t 	y 	t 	g
Remount all mounted filesystems in read-only mode 	u 	g 	u 	l
Forcefully restores framebuffer console.
For ARM processors, cause ETM buffer dump instead. 	v 	k 	v 	v
Display list of blocked (D state) tasks 	w 	, 	z 	w
Used by xmon interface on PowerPC platforms. Disables lockdown (Secure Boot restrictions) on some kernels. 	x 	q 	x 	x
Show global CPU registers (SPARC-64 specific) 	y 	f 	y 	j
Dump the ftrace buffer 	z 	; 	w 	z
Print a summary of available magic SysRq keys 	space 	space 	space 	space
```
