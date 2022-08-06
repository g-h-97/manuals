
- LMS: Licence Management Server
- EMS: Element Management Server

# Download from CLI

```
curl --header 'Host: files.support.sandvine.com' --user-agent 'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:88.0) Gecko/20100101 Firefox/88.0' --header 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8' --header 'Accept-Language: en-US,en;q=0.5' --referer 'https://files.support.sandvine.com/' --cookie '_ga=GA1.2.1576126583.1545230740; experimentation_subject_id=IjMxZmU5ZGY2LWQwZjAtNDU4MC1hNTc2LWQwYjhmMWIxNDMyOCI%3D--9109e1564b3eed1f3b368dedd26a4a9c51bee051; _fbp=fb.1.1606399635669.1153138245' --header 'Upgrade-Insecure-Requests: 1' '[URL]' --output '[OUTPUT_NAME]' -k
```

Example

```
curl --header 'Host: files.support.sandvine.com' --user-agent 'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:88.0) Gecko/20100101 Firefox/88.0' --header 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8' --header 'Accept-Language: en-US,en;q=0.5' --referer 'https://files.support.sandvine.com/' --cookie '_ga=GA1.2.1576126583.1545230740; experimentation_subject_id=IjMxZmU5ZGY2LWQwZjAtNDU4MC1hNTc2LWQwYjhmMWIxNDMyOCI%3D--9109e1564b3eed1f3b368dedd26a4a9c51bee051; _fbp=fb.1.1606399635669.1153138245' --header 'Upgrade-Insecure-Requests: 1' 'https://files.support.sandvine.com/software/ActiveNetworkIntelligence/ActiveLogic/22.40/22.40.08/packetlogic2-xeon-plos_64-22.40.08.1.tar.gz.gpg?token=eyJhbGciOiJSUzUxMiIsInR5cCI6IkpXVCJ9.eyJleHAiOiIyMDIyLTAyLTIyVDA4OjEzOjE0LjEzNjg0Mi0wNTowMCIsIm5hbWUiOiJoZ3VlbmZhZkBhcmVzYWxnZXJpZS5jb20iLCJwZXJtcyI6eyJjYW5fZG93bmxvYWRfZG9jcyI6dHJ1ZSwiY2FuX2Rvd25sb2FkX2xpY2Vuc2VzIjp0cnVlLCJjYW5fZG93bmxvYWRfc29mdHdhcmUiOnRydWUsImNhbl9ncmFudF9hY2Nlc3MiOmZhbHNlLCJjYW5faW1wZXJzb25hdGUiOmZhbHNlLCJjYW5fbG9naW5fdmlhX2h0dHAiOnRydWUsImNhbl9sb2dpbl92aWFfc3NoIjp0cnVlLCJjYW5fc3RvcmVfZmlsZXNfb25fc2VydmVyIjp0cnVlLCJjYW5fdmlld19hY2Nlc3NfY29kZSI6ZmFsc2V9LCJ1aWQiOiIyMjY2NjEifQ.arsuSM8fEM-EXQjT0rCPWA7CDUvDOXuyztPiMCRHP653pO5wWzILv1b05igXcjDbOuauJGKqFoEfg3mfKKPtyzJS6RAU98aQQK6_YdsgCeHjQ3fYku6I2ylcz5NOiLZl8AbC7o6SpD0-y0uGzepeo6Tpp5gR4ATFLO5P2j1eLwU&isWeb=1' --output 'packetlogic2-xeon-plos_64-22.40.08.1.tar.gz.gpg' -k
```

# License Generator (Internet)

Internet exposed Sandvine license generator, requires the `machine-id` which you can get either by PLClient (down status bar) or CLI `show system information machine-id`

```
http://194.153.91.40/pldownload/licenses/[machine-id]
```

# Ctrl+d under Zones > Drdl

Show debug info under zones

# PRE Connections

Each connection is `1088` Bytes
Connection memory size: 1088 bytes starting firmware 17.2.4.12/18.1.2, and 704 bytes for older firmware.

# IMSI/IMEI Catchers

## Stingray

The Stingray is a device that pretends to be a cell tower by generating a signal that is stronger to the target's device that the real tower literally or by being closer to the target ( the later is more likelly ).

By making a rouge cell tower attackers can get the phone's IMSI/IMEI number since the phone will connect to it. The IMSI/IMEI is a unique number that resides on the SIM card, hence the cell provider can easily correlate the IMSI/IMEI with the phone number, then the full target's identity.

Malware & Spyware Injection through

- Web Browser Redirects
- Baseband Injection

## DRTBox (Dirtbox)

Work like the Stingray other than it's used in airplanes (Airborn) instead. This makes the radius of the coverage much larger.

# Deep Packet Inspection / Injection

## Traffic Injection

### In Path (Offline)

Out of the traffic link

### On Path (Online)

By tapping on the traffic link using a TAP `Test Access Point`,



## Training

### Sandvine 101 (Corporate Overview)
> https://learning.sandvine.com/learn/course/50/play/599/sandvine-101

