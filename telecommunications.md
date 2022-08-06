

# 2G:

## Hardware

### Vertical Antennas

Used for Radio Frequency `RF` communications

### Circular Antennas

- Used for microwave communications
- Line Of Site `LOS` communications between two antennas


## Base Transceiver Station BTS

Base Station Subsystem `BSS` like a RAN
NSS for core network functionality

## Base Station Controller BCS

Is the controller that is connected to the BTS to make decisions such as handover

- Processing Unit
- TRx
- ?

## Core Network CS

2G networks are divided in to two part Circuit Switched `CS` for voice communications & Packet Switched `PS` for Data communications

## Circuit Switching

MSC:


## Packet Switching

SGSN
GGSN

## BSS (Like RAN)

BTS
BSC Base Station Controller, for controlling the number of BTSs

# 3G:

## Universal Terrestrial Radio Access Network UTRAN

Node-B
RNC Radio Network Controller, for controlling the number of Node-Bs

## Core Network CN

Like 2G networks, 3G nets also are characterized by two types of switching `CS` for voice and `PS` for data

# 4G/LTE:

The new 4G/LTE architecture is based on System Architecture Evolution `SAE` principle

The Evolved User Equipment `E-UE` connects directly to the Evolved Node B `E-NodeB` for a faster handover, since the handover decision is done at the `E-NodeB` level.

The Radio Access Network `RAN` part in LTE networks is called Evolved Universal Terrestrial Radio Access Network or `E-UTRAN` which is connected to a core network called Evolved Packet Core i.e `EPC`

Radio Network Controller `RNC`

## Evolved Universal Terrestrial Radio Access Network E-UTRAN

The main element is `E-UTRAN` is the `E-NodeB`, `E-NodeB`s are connected to each other by an interface called `X2` since there is no central controller to manage handovers meaning that they must communicate in a mesh network

## Evolved Packet Core

### Signalling Plane / Control Plane

#### Mobility Management Equipment MME

`E-NodeB` connects to it to pass signalling traffic/flow

- Authentication
- Tracking

#### Home Station Subsystem HSS

Permanent Data Base for all subscriber information

### User Plane / Data Plane

#### Serving Gateway SGW

`E-NodeB` connects to it to pass data traffic/flow, then the `SGW` will connect to the `PGW`

#### PDN or Paging Gateway PGW

The `PGW` connects to the Public Data Network `PDN` as well as to the Policy Control and Charging Rules Function `PCRF`

- IP Allocation


# 5G

Full IP Connectivity

# Elements

## PCRF

## PCEF

## OCS

## OFCS

# Interfaces

`S1`: The interface between the `E-UTRAN` and `EPC`
    - `S1-C`: Control Plane is a sub interface of the `S1` interface, which represents Control Plane Traffic between the `E-NodeB`s and the `MME`
    - `S1-U`: User Plane is a sub interface of the `S` interface, it represents the Data Plane Traffice between the `E-NodeB`s and the `SGW`

`Gx`: `PCRF` -> `PCEF`
`Gy`: `OCS` -> `PCEF`
`Gz`: `OFCS` -> `PCEF`

# Phenomena

## Cell Breathing

This occurs when a particular `NodeB` gets overloaded, by reducing the coverage radius of that particular `NodeB` and increasing the radius of neighboring `NodeB`s by doing so the edge users i.e User Equipment/Mobile Stations `UE/MS` of the overloaded `NodeB` are going to be forced to switch to the neighboring ones by doing what's called a group handover; Cell Breathing is a form of Load Balancing in Code Division Multiple Access `CDMA` based networks.

# Circuit Switching Fall Back CSFB

This functionality allows the `UE/MS` to drop to 2G `GSM` or 3G `UMTS` when a voice call is initiated while the device is connected to 4G `LTE` and the network does not support IP Multimedia System `IMS` i.e no Voice Over LTE `VoLTE` support; As soon as the voice call ends the `UE/MS` switches back to 4G `LTE` mode.

# Network Core Operating Systems

## Magma Core

`https://magmacore.org`
