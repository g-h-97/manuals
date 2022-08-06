

# Interface Configuration Files

To setup static network interface configuration in redhat related distros edit `/etc/sysconfig/network-scripts/ifcfg-[IF_NAME]` by replacing the `[IF_NAME]` with the interface name.

# NMCLI

## Don't Stop Asking DHCP

To make Network Manager ask for a lease until an attempt is successful

```bash
nmcli connection modify [IF_NAME] ipv4.dhcp-timeout infinity
```

## Static IP Address

Setting up a static IP address for an interface, this command will edit the interface config file by adding `IPADDR=[ADDRESS/SUBNET_MASK_PREFIX]` to it.

```bash
nmcli connection modify [IF_NAME] ipv4.address [ADDRESS/SUBNET_MASK_PREFIX]
```
# Rsyslog

## Server

To enable the `rsyslog` server capability edit the file `/etc/rsyslog.conf` by uncommenting the lines

```
ModLoad imudp
UDPServerRun 514
```

Then restart the service

```
systemctl restart rsyslog
```

## Client

In order to configure the clients to send log data to the server, edit `/etc/sysconfig/netconsole/`

```
SYSLOGADDR=[RSYSLOG_SERVER_ADDR]
SYSLOGPORT=[RSYSLOG_SERVER_PORT]
```

Then restart the `netconsole` service

```
systemctl restart netconsole
systemctl enable netconsole
```

# Kernel Tunable

## Temporary Change Using Sysclt



## Permanent Change

Edit the file `/etc/sysclt.conf`
