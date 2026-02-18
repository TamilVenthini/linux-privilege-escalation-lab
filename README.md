# Linux Privilege Escalation – Sudo Misconfiguration Lab

## Platform
TryHackMe Profile: https://tryhackme.com/p/tamilventhininatarajan 
Room: https://tryhackme.com/room/linuxprivesc

---

## Objective
Demonstrate privilege escalation through insecure sudo configuration.

---

## Initial Access Level
User: user  
UID: 1000  
No root privileges.

---

## Enumeration

Command used:
sudo -l

Finding:
User allowed to run multiple interactive binaries as root with NOPASSWD.

---

## Vulnerability Identified

Improper sudoers configuration allowed execution of shell-capable binaries as root.

This violates the Principle of Least Privilege.

---

## Exploitation Methods Demonstrated

1. sudo vim → shell escape using :!sh  
2. sudo find → -exec /bin/sh

---

## Proof of Escalation

whoami → root

---

## Root Cause

Misconfigured sudo policy allowing unrestricted execution of interactive programs.

---

## Mitigation

- Remove NOPASSWD for interactive binaries
- Restrict sudo commands with argument-level control
- Avoid preserving LD_PRELOAD
- Enable logging and auditing
