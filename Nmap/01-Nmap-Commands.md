# Nmap Commands Cheat Sheet

> **Purpose:** Quick reference for the most commonly used Nmap commands during network enumeration, penetration testing, HTB labs, and CTFs.

---

# Verify Installation

Check installed version

```bash
nmap --version
```

Show help

```bash
nmap --help
```

---

# Basic Syntax

```bash
nmap [Scan Type] [Options] <Target>
```

Example

```bash
nmap 192.168.1.10
```

---

# Target Specification

Single IP

```bash
nmap 192.168.1.10
```

Hostname

```bash
nmap example.com
```

Multiple Hosts

```bash
nmap 192.168.1.10 192.168.1.20
```

Subnet

```bash
nmap 192.168.1.0/24
```

IP Range

```bash
nmap 192.168.1.1-100
```

Targets from File

```bash
nmap -iL targets.txt
```

Exclude Host

```bash
nmap 192.168.1.0/24 --exclude 192.168.1.10
```

---

# Host Discovery

Ping Scan (No Port Scan)

```bash
nmap -sn 192.168.1.0/24
```

Disable Host Discovery

Useful when ICMP is blocked.

```bash
nmap -Pn TARGET
```

ARP Scan (Local Network)

```bash
nmap -PR TARGET
```

---

# Port Scanning

Default Scan

```bash
nmap TARGET
```

TCP SYN Scan (Recommended)

```bash
sudo nmap -sS TARGET
```

TCP Connect Scan

```bash
nmap -sT TARGET
```

UDP Scan

```bash
sudo nmap -sU TARGET
```

Scan Specific Port

```bash
nmap -p 80 TARGET
```

Multiple Ports

```bash
nmap -p 22,80,443 TARGET
```

Port Range

```bash
nmap -p 1-1000 TARGET
```

All Ports

```bash
nmap -p- TARGET
```

Top 100 Ports

```bash
nmap --top-ports 100 TARGET
```

Top 1000 Ports (Default)

```bash
nmap TARGET
```

Fast Scan

```bash
nmap -F TARGET
```

---

# Service Enumeration

Version Detection

```bash
nmap -sV TARGET
```

Service Detection on All Ports

```bash
nmap -sV -p- TARGET
```

---

# Operating System Detection

```bash
sudo nmap -O TARGET
```

---

# Aggressive Scan

Includes:

- OS Detection
- Version Detection
- Default NSE Scripts
- Traceroute

```bash
sudo nmap -A TARGET
```

---

# Nmap Scripting Engine (NSE)

Run Default Scripts

```bash
nmap -sC TARGET
```

Run Specific Script

```bash
nmap --script=http-title TARGET
```

Run SMB Scripts

```bash
nmap --script smb* TARGET
```

Run Vulnerability Scripts

```bash
nmap --script vuln TARGET
```

---

# Timing Options

Normal

```bash
-T3
```

Faster

```bash
-T4
```

Very Aggressive

```bash
-T5
```

Example

```bash
nmap -T4 TARGET
```

---

# Output Options

Normal Output

```bash
-oN scan.txt
```

XML

```bash
-oX scan.xml
```

Grepable

```bash
-oG scan.gnmap
```

All Formats

```bash
-oA scan
```

---

# Verbosity

Verbose

```bash
-v
```

Very Verbose

```bash
-vv
```

Debug

```bash
-d
```

---

# Firewall Evasion (Introduction)

Fragment Packets

```bash
-f
```

Spoof MAC Address

```bash
--spoof-mac
```

Decoy Scan

```bash
-D RND:10
```

> Learn and use these only in authorized environments.

---

# Useful Combinations

HTB Initial Enumeration

```bash
nmap -sC -sV TARGET
```

Full TCP Scan

```bash
sudo nmap -sS -p- TARGET
```

Fast Service Detection

```bash
nmap -T4 -sV TARGET
```

Aggressive Scan

```bash
sudo nmap -A TARGET
```

UDP Enumeration

```bash
sudo nmap -sU TARGET
```

Scan Without Ping

```bash
nmap -Pn TARGET
```

Save Results

```bash
nmap -sC -sV -oA initial TARGET
```

---

# Wireshark Practice

Capture traffic while scanning

```bash
sudo nmap -sS TARGET
```

Observe:

- SYN
- SYN/ACK
- RST

TCP Connect Scan

```bash
nmap -sT TARGET
```

Observe:

- SYN
- SYN/ACK
- ACK
- RST

This matches the practical lab demonstrated in the source video, where Nmap scans were analyzed in Wireshark to observe packet-level behavior. 

---

# HTB Workflow

Step 1

```bash
nmap -sn TARGET
```

↓

Step 2

```bash
sudo nmap -sS -p- TARGET
```

↓

Step 3

```bash
nmap -sC -sV TARGET
```

↓

Step 4

Research services and versions.

↓

Step 5

Run targeted enumeration tools.

---

# Most Used Commands ⭐

```bash
nmap TARGET

sudo nmap -sS TARGET

nmap -sT TARGET

sudo nmap -sU TARGET

nmap -Pn TARGET

nmap -sn TARGET

nmap -p- TARGET

nmap -sV TARGET

sudo nmap -O TARGET

sudo nmap -A TARGET

nmap -sC TARGET

nmap -sC -sV TARGET

nmap -T4 TARGET

nmap -oA scan TARGET
```

---

# Common Mistakes

❌ Forgetting `sudo` for SYN scans.

❌ Running `-A` immediately without understanding the target.

❌ Assuming an open port is vulnerable.

❌ Ignoring UDP services.

❌ Forgetting to save scan results.

❌ Scanning all 65,535 ports unnecessarily.

❌ Misinterpreting filtered ports.

---

# Best Practices

- Start with host discovery before full scans.
- Use `-sS` when possible for TCP enumeration.
- Run `-sC -sV` after identifying open ports.
- Save results using `-oA` for documentation.
- Correlate Nmap results with Wireshark captures.
- Enumerate services thoroughly before attempting exploitation.

---

# Quick Reference Workflow

```text
Host Discovery
      ↓
TCP SYN Scan
      ↓
Identify Open Ports
      ↓
Service & Version Detection
      ↓
Run NSE Scripts
      ↓
Research Services
      ↓
Exploitation (if authorized)
```

---

# Pro Tips

- **`-sC -sV`** is the command you'll use most often in HTB and labs.
- Use **`-p-`** to avoid missing services running on non-standard ports.
- Save every important scan with **`-oA`** to preserve results in multiple formats.
- Analyze scans alongside **Wireshark** to understand how Nmap interacts with target systems at the packet level.
- Enumeration is iterative—re-scan when you discover new hosts, services, or network paths.
