# Cisco IOS Commands Cheat Sheet
**Course:** Jeremy's IT Lab CCNA
**Coverage:** 20 July 2026 – 25 July 2026

---

# Device Modes

| Command | Purpose |
|----------|---------|
| `enable` | Enter Privileged EXEC mode |
| `disable` | Return to User EXEC mode |
| `configure terminal` | Enter Global Configuration mode |
| `exit` | Exit current mode |
| `end` | Return directly to Privileged EXEC mode |

---

# Device Identification

## Change Hostname

```bash
hostname R1
```

Example

```bash
hostname SW1
```

---

# Interface Configuration

Enter interface configuration mode

```bash
interface g0/0
```

Configure multiple interfaces

```bash
interface range f0/3-24
```

Configure multiple non-consecutive interfaces

```bash
interface range f0/5-6,f0/9-12
```

---

# IP Address Configuration

Assign IP address

```bash
ip address <ip> <subnet-mask>
```

Example

```bash
ip address 192.168.1.254 255.255.255.0
```

---

# Interface Control

Enable interface

```bash
no shutdown
```

Disable interface

```bash
shutdown
```

---

# Interface Speed & Duplex

Set interface speed

```bash
speed 10
```

```bash
speed 100
```

```bash
speed 1000
```

Return to auto negotiation

```bash
speed auto
```

Configure duplex

```bash
duplex full
```

```bash
duplex half
```

```bash
duplex auto
```

---

# Interface Description

Add description

```bash
description ## to SW1 ##
```

Example

```bash
description ## not in use ##
```

---

# Static Routing

Configure static route

```bash
ip route <destination-network> <mask> <next-hop-ip>
```

Example

```bash
ip route 192.168.3.0 255.255.255.0 192.168.12.2
```

---

Configure static route using exit interface

```bash
ip route 192.168.3.0 255.255.255.0 g0/1
```

---

Configure using both

```bash
ip route 192.168.3.0 255.255.255.0 g0/1 192.168.13.3
```

---

Remove static route

```bash
no ip route 192.168.3.0 255.255.255.0 192.168.12.2
```

---

# Default Route

Configure default route

```bash
ip route 0.0.0.0 0.0.0.0 192.168.1.1
```

---

# Verification Commands

Show interface summary

```bash
show ip interface brief
```

---

Show routing table

```bash
show ip route
```

---

Show interface information

```bash
show interfaces
```

---

Show interface status

```bash
show interfaces status
```

---

Display running configuration

```bash
show running-config
```

---

Display startup configuration

```bash
show startup-config
```

---

Filter running configuration

```bash
show running-config | include ip route
```

---

# Save Configuration

Copy running configuration to startup configuration

```bash
copy running-config startup-config
```

Short command

```bash
write
```

or

```bash
write memory
```

---

# Connectivity Testing

Ping

```bash
ping <ip-address>
```

Example

```bash
ping 192.168.3.1
```

---

Trace packet path

```bash
traceroute <ip-address>
```

---

# Windows Networking Commands

Display IP configuration

```cmd
ipconfig
```

---

Display detailed configuration

```cmd
ipconfig /all
```

---

# Useful CLI Features

Show available options

```bash
?
```

Example

```bash
ip route ?
```

---

Repeat previous command

```text
↑
```

---

Move cursor to beginning of command

```text
Ctrl + A
```

---

Autocomplete command

```text
Tab
```

*(Works on many terminals, but not on all Cisco devices.)*

---

# Interface Status Reference

| Status | Meaning |
|---------|---------|
| Up/Up | Interface and protocol operational |
| Up/Down | Physical layer up, protocol down |
| Down/Down | Cable disconnected or no link |
| Administratively Down | Interface disabled using `shutdown` |

---

# Routing Table Codes

| Code | Meaning |
|------|---------|
| C | Connected Route |
| L | Local Route |
| S | Static Route |

---

# Frequently Used Commands

```bash
enable

configure terminal

hostname

interface

interface range

ip address

description

speed

duplex

shutdown

no shutdown

ip route

show ip interface brief

show interfaces

show interfaces status

show ip route

show running-config

show startup-config

show running-config | include ip route

copy running-config startup-config

write

write memory

ping

traceroute
```

---

# Commands to Remember for the CCNA

✅ `show ip interface brief`

✅ `show ip route`

✅ `show running-config`

✅ `show startup-config`

✅ `copy running-config startup-config`

✅ `ip route`

✅ `interface range`

✅ `shutdown`

✅ `no shutdown`

✅ `ping`

---

# Pro Tips

- Always run `show ip interface brief` before troubleshooting.
- Use `show ip route` to verify routing decisions.
- Save your configuration with `copy running-config startup-config` before closing the lab.
- Add interface descriptions to make troubleshooting easier.
- Disable unused interfaces to improve network security.
- Use `show running-config | include <keyword>` to quickly locate configuration lines.
- Test connectivity with `ping` after every major configuration change.

