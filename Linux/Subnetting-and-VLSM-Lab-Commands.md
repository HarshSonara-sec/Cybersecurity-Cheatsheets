# ============================================================
# Networking Commands Cheatsheet
# Topic: Subnetting, VLSM & Packet Tracer Labs
# Date: 2026-07-28
# Last Updated: 2026-07-28
# Source: Jeremy's IT Lab CCNA - Day 15
# ============================================================

# Subnetting, VLSM & Packet Tracer Commands Cheatsheet

## Overview

This cheatsheet contains important Cisco IOS commands and quick references used while practising subnetting, VLSM, packet flow analysis, and routing troubleshooting in Cisco Packet Tracer.

---

# 1. Interface Verification Commands

## Check Interface Status

```bash
show ip interface brief
```

Purpose:

- Displays all router interfaces.
- Shows IP addresses.
- Shows interface status.
- Quickly identifies shutdown interfaces.

---

## Check Detailed Interface Information

```bash
show interfaces
```

Purpose:

- Displays detailed interface statistics.
- Shows errors, encapsulation, and counters.

---

## Enable an Interface

```bash
interface g0/0
no shutdown
```

Purpose:

- Activates a disabled interface.

---

# 2. IP Address Configuration

## Configure IPv4 Address

```bash
interface g0/0
ip address <IP_ADDRESS> <SUBNET_MASK>
```

Example:

```bash
interface g0/0
ip address 192.168.1.254 255.255.255.0
```

---

# 3. Routing Verification Commands

## Display Routing Table

```bash
show ip route
```

Purpose:

- Displays connected routes.
- Displays static routes.
- Displays learned routes.

---

## Check Specific Route Information

```bash
show ip route <network>
```

Example:

```bash
show ip route 192.168.3.0
```

---

# 4. Static Routing Troubleshooting

## Configure Static Route

```bash
ip route <destination_network> <subnet_mask> <next_hop>
```

Example:

```bash
ip route 192.168.3.0 255.255.255.0 192.168.12.2
```

---

## Remove Static Route

```bash
no ip route <destination_network> <subnet_mask> <next_hop>
```

Example:

```bash
no ip route 192.168.3.0 255.255.255.0 192.168.12.2
```

---

# 5. Connectivity Testing

## Test Connectivity

```bash
ping <destination_IP>
```

Example:

```bash
ping 192.168.3.1
```

Purpose:

- Confirms Layer 3 connectivity.

---

## Trace Packet Path

```bash
traceroute <destination_IP>
```

Example:

```bash
traceroute 8.8.8.8
```

Purpose:

- Shows the path packets take through routers.

---

# 6. ARP Commands

## Display ARP Table

```bash
show arp
```

Purpose:

- Displays IP-to-MAC mappings.

---

## Clear ARP Cache

```bash
clear arp-cache
```

Purpose:

- Removes stored ARP entries.

---

# 7. Packet Tracer Useful Commands

## View Current Configuration

```bash
show running-config
```

Purpose:

- Displays the active device configuration.

---

## Save Configuration

```bash
copy running-config startup-config
```

or:

```bash
write
```

Purpose:

- Saves configuration after completing a lab.

---

## Enter Privileged EXEC Mode

```bash
enable
```

---

## Enter Global Configuration Mode

```bash
configure terminal
```

or:

```bash
conf t
```

---

# 8. Subnetting Quick Reference

## Calculate Usable Hosts

```
2^(Host Bits) - 2
```

---

## Calculate Number of Subnets

```
2^(Borrowed Bits)
```

---

## VLSM Planning Rules

1. Identify host requirements.
2. Sort largest to smallest.
3. Allocate the largest subnet first.
4. Calculate network, usable range, and broadcast address.
5. Verify no overlapping subnets.

---

# 9. Troubleshooting Checklist

## If Ping Fails:

Check:

```bash
show ip interface brief
```

- Are interfaces up?
- Are IP addresses correct?

---

Check routing:

```bash
show ip route
```

- Is the destination network present?

---

Test hop-by-hop:

```bash
ping <next-hop-IP>
```

---

# Key Takeaways

- `show ip interface brief` is the fastest interface troubleshooting command.
- `show ip route` is essential for routing verification.
- Always save configurations after successful labs.
- Ping verifies connectivity, while traceroute shows packet paths.
- Proper subnet planning prevents routing and addressing issues.
