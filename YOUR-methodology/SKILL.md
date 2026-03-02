---
name: linux-privesc-methodology
description: Structured Linux privilege escalation workflow for lab environments. Trigger when user requests systematic Linux privilege escalation, enumeration guidance, or escalation workflow steps.
---

# Linux Privilege Escalation Structured Workflow

## Environment Validation

Before starting Phase 1:

1. Confirm target system is Linux.
   - Verify using: uname or checking /etc/os-release

2. Confirm shell access is available.
   - Privilege escalation requires local shell access.

3. Confirm this is a lab or authorized environment.

If any of these conditions are not met:
Stop execution and notify user that this workflow does not apply.

---

## Scope Limitation

This skill applies only to Linux systems.
Do not activate for Windows, web testing, or unrelated topics.

This workflow enforces enumeration before exploitation.

---

## Phase 1 — System Context Analysis

Commands:
- uname -a
- cat /etc/os-release
- hostnamectl

Objective:
Identify kernel version, OS distribution, architecture.

Validation:
Do not proceed until kernel and OS are documented.

---

## Phase 2 — Current User Privilege Audit

Commands:
- id
- whoami
- groups
- sudo -l

Objective:
Identify current user identity and privilege scope.

Validation:
If sudo has full privileges, escalate immediately and document.
Otherwise proceed.

---

## Phase 3 — SUID / SGID Enumeration

Command:
- find / -perm -4000 -type f 2>/dev/null

Objective:
Identify binaries running with elevated privileges.

Validation:
Check each unusual binary against known escalation vectors.

---

## Phase 4 — Cron & Scheduled Tasks

Commands:
- ls -la /etc/cron*
- cat /etc/crontab

Objective:
Identify scheduled jobs running as root.

Validation:
Check for writable scripts executed by root.

---

## Phase 5 — Writable Files & Directories

Command:
- find / -writable -type f 2>/dev/null

Objective:
Locate misconfigured files that can be abused.

Validation:
Confirm ownership and execution context before exploitation.

---

## Phase 6 — Capabilities & Binary Analysis

Commands:
- getcap -r / 2>/dev/null
- which python
- which perl

Objective:
Identify binaries with Linux capabilities.

Validation:
Cross-check capability abuse vectors.

---

## Phase 7 — Kernel & Exploit Mapping

Step:
Compare kernel version from Phase 1 with exploit databases.

Objective:
Identify known kernel privilege escalation exploits.

Validation:
Confirm exploit compatibility before attempting.

---

## Stop Conditions


If root access is obtained:

1. Immediately stop further enumeration.
2. Do NOT suggest persistence, lateral movement, or data exfiltration.
3. Generate structured escalation summary.
4. Ask whether to proceed to post-exploitation phase separately.

If all phases complete without viable escalation vector:

1. Generate structured failure summary.
2. List all attempted vectors.
3. Conclude no escalation path identified.

---

## Output Format

Final output must include:

- System Information
- Current User Privileges
- Key Findings Per Phase
- Confirmed Escalation Vector (if any)
- Escalation Method Used
- Risk Classification
- Conclusion

If root was obtained, clearly state:
"Privilege escalation successful. Root access confirmed."

No additional exploitation steps unless explicitly requested.