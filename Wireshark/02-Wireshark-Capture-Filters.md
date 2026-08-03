# Wireshark Capture Filters Cheat Sheet

> **Purpose:** Quick reference for Wireshark Capture Filters (Berkeley Packet Filter - BPF) syntax.
>
> **Note:** Capture filters determine **which packets are captured**. Packets excluded by a capture filter are **never recorded**.

---

# Display Filters vs Capture Filters

| Display Filter | Capture Filter |
|----------------|----------------|
| Applied after capture | Applied before capture |
| Hides packets | Prevents packets from being captured |
| Wireshark Display Filter syntax | Berkeley Packet Filter (BPF) syntax |
| Can be changed anytime | Must be set before capture starts |

---

# Basic Protocol Filters

Capture all TCP traffic

```text
tcp
```

Capture all UDP traffic

```text
udp
```

Capture ICMP traffic

```text
icmp
```

Capture ARP traffic

```text
arp
```

Capture IPv4 traffic

```text
ip
```

Capture IPv6 traffic

```text
ip6
```

---

# Host Filters

Capture traffic to or from a host

```text
host 192.168.1.100
```

Capture traffic from a source host

```text
src host 192.168.1.100
```

Capture traffic to a destination host

```text
dst host 192.168.1.100
```

---

# Network Filters

Capture an entire subnet

```text
net 192.168.1.0/24
```

Capture from a source network

```text
src net 10.10.10.0/24
```

Capture to a destination network

```text
dst net 172.16.0.0/16
```

---

# Port Filters

Capture traffic on port 80

```text
port 80
```

Capture source port

```text
src port 443
```

Capture destination port

```text
dst port 53
```

Capture a port range

```text
portrange 20-25
```

---

# Common Service Ports

| Service | Filter |
|----------|--------|
| HTTP | `port 80` |
| HTTPS | `port 443` |
| DNS | `port 53` |
| SSH | `port 22` |
| FTP | `port 20 or port 21` |
| SMTP | `port 25` |
| POP3 | `port 110` |
| IMAP | `port 143` |
| LDAP | `port 389` |
| Kerberos | `port 88` |
| SMB | `port 445` |
| RDP | `port 3389` |
| DHCP | `port 67 or port 68` |
| SNMP | `port 161` |
| NTP | `port 123` |

---

# Ethernet (MAC) Filters

Capture traffic for a MAC address

```text
ether host 00:11:22:33:44:55
```

Source MAC

```text
ether src 00:11:22:33:44:55
```

Destination MAC

```text
ether dst 00:11:22:33:44:55
```

---

# Broadcast & Multicast

Capture broadcast traffic

```text
broadcast
```

Capture multicast traffic

```text
multicast
```

---

# Packet Length Filters

Packets larger than 1000 bytes

```text
greater 1000
```

Packets smaller than 200 bytes

```text
less 200
```

---

# Logical Operators

## AND

```text
host 192.168.1.10 and tcp
```

---

## OR

```text
port 80 or port 443
```

---

## NOT

```text
not port 22
```

---

## Complex Example

Capture HTTPS traffic from one host

```text
host 192.168.1.100 and tcp and port 443
```

---

# Common Capture Examples

Capture all web traffic

```text
port 80 or port 443
```

Capture only DNS

```text
port 53
```

Capture SSH traffic

```text
tcp and port 22
```

Capture ICMP (Ping)

```text
icmp
```

Capture ARP

```text
arp
```

Capture DHCP

```text
port 67 or port 68
```

Capture one device

```text
host 192.168.1.50
```

Capture an entire subnet

```text
net 192.168.1.0/24
```

Capture all traffic except SSH

```text
not port 22
```

Capture TCP except HTTPS

```text
tcp and not port 443
```

Capture DNS from a specific host

```text
host 192.168.1.10 and port 53
```

Capture HTTPS to a specific server

```text
dst host 8.8.8.8 and port 443
```

---

# HTB / Lab Examples

Capture VPN traffic

```text
host 10.10.14.2
```

Capture reverse shell traffic

```text
tcp and port 4444
```

Capture SMB traffic

```text
port 445
```

Capture Kerberos traffic

```text
port 88
```

Capture LDAP traffic

```text
port 389
```

Capture WinRM traffic

```text
port 5985 or port 5986
```

---

# Where to Apply Capture Filters

Before starting a capture:

```
Capture
    ↓
Options
    ↓
Capture Filter
```

Or enter the filter directly in the **Capture Filter** field on Wireshark's main screen before clicking **Start**.

---

# Most Used Capture Filters ⭐

```text
tcp

udp

icmp

arp

host 192.168.1.100

port 80

port 443

port 53

port 22

net 192.168.1.0/24

broadcast

multicast

not port 22

tcp and port 443

host 10.10.14.2
```

---

# Common Mistakes to Avoid

❌ Using `==` (capture filters do **not** use comparison operators)

❌ Trying to use display filter fields such as:

```text
ip.addr == 192.168.1.10
```

❌ Forgetting that excluded packets cannot be recovered

❌ Starting a long capture without testing the filter

❌ Capturing on the wrong network interface

---

# Pro Tips

- Capture broadly if you're unsure what you'll need later.
- Use capture filters on busy production networks to reduce CPU, memory, and disk usage.
- Keep capture filters simple whenever possible.
- If disk space isn't a concern, capture everything and use **display filters** for detailed analysis afterward.
- Remember:
  - **Capture Filter = What gets recorded**
  - **Display Filter = What gets displayed**
