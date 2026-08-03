# Wireshark Display Filters Cheat Sheet

> **Purpose:** Quick reference for the most commonly used Wireshark display filters.
>
> **Note:** Display filters only affect what is **shown** in Wireshark. They do **not** remove packets from the capture.

---

# Basic Filters

| Filter | Description |
|---------|-------------|
| `frame` | All captured frames |
| `eth` | Ethernet traffic |
| `ip` | IPv4 packets |
| `ipv6` | IPv6 packets |
| `tcp` | TCP packets |
| `udp` | UDP packets |
| `icmp` | ICMP packets |
| `arp` | ARP packets |
| `dns` | DNS traffic |
| `dhcp` | DHCP traffic |
| `http` | HTTP traffic |
| `tls` | TLS/SSL traffic |

---

# IP Address Filters

## Specific IP

```
ip.addr == 192.168.1.10
```

## Source IP

```
ip.src == 192.168.1.10
```

## Destination IP

```
ip.dst == 192.168.1.10
```

## Multiple IPs

```
ip.addr == 192.168.1.10 || ip.addr == 192.168.1.20
```

---

# MAC Address Filters

## Specific MAC

```
eth.addr == 00:11:22:33:44:55
```

## Source MAC

```
eth.src == 00:11:22:33:44:55
```

## Destination MAC

```
eth.dst == 00:11:22:33:44:55
```

---

# Port Filters

## Any Port

```
tcp.port == 80
```

```
udp.port == 53
```

## Source Port

```
tcp.srcport == 443
```

## Destination Port

```
tcp.dstport == 443
```

---

# Common Service Ports

| Service | Filter |
|----------|--------|
| HTTP | `tcp.port == 80` |
| HTTPS | `tcp.port == 443` |
| SSH | `tcp.port == 22` |
| FTP | `tcp.port == 21` |
| Telnet | `tcp.port == 23` |
| SMTP | `tcp.port == 25` |
| DNS | `udp.port == 53` |
| DHCP | `udp.port == 67 || udp.port == 68` |
| SMB | `tcp.port == 445` |
| RDP | `tcp.port == 3389` |
| LDAP | `tcp.port == 389` |
| Kerberos | `tcp.port == 88` |

---

# TCP Filters

All TCP

```
tcp
```

SYN

```
tcp.flags.syn == 1
```

SYN only

