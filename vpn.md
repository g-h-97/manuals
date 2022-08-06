
# WireGuard

## Server

Generate keys

```
(umask 077 && wg genkey > wg-private.key)
wg pubkey < wg-private.key > wg-public.key
```

Create interface configuration file `vim /etc/wireguard/wg0.conf` with the following content, to get the `PrivateKey` cat `wg-private.key` file and copy its contents 

```
[Interface]

PrivateKey = 
ListenPort = 51820
```

Create and start the wireguard interface `wg0`, 
- The `[IP/SUF]` is the IP address of the wiregueard server in the VPN network

```
ip link add wg0 type wireguard
ip address add [IP/SUF] dev wg0
wg setconf wg0 /etc/wireguard/wg0.conf
ip link set wg0 up
```

Check the interface configuration

```
ip address
wg show wg0
```

## Client

The configuration process for the clients is pretty much the same as the server with some minor differences

```
(umask 077 && wg genkey > wg-private-client.key)
wg pubkey < wg-private-client.key > wg-public-client.key
```

Create the peer's configuration file on the server `~/wg-client.conf`, 
- In this case the `Address` is the IP address with mask bits of the client on the VPN network
- `AllowedIPs` is a list of VPN IP addresses of wireguard server(s)
- `Endpoint` is the public IP address of the wireguard server

```
[Interface]

PrivateKey = 
Address = [IP/SUF]

[Peer]

PublicKey =
AllowedIPs = [IP/SUF]
Endpoint = [IP/SUF]
```

Now edit the `wg0.conf` file on the server and add the peer to it as follows
- `AllowedIPs` is the IP address of the client on the VPN network

```
[Peer]

PublicKey = 
AllowedIPs = [IP/SUF]
```

Finally, sync the configuration to the interface with `wg syncconf wg0 /etc/wireguard/wg0.conf`
