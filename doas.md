
# Commands

Create `/etc/doas.conf` and write rules using these key words

```bash
permit          # allow
deny            # refuse
keepenv         # keep the user's environment variables
nopass          # allow to run as root without password
persist         # remember priviliges for 5 minutes
setenv          # set a specific environment variable or more if keep env breaks things
cmd             # a command
[user]          # user name
:[group]        # group name
```

# Samples

Configuration sample

```bash
permit :wheel                               # allow the users in group wheel to run commnds as root with password
permit nopass user                          # allow user without
permit user1 as user2                       # allow user1 to run all commands as user2 with password
permit nopass user1 as user2 cmd vim        # allow user1 to run vim as user2
permit setenv { ENV=value } user1 as user2 cmd firefox      # allow user1 to run firefox as user2 with `ENV` variable set ot `value`

deny user1 cmd vim                          # deny user1 running vim as root

```

