---
tags:
  - network
definition: A list of common networking terms.
---

# DHCP
Dynamic Host Configuration Protocol


# DNS
Domain Name Server
A server that resolves IP addresses to domain names and vice versa. Your device's connection to this server makes it possible, for example, to enter `tuportal.temple.edu` into the address bar and access that site. 

You can find your DNS server by using the `ipconfig /all` command.

The DNS servers all Temple devices should be assigned to are:
```
155.247.225.230
155.247.225.231
```

It's possible in some cases for a DNS server to have filtering policies which prevent a device from accessing certain sites. I haven't encountered this on Temple devices yet, but it has occurred on personal devices connected to private LANs. 

# Gateway
The access point to the world-wide web in a LAN. Typically a modem in residential LANs. You can find the [[#IPv4]] address of your gateway with the `ipconfig /all` command on Windows, then finding the result for `Default Gateway`. 

# HTTP/HTTPS
Hypertext Transfer Protocol. The specification for messages sent and received via web servers. HTTPS refers to the version which encrypts the content of its messages. 

# IP Address

## IPv4
The most common protocol for assigning and reading IP addresses. 
## IPv6
Concerns about the limitations of available IPv4 addresses led to the definition of a new specification with a greater total possible number of addresses. 


# LAN
Local Area Network
The network served by a gateway. It is separated from the [[#WAN]] through the use of [[#DHCP]]. 

# Localhost
A hostname referring to the computer itself. Also known as the "loopback" address.  
IP addresses:
```
127.0.0.1

and sometimes
0.0.0.0
```

# MAC Address
"Medium access control address". Also called a "physical address". 
A hard-coded address assigned to every computer's network card. 
You can find your device's MAC address with the `ipconfig /all` command on Windows, then finding the result for `Physical Address`. 

# Ping
A command for detecting the presence and connectivity of a device.  

# Port
The channel through which network activity is passing through the computer's network adapter to or from an application.

Default ports to be familiar with:

| Port | Purpose       |
| ---- | ------------- |
| 80   | [[#HTTP]]/TCL |
| 27   | SSH           |


# VLAN
Virtual Local Area Network
Temple LANs are divided into two subnets or VLANs: staff and student. You can tell which VLAN a device is connected to by the first two octets of its IPv4 address. 

## Staff IP
`155.247.xxx.xxx`
## Student IP
`129....

# WAN
Wide-area Network

# WLAN
Wireless Local Area Network


