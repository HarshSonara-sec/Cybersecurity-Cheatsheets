# ============================================================
# Networking Commands Cheatsheet
# Topic: VLANs & Inter-VLAN Routing
# Date: 2026-07-30
# Last Updated: 2026-07-30
# Source: Jeremy's IT Lab CCNA - Days 17, 18 & 19
# ============================================================

# VLANs & Inter-VLAN Routing Commands Cheatsheet

## Overview

This cheatsheet contains the Cisco IOS commands used for VLAN creation, trunk configuration, Router-on-a-Stick (ROAS), Layer 3 switching, verification, and troubleshooting.

---

# 1. Enter Configuration Mode

## Enable Privileged EXEC Mode

```bash
enable
```

Purpose:

- Enter Privileged EXEC mode.

---

## Enter Global Configuration Mode

```bash
configure terminal
```

Shortcut:

```bash
conf t
```

Purpose:

- Configure the switch or router.

---

# 2. VLAN Configuration

## Create a VLAN

```bash
vlan 10
```

Purpose:

- Creates VLAN 10.

---

## Name a VLAN

```bash
name Sales
```

Example:

```bash
vlan 10
name Sales
```

---

## Display VLAN Information

```bash
show vlan brief
```

Purpose:

- Displays VLAN IDs.
- Displays VLAN names.
- Displays assigned access ports.

---

# 3. Access Port Configuration

## Enter Interface Configuration

```bash
interface fastEthernet 0/1
```

or

```bash
interface gigabitEthernet 0/1
```

---

## Configure Access Mode

```bash
switchport mode access
```

Purpose:

- Converts the interface into an access port.

---

## Assign VLAN to an Access Port

```bash
switchport access vlan 10
```

Purpose:

- Places the interface into VLAN 10.

---

# 4. Trunk Port Configuration

## Configure Trunk Mode

```bash
switchport mode trunk
```

Purpose:

- Converts the interface into a trunk port.

---

## Configure Native VLAN

```bash
switchport trunk native vlan 99
```

Purpose:

- Sets VLAN 99 as the Native VLAN.

---

## Allow Specific VLANs

```bash
switchport trunk allowed vlan 10,20,30
```

Purpose:

- Allows only selected VLANs across the trunk.

---

## Verify Trunk Ports

```bash
show interfaces trunk
```

Purpose:

- Displays trunk interfaces.
- Shows Native VLAN.
- Displays allowed VLANs.

---

# 5. Interface Verification

## Display Interface Status

```bash
show ip interface brief
```

Purpose:

- Displays interface status.
- Shows assigned IP addresses.

---

## Display Switchport Information

```bash
show interfaces switchport
```

Purpose:

- Displays interface mode.
- Shows VLAN assignment.
- Displays trunk configuration.

---

# 6. Router-on-a-Stick (ROAS)

## Create a Subinterface

```bash
interface g0/0.10
```

Purpose:

- Creates a subinterface for VLAN 10.

---

## Configure 802.1Q Encapsulation

```bash
encapsulation dot1Q 10
```

Purpose:

- Associates the subinterface with VLAN 10.

---

## Configure Native VLAN

```bash
encapsulation dot1Q 99 native
```

Purpose:

- Assigns VLAN 99 as the Native VLAN.

---

## Assign an IP Address

```bash
ip address 192.168.10.1 255.255.255.0
```

Purpose:

- Configures the default gateway for the VLAN.

---

# 7. Layer 3 Switching

## Enable Layer 3 Routing

```bash
ip routing
```

Purpose:

- Enables routing on a multilayer switch.

---

## Create an SVI

```bash
interface vlan 10
```

Purpose:

- Creates the Switch Virtual Interface (SVI).

---

## Assign an IP Address to an SVI

```bash
ip address 192.168.10.1 255.255.255.0
```

---

## Enable the SVI

```bash
no shutdown
```

---

# 8. Verification Commands

## Display Running Configuration

```bash
show running-config
```

Shortcut:

```bash
show run
```

Purpose:

- Displays the current device configuration.

---

## Display MAC Address Table

```bash
show mac address-table
```

Purpose:

- Displays learned MAC addresses.
- Shows which interfaces learned each MAC address.

---

## Test Connectivity

```bash
ping <destination-ip>
```

Example:

```bash
ping 192.168.20.10
```

Purpose:

- Verifies Layer 3 connectivity.

---

# 9. Save Configuration

## Save Running Configuration

```bash
copy running-config startup-config
```

Shortcut:

```bash
write
```

Purpose:

- Saves the configuration after completing the lab.

---

# 10. Troubleshooting Checklist

## VLAN Issues

Verify:

```bash
show vlan brief
```

- Does the VLAN exist?
- Is the access port assigned correctly?

---

## Trunk Issues

Verify:

```bash
show interfaces trunk
```

- Is the trunk operational?
- Are the required VLANs allowed?
- Does the Native VLAN match?

---

## Router-on-a-Stick Issues

Verify:

- Correct subinterface numbers.
- Correct `encapsulation dot1Q` configuration.
- Correct IP addresses.
- Physical interface is enabled.

---

## Layer 3 Switching Issues

Verify:

```bash
show ip interface brief
```

- Is the SVI up?
- Is `ip routing` enabled?
- Are the VLANs active?

---

# Key Takeaways

- `show vlan brief` verifies VLAN creation and port assignments.
- `show interfaces trunk` is the primary command for trunk troubleshooting.
- `show interfaces switchport` confirms access or trunk mode.
- `show mac address-table` verifies MAC learning.
- `ip routing` enables Layer 3 functionality on multilayer switches.
- Always save your configuration after completing a lab.
