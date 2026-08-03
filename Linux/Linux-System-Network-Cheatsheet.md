# Linux System & Network Commands Cheat Sheet
**OS:** Kali Linux (Zsh Compatible)
**Purpose:** Quick reference for system information, networking, hardware, and everyday Linux commands.

---

# 1. Operating System Information

## Show Linux Distribution
```bash
cat /etc/os-release
```

Example Output:
```
PRETTY_NAME="Kali GNU/Linux Rolling"
VERSION="2026.2"
```

---

## Kernel Version
```bash
uname -r
```

Example:
```
6.12.0-kali-amd64
```

---

## Full System Information
```bash
uname -a
```

Shows:
- Kernel
- Hostname
- Architecture
- Build Date

---

## Detailed Host Information
```bash
hostnamectl
```

Displays:
- Hostname
- OS Version
- Kernel
- Architecture
- Virtualization
- Hardware Vendor

---

## Current Hostname
```bash
hostname
```

---

# 2. CPU Architecture

## Check Architecture
```bash
uname -m
```

Possible outputs:

| Output | Meaning |
|---------|----------|
| x86_64 | 64-bit Intel/AMD |
| aarch64 | 64-bit ARM |
| armv7l | 32-bit ARM |
| i686 | 32-bit Intel |

---

## Check if System is 64-bit
```bash
getconf LONG_BIT
```

Output:
```
64
```

---

## CPU Information
```bash
lscpu
```

Shows:
- CPU Model
- Architecture
- Cores
- Threads
- Virtualization
- Cache

---

# 3. Memory Information

## RAM Usage
```bash
free -h
```

---

## Detailed Memory Info
```bash
cat /proc/meminfo
```

---

# 4. Disk Information

## Disk Usage
```bash
df -h
```

---

## Mounted Drives
```bash
lsblk
```

---

## Partition Information
```bash
sudo fdisk -l
```

---

## NVMe/SATA Devices
```bash
lsblk -o NAME,SIZE,TYPE,FSTYPE,MOUNTPOINT
```

---

# 5. Hardware Information

## PCI Devices
```bash
lspci
```

Useful for:
- GPU
- Network Card
- Audio
- USB Controllers

---

## USB Devices
```bash
lsusb
```

---

## Complete Hardware Summary
```bash
sudo lshw -short
```

---

## BIOS Information
```bash
sudo dmidecode -t bios
```

---

## Motherboard Information
```bash
sudo dmidecode -t baseboard
```

---

## System Information
```bash
sudo dmidecode -t system
```

---

# 6. Network Information

## Show All Network Interfaces
```bash
ip a
```

---

## Short Interface List
```bash
ip link
```

---

## Routing Table
```bash
ip route
```

---

## Default Gateway
```bash
ip route | grep default
```

---

## IP Address Only
```bash
hostname -I
```

---

## Public IP Address
```bash
curl ifconfig.me
```

Alternative:
```bash
curl ipinfo.io/ip
```

---

## DNS Servers
```bash
cat /etc/resolv.conf
```

---

## Network Connections
```bash
ss -tuln
```

---

## Open Ports
```bash
sudo ss -tulpn
```

---

## Ping Google
```bash
ping google.com
```

---

## Trace Route
```bash
traceroute google.com
```

Install if missing:
```bash
sudo apt install traceroute
```

---

## DNS Lookup
```bash
dig google.com
```

or

```bash
nslookup google.com
```

---

# 7. Wi-Fi Information

## Wireless Interfaces
```bash
iw dev
```

---

## Wi-Fi Scan
```bash
sudo iw dev wlan0 scan
```

---

## Wi-Fi Link Status
```bash
iw dev wlan0 link
```

---

# 8. User Information

## Current User
```bash
whoami
```

---

## Logged In Users
```bash
who
```

---

## User ID
```bash
id
```

---

## Current Shell
```bash
echo $SHELL
```

---

## Current Directory
```bash
pwd
```

---

# 9. Storage

## Directory Size
```bash
du -sh .
```

---

## Home Folder Usage
```bash
du -sh ~/*
```

---

## Largest Files
```bash
find . -type f -exec du -h {} + | sort -hr | head
```

---

# 10. Process Management

## Running Processes
```bash
ps aux
```

---

## Interactive Process Viewer
```bash
htop
```

Install:
```bash
sudo apt install htop
```

---

## Top Processes
```bash
top
```

---

## Kill Process
```bash
kill PID
```

Force:
```bash
kill -9 PID
```