#### Topics
- Sandvine Market - Network Intelligence
- The problems we solve
- Why it's important
- How we solve the problems - ANI Portfolio
- The value we deliver

#### Sandvine Market

- 100 Country
- 500 Operator
- 2.5 Billion Subscriber

#### The problems we solve

- Contextual Visibility
Allows for building a profile on the type of users, such as (Social Butterfly, Upsell Potential, Influencer, Professional Gamer, Streamer, Roaming Adventurer, Casual Gamer, Unhappy Customer, Shopper...)

- Quality of Experience
The internet is shifting towards the OTT 2.0 or Over The Top Second generation era where a large chunk of network traffic consists of Video and Streaming traffic

- Patent Pending ANI Classification Engine
The traffic is getting more and more hard to recognize using the traditional methods of traffic recognition and identification since traffic header, DNS, SNI (Server Name Indicator) are getting encrypted. This is where ACE comes in, being based on AI this tech

- Traffic visibility is the core of QoE
Gaming QoE
Video QoE

- Can your network meet the needs of OTT 2.0
ActiveLogic is the right solution for that, it uses ANI Classification Engine.
High performance
works on virtualization infrastructure (AWK, Hypervisors...)

- 5G
CUPS Control and User plane Separation

#### Full Portfolio of Use Cases for Network Operators

- Analytics
- Network Operators
- Revenue Generation
- Revenue Assurance
- Regulatory Compliance
- Save Money ROI
- Make Money ROI

## Sandvine PacketLogic

> Source: https://citizenlab.ca/2018/03/bad-traffic-sandvines-packetlogic-devices-deploy-government-spyware-turkey-syria/

Netintact -> Procera -> Sandvine. This is the diagram the shows sandvine roots, it started with the *Swidish* company `Netintact` which is the mother company behind the `PacketLogic` DPI system, which then got bought around 2006 by the ??? Company `Procera` finally the *Canadian* company `Sandvine` bought the later.

- PIC `PacketLogic Intelligence Center`
- PRE `PacketLogic Real-time Enforcement`
- PSM `PacketLogic Subscriber Manager`

- MPE `Maestro Policy Engine`

### DRDL

Datastream Recognition Definition Language, used on `Active Logic` products & it's or also called `signautres` is a file that can be downloaded from `https://files.support.sandvine.com` that serves as an update to traffic detection using signatures. The update happens every week.

- DRDL (Datastream Definition Recognition Language) = Traffic Signatures
    - DRDL version depends on the Firmware version
    - DRDL versions A[15-18]
- Custom DRDL build for all sites
    - This is due to a DNS issue (?)
- The same procedure on both PREs and vPREs
    - Upload DRDL using PLClient to "dir"
    - Command "system update signatures file [SIG_FILE]"
- Traffic Interruption to 0%, lasts ~5s (?)

### LTIP

Loadable Traffic Identification Protocol, 
- Used on `Policy Engine` products
- Released every month, unless there are big changes to a core protocol

### Credentials
The default password of the PacketLogic is always 

(for older versions of packetlogic software)
(ssh)
username: `pladmin`
password: `pldemo00` || `pldemo01`
(plclient)
username: `admin`
password: `pldemo00` || `pldemo01`

(for newer versions of packetlogic software)
(ssh & plclient)
username: `admin`
passowrd: `password`

When it's on the default settings. In order to drop in to the shell of the device use `unhide netintact` to reveal the `netintact` command you'll be prompted for a password which is internal to sandvine workers.


### Devices

`PRE`: PacketLogic Real-Time Enforcement

- High Processing Power
- Multiple 100Gbit interfaces (Two right, Two center, Two left)
- Low Storage Capacity (4 Storage Devices, 2 For System)
- Two 1100W PSU (Requires Higher Wattage)

`PIC`: PacketLogic Intelligence Center

- High Storage Capacity (High Storage Device Count)
- No 100Gbit interfaces
- Two 750W PSU

`PSM`: PacketLogic Subscriber Manager

- Two 750W PSU

### Serial Interface Baud Rate

9200 ??
PIC/PSM = 9600 b/s(baud)
PRE = 115200 b/s(baud)

Starting from ActiveLogic the baud rate is 115200 b/s for all devices.

# BlackArch Tools

- yersinia
- yate-bts
- zmap
- xsrfprobe
- xrop
- xporbe2
- xplico

- wifijammer
- wificurse

# Plclient

## Linux


### Ubuntu/Debian

```
libxcb-xinerama0
libdouble-conversion3
```

After installing the `libdouble-conversion3` package, symbolicly link the installed version 3 library to the version 1 which is not installed since `plclient` will explicitly look for `libdouble-conversion.os.1`

```
sudo ln -s /usr/lib/x86_64-linux-gnu/libdouble-conversion.so.3 /usr/lib/x86_64-linux-gnu/libdouble-conversion.os.1
```

# Connections Memory Usage Calculations

Old Method:
`1080 Bytes/Connection`

New Method:
yassine -> `1680 Bytes/Connection`
new -> `1856 Bytes/Connection`


# LRU (List Resource Used)

When connection count hit the "MAX_CONNECTIONS" limit, the LRU starts to raise
