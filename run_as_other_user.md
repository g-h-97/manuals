

```bash
# as user 1 to get hexkey
# for the host
xauth list | grep `uname -a`

# as user 2 without sudo
export DISPLAY=:0
xauth add $DISPLAY . hexkey

# if access not required
xauth remove $DISPLAY
```

```bash
# disable x access control
xhost +

# enable x access control
xhost -

# add user or host
xhost +[name]

# remove user of host
xhost -[name]
```
