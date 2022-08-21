

# Privilege Levels

In total Cisco devices has 16 privilege levels `0 - 15`, You will start with low privilege mode which has the number `1`, typing `enable` will immediately grant you privilege level `15` however you can type `enable [LEVEL]` to get to what ever level you want.

The privileged mode `15` has a prompt that end with a hashtag `#` straight after the `hostname`, to check all available command use the question mark symbol `?` in an empty line or within a command to show it's parameters.

If you're in configuration mode which has `()` with some text in them after the `hostname` indicating what config mode it's for, and want to use a *privilege 15* command in config mode use the `do` command before that.

```
do show interface breif
```

To check what privilege level you're in

```
show privilege
```

# Link Types

## Straight Through

## Cross Over

## Serial

A serial link requires

```
clock rate [BAUD_RATE]
```

## Fiber

# IEEE Standards

## 802.3

Ethernet standard

## 802.11 Wifi

This is the wireless family of standards

### 802.1X

LAN/WLAN authentication using an authentication server

## 802.1Q Trunk

Allow traffic from multiple VLANs to be transmitted over a single link without interference by tagging each packet with it's corresponding VLAN ID when passing over the trunk link. It's also called `dot1q` or `dot1Q`.

# IP Addressing

## IPv4

An IPv4 address is a `32bit` number where each byte is separated from the other by a dot `.`
It can be represented in any number base such as *binary, decimal, hexadecimal, base32...*

To check the IP addresses on a Cisco device use the command, in privileged mode or with `do` in config mode

```
show ip interface brief
```

### VLSM

`Variable Length Subnet Mask` is a subnetting method that allow for dividing "subnet" a network address to multiple smaller sub networks in CIDR `Classless Inter Domain Routing` format.

This is done by borrowing some *host* bits and using them as *network* bits instead.

Here is a simple example

```
10.1.10.1/24 -> 00001010.00000001.00001010.00000001/11111111.11111111.11111111.00000000
```

By taking one additional bit to the network side, Will be ( The Subnet Mask Will Change )

```
                                                                               v
10.1.10.1/25 -> 00001010.00000001.00001010.00000001/11111111.11111111.11111111.10000000
```

### Multi-Access Network

A network is called `Multi-Access` when it's able to support more than two addresses in the subnet meaning a mask prefix that equals or more than `/29`.

### NBMA

`No Broad Cast Multi-Access` network.

### IP Summarization

Let's summarize 10.16.0.0/24, 
                     .2.0/24,
                     .4.0/24,
                     .6.0/24

```
00001010.00010000.00000000.00000000 = 10.16.0.0
00001010.00010000.00000110.00000000 = 10.16.6.0
11111111.11111111.11111000.00000000 = 255.255.128.0 WildCard = 0.0.7.255
                                              +64
                                              +32
                                              +16
                                              + 8

                                              248
```

### Subnet/WildCard Mask vs Bits

A MASK is set of 32 bits that as soon as they changed value once the stay that way, it can be a Subnet MASK or Wildcard MASK

```
M 255.255.255.  0   = 11111111.11111111.11111111.0
W   0.  0.  0.255   = 00000000.00000000.00000000.11111111
```

A Subnet or Wildcard bits is series of 32 bits that can be individually changed to 0 or 1, just like and IP address. One example of Wildcard bits usage is in ACLs to match some type of specific traffic.

```
M 254.172.255.  1   = 11111110.10101010.11111111.00000001
W   1. 85.  0.254   = 00000001.01010101.00000000.11111110
```

## IPv6

Is a `64bit` number separated by a colon `:` each `16bit` = `2` Bytes

# Network Types (LAN...)

- PAN `Personal Area Network`
- LAN `Local Area Network`
- MAN `Metropolitan Area Network`
- WAN `Wide Area Network`

# Network Layers

## Three-tier hierarchical model

- Core
- Distribution
- Access

# OSI Model

`Open Systems Interconnection`

## Transport Layer

- TCP
- UDP

## Data-Link Layer

- PPP
- HDLC
- Frame-Relay

# DCE & DTE

- `Date Circuit-terminating Equipment`

The processing end of the link

- `Data Terminal Equipment`

The terminal device, such as user's equipment. The precise definition is not clear yet!

# CSU & DCU

`Channel Service Unit`

`Data Service Unit`


# QoS ToS(DSCP) CoS QoE

## QoS

`Quality of Service`


## ToS

> Source: https://networklessons.com/cisco/ccie-routing-switching/ip-precedence-dscp-values

Uses the `Differentiated Service Code Point` protocol or `DSCP` for short, it's a protocol that uses the `ToS` filed in the IP protocol header to specify packet priority.

+------------+-----------+---+---+-----------+---+---+---+---+
|            | high 3bis |   |   | low 5bits |   |   |   |   |
+------------+-----------+---+---+-----------+---+---+---+---+
| bit number | 0         | 1 | 2 | 3         | 4 | 5 | 6 | 7 |
+------------+-----------+---+---+-----------+---+---+---+---+

