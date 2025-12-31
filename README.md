# Linux Admin Foundations — Deep Refresh

This repository documents my in-depth Linux refresh with a strong focus on
**system administration fundamentals**, **permissions**, **access control**, and
**process management**.

Rather than basic command memorization, this project emphasizes:
- How Linux actually evaluates permissions and executes programs
- Real-world failure scenarios and misconfigurations
- Troubleshooting patterns used by system administrators
- Kernel vs shell responsibilities

All work is performed on Ubuntu Linux and validated through hands-on drills.

---

## Learning Philosophy

This repository follows a few core principles:

- Every concept is validated through a practical drill
- Misconfigurations are intentional and analyzed
- Emphasis is placed on *why* Linux behaves the way it does
- Notes include mistakes, misconceptions, and corrections

This mirrors how issues present themselves in real production environments,
not in sanitized tutorials.

---

## Environment

- OS: Ubuntu (ext4 filesystem)
- Shell: Bash
- Tools: coreutils, acl
- Hardware: Lenovo ThinkPad T480

---

## Progress Overview

### Block 01 — Permissions & Ownership (Advanced)
- Owner vs group permission evaluation order
- Directory traversal vs file access
- setgid and shared directory collaboration
- Real-world permission pitfalls and failures

---

### Block 02 — Access Control Lists (ACLs)
- ACLs as exceptions to POSIX permissions
- `getfacl` / `setfacl` usage
- ACL masks and effective permissions
- Debugging misleading `ls -l` output
- Understanding why permissions *appear* correct but fail

---

### Block 03 — Special Permissions & Sticky Bit
- setuid and setgid behavior
- Sticky bit enforcement on shared directories
- Octal representation of special permissions
- Security implications of special bits
- Why Linux does not “fall back” between permission classes

---

### Block 04 — Process Management & Job Control
- Process lifecycle and execution model
- PID vs PPID vs job IDs
- Foreground vs background jobs
- Shell job control vs kernel processes
- Linux signals (`SIGTERM`, `SIGKILL`, `SIGSTOP`, `SIGCONT`)
- Safe vs forceful process termination
- Process priority, scheduling, and `nice` values
- Understanding why processes feel “unkillable”

---

## Status

✅ **Blocks 01–04 completed**  
📌 Repository is actively maintained and expanded as I progress through
advanced Linux administration topics and **automation-focused skill building**.

Next focus: **Bash and Python scripting mastery for automation, system tasks,
and operational efficiency**


## Notes

This repository is intentionally structured as a **deep technical refresh**,
not an introductory Linux guide. It is designed to reflect the level of
understanding expected of system administrators, cloud support engineers,
and platform engineers in real environments.

