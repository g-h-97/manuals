

# Theory

## Processes :

### Confined & Unconfined :

These are the selinux contexts for any subject or object

 `user:role:type:level`

User ends in `_u`
Role ends in `_r`
Type ends in `_t`

> they can be modified using the "chcon" (change context) command, and seen with "ls"
``
  chcon -u [binary]# user
  chcon -r [binary]# role
  chcon -t [binary]# type
  chcon -l [binary]# level

  ls -Z # list the files contexts
``
> contexts can be restored using the command

``  restorecon [flag] [binary]``

Setting a binary to "bin_t" type will make it run in "unconfined_service_t" wich is controled by DAC instead of MAC
so for example if the "httpd" daemon is running under the "httpd_t" type it's going to confined and MAC are applied, but under the "bin_t" it can access any object that it's allowed to by DAC

## Users :

### Confined & Unconfined :

Every linux user is maped to an selinux user, this allows every user to inherit restrictions from his selinux user

> this mapping can be seen by running

  `semanage login -l`

In redhat linux every user is automatically mapped to the `_default_` user which is mapped to the `unconfined_u` selinux user

> to check if the user is confined or not run this command as the user

  `id -Z`

> to list all the available selinux users run
> Note : that seinfo is not installed by default, `setools-console` package in redhat or fedora

  `seinfo -u`

If an unconfined user runs a confined process he will be restricted by the process limitations

# man

You can look for SELinux related man pages using

```bash
man -k selinux
```

# The Z Flag

## mv

By default `mv` utility will preserve the moved objects contexts for security reasons, like moving you home directory content to your web server's directory by mistake, This will prevent the web server process from accessing you content even if it's in the web server's directory.

If you want to change the moved files contexts just like if you've typed `restorcon`, use the `-Z` flag with the `mv` command.

# Docker

## Docker Volumes

Containers can't access volume content unless it's able to read it and SELinux will deny any attempts to read files that the container isn't allowed to read in the policy. However the file context type and MCS labels can be changed manually using the `chcon` command in the following manner

```bash
chcon -t container_file_t -l s0:c0,c100 /path/to/file
```

The issue is that the container's MCS label changes every time you restart the container, so unless you're planing to never restart your container this might be useful or for testing purposes. But there is an even better way to relabel volumes on the fly every time the container is started and the label will always match, and it's by using the uppercase **Z** or the lowercase **z** mount options.

The uppercase *Z* will label the volume will that particular MCS label for example `container_file_t:s0:c0,c100` which means no other container will be able to access it's contents even if it's explicitly shared, this is useful for exclusive content such as certs, keys...

The lowercase *z* on the other hand will not attach the MCS label like this `container_file_t:s0` so this content will be accessible from any container since they're all able to read content with type `container_file_t`.

An Important Note that is messing in the documentation is that mount options can be comma separated, like for example `ro` options with the `z` option are used like this `-v /path/in/host:/path/in/container:ro,z` and also `:z,ro` is correct, and for docker compose `- /path/in/host:/path/in/container:ro,z`.

## Docker Socket

Install `selinux-dockersock` SELinux module and load it

# semanage

## fcontext

### Equivalency

Making a new directory an equivalent of an old directory is done using the `-e` flag after adding the directory context using the `-a`.

For example we want to change the users directory from `/home` to `/users` for some reason, first we look for the default `/home` directory selinux type

```bash
ls -lZ / | grep home$
```

Under fedora 33 the label is `home_root_t`, this is different from the root user's home directory `admin_home_t`. The we run the following to essentially make `/home` & `/users` equivalent

```bash
semanage -a home_root_t '/users(/.*)?'
semanage -a -e /users /home
```

## port

Manage which ports you processes are able to listen to

```bash
semanage port -a -t [TYPE] -p {tcp | udp} [PORT]
```

List all SELinux ports

```
semanage port --list
semanage port -l
```

# setroubleshoot



# audit2allow

```bash
grep [OBJECT | SUBJECT] /var/log/audit/audit.log | audit2allow
```


# Troubleshooting

There are mainly four sources of issues if you're facing SELinux AVCs

- Labelling Problems
-
