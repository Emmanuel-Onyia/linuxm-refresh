# Linux Admin Foundations — Deep Refresh

This repository documents my in-depth Linux refresh with a strong focus on
**system administration fundamentals**, **permissions**, and **access control**.

Rather than basic command memorization, this project emphasizes:
- How Linux actually evaluates permissions
- Real-world failure scenarios
- Troubleshooting patterns used by system administrators

All work is performed on Ubuntu Linux and validated through hands-on drills.

---

## Learning Philosophy

This repository follows a few core principles:

- Every concept is validated through a practical drill
- Misconfigurations are intentional and analyzed
- Emphasis is placed on *why* Linux behaves the way it does
- Notes include mistakes, misconceptions, and corrections

This mirrors how issues present themselves in real production environments.

---

## Environment

- OS: Ubuntu (ext4 filesystem)
- Shell: Bash
- Tools: coreutils, acl
- Hardware: Lenovo ThinkPad T480

---

## Progress Overview

### Block 01 — Permissions & Ownership (Advanced)
- Owner vs group permission evaluation
- Directory traversal vs file access
- setgid and shared directory collaboration
- Real-world permission pitfalls

### Block 02 — Access Control Lists (ACLs)
- ACLs as exceptions to POSIX permissions
- getfacl / setfacl usage
- ACL masks and effective permissions
- Debugging misleading `ls -l` output

---

## Status

This repository is actively maintained and updated as I progress through
additional Linux administration topics.

