# dumpcap Commands Cheat Sheet

> **Purpose:** Quick reference for `dumpcap`, Wireshark's command-line packet capture tool.
>
> **Why use dumpcap?**
>
> - Lower resource usage than Wireshark
> - Faster packet capture
> - Ideal for servers and SSH sessions
> - Supports long-term packet collection
> - Used internally by Wireshark

---

# Verify Installation

Check the installed version

```bash
dumpcap --version
```

---

# Display Help

```bash
dumpcap --help
```

---

# List Available Interfaces

```bash
dumpcap -D
```

Example:

```
1. eth0
2. wlan0
3. lo
```

---

# Capture on an Interface

Capture from interface 1

```bash
sudo dumpcap -i 1
```

Capture from wlan0

```bash
sudo dumpcap -i wlan0
```

Capture from eth0

```bash
sudo dumpcap -i eth0
```

---

# Save Capture to a File

```bash
sudo dumpcap -i eth0 -w capture.pcapng
```

Specify a full path

```bash
sudo dumpcap -i eth0 -w /home/user/captures/network.pcapng
```

---

# Stop a Capture

Press:

```text
Ctrl + C
```

dumpcap closes the capture cleanly and saves the file.

---

# Capture a Fixed Number of Packets

Capture 100 packets

```bash
sudo dumpcap -i eth0 -c 100
```

Capture 1000 packets

```bash
sudo dumpcap -i eth0 -c 1000
```

---

# Capture for a Fixed Duration

Capture for 60 seconds

```bash
sudo dumpcap -i eth0 -a duration:60
```

Capture for 10 minutes

```bash
sudo dumpcap -i eth0 -a duration:600
```

---

# Stop After File Size

Stop when file reaches 100 MB

```bash
sudo dumpcap -i eth0 -a filesize:100000
```

---

# Ring Buffer (File Rotation)

Create a new file every 100 MB and keep the latest 10 files

```bash
sudo dumpcap -i eth0 \
-b filesize:100000 \
-b files:10 \
-w capture.pcapng
```

Useful for:

- SOC monitoring
- Servers
- Continuous packet capture
- Long-running investigations

---

# Capture Filters (BPF)

Capture HTTP traffic

```bash
sudo dumpcap -i eth0 -f "port 80"
```

Capture HTTPS traffic

```bash
sudo dumpcap -i eth0 -f "port 443"
```

Capture DNS traffic

```bash
sudo dumpcap -i eth0 -f "port 53"
```

Capture one host

```bash
sudo dumpcap -i eth0 -f "host 192.168.1.100"
```

Capture a subnet

```bash
sudo dumpcap -i eth0 -f "net 192.168.1.0/24"
```

Capture everything except SSH

```bash
sudo dumpcap -i eth0 -f "not port 22"
```

---

# Promiscuous Mode

Enable (default on most interfaces)

```bash
sudo dumpcap -i eth0 -p
```

> **Note:** The `-p` option disables promiscuous mode. If omitted, dumpcap typically captures in promiscuous mode (where supported). Check your interface and platform behavior.

---

# Monitor Mode (Wireless)

List supported interfaces

```bash
dumpcap -D
```

If your wireless adapter supports monitor mode, enable it using your wireless tools before capturing. `dumpcap` captures from the interface once monitor mode is active.

---

# Snapshot Length (SnapLen)

Capture only the first 128 bytes of each packet

```bash
sudo dumpcap -i eth0 -s 128
```

Capture full packets

```bash
sudo dumpcap -i eth0 -s 0
```

Using a smaller snap length reduces disk usage but may omit application-layer data.

---

# Capture Multiple Interfaces

Capture from eth0 and wlan0

```bash
sudo dumpcap -i eth0 -i wlan0 -w multi-interface.pcapng
```

---

# Flush Packets to Disk

Write packets to disk more frequently

```bash
sudo dumpcap -i eth0 --update-interval 100
```

Useful when monitoring live captures.

---

# View Capture Statistics

```bash
dumpcap -S
```

Shows capture statistics while packets are being collected.

---

# Common File Formats

Save as PCAPNG (recommended)

```bash
capture.pcapng
```

Legacy PCAP

```bash
capture.pcap
```

**PCAPNG** supports:

- Multiple interfaces
- Comments
- Better metadata
- Modern Wireshark features

---

# Useful Linux Commands

Check capture files

```bash
ls -lh *.pcap*
```

Check file size

```bash
du -sh capture.pcapng
```

Create a capture directory

```bash
mkdir -p ~/Captures
```

Move captures

```bash
mv *.pcapng ~/Captures/
```

Compress captures

```bash
gzip capture.pcapng
```

Extract a compressed capture

```bash
gunzip capture.pcapng.gz
```

---

# Practical Examples

Capture 500 packets

```bash
sudo dumpcap -i eth0 -c 500 -w test.pcapng
```

Capture HTTPS traffic for 5 minutes

```bash
sudo dumpcap -i eth0 \
-f "port 443" \
-a duration:300 \
-w https_capture.pcapng
```

Capture HTB VPN traffic

```bash
sudo dumpcap -i tun0 -w htb_lab.pcapng
```

Capture only DNS traffic

```bash
sudo dumpcap -i eth0 \
-f "port 53" \
-w dns_capture.pcapng
```

Continuous rotating capture

```bash
sudo dumpcap \
-i eth0 \
-b filesize:100000 \
-b files:20 \
-w rotating_capture.pcapng
```

---

# Typical Workflow

```text
List Interfaces
        ↓
Choose Interface
        ↓
(Optional) Apply Capture Filter
        ↓
Start Capture
        ↓
Save PCAPNG
        ↓
Open in Wireshark
        ↓
Analyze with Display Filters
```

---

# HTB / Penetration Testing Examples

Capture VPN traffic

```bash
sudo dumpcap -i tun0 -w vpn.pcapng
```

Capture SMB traffic

```bash
sudo dumpcap -i tun0 -f "port 445"
```

Capture Kerberos traffic

```bash
sudo dumpcap -i tun0 -f "port 88"
```

Capture LDAP traffic

```bash
sudo dumpcap -i tun0 -f "port 389"
```

Capture WinRM traffic

```bash
sudo dumpcap -i tun0 -f "port 5985 or port 5986"
```

---

# Most Used Commands ⭐

```bash
dumpcap --version

dumpcap -D

sudo dumpcap -i eth0

sudo dumpcap -i tun0

sudo dumpcap -i eth0 -w capture.pcapng

sudo dumpcap -i eth0 -c 100

sudo dumpcap -i eth0 -a duration:60

sudo dumpcap -i eth0 -f "port 443"

sudo dumpcap -i eth0 -f "host 192.168.1.100"

sudo dumpcap -i eth0 \
-b filesize:100000 \
-b files:10 \
-w capture.pcapng
```

---

# Common Mistakes to Avoid

❌ Forgetting to use `sudo` when required

❌ Capturing on the wrong interface

❌ Confusing **capture filters** (`-f`) with Wireshark **display filters**

❌ Filling the disk by running unlimited captures

❌ Using a very small snap length when full packet payloads are needed

❌ Forgetting to use ring buffers for long-running captures

---

# Pro Tips

- Use **PCAPNG** instead of PCAP unless compatibility requires otherwise.
- Save captures with descriptive filenames (e.g., `dns_issue_2026-08-03.pcapng`).
- Use ring buffers for servers and continuous monitoring.
- Apply capture filters only when you're confident about the traffic you need.
- Open the resulting `.pcapng` file in Wireshark and use **display filters** for detailed analysis.
- For HTB labs, capturing on **`tun0`** is often the most useful when analyzing VPN traffic.