The `ToS` filed is one byte where the lower 5 bits represent the service type (which aren't used as often as the priority bits) and the higher 3 bits the priority of the packet, the following tables represents each filed respectively.

High order 3 bits:

+------+----------------------+
| bits | Priority             |
+------+----------------------+
| 000  | routine              |
+------+----------------------+
| 001  | priority             |
+------+----------------------+
| 010  | immediate            |
+------+----------------------+
| 011  | flash                |
+------+----------------------+
| 100  | flash override       |
+------+----------------------+
| 101  | critical             |
+------+----------------------+
| 110  | internetwork control |
+------+----------------------+
| 111  | network control      |
+------+----------------------+

Low order 5 bits, in the old `RFC` standard ( Contine Reading for The New Standard )

+------------+--------------------+------------------+
| bit number | 0                  | 1                |
+------------+--------------------+------------------+
| 3          | normal delay       | low delay        |
+------------+--------------------+------------------+
| 4          | normal throughput  | high throughput  |
+------------+--------------------+------------------+
| 5          | normal reliability | high reliability |
+------------+--------------------+------------------+
| 6 & 7      | reserved for       | future use       |
+------------+--------------------+------------------+

Low order 5 bits, in the new `RFC 1349` standard the bit number `7` is called `MBZ` meaning `Must Be Zero` and it's used for test's only ( Notice bellow only 4 bits are used )

+------+------------------------+
| bits | meaning                |
+------+------------------------+
| 1000 | minimize delay         |
+------+------------------------+
| 0100 | maximize throughput    |
+------+------------------------+
| 0010 | maximize reliability   |
+------+------------------------+
| 0001 | minimize monitary cost |
+------+------------------------+
| 0000 | normal service         |
+------+------------------------+


## CoS

`Class of Service`

## QoE

Quality of Experience takes into account the entire path from end user devices to the internet rather than taking care of the network part only as `QoS` does, this approach has the advantage of getting highly reliable information regarding what the end user is going through when he brows the web.

# Layer 7 Protocols (Application)

## DHCP

`Dynamic Host Control Protocol` is a layer 7 protocol using `UDP` it allows network nodes to get assigned *IP, Gateway & DNS* information dynamically

The steps of this process are called `DORA` for short, and they are as follows

1. DHCP Discover
2. DHCP Offer
3. DHCP Request
4. DHCP Acknowledge

### DHCP Pool

```
ip dhcp pool [NAME]
network [NET_ADDR] [MASK]
default-router [GW_ADDR]
dns-server [ADDR0] [ADDR1]...
lease {DAYS [HOURs] [MINs] | [infinite]}
domain-name [DOMAIN]
```

Where `NAME` is a string or an integer.

### Range Exclusion

```
ip dhcp excluded-address [LOW_ADDR] [HIGH_ADDR]
```

### DHCP Relay Agent

To forward DHCP traffic to different networks or subnets use the `helper-address` command under the `ip` command with the IP address of the DHCP server

```
ip helper-address [DHCP_SERVER_ADDRESS]
```

### DHCP Database Agent

The database agent is not required, however it's recommended to set it up.

### DHCP Snooping

This will prevent rouge DHCP servers on the network from being able to offer IP addresses to the network clients with the goal of performing MITM attacks.

It works by making the interface that the DHCP server is connected to a `trusted` interface so that any `DHCP Discover` will be forwarded to that port only.

```
ip dhcp snooping
ip dhcp snooping vlan [VLAN_ID]

interface [INT]
ip dhcp snooping trust
```

An other important thing is to enable rate limiting in order to prevent DOS attacks on the valid DHCP server, and this is done per interface basis by specifying how Packets are allowed Per Second `PPS`. Enabling this security feature will cause the rouge host's interface to eventually be taken down if the rate limit is exceeded.

```
interface [INT]
ip dhcp snooping limit rate [PPS]
```

Additionally you may want to disable DHCP options forwarding, to prevent `option 82`

```
no ip dhcp snooping information option
```

Finally 

```
show ip dhcp snooping
```


### Troubleshooting

```
show ip dhcp binding
show ip dhcp conflict
show ip dhcp database
show ip dhcp server statistics
```

## DNS

`Domain Name Service` is a service that resolves Host names to IP addresses `Host -> IP` on the network and the other way around `IP -> Host`, the former is called `Forward Resolution` or `Forward Lookup` while the later is called `Reverse Resolution` or `Reverse Lookup`.

```
ip host [Host.Domain] [IP_ADDR]
```



## NTP ?

`Network Time Protocol` allows nodes to synchronise clock over an `NTP Server`, this can be done with or without authentication.



# Layer 4 Protocols (Transport)

## TCP

`Transmission Control Protocol` is connection oriented layer 4 protocol with many features such as

- Retransmission
- Packet order

## UDP

`User Datagram Protocol` is connectionless layer 4 protocol, used mainly in real-time application such video and voice transmission over the networks due to it's low latency.

# Layer 3 Protocols (Network)

## HSRP/VRRP/GLBP

These protocols provide a virtual interface for the hosts on the network, this virtual interface abstracts two or more physical interfaces with a single MAC address which will be the gateway for the network.

`HSRP` or Hot Standby Router Protocol
`VRRP` or Virtual Redundancy Router Protocol

## Routing Protocols

### Link-State vs Distance-Vector

In `Link-State` routing the router shares information about it's neighbors only, whereas in the `Distance-Vector` the  information about the entire Autonomous Systems is shared.


#### Routing Decisions

One of the most important things is how the router "chooses" which route to send the packet, in `LS` method it's selected based on the `Cost` of the route, while `DV` this decision is based on the `Number of Hops`.

#### Convergence Time

`LS` based routing algorithms have fast convergence times, while `DV` ones take longer to do so.

#### Examples

> Link-State
- `OSPF`

> Distance-Vector
- `RIP`
- `EIGRP`

### Administrative Distance

The lower the route's AD the higher it's priority in the routing table

- Static Route -> 1
- EIGRP -> 90
- OSPF -> 110
- iBGP -> 200


### OSPF

#### Acronyms

`LSR`: Link State Request
`LSA`: Link State Advertisement
`LSDB`: Link State Database
`DBD`: Database Description
`DR`: Designated Router
`BDR`: Backup Designated Router
`ABR` Area Border Router
`ASBR`: Autonomous System Boundary Router

#### Keywords

- Area
- Stub Area
- Inter Area Routing
- Intra Area Routing

#### Router ID

Each router on an OSPF routed network has a `32 bit` dot byte separated number that represent the router in the network which is called the `router-id`.

This ID can be changed using the command

```
ip ospf [PID]
router-id [A.B.C.D]
```

The router ID can be manually or automatically assigned, and these are the steps by priority

- The manually assigned ID
- The highest IP address of one of the loopback interface
- The highest IP address of one of the interfaces

#### DR & BDR


Since OSPF is a link state routing protocol each router need to know about every other router in the topology, for example if there are 4 routers there would be 6 adjacencies in total base on the equation

$n*(n-1)/2$

Where $n$ is the number of nodes in the graph. This is clearly is not efficient in terms of link negotiations, for this reason the `DR` and `BDR` were invented.


#### ABR & ASBR

`ABR` or `Area Border Router` is router which have interfaces belonging to multiple areas at once, and areas use the same routing protocol by definition.

`ASBR` or `Autonomous System Boundry Router` is a router which have interfaces belonging to multiple Autonomous Systems at the same time, meaning networks that use different routing protocols.

#### Overview

> Note: this is about `OSPF v2` meant for `ipv4` only, and not `OSPF v3` which is for `ipv6`

`OSPF` (Open Shortest Path First) is a `Linke-State` intradomain routing protocol, meaning that it checks it's neighbors links to check whether they're running or not; This is done by sending `LSA` (Link State Advertisment) packets to build `LSDB` (Link State Database) over which the best information is then copied to the routing table. The `OSPF` protocol uses the multicast address to send/receive protocol specific packets such as the Hello packet.

The cost function is like the following

$Cost = Reference_Speed / Link_Speed$

> Where:
>       Reference_Speed = 100 Mbps = 1.000.000 bps

Note that if multiple routes have the same cost OSPF will loadbalance the traffic amongst them.


The basic steps required to setup `OSPF` on a router are

```
router ospf [PID]

netowrk [NETWORK] [WILD_MASK]
```

Setting up the default route

```
default-information originate
```

Disabling `OSPF` Hello and `LSA`s packets on a specific interface

```
passive-interface [INTERFACE]
```

Setting the router's priority so that it has better chance of becoming the network `DR` or `BDR`, it takes values in the range `[1 - 255]` the higher the number the higher the probability in the election process. The default value is `1` and routers with value equal to `0` cannot become the `DR` or the `BDR`

```
ip ospf priority {1 - 255}
```

Set the network type of the `OSPF` interface

```
ip ospf netowrk {broadcast | point-to-point}
```

#### OSPF Network Types

- Broadcast
- Non-Broadcast
- Point-to-Multi-Point
- Point-to-Multi-Point Non-Broadcast
- Point-to-Point

##### Non-Broadcast

An example topology for that is the one bellow, where the routers 2, 3 & 4 can't reach each other with broadcast traffic since the router 1 is not going to forward "layer 2" traffic.

    ___ 2
  /
1+----- 3
`  \____ 4`

In this type we should configure the adjacencies of `DROther` routers with the `DR` & `BDR` manually, since they are on different broadcast domain.

```
ip ospf `
```

Also the `Hello` and `Dead` intervals are going to change from `10s` to `40s` & from `30s` to `120s` respectively.

##### Point-to-Multi-Point

This type eliminates the need for a `DR` or a `BDR`

##### Point-to-Multi-Point Non-Broadcast

This also does not need a `DR` and a `BDR`, however this needs manual adjacencies configuration.

#### Reference Bandwidth

```
ip ospf 1
auto-cost reference-bandwidth [Mbps]
```

#### OSPF Troubleshooting

Check the `Neighbors` and the `State` of the link with them

```
ip show ospf neighbor
```

Check whether `OSPF` is enabled in interface INTERFACE

```
show ip ospf interface [INTERFACE]
```

Check the `LSDB`

```
show ip ospf database
```

Verify the `OSPF` Section in the `running` configuration

```
show run | section ospf
```

Access lists might be blocking `OSPF` packets

```
# list all access lists
show access-lists

# edit access list
ip access-list extended [NAME]

# add permit rule
[PRIORITY] permit ospf any any
```

Debug `OSPF` Hello packets, this helps debug mismatch configuration like subnetmask and hello-dead intervals and so on

```
debug ip ospf hello
debug ip ospf packet
debug ip ospf adj

clear ip ospf process
```

### EIGRP

`Enhanced Internal Gateway Routing Protocol` is a Distance Vector routing protocol meaning ...

#### Split-Horizon

Fill this when you want

### ISIS

`Intermediate-System to Intermediate-System` is a link state routing protocol

### BGP

`Border Gateway Protocol` is a `Vector State` interdomain routing protocol that uses the `Best Path` algorithm

#### iBGP

`internal Border Gateway Protocol`

#### eBGP

`external Border Gateway Protocol`


## VoIP

`Voice over Internet Protocol` is way to make real time communication over a network that is base on the `IP` protocol, this involves using.

### SIP

### RTP

`Real Time Protocol`

### SCCP (Skinny Protocol)

`Skinny Client Control Protocol`

### CODEC

`Coder / Decoder` is software that translates `Analog` wave forms such as *Voice* pressure waves to the `Digital` Domain so that it is transmittable over a digital network.

Codecs such as

```
G.711 PCMU ( U for USA )
G.711 PCMA ( A for ALL )
```

### MOS & R-Factor

Mean Opinion Score, is a metric from [1, 5] of how well the VoIP call was. MOS used to relay on user provided feedback after each phone call to, however this is no longer required.

The R-Factor replaced MOS for more precision, it provides a range from [1, 120].

## VPN

`Virtual Private Network`

### Protocols

#### GRE

`Generic Route Encapsulation` allow multicast traffic to be tunneled over the network

- Protocol 47
- Port

#### IPSec

`Internet Protocol Security` is a collection of protocols that helps encrypt VPN traffic

- Port 500 (IKE)
- Port 4500 (NAT-Traversal)
- Port N/A (ESP)
- Port N/A (AH)


#### PPTP

- TCP Port 1723
- GRE Port N/A

#### SSTP

- TCP Port 443

#### L2TP

- UDP Port 1701

#### L2TP with IPSec

- UDP Port 1701 (L2TP)
- UDP Port 500 (IPSec)
- UDP Port 4500 (NAT-Traversal)

#### OpenVPN

- UDP Port 1194
- TCP Port 1194

#### IKEv2

- UDP Port 500 (IPSec IKEv2)
- UDP Port 4500 (NAT Traversal)





# Layer 2 Protocols (Data-Link)

## CDP & LLDP

The `Cisco Discovery Protocol` and `Link-Layer Discovery Protocol` are used to find out who is the neighboring node sending these. The information in the packets include ** Device Type, Software Version, Host Name **.

It's worth mentioning that `CDP` is a Cisco proprietary protocol, while `LLDP` is an open standard while being much more powerful than the former since you can specify the information to be shared with other nodes manually, as well as the ability to toggle either transmission or reception separately which is not possible in `CDP`.

```
# start CDP or LLDP
cdp run
lldp run

# start CDP on single interface (Disable Globally First)
cdp enable

# check CDP neighbors
show cdp neighbors {detail}
show lldp neighbors

# start LLDP transmit and recive per interface basis
lldp transmit
lldp recive
```

## STP

`Spanning Tree Protocol` is responsible for preventing loops in a network.

For details on STP

```
show spanning-tree
```

### BPDU : `Bridge Protocol Data Unit`



### Types

#### RSTP : `Rapid STP`


#### PVST+ : `Per VLAN Spanning Tree +`

## ARP

`Address Resolution Protocol` maps MAC addresses to IP addresses

```
# For the ARP table
show ip arp
```

## Frame-Relay ?

Works with sub interfaces as PPP links

### PVC

`Private Virtual Circuit` it a link a connection from one site to an other.


### DLCI

`Data Link Connection Identifier`

### LMI

`Local Management Interface` Is the management protocol that is sent between frame-relay switches to communicate which `DLCI`s are available and whether there is a congestion in the network or not.

## PPP (Point-to-Point Protocol) ?

In configuration mode the `hostname`, `username` & `password` must be specified, please note that `hostname` and `username` represents the same thing and each node must know the `hostname` of the other node in a form of a `username`.

So in the configuration mode `configure terminal`, On R1

```
hostname r1
username r2 passwrod PASSWORD
do debug ppp negotiation
interface serial 2/0
```

And on the other end R2

```
hostname r2
username r1 password PASSWORD
do debug ppp negotiation
interface serial 2/0
```

Continuing the configuration on R1 as the `DCE` and R2 as the `DTE` in the `config-if` mode

```
encapsulation ppp
ppp authentication chap
ip address [IP_ADDR] [MASK]
clock rate threshold 64000
no shutdown
```

On R2

```
encapsulation ppp
ppp authentication chap
ip address [IP_ADDR] [MASK]
no shutdown
```

### Authentication

#### PAP

`Password Authentication Protocol` this authentication method sends password on plaintext with is really dangerous.

```
ppp authentication pap
```

#### CHAP

`Challenge Handshake Authentication Protocol` allows to use a challenge-response authentication

```
ppp authentication chap
```

#### EAP

`Extensible Authentication Porotocol`

#### MS-CHAP

- MS-CHAP `Microsoft CHAP`
- MS-CHAP-V2 `Microsoft CHAP V2`

## HDLC

`High-level Data Link Control`

- Cisco proprietary protocol
- Bit oriented
- Point-to-point and multipoint
- No authentication mechanism

# Metro-Ethernet ?


# SD-WAN

The new VPN stuff

## OMP Protocol

`Overlay Management Protocol`

## vSmart

SD-WAN Controller

# Sub Interfaces

To create sub interfaces make sure that you're in the parent interface configuration mode and it's `no shutdown`, specify the sub interface with the `interface` command followed by the type then the `ID` which should be the same as the parent's then a dot `.` followed by the sub interface's number `SUBINT_NUMBER`

```
interface [TYPE] [ID]
no shutdown
interface [TYPE] [ID.SUBINT_NUMBER]
```

After this you can configure the sub interface just like you would do with a physical one, here are some useful examples

```
ip address [ADDR] [MASK]
encapsulation dot1Q [VLAN]
```



# VLANs

`Virtual Local Area Network` 

To put a switch port or a range of interfaces in either `access` or `trunk` mode use the following list of commands respectively

```
switchport mode access
switchport access vlan [VLAN_ID]
```

```
switchport trunk encapsulation { dot1q | isl }
switchport mode trunk
```

To check which ports are on which VLAN

```
show vlan breif

show interface status
```

## VTP & DTP

`VLAN Trunking Protocol` & `Dynamic Trunking Protocol`

## Access & Trunking Protocols

In Access mode only the allowed VLAN tag is allowed through that interface, so the packets must be tagged with the same VLAN tag to get passed to the VLANs it's meant for; One important aspect through is that VLAN tags don't make it to the VLAN networks them selves since they're only needed in switch to switch communications.

Trunk mode however is a mode that allows packets from all VLANs to coexist in the same wire as long as every packet is tagged or encapsulated with/in the appropriate VLAN ID/header.

### 802.1Q

Is the standard protocol encapsulation for trunk packets, also called `dot1q`.

### ISL

`Inter-Switch Link` Is the cisco proprietary variant of trunk encapsulation.

# Switching

## Transparent Switching Methods

- Learning
- Filtering
- Flooding
- Forwarding
- Aging


## Multi Layer Switch

Multi layer switches are able to function in both OSI model layers 2 & 3

```
# to make the interface a layer 3 one
no switchport
```

### Routing

Multi layer switches support routing hence the "Multi-Layer", to enable this capability which is disabled by default

```
ip routing
```

### SVI

`Switch Virtual Interface` are a multi-layer switch feature that allows for creating a layer 3 virtual interface.

For example for creating an `SVI` in a VLAN network

```
interface vlan [NUMBER]
ip address [ADDR]
```

#### SVI Not Routing

> https://learningnetwork.cisco.com/s/question/0D53i00000Kt58BCAR/svi-routing-issue
> https://community.cisco.com/t5/switching/svi-does-not-route-traffic/td-p/2559720

`no ip cef`

# EtherChannel

Etherchannels allow for port aggregation in Cisco equipment either by using Cisco's proprietary protocol `PAgP` -> `Port Aggregation Protocol` or the open standard `LACP` -> `Link Aggregation Control Protocol`. Etherchannel in able to handle up to 8 ports total in a single logical channel group.

It's also called *Bonding, Teaming, LAG -> `Link Aggregation Group`*

> Warning: Every time a new Etherchannel is about to be defined, make sure that the interfaces in question are `shutdown` on both sides other ways you'll face issues making the negotiations between the two logical links in case a dynamic protocol is being used.

## Layer 2

```
interface range [TYPE] [SLOT/START_PORT - END_PORT]
switchport mode trunk
channel-protocol {lacp | pagp}
channel-group [GROUP_NUMBER] mode {on | active | passive | auto | desirable}
end
```

- Dummies

```
enable
configure terminal
interface range [TYPE] [SLOT/START_PORT -END_PORT]
switchport mode {trunk | access}

#if in vlan use access
switchport mode access vlan [NUMBER]

channel-group [GROUP_NUMBER] mode {on | auto | desirable | passive | active}
end
```

- Protechgurus

```
interface range [TYPE] [SLOT/START_PORT -END_PORT]
channel-group [GROUP_NUMBER] mode {on | auto | desirable | passive | active}
exit
interface port-channel [GROUP_NUMBER]
switchport mode {trunk | access}
```

- Test

```
interface range [TYPE] [SLOT/START_PORT - END_PORT]
channel-protocol {lacp | pagp}
channel-group [GROUP_NUMBER] mode {on | auto | desirable | active | passive}
exit

interface port-channel [GROUP_NUMBER]
switchport mode trunk
switchport mode access
switchport access vlan [ID]
```

## Layer 3 Port Channel

This creates the ether channel

```
interface port-channel [GROUP_NUMBER]

ip address [IP] [MASK]

end

show running-config interface port-channel [GROUP_NUMBER]
```

> Where GROUP_NUMBER = `{1 - 256}`, however you can only create a maximum of `128` port channels in total

This adds any port to the `port-channel [GROUP_NUMBER]` that we've created before

```
interface range [TYPE] [SLOT/START_PORT -END_PORT]

channel-protocol {lacp | pagp}

channel-group [GROUP_NUMBER] mode {on | auto | desirable | passibe | active}

show running config interface [TYPE] [SLOT/PORT]
show interfaces [TYPE] [SLOT/PORT] etherchannel
```

> Where: TYPE = {fastethernet | gigabitethernet | tengigabitethernet}

Note that `LACP` supports `{passive | active}` only, and `PAgP` supports `{auto | desirable}` only. In `on` mode the interfaces will not do any negotiations and the interfaces on the other end must be set to `on`.

For `LACP` the port priority cat be set also, the lower the number the higher the priority. The default is `32768`

```
lacp port-priority {1 - 65535}

show lacp sys-id
```

- Examples

```
int range gig 0/1 -3

channel-group 1 mode on

end
```

## Load Balancing

```
port-channel load-balance {src-mac | dst-mac | src-dst-mac | src-ip | dst-ip | scr-dst-ip | src-port | dst-port | src-dst-port}

show etherchannel load-balance
```

## Min Links

This set the minimum number of available links in "link-up state" to bring the `port-channel` to the up state. Note that this is only supported on `LACP`

```
interface port-channel [GROUP_NUMBER]

port-channel min-links [NUMBER]

end

show running-config interface port-channel [GROUP_NUMBER]
show interface [TYPE] [SLOT/PORT] etherchannel
```

## LACP 1:1 Redundancy

This feature uses only two ports the higher priority one is `active` and the lower priority port is on `standby` mode. This require the `min-link` feature to be set to `1` to allow the `port-channel` to switch to the `link-up` state even this one port only

```
interface port-channel [GROUP_NUMBER]

lacp fast-switchover

lacp max-bundle 1

port-channel min-links 1

end

show running-config port-channel [GROUP_NUMBER]
show interface [TYPE] [SLOT/PORT] etherchannel
```

- Example

```
configure terminal

lacp system-priority 33000

interface range fastethernet 5/6 -7

channel-protocol lacp

channel-group 1 mode active

interface fastethernet 5/6

lacp port-priority 33000

interface port-channel 1

lacp fast-switchover

lacp max-bundle 1

port-channel min-links 1

end
```



# Virtual Switching System

## Keywords

`VSS`: Virtual Switching System
`VSL`: Virtual Switch Link
`MEC`: MultiChassis EtherChannel
`SSO`: Stateful Switch Over
`NSF`: Non Stop Forwarding
`NFSU`:
`RPR`: Route Processor Redundancy

## Overview

This feature allows for clustering tow cisco switches to from one logical/virtual switch. One of the two switches take the `Active` role while the other take `Standby` role, the communication between the two is done using the `VSL` which is an `EtherChannel`.

An Access switch or a "client" can form an `EtherChannel` with both the switches since they're one logical switch and which is called `MEC`.

The `VSS` configuration offers redundancy by having the `Standby` switch monitoring the `Active` switch for failure signs by the `VSL`, if the `Active` switch fails the `Standby` will take over as the `Active` one until it recovers. If for whatever reason the `VSL` fails both the switches will be `Active` and the Dual-Active Detection will initiate a recovery.

## Configuration

Enable `SSO` and `NSF`

```
redundancy
sso
exit
router [PROTOCOL] [PID]
nsf
end
```

Assigning Virtual switch domain and switch numbers

```
switch virtual domain [NUMBER]
switch [SWITCH_NUMBER]
```

Configuring `VSL` port channel and ports

```
interface port-channel [GROUP_NUMBER]
switch virtual link [SWITCH_NUMBER]
no shutdown
exit
```

> The domain `NUMBER` must be the same on both switches, while the `SWITCH_NUMBER` must be different alongside the `GROUP_NUMBER`.

Adding the `VSL` configuration we did earlier to the physical `VSL` tengigabit ports

```
interface range [TYPE] [SLOT/START_PORT - END_PORT]
channel-group [GROUP_NUMBER] mode on
no shutdown
```

> Note here that the `GROUP_NUMBER` is different on every switch.

Start the conversion process on both switches

```
switch convert mode virtual
```

After reboot, check the configuration on the `Active` switch since the `Standby` switch will no longer by available for configuration

```
show switch virtual
show switch virtual role
show switch virtual link
```




```
switch [SWITCH_NUMBER] priority [PRIORITY]
```


```
reload
redundancy reload peer
redundancy force-switchover
redunduncy reload shelf
```

# Access Control Lists

Access Control Lists or `ACL`s represent a system to match packets and perform an action based on a LIST of RULES that ends with an explicit deny for all types of traffic. 

`NOTE 1:` Access Control Lists are ALWAYS read/interpreted from TOP.
                                                               |
                                                            to |
                                                               V
                                                            BOTTOM

`NOTE 2:` ACLs aren't of much use if they are not applied to the interfaces as `in` for inbound or `out` for outbound traffic matching rules.

There are mainly two types of ACLs as follows:

## Standard

The Standard Access List is only able to match on/look at on the source IP address of the traffic, it can match on one IP or range of IPs. Based on the definition, we can conclude that Standard ACLs are limit to a subset of Layer 3 when inspecting traffic.

Standard ACLs are numbered in the rage `[1, 99]`, and they also could be named `NACL` Named Access Control List.

### Matching Basics

Matching on a single IP with key word `host` or IP address with wildcard bits `0.0.0.0` or by just specifying the IP address with no mask added by Assuming 32 bit Match in STD ACLs. The following is an example of how to apply a `permit` rule for a single source IP in STD ACL.

```
permit host [IP]
permit [IP] 0.0.0.0
permit [IP]
```

### Standard ACL Syntax

#### Numbered

To create a number access list

```
access-list [NUMBER]
```

#### Named

To create a named access list

```
ip access-list standard [NAME|NUMBER]
[ACTION] [SourceIP]
```

This will put us in `(config-std-nacl)` mode, and number the access list rules automatically making inserting new lines in the middle that much easier. Any time you want to add or remove a rule

```
ip access-list standard [NAME|NUMBER]
[RULE_NUMBER] [ACTION] [SourceIP]
```

## Extended

As we've discussed earlier Standard ACLs are limit to Layer 3 matching, with Extended ACLs we've got the ability to match/inspect traffic based on Source & Destination IP addresses AND any Layer 4 protocol as well as on port number. This allows for far more precise and flexible matching of traffic under various conditions.

- Qos
- Marking Traffic

Extended ACLs are numbered in the rage `[100, 199]`, and they also could be named `NACL` Named Access Control List.

### Extended ACL Syntax

```
access-list
[ACTION] [PROTOCOL] eq [SRC_PRT] [SRC_IP] [DST_IP] eq [DST_PRT]
```

## Apply to Interface

```
interface [INT]
ip access-group [NUMBER|NAME] {in|out}
```

Interface types that allow ACLs application
- L3 Physical Switch Port
- Router Interface
- Switch Virtual Interfaces SVIs (int vlan [NUMBER])
- IP Sub-Interfaces

## Apply to VTY Line ?????????????????

```
line vty [NUMBER]
access-class
```

## Troubleshooting Commands

```
show access-lists
```

# Grep Output ??????????????????????

To grep for somthing in a cisco device you can use `include` or to grep for the opposite use `exclude` the main command for both of these is the `section` command since `include` & `exclude` are aliases for `section include` & `section exclude` respectively, this is done in the same way that a unix like OS does it meaning after a pipe `|`

To find line with {expression} in the output

```
[CMD] | include {expression}
[CMD] | in {expression}
```

To remove lines with {expression}

```
[CMD] | exclude {expression}
[CMD] | ex {expression}

show ip interface brief | exclude unassigned

# can be shortened to
sh ip int brief | ex unass
```

# ROAS ( Router On A Stick )

`Router On A Stick` is router that is connected to the network with only one interface, this means that in order for it to route between subnets sub interfaces must be used. 

`ROAS` is mostly used in inter VLAN Routing as the following example shows if the router is connected with the `ethernet 0/0` to a trunk link that carries packet from VLANs `10, 11` and `12`

```
interface ethernet 0/0.10
encapsulation dot1Q 10
exit

interface ethernet 0/0.11
encapsulation dot1Q 11
exit

interface ethernet 0/0.12
encapsulation dot1Q 12
exit
```

# Port Mirroring

Unlike in a network simulation software it's much more complicated to capture traffic in the network links for analysis, thats not to say that it's not doable however it requires a bit of setup to do.

- Mirror a Port to an other Port and hook into it, it's called `mirroring`, `monitoring` & `SPAN`. This will basically make the mirrored port work like a hub but just on the mirrored interface where the switch will copy the traffic on all mirrored interfaces.

- Put a Hub in the link you want to eavesdrop on ( Requires Hardware )

```
monitor session [NAME] source interface [SOURCE_INT]
monitor session [NAME] destination interface [TARGET_INT]

# To check
show monitor session [NAME]
```

## SPAN

`Switch Port Analyzer` is a way to sniff and analyze network traffic of an interface on an other interface by copying the traffic as it is. There is also `RSPAN` which stands for `Remote SPAN` that will allow for traffic sniffing over the network by creating a tunnel an forwarding the captured traffic from the source device to a remote port on an other device which allow for analysis.

# Debugging

To start debugging some functionality

```
debug [WHAT?]
```

To stop debugging

```
un all
```

# Cloud

- SaaS `Software as a Service`

> Provides software only no more, meaning that the user can't control the underlaying layers such as the OS...

- PaaS `Platform as a Service`

> This provides control over the Operating System layer only.

- IaaS `Infrastructure as a Service`

> This model allow for full control over the underlaying infrastructure.

# Server Types

## Authentication

### TACACS

`Terminal Access Controller Access-Control System`

### XTACACS

`Extended TACACS` Introduced by Cisco with no backward compatibility with the original implementation

### TACACS+

`TACACS Plus` Also developed by Cisco 

### RADIUS

Auth server


# PIS ( Packet Inspection Systems )

## Types

### SPI ( Shallow Packet Inspection )

The SPI is what every router or switch does, meaning that only the layer2 and 3 packet information are checked I.E the destination & source MAC and IP addresses are verified.



### MPI ( Medium Packet Inspection )

### DPI ( Deep Packet Inspection )

# Cisco Firmware Upgrade

```
enable
copy usbflash0:cat3k_caa-universalk9.16.03.09.SPA.bin flash:
config terminal
boot system flash:cat3k_caa-universalk9.16.03.09.SPA.bin
platform software package install switch file flash:cat3k_caa-universalk9.16.03.09.SPA.bin
write
reload

request platform software package clean
show version
```

# Wireless

## Modes

- Autonomous mode (Standalone)
- Lightweight mode (Requires WLC to work)


## Split-MAC Architecture

This type of wireless architecture is when Wireless controller is introduced on the network.

### WLC

Wireless Lan Controller, works as a central brain to multiple APs 

### CAPWAP & LWAPP

Control And Provision Wireless Access Points, Protocol allows an access point to talk to its controller over large distances over different networks or even the internet. This is done by using two logical tunnels between the WLC and the AP.

- One for control plane at UDP 5246
- One for data plane at UDP 5247

### Operation Modes

- `Local`: Sends all traffic to the controller (Control + Data) as if the controller is on the same location(?)
- `Bridge`
- `Flexconnect`: If the WLC drops for what ever reason, the AP will switch traffic locally instead of disassociating
- `Monitor`: This mode help detect wireless based attacks such as rouge access points nearby
- `Reap`
- `Rogue`: Similar to Monitor mode
- `Se-connect`: Spectrum Analyzer mode
- `Sniffer`: The AP turns in to promiscuous mode to sniff the traffic on the area as a packet capture of `pcap` file

# MPLS

`FEC`: Forwarding Equivalence Class
`LSP`: Label Switched Path
`LSR`: Label Switched Router
`LDP`: Label Distribution Protocol

- Packets are forwarded based on their `FEC` to the right `LSP` by an `LSR`
- Labels are shared across the network using `LDP`

# EPC Embedded Packet Capture Example

- Create an extended ACL in global config mode
> ip access-list extended PCAP_ACL

- Create a buffer for the PCAP in privileged mode
> monitor buffer BUF size 2048 max-size 1518 linear

- Added the ACL to the buffer
> monitor capture buffer BUF filter access-list PCAP_ACL

- Create a capture point on an interface
> monitor capture point ip cef POINT fastethernet 0/1 both

- Attache the buffer to the capture point
> monitor capture point associate POINT BUF

- Start capture
> monitor capture point start POINT

- Wait for a while for the buffer to fill-up
> monitor capture point stop POINT

- List buffer contents (In HEX)
> monitor capture buffer BUF dump

- Export pcap to tftp machine
> monitor capture buffer BUF export tftp://IP/BUF.pcap

- Clean
> no monitor capture point ip cef POINT fastEthernet 0 both
> no monitor capture buffer BUF
