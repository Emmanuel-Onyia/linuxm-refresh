# Block 03 — Special Permissions (setuid, setgid, sticky bit)

This block focuses on **Linux special permissions** and how they affect execution identity, group behavior, and safe file deletion in shared environments.

Unlike standard read/write/execute permissions, special permissions change **how Linux evaluates access and privilege at runtime**. These mechanisms are powerful and commonly misconfigured, so the emphasis of this block is **understanding behavior, not memorization**.

---

## Concepts Covered

### 1. setuid (Set User ID)
- Causes an executable to run with the **file owner’s user ID**
- Commonly used by system binaries owned by `root`
- Applies **only to compiled binaries**
- Ignored by the kernel when set on scripts (for security reasons)

Key takeaway:
> setuid does not mean “run as root” — it means “run as the file owner.”

---

### 2. setgid (Set Group ID)
- On executables: runs with the **file’s group ID**
- On directories: forces **group inheritance** for newly created files
- Widely used in shared/team directories to prevent permission drift

Key takeaway:
> setgid ensures consistent group ownership in collaborative environments.

---

### 3. Sticky Bit
- Applies primarily to directories
- Prevents users from deleting or renaming files they do not own
- Even when the directory is world-writable
- Classic example: `/tmp`

Key takeaway:
> Sticky bit allows shared write access without shared delete authority.

---

## Drills Completed

### Drill 01 — setuid (Identity Switching)
- Demonstrated that setuid is ignored on scripts
- Verified correct behavior using a compiled C binary
- Observed difference between real UID and effective UID
- Confirmed kernel-enforced privilege switching

---

### Drill 02 — setgid (Files vs Directories)
- Verified setgid behavior on executables (effective GID change)
- Verified group inheritance in setgid directories
- Observed interaction with `umask`
- Confirmed real-world shared directory behavior

---

### Drill 03 — Sticky Bit (Safe Shared Directories)
- Tested deletion behavior with and without sticky bit
- Identified path traversal as a prerequisite for deletion
- Correctly tested sticky bit in `/tmp`
- Confirmed deletion restriction based on file ownership

---

### Drill 04 — Reading Permissions Correctly
- Interpreted `s` vs `S` and `t` vs `T`
- Mapped symbolic permissions to octal form
- Used `stat` as the authoritative source of truth
- Identified inert vs active special permissions

---

### Drill 05 — Misconfigurations & Security Implications
- Identified dangerous patterns (world-writable setuid binaries)
- Understood PATH hijacking risks
- Recognized why special permissions must be tightly controlled
- Mapped Linux misconfigurations to cloud/IAM failures

---

## Security Mindset Developed

- Special permissions are **not defaults**
- Every special bit increases attack surface
- Misconfigurations are more dangerous than missing permissions
- `stat` should always be used to verify intent
- Least privilege applies at the filesystem level

---

## AWS / Cloud Analogy (Mental Model)

| Linux Concept | Cloud Analogy |
|-------------|---------------|
| setuid | IAM Role AssumeRole |
| setgid directory | Shared S3 bucket with enforced ownership |
| sticky bit | Object-owner delete control |
| misconfigured permissions | Over-permissive IAM policies |

---

## Current Status

- Concepts understood conceptually
- Behavior verified through hands-on drills
- Additional repetition planned for confidence and fluency

This block will be revisited as part of future security and privilege-escalation labs.
