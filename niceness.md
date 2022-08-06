> Sources:
>


# Definition

Niceness is the propriety of a process where it signifies how nice the process is by the amount of CPU time it's taking from it's allocated time frame.

If a process is being nice it's said to have a low priority or `niceness > 0` otherwise it's a normal process if `niceness = 0` or a high priority if `niceness < 0`.

Processes niceness level can range from `-20` ( Really High Priority ) to `19` ( Supper [Nice/Low Priority] ), [ -20, 19 ] inclusive.

# Starting with X niceness

If you want to start a process with a said level of niceness user `nice`

```bash
nice -n [value] [command]
```

# Changing niceness of running process

```bash
renice [value] -p [pid]
```

# Setting the default niceness

In order to set a default niceness value for a user or group edit `/etc/security/limits.conf` by adding lines of the following format

```bash
# for a user
[user] [soft|hard] priority [value]
# for a group
[@group] [soft|hard] priority [value]
```

