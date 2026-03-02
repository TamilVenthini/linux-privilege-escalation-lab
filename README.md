# Linux Privilege Escalation Lab – Structured Methodology Framework

This repository is not just a single sudo misconfiguration lab.

It also includes a structured Linux privilege escalation framework designed to enforce:

- Environment validation before execution
- Sequential enumeration phases
- Validation gates between phases
- Defined stop conditions
- Structured reporting format
- Decision-based workflow logic

The goal of this project is to move from random command execution to systematic security methodology design.

See `YOUR-methodology/` for the complete workflow framework.

---


# Linux Privilege Escalation – Sudo Misconfiguration Lab

## Full Report

[Download Full Lab Report](linux-privilege-escalation.pdf)


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
