This is about linux firewall front end 'iptables' to control the kernel firewall 'Netfilter', Sources :
> Amazing channel https://www.youtube.com/user/mikemurphycs/videos
> Mike Murphy iptables series : https://www.youtube.com/watch?v=jgH976ymdoQ
> https://www.linuxtopia.org/Linux_Firewall_iptables/
> iptables flow diagram in 'mans' folder

# Basics :

## iptables tables (lowercase) :

- filter
- nat
- mangel
- raw
- security

### The filter table :

Implements Discretionary Access Controls to permitt or deny packets

Chains :

- INPUT : packets destined for the localhost
- FORWARD : packets routed through this host to another distination
- OUTPUT : packets generated by this host going to the network

### the nat table :

Consulted whenever a packet creates a new connection

Chains :

- PREROUTING : changes packets as they arrive from the net interface
- OUTPUT : changes localy generated packets before sending(ex:browser)
- POSTROUTING : changes packets that are going to be sent(ex:from lan)

### the mangle table :

For specialized packet alteration (changes) "rarely used"

Chains :

- PREROUTING : change packet before routing
- INPUT : change packet destined for the host (before app)
- FORWARD : change packet as it's routed
- OUTPUT : change before sending
- POSTROUTING : change packet as it's about te be sent

### the raw table :

For bypassing the firewall altogether

Chains :

- PREROUTING :
- OUTPUT :

### the security table :

Used after the filter table to implement Mandatory Access Control (SELinux) network rules

Chains :

- INPUT :
- OUTPUT :
- FORWARD :


## iptables chains (UPPERCASE) :

- PREROUTING
- INPUT
- FORWARD
- OUTPUT
- POSTROUTING

> Note : user can define new chains
> not add chains can exist in all tables
> chains are executed from top to bottom in the specified order

## iptables targets (UPPERCASE) :

```
	ACCEPT : alow the packet in
	DROP : "delete" the packet without notifiying the sender
	DSCP
	DNAT
	SNAT
	ECN
	REJECT : "delete" the packet and notify the sender using 'icmp' protocol, (see --reject-with)
	REDIRECT
	RETURN
	MASQUERADE : replace the source address, (eg nat)
	MIRROR
	MARK
	QUEUE
	TCPMSS
	TOS
	LOG :  log in journald or syslogd
	ULOG : send log data to an interface (eg: database)
```

> Note : the target is specified after '-j' jump to target or chain if the packet matches the rule

# Rules From / To File :

```
	*filter # this is the table name
	:INPUT ACCEPT [0:0] # input chain default accept policy, with counter to 0 every time
	:OUTPUT ACCEPT [0:0] # output chain default accept policy
	:FORWARD ACCEPT [0:0] # forward chain default accept policy

	-A INPUT -i lo -j ACCEPT # accept all input trafic from loopback interface
	-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT # accept our own trafic			 < \
	-A INPUT -p icmp -j ACCEPT # accept ping requests						   |
	-A INPUT -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT # accept new ssh trafic and keep it
	-A INPUT -j REJECT --reject-with icmp-host-prohibited # after that reject all other trafic in input
	-A FORWARD -j REJECT --reject-with icmp-host-prohibited # reject all forward trafic sice this is not a router
	COMMIT # apply changes to the Netfilter
```

```bash
# To apply rules from file
iptables-restor < rules

# To export rules to file
iptables-save > rules
```










