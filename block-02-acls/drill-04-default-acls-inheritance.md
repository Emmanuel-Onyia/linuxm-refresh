# Drill 04 — Default ACLs and Inheritance

## Goal

To demonstrate how **default ACLs** control permission inheritance for newly
created files and directories, and to distinguish between **access ACLs** and
**default ACLs**.

This drill completes the ACL model by showing how permissions can be enforced
predictably over time without manual intervention.

---

## Setup

Create a shared directory:

```bash
mkdir ~/shared
```

Verify its initial ACLs:
```bash
getfacl ~/shared
```

## Commands

Set a default ACL for a named user:
```bash
setfacl -d -m u:acluser:rw ~/shared
```

Inspect the directory ACL:
```bash
getfacl ~/shared
```
Create a file inside the directory:
```bash
touch ~/shared/inherited.txt
```
Inspect the inherited ACL on the file:
```bash
getfacl ~/shared/inherited.txt
```

## Observation

- The directory contains default: ACL entries
- A separate default:mask:: entry exists
- Newly created files inherit ACL entries automatically
- Inherited files do not retain the default: prefix
- Files contain access ACLs derived from the directory defaults

## Explanation

Default ACLs act as templates.

When a new file or directory is created:
- Default ACL entries are copied
- The copied entries become access ACLs
- Files cannot contain default ACLs themselves
The default ACL mask defines the maximum effective permissions for inherited
group-class entries independently of the directory’s current access ACL.

## Verification

- Confirm that default ACLs appear only on the directory
- Confirm that inherited files contain access ACLs, not default ACLs
- Confirm that inherited permissions match the directory’s default ACL rules

## Key Takeaways

- Default ACLs apply only at object creation time
- They do not retroactively affect existing files
- Files inherit ACLs but cannot retain default: entries
- Default ACLs enable predictable, directory-scoped permission inheritance
- Default ACL masks and umask serve different purposes
