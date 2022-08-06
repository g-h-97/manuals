
# Theory

## 

- Control Plane
- Data Plane (Forwarding Plane)
- Management Plane (Application)

## SDN: Software Defined Networking

The full potential of a Software Defined Network isn't going to appear unless the services infrastructure is `NFVed` in the first place, since migrating a service from one host to another will require network changes. Hence making our networks software defined will make the operation much easier by introducing what is known as the "Controller" on the "Control Plane", which will push the required "Flow Table" Entries to the "Data Plane" Layer made of white box "Switched & Routers", this will allow the traffic to flow as usual to the migrated service without any human intervention.

## NFV: Network Function Virtualization

In essence, NFV is deploying network services such as `DHCP, DNS...` on software instead of hardware appliances directly.

## North & South Bound APIs

Northbound API is the communication channel that allows the application layer to talk to the controller, interfaces such as `Python, RESTAPI ...` are used

Southbound API is the communication channel between the controller and the networking equipment, it uses protocols such as `OpenFlow, NetConf ...` to configure the `Flow Tables` on the network devices.


## Protocols

- OpenFlow
- P4
- OVSDB
- NETCONF
- SNMP
- BGP
- More...

## YANG Modles

YANG is a data modeling language, aimed at modeling the data manipulated by the `NETCONF` protocol, It is based on the `Northbound / Southbound` concept which is also called `Producer / Consumer` interaction. In this type of communication the `Producer` provided APIs that the `Consumer` can use to request(consume) data from the producer; The data is stored by the `Producer` on a SAL storage and read by the `Consumer` from there.

- IEFT
- OpenConfig
- Native (Hardware Vendor's)

This a `json` like representation of data such as interfaces, ports...

## Layers

- Infrastructure Layer (Switches, Routers...)
- Control Layer (Controllers)
- Application Layer (Controllers Management)

## Controllers

### ODL: OpenDayLight

Developed by the Linux Foundation

#### Components

- odlparent
- controller
- MD-SAL (Model Driver Service Abstraction Layer)
- yangtools

### ONOS: Open Network Operating System

Developed by the Open Networking Foundation `ONF` at `https://opennetworking.org`
URL: `https://wiki.onosproject.org`


# Application

## Mininet

### Topologies

- linear
- single

## Controllers

### ODL: OpenDayLight

#### Installation

This installation process was done on Archlinux, the required packages are

- opendaylight package from the official web site
    - https://docs.opendaylight.org/en/latest/downloads.html
- java JRE (Java Runtime Environment) 11 `jre11-openjdk`

Commands:
`Note: use sudo if required`

```
yay -S jre11-openjdk

# to check what version of jre is running
archlinux-java get

# to set it to the right one (jre11)
archlinux-java set java-11-openjdk
```

After setting up the java environment, run `karaf` after inflating the `opendaylight-version.tar.gz`

```
gzip -d opendaylight-version.tar.gz
tar xvf opendaylight-version.tar.gz
cd opendaylight-version.tar.gz/bin
./karaf
```

#### Features

Installing `karaf` features

- `ALTO`: Application Layer Traffic Optimization


### ONOS: Open Network Operating System

- Before deploying ONOS, java must be installed on the host

``` Ubuntu
apt install openjdk-11-jdk
```

``` Archlinux
yay -S jre11-openjdk

# to check what version of jre is running
archlinux-java get

# to set it to the right one (jre11)
archlinux-java set java-11-openjdk
```

- Download the `.tar.gz` file from `https://wiki.onosproject.org/display/ONOS/Downloads`
- Extract it using `tar xzf onos-[version].tar.gz`
- Create `sdn` using `useradd sdn --system --group`
- Start ONOS using `bin/onos-service start`

- Access the web UI `http://[IP]:8181/onos/ui/index.html`
    - Username: unos
    - Password: rocks


- Install the following `Applications` to enable southbound communications with network hardware using `Openflow` and `OVSDB` protocols respectively
    - `Openflow Provider Suite`
    - `OVSDB Provider`

#### Testing

Create a simple topology using mininet `sudo mn --controller=remote,ip=[Controller_IP] topo=linear,4`, this should show on the topology view in the ONOS Web UI as 4 switches.
