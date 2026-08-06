# Enumeration Workflow Cheatsheet

## Objective

A quick reference for performing structured enumeration during penetration testing.

---

## Standard Workflow

```text
Target Discovery
        ↓
Port Scan
        ↓
Service Detection
        ↓
Version Detection
        ↓
Service Enumeration
        ↓
Technology Fingerprinting
        ↓
Directory Enumeration
        ↓
Correlate Findings
        ↓
Vulnerability Assessment
        ↓
Exploitation
```

---

## Nmap

**Purpose**

Identify open ports, services and versions.

**Common Command**

```bash
nmap --privileged -sC -sV <target-ip>
```

---

## FTP

**Check**

* Anonymous login
* Directory listing
* Read permission
* Write permission

---

## SMB

**Check**

* Shares
* Anonymous access
* Read permission
* Write permission
* Interesting files

---

## HTTP

**Check**

* Default pages
* Login portals
* phpMyAdmin
* WebDAV
* Tomcat
* phpinfo

---

## Directory Enumeration

```bash
gobuster dir \
-u http://<target-ip> \
-w /usr/share/wordlists/dirb/common.txt
```

Look for:

* Admin panels
* Backup files
* Upload directories
* Hidden applications
* Development pages

---

## Questions to Ask

* What service is running?
* Which version is installed?
* Is authentication required?
* Is anonymous access allowed?
* Are default credentials likely?
* Is sensitive information exposed?
* Which service presents the most promising attack path?

---

## Common Mistakes

* Running exploits before enumeration.
* Ignoring version information.
* Relying on a single tool.
* Skipping manual verification.
* Failing to document findings.

---

## Best Practices

* Enumerate every exposed service.
* Verify findings manually.
* Keep detailed notes.
* Correlate information across multiple services.
* Select an attack path based on evidence rather than assumptions.
