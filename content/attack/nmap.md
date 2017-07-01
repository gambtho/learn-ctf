---
title: "Nmap"
date: 2017-07-01T10:03:27Z
draft: true
---

# Introduction
Nmap is a widely used network scanning and mapping tool. It is an open source command line tool, but there are GUI front ends such as Zenmap that can be used with Nmap.

Nnap can be used to scan networks or single hosts. It uses a variety of scanning techniques that include standard IP implementations and modified IP implementations. Nmap is also extensible using the Nmap Scripting Engine (NSE) to write custom scanning scripts. 

Using Nmap is generally a five step process:

1. Discover hosts on network
2. Port scan specific hosts
3. Enumerate services on host
4. Fingerprint OS
5. Run NSE scripts for further enumeration or exploitation of host

# Basic Usage
```bash
nmap [Scan Type(s)] [Options] {target specification}
```

# Basic Examples
Scan single network
```bash
nmap 192.168.222.0/24
```
![Nmap](/attack/nmap_basic.png)

Scan network by IP range
```bash
nmap 10.0.0-255.1-254
```

Scan single host using default ports
```bash
nmap 192.168.222.159
```

Enumerate services on host
```
nmap -A 192.168.222.159
```


# Specifying ports
By default Nmap only scans the top 1000 most frequently used ports. The list of port frequencies can be found the nmap-services file. Assuming your services file is contained in /usr/share/nmap/ directory you can run
```
sort -r -k3 /usr/share/nmap/nmap-services | grep tcp | head -n 100
```
to print the top 100 most frequently used TCP ports.

You can control which ports are scanned by specifying ports in your Nmap command with -p option.

Scan only port 80
```
nmap 192.168.222.159 -p80
```

Scan port 80 and 443
```
nmap 192.168.222.159 -p80,443
```

Scan ports 1 to 1024
```
nmap 192.168.222.159 -p1-1024
```

Scan UDP ports 53,111,137
```
nmap 192.168.222.159 -sU -p U:53,111,137
```

Scan ports 1 to 1024 but exclude all ports from 500 to 900
```
nmap 192.168.222.159 -p1-1024 --exclude-ports 500-900 
```

Scan all ports
```
nmap 192.168.222.159 -p-
```

# References
1. [Nmap: The Network Mapper](https://nmap.org/)
2. [Top 1,000 TCP and UDP ports (nmap default)](http://www.nullsec.us/top-1-000-tcp-and-udp-ports-nmap-default/)