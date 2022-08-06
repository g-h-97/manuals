> Sources:
> https://www.osradar.com/how-to-install-and-configure-master-bind-dns-server-on-ubuntu-20-04/

# Fedora33

## named.conf

```bash

//
// named.conf
//
// Provided by Red Hat bind package to configure the ISC BIND named(8) DNS
// server as a caching only nameserver (as a localhost DNS resolver only).
//
// See /usr/share/doc/bind*/sample/ for example named configuration files.
//

options {
	listen-on port 53 { 127.0.0.1; 10.1.10.2; };
	listen-on-v6 port 53 { ::1; };
	directory 	"/var/named";
	dump-file 	"/var/named/data/cache_dump.db";
	statistics-file "/var/named/data/named_stats.txt";
	memstatistics-file "/var/named/data/named_mem_stats.txt";
	secroots-file	"/var/named/data/named.secroots";
	recursing-file	"/var/named/data/named.recursing";
	allow-query     { localhost; 10.1.10.0/24; };
#	allow-query-cache 	{ none; };

	/*
	 - If you are building an AUTHORITATIVE DNS server, do NOT enable recursion.
	 - If you are building a RECURSIVE (caching) DNS server, you need to enable
	   recursion.
	 - If your recursive DNS server has a public IP address, you MUST enable access
	   control to limit queries to your legitimate users. Failing to do so will
	   cause your server to become part of large scale DNS amplification
	   attacks. Implementing BCP38 within your network would greatly
	   reduce such attack surface
	*/
	recursion yes;

	dnssec-enable yes;
	dnssec-validation yes;

	managed-keys-directory "/var/named/dynamic";
	geoip-directory "/usr/share/GeoIP";

	pid-file "/run/named/named.pid";
	session-keyfile "/run/named/session.key";

	/* https://fedoraproject.org/wiki/Changes/CryptoPolicy */
	include "/etc/crypto-policies/back-ends/bind.config";
};

logging {
        channel default_debug {
                file "data/named.run";
                severity dynamic;
        };
};

zone "." IN {
	type hint;
	file "named.ca";
};

zone "dom.net" IN {
type master;
file "forward.dom.net";
allow-update { none; };
};

zone "10.1.10.in-addr.arpa" IN {
type master;
file "reverse.dom.net";
allow-update { none; };
};

include "/etc/named.rfc1912.zones";
include "/etc/named.root.key";

```

## Forward zone

Path `/var/named/forward.dom.net`

```bash
$TTL 604800
@	IN	SOA	fedora.dom.net.	root.dom.net.	(
		2011071001	;serial
		604800		;refresh
		86400		;retry
		2419200		;expire
		806400 )		;min TTL

;
@	IN	NS	fedora.dom.net.
fedora	IN	A	10.1.10.2
arch	IN	A	10.1.10.3
```

## Reverse zone

Path `/var/named/reverse.dom.net`

```bash

$TTL 604800
@	IN	SOA	fedora.dom.net.	root.dom.net.	(
		2011071001	;serial
		604800		;refresh
		86400		;retry
		2419200		;expire
		806400 )		;min TTL

;
@	IN	NS	fedora.dom.net.
fedora	IN	A	10.1.10.2
2	IN	PTR	fedora.dom.net.
3	IN	PTR	arch.dom.net.

```