---

# 11. Services

## Running Services
```bash
systemctl list-units --type=service --state=running
```

---

## Service Status
```bash
systemctl status ssh
```

---

## Start Service
```bash
sudo systemctl start ssh
```

---

## Stop Service
```bash
sudo systemctl stop ssh
```

---

## Enable on Boot
```bash
sudo systemctl enable ssh
```

---

# 12. Package Management (APT)

## Update Packages
```bash
sudo apt update
```

---

## Upgrade Packages
```bash
sudo apt upgrade
```

---

## Install Package
```bash
sudo apt install package_name
```

---

## Remove Package
```bash
sudo apt remove package_name
```

---

## Search Package
```bash
apt search package_name
```

---

# 13. File Operations

## List Files
```bash
ls
```

Detailed:
```bash
ls -lah
```

---

## Copy
```bash
cp source destination
```

---

## Move
```bash
mv source destination
```

---

## Delete
```bash
rm file
```

Recursive:
```bash
rm -rf directory
```

---

## Create Directory
```bash
mkdir folder
```

---

## Create Empty File
```bash
touch file.txt
```

---

## View File
```bash
cat file.txt
```

---

## Edit File
```bash
nano file.txt
```

or

```bash
vim file.txt
```

---

# 14. Searching

## Find File
```bash
find / -name filename
```

---

## Search Text
```bash
grep "text" file.txt
```

Recursive:
```bash
grep -r "password" .
```

---

# 15. Downloads

## Download File
```bash
wget URL
```

or

```bash
curl -O URL
```

---

# 16. Compression

## Create ZIP
```bash
zip -r archive.zip folder
```

---

## Extract ZIP
```bash
unzip archive.zip
```

---

## Create tar.gz
```bash
tar -czvf archive.tar.gz folder
```

---

## Extract tar.gz
```bash
tar -xzvf archive.tar.gz
```

---

# 17. Permissions

## Show Permissions
```bash
ls -l
```

---

## Change Permission
```bash
chmod 755 file
```

---

## Change Owner
```bash
sudo chown user:user file
```

---

# 18. System Monitoring

## Uptime
```bash
uptime
```

---

## Load Average
```bash
cat /proc/loadavg
```

---

## Logged-in Sessions
```bash
w
```

---

## Journal Logs
```bash
journalctl
```

Latest Boot:
```bash
journalctl -b
```

Errors Only:
```bash
journalctl -p err -b
```

---

# 19. Power Management

## Shutdown
```bash
sudo shutdown now
```

---

## Reboot
```bash
sudo reboot
```

---

## Power Off
```bash
sudo poweroff
```

---

# 20. Useful Zsh Commands

## Reload Zsh Configuration
```bash
source ~/.zshrc
```

---

## Edit Zsh Configuration
```bash
nano ~/.zshrc
```

---

## Show PATH
```bash
echo $PATH
```

---

## Show Command History
```bash
history
```

Search History:
```bash
history | grep ssh
```

---

# 21. Cybersecurity Commands

## Check Tun0 Interface (Hack The Box/VPN)
```bash
ip a | grep tun0
```

---

## Network Scan
```bash
nmap -sV TARGET_IP
```

---

## Aggressive Scan
```bash
nmap -A TARGET_IP
```

---

## Check Listening Ports
```bash
sudo ss -tulpn
```

---

## ARP Table
```bash
arp -a
```

or

```bash
ip neigh
```

---

# Quick Command Summary

| Task | Command |
|------|---------|
| Linux Version | `cat /etc/os-release` |
| Kernel | `uname -r` |
| Full System | `uname -a` |
| Host Info | `hostnamectl` |
| Architecture | `uname -m` |
| CPU Info | `lscpu` |
| RAM | `free -h` |
| Disk Usage | `df -h` |
| Drives | `lsblk` |
| Network Interfaces | `ip a` |
| Routing Table | `ip route` |
| Public IP | `curl ifconfig.me` |
| Open Ports | `ss -tuln` |
| Running Processes | `ps aux` |
| Interactive Process Viewer | `htop` |
| Running Services | `systemctl list-units --type=service --state=running` |
| Package Update | `sudo apt update && sudo apt upgrade` |
| Current User | `whoami` |
| Shell | `echo $SHELL` |
| Current Directory | `pwd` |
| History | `history` |

---

**Tip:** Use `man <command>` (e.g., `man ls`) to read the manual page for any command, or use `<command> --help` for a quick overview of available options.

