This is about the OSI model
> Sources
> Hussein Nasser " The OSI Model - Explained Example " Youtube Video


# Definition

Open Systems Interconnection model is an architecture that describes how data gets passed between different layers of abstraction an Information Technology systems and infrastructures

7. Application
6. Presentation
5. Session
4. Transport
3. Network
2. Data Link
1. Physical

# Layers

## Application

- Request

|---------|
| Request |
|---------|

## Presentation

Encryption using HTTPS/TLS

- Encryption
- Decryption

|---------|
| )?#@!** |
|---------|

## Session

Since a single client can establish multiple connections to a single server at any time these sessions must be differentiated by a session id or tag since all information from layer 1 to 4 is going to be identical. You can think of it as opening multiple pages of the same website in a single machine.

- Session Tag

|---------|-----|
| )?#@!** | sid |
|---------|-----|

## Transport

- Segment

- Source Port Number
- Destination Port Number (Target)
- Segment Numbers

|-------|---------|-----|-------|
| dport | )?#@!** | sid | sport |
|-------|---------|-----|-------|

## Network

- Packets

- Source IP Address
- Destination IP Address

|-----|-------|---------|----|-------|-----|
| dip | dport | )?#@!** | id | sport | sip |
|-----|-------|---------|----|-------|-----|

## Data Link

This layer sees the data as a bunch of bits only, so it splits them into

- Frames

Regardless of where they are split.

- Source MAC Address
- Destination MAC Address

|------|-----|-------|---------|-----|-------|------|------|
| dmac | dip | dport | )?#@!** | sid | sport | sip= | smac |
|------|-----|-------|---------|-----|-------|------|------|

## Physical

A signal that could be " Electrical, Optical, Radio ... "
