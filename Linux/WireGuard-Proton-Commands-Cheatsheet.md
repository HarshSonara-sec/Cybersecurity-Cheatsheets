# WireGuard + Proton VPN — Command Cheatsheet

## Install / Verify
```bash
sudo apt update
sudo apt install wireguard
sudo modprobe wireguard
lsmod | grep wireguard
wg --version
```

## Configuration
```bash
sudo mkdir -p /etc/wireguard
sudo cp ~/Downloads/<config>.conf /etc/wireguard/proton.conf
sudo chmod 600 /etc/wireguard/proton.conf
```

## Inspect Without Exposing Private Key
```bash
sudo grep -E '^(Address|DNS|PublicKey|Endpoint|AllowedIPs|PersistentKeepalive)' /etc/wireguard/proton.conf
```

## VPN Control
```bash
sudo wg-quick up proton
sudo wg-quick down proton
sudo wg show proton
```

## Interface / Routing
```bash
ip link show
ip addr show proton
ip rule
ip -6 rule
ip route
ip -6 route
ip route show table all
ip -6 route show table all
```

## Public IP Tests
```bash
curl -4 https://icanhazip.com
curl -6 https://icanhazip.com
```

## DNS
```bash
resolvectl status
```

## Firewall Inspection
```bash
sudo nft list ruleset
sudo iptables -S
sudo iptables -S OUTPUT
sudo ip6tables -S OUTPUT
```

## Kill-Switch Test
```bash
sudo wg-quick down proton
curl -4 --max-time 5 https://icanhazip.com
curl -6 --max-time 5 https://icanhazip.com
sudo wg-quick up proton
sudo wg show proton
```

## Backup Configuration
```bash
sudo cp /etc/wireguard/proton.conf /etc/wireguard/proton.conf.backup
```

## Important Safety Rules
- Never paste or commit `PrivateKey`.
- Never upload `/etc/wireguard/proton.conf` to GitHub.
- Redact personal IPs/MAC addresses when documenting personal systems.
- Do not blindly modify firewall rules.
- Test both IPv4 and IPv6.
- Confirm a recent WireGuard handshake before relying on the tunnel.
