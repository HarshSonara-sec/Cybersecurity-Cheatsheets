# EtherChannel Cheatsheet

## Purpose

- Combines multiple physical links into one logical link.
- Increases bandwidth.
- Provides redundancy.
- Prevents unnecessary STP blocking.

---

## Protocols

| Type | Standard | Modes |
|------|----------|-------|
| Static | None | On |
| PAgP | Cisco Proprietary | Desirable / Auto |
| LACP | IEEE 802.3ad (802.1AX) | Active / Passive |

---

## LACP Mode Compatibility

| Side A | Side B | Forms? |
|--------|--------|--------|
| Active | Active | ✅ |
| Active | Passive | ✅ |
| Passive | Passive | ❌ |

---

## PAgP Mode Compatibility

| Side A | Side B | Forms? |
|--------|--------|--------|
| Desirable | Desirable | ✅ |
| Desirable | Auto | ✅ |
| Auto | Auto | ❌ |

---

## Requirements

- Same speed
- Same duplex
- Same VLAN configuration
- Same trunk/access mode
- Same native VLAN (if trunk)
- Same switch

---

## Advantages

- Higher bandwidth
- Link redundancy
- Load balancing
- Fast failover
- Simplified management

---

## Common Commands

```cisco
show etherchannel summary
show etherchannel port-channel
show interfaces trunk
show spanning-tree
```

---

## Common Mistakes

❌ Mixing interface speeds

❌ Different VLAN configurations

❌ Passive ↔ Passive (LACP)

❌ Auto ↔ Auto (PAgP)

❌ Different switchport modes

---

## Enterprise Tip

- Prefer **LACP** over PAgP.
- Treat the Port-Channel as one logical interface.
- Verify the bundle before troubleshooting STP.
