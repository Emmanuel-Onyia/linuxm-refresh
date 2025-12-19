# Block 01 — Permissions & Ownership (Advanced)

This block revisits Linux file and directory permissions from a **system
administrator’s perspective**.

The focus is not on learning syntax, but on understanding **how Linux evaluates
permissions**, why access failures occur, and how these issues present themselves
in real production environments.

---

## Objectives

By completing this block, the goal was to:

- Understand Linux permission evaluation order (owner → group → others)
- Identify why permissions that “look correct” can still fail
- Build intuition for directory traversal vs file-level access
- Learn how group ownership and inheritance affect collaboration

---

## Topics Covered

### Owner vs Group Permission Evaluation
- Demonstrated that Linux does not fall back to group permissions when the user
  matches the file owner
- Showed how owners can lock themselves out of their own files

### Directory Permissions vs File Permissions
- Explored how directory execute (`x`) permission controls access to files
- Reinforced that file permissions alone are insufficient without directory traversal

### setgid and Shared Collaboration
- Introduced the setgid bit on directories
- Explained how group inheritance prevents permission drift in shared environments
- Connected the concept to real-world shared directories (e.g. `/srv`, `/var/www`)

---

## Key Takeaways

- Permission evaluation is deterministic and order-based
- Directory permissions are gatekeepers to file access
- Group permissions are not a fallback for owners
- setgid is essential for stable collaboration in multi-user systems

---

## Notes

This block intentionally included confusion and misconfigurations.
Understanding *why* those failures occurred was the primary learning objective.
