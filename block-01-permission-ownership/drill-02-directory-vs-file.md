# Drill 02 — Directory Permissions vs File Permissions

## Objective

This drill demonstrates that **file permissions do not supersede directory
permissions** and that directory traversal permissions are evaluated before
file-level permissions.

The goal is to correct the assumption that a readable file should always be
accessible.

---

## Scenario

A file is configured to be readable by the user. However, the directory
containing the file does not allow traversal.

At first glance, it appears that the file should still be readable. This drill
demonstrates why that assumption is incorrect.

---

## Setup

Create a directory and a file inside it:

```bash
mkdir secure_dir
echo "Top secret data" > secure_dir/secret.txt
```

Apply permissions:

```bash
chmod 644 secure_dir/secret.txt
chmod 600 secure_dir
```
Inspect permissions:

```bash
ls -ld secure_dir
ls -l secure_dir/secret.txt
```

At this stage:

- The file is readable
- The directory does not have execute (x) permission


## Observation

Attempt to read the file:

```bash
cat secure_dir/secret.txt
```

The command fails with:
'Permission denied'

This occurs even though the file itself has read permission.


## Explanation

Linux requires two independent permission checks to access a file:

- Execute (x) permission on every directory in the path
- Appropriate permission on the file itself (e.g., read r)

Directory permissions control access to the path, not the contents of the
file.

Without execute permission on the directory:

- The directory cannot be entered
- Files inside cannot be accessed
- File permissions are never evaluated

## Permission Meaning Comparison
Permission	File Meaning		Directory Meaning
r		Read file contents	List directory contents
w		Modify file		Create, delete, or rename files
x		Execute file		Traverse directory / access files

In this drill, directory traversal is blocked, so access fails.

## Real-World Relevance

This behavior is intentionally used in real systems to:

- Protect sensitive directories
- Restrict log access
- Hide filenames while allowing controlled service access

For example:

- Log files may be world-readable
- But the log directory itself restricts traversal

This prevents casual inspection while preserving controlled access.

## Key Takeaways

- Directory permissions act as gatekeepers
- File permissions do not override directory permissions
- Execute (x) permission on directories is required to access files
- Always check directory permissions when troubleshooting access issues


## Common Mistake Addressed

Incorrect assumption:
“If a file is readable, it should be accessible.”

Correct understanding:
“Directory traversal permission is required before file permissions are evaluated.”
