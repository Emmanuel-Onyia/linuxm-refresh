# Drill 03 — Breaking Access with the ACL Mask

## Goal

To demonstrate how ACLs can appear correctly configured while access still
fails, and to prove that the ACL **mask** is a hard permission ceiling that
overrides explicit ACL entries.

This drill intentionally creates a failure scenario commonly encountered in
real systems.

---

## Setup

Ensure the ACL from Drill 02 is still in place:

```bash
getfacl sample.txt
```

Expected structure includes:
- user:acluser:rw-
- mask::rw-

## Commands

Lower the ACL mask to read-only:
```bash
setfacl -m m:r-- sample.txt
```

Inspect permissions again:
```bash
getfacl sample.txt
ls -l sample.txt
```

Test access as the named user:
```bash
sudo -u acluser bash
cat sample.txt
echo "test" >> sample.txt
exit
```

## Observation

- The named user entry still displays rw-
- The ACL mask is now r--
- ls -l shows group permissions as read-only
- Reading the file succeeds
- Writing to the file fails with “Permission denied”

## Explanation

The ACL mask defines the maximum effective permissions for all group-class
entries, including named users.

Effective permissions are calculated as:
```
(named ACL entry) AND (mask)
```

In this case:
- Named user permission: rw-
- Mask: r--
- Effective permission: r--

Although the ACL entry appears to grant write access, the mask silently removes
it.

## Misconfiguration (Intentional)

The mask was intentionally reduced to demonstrate how ACLs can fail in ways that are not visible through ls -l alone.
This mirrors real-world incidents where permissions appear correct but access is denied.

## Verification

- Confirm that getfacl still shows user:acluser:rw-
- Confirm that mask::r-- exists
- Confirm that write access fails for acluser
- Confirm that read access still succeeds

## Key Takeaways

- ACL entries do not guarantee access
- The mask always caps effective permissions
- Effective permissions must be evaluated, not assumed
- ACL-related failures often stem from misunderstood masks
- getfacl is required for accurate diagnosis
