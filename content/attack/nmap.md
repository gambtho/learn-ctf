---
title: "Nmap"
date: 2017-07-24T17:03:44Z
draft: true
---

# Introduction
Nmap is a widely used network scanning and mapping tool. It is an open source command line tool, but there are GUI front ends such as Zenmap that can be used with Nmap.

Nnap can be used to scan networks or single hosts. It uses a variety of scanning techniques that include standard IP implementations and modified IP implementations. Nmap is also extensible using the Nmap Scripting Engine (NSE) to write custom scanning scripts. 

Using Nmap is generally a four step process:

1. Discover hosts on network
2. Port scan specific hosts
3. Enumerate services on host and fingerprint OS
5. Run NSE scripts for further enumeration or exploitation of host

# Basic Usage
```bash
nmap [Scan Type(s)] [Options] {target specification}
```

# Basic Examples
Ping scan single network and disable DNS lookup
```bash
nmap -n -sn 10.0.1.0/24
```
![Nmap default scan](/attack/nmap_default.png)

Scan network by IP range
```bash
nmap 10.0.0-255.1-254
```

Scan single host using default ports
```bash
nmap 192.168.222.159
```

Enumerate services, fingerprint OS, and run script scans on single host
```
nmap -A 192.168.222.159
```

Run vsftpd backdoor script scan on single host
```
nmap --script ftp-vsftpd-backdoor 192.168.222.159
```
![Nmap vsftpd script scan](/attack/nmap_vsftpd_script.png)

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


# Nmap Scripting Engine (NSE)
The NSE scripts are typically located in /usr/share/nmap/scripts/ or /usr/local/share/nmap/scripts for Linux or C:\Program Files\Nmap\scripts for Windows.

A count of the files in scripts directory reveals that Nmap v7.50 comes preloaded with 567 scripts. Many scripts for testing or even exploiting various services and vulnerabilities exist. There are too many scripts to discuss all of them here in this article. The best thing to do is read the script documentation in the script file and/or try the script on vulnerable and non-vulnerable hosts to see what the results look like.

If a script that meets your needs doesn't exist you can write your own. NSE scripts are written in Lua.


# References
1. [Nmap: The Network Mapper](https://nmap.org/)
2. [Top 1,000 TCP and UDP ports (nmap default)](http://www.nullsec.us/top-1-000-tcp-and-udp-ports-nmap-default/)
3. [Guide to using Nmap to scan for the Heartbleed bug](https://gist.github.com/bonsaiviking/10402038)
