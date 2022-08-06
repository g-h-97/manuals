> Sources:
> https://stackoverflow.com/questions/21498667/how-to-limit-user-commands-in-linux
> http://at.magma-soft.at/sw/blog/posts/The_Only_Way_For_SSH_Forced_Commands/

# Rbash Method

Let's say we have three users that we want each of them to run a single different command than the others and only that command no more no less.

> NOTE: All command are being run as `root` via `doas`

First create a `$HOME/bin` directory for each user, and make it read only for them

```bash
mkdir /home/{user1/bin,user2/bin,user3/bin}
chmod 755 /home/{user1/bin,user2/bin,user3/bin}
```

Then create symbolic links for the command the each user should be able to run in to it's local bin directory

```bash
ln -s /bin/com1 /home/user1/bin
ln -s /bin/com2 /home/user2/bin
ln -s /bin/com3 /home/user3/bin
```

Also add the `PATH` variable to point to their local `bin` directories only

```bash
echo "PATH=\$HOME/bin" | tee -a /home/{user1/.bashrc,user2/.bashrc,user3/.bashrc}
chattr +i /home/{user1/.bashrc,user2/.bashrc,user3/.bashrc}
```

Next create a symbolic link from `/bin/bash` to `/bin/rbash`, which I didn't have in `Archlinux` but it might be available in other distributions. rbash is restricted bash with doesn't allow the user to do anything particularly bad and it just the same as running `bash -r` or `bash --restricted` although `chsh` doesn't accept additional flags to the shell parameter.

```bash
ln -s /bin/{bash,rbash}
```

Finally change all users shells to `rbash` using `chsh`

```bash
chsh -s /bin/rbash user1
chsh -s /bin/rbash user2
chsh -s /bin/rbash user3
```

# ACL Method

Set files access control lists to deny the user `rwx` read, write, execute rights

Just change the permissions `rwx` as required

```bash
getfacl /bin/com

setfacl -m u:user:rwx /bin/com
```

> NOTE: The issue is that this needs to be done to all commands that the user can't run.

# The `Only` Way

> http://at.magma-soft.at/sw/blog/posts/The_Only_Way_For_SSH_Forced_Commands/