```
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

ACK

```
tcp.flags.ack == 1
```

FIN

```
tcp.flags.fin == 1
```

RST

```
tcp.flags.reset == 1
```

PSH

```
tcp.flags.push == 1
```

URG

```
tcp.flags.urg == 1
```

---

# TCP Analysis Filters

Retransmissions

```
tcp.analysis.retransmission
```

Duplicate ACK

```
tcp.analysis.duplicate_ack
```

Lost Segment

```
tcp.analysis.lost_segment
```

Out of Order

```
tcp.analysis.out_of_order
```

Fast Retransmission

```
tcp.analysis.fast_retransmission
```

Zero Window

```
tcp.analysis.zero_window
```

Window Full

```
tcp.analysis.window_full
```

Keep Alive

```
tcp.analysis.keep_alive
```

---

# UDP Filters

All UDP

```
udp
```

DNS

```
udp.port == 53
```

DHCP

```
udp.port == 67 || udp.port == 68
```

NTP

```
udp.port == 123
```

SNMP

```
udp.port == 161
```

---

# ICMP Filters

All ICMP

```
icmp
```

Echo Request (Ping)

```
icmp.type == 8
```

Echo Reply

```
icmp.type == 0
```

Destination Unreachable

```
icmp.type == 3
```

Time Exceeded

```
icmp.type == 11
```

---

# ARP Filters

All ARP

```
arp
```

ARP Requests

```
arp.opcode == 1
```

ARP Replies

```
arp.opcode == 2
```

---

# DNS Filters

All DNS

```
dns
```

Queries Only

```
dns.flags.response == 0
```

Responses Only

```
dns.flags.response == 1
```

NXDOMAIN

```
dns.flags.rcode == 3
```

Specific Domain

```
dns.qry.name == "example.com"
```

A Record

```
dns.a
```

AAAA Record

```
dns.aaaa
```

MX Record

```
dns.mx
```

PTR Record

```
dns.ptr.domain_name
```

---

# DHCP Filters

All DHCP

```
dhcp
```

Discover

```
dhcp.option.dhcp == 1
```

Offer

```
dhcp.option.dhcp == 2
```

Request

```
dhcp.option.dhcp == 3
```

ACK

```
dhcp.option.dhcp == 5
```

---

# HTTP Filters

All HTTP

```
http
```

GET Requests

```
http.request.method == "GET"
```

POST Requests

```
http.request.method == "POST"
```

Responses

```
http.response
```

Status 200

```
http.response.code == 200
```

Status 404

```
http.response.code == 404
```

Host

```
http.host == "example.com"
```

URI Contains

```
http.request.uri contains "login"
```

User-Agent

```
http.user_agent
```

Cookies

```
http.cookie
```

---

# HTTPS / TLS Filters

All TLS

```
tls
```

Client Hello

```
tls.handshake.type == 1
```

Server Hello

```
tls.handshake.type == 2
```

Certificate

```
tls.handshake.certificate
```

SNI

```
tls.handshake.extensions_server_name
```

---

# Packet Size Filters

Packets Larger Than 1000 Bytes

```
frame.len > 1000
```

Packets Smaller Than 100 Bytes

```
frame.len < 100
```

Exact Size

```
frame.len == 1500
```

---

# TCP Stream Filters

Specific TCP Stream

```
tcp.stream == 0
```

Specific UDP Stream

```
udp.stream == 0
```

---

# Time Filters

Packets After 10 Seconds

```
frame.time_relative > 10
```

Packets Before 5 Seconds

```
frame.time_relative < 5
```

---

# String Search Filters

Contains "admin"

```
frame contains "admin"
```

Contains "password"

```
frame contains "password"
```

Contains "HTTP"

```
frame contains "HTTP"
```

---

# Logical Operators

AND

```
tcp && ip.addr == 192.168.1.10
```

OR

```
dns || http
```

NOT

```
!icmp
```

Complex Example

```
tcp && ip.addr == 192.168.1.50 && tcp.port == 443
```

---

# Investigation Filters

Traffic to One Host

```
ip.addr == 192.168.1.100
```

Failed Web Requests

```
http.response.code >= 400
```

DNS Errors

```
dns.flags.rcode != 0
```

Reset Connections

```
tcp.flags.reset == 1
```

Retransmissions

```
tcp.analysis.retransmission
```

Large Packets

```
frame.len > 1400
```

---

# Most Used Filters ⭐

```
ip.addr == x.x.x.x

tcp

udp

dns

http

tls

icmp

arp

tcp.port == 80

tcp.port == 443

tcp.stream == 0

tcp.analysis.retransmission

tcp.flags.reset == 1

http.request.method == "GET"

dns.qry.name == "example.com"

frame.len > 1000
```

---

# Quick Reminder

| Capture Filter | Display Filter |
|----------------|----------------|
| Before capture | After capture |
| Uses BPF syntax | Uses Wireshark syntax |
| Reduces captured packets | Hides or shows packets only |

---

# Common Mistakes to Avoid

❌ Using `=` instead of `==`

❌ Confusing capture filters with display filters

❌ Using `host` (capture filter syntax) as a display filter

❌ Forgetting quotation marks around strings

❌ Using `and`/`or` instead of `&&`/`||` (both work, but `&&` and `||` are more common among experienced users)

---

# Pro Tips

- Start broad (`tcp`, `dns`) and narrow your search gradually.
- Combine protocol, IP, and port filters for precise results.
- Save frequently used filters using Wireshark's **Display Filter Expressions**.
- Use `tcp.stream` after identifying an interesting packet to isolate an entire conversation.
- Pair display filters with **Follow TCP Stream** and **Expert Information** for faster investigations.
