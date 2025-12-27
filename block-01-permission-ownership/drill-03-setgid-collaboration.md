# Drill 03 — setgid and Shared Directory Collaboration

## Objective

This drill demonstrates how the **setgid bit on directories** enforces consistent
group ownership for files created in shared locations, and why it is essential
for stable collaboration in multi-user environments.

The goal is to understand **group inheritance**, prevent permission drift, and
recognize where setgid is used in real systems.

---

## Scenario

Multiple users collaborate within a shared directory. All users belong to the
same project group, and files created in the directory must remain accessible
to the entire group.

Without proper configuration, newly created files may inherit the creator’s
default group, breaking collaboration over time.

This drill demonstrates how setgid solves this problem.

---

## Setup

Create a shared directory:

```bash
mkdir shared
```

Set the group ownership of the directory:

```bash
chgrp emmanuel shared
```

Apply permissions with the setgid bit enabled:

```bash
chmod 2770 shared
ls -ld shared
```bash


Expected output resembles:

```bash
drwxrws--- 2 emmanuel emmanuel ...
```

Note the s in the group execute position, indicating setgid is active.


##Expected State

At this stage:
- Owner has full access (rwx)
- Group has full access (rwx)
- Others have no access
- The directory enforces group inheritance via setgid


##Observation

Create a file inside the shared directory:

```bash
echo "Shared data" > shared/data.txt
ls -l shared/data.txt
```

The file inherits the group ownership of the parent directory, even if the
creator’s default group differs.

## Explanation

- When the setgid bit is applied to a directory:
- New files and subdirectories inherit the directory’s group
- Group ownership remains consistent
- Permission drift is prevented

Without setgid:
- Files inherit the creator’s primary group
- Group ownership becomes inconsistent
- Collaboration breaks over time

The numeric permission 2770 breaks down as:
- 2 → setgid
- 7 → owner permissions (rwx)
- 7 → group permissions (rwx)
- 0 → no access for others

## Real-World Relevance

setgid directories are commonly used in:
- /srv and /srv/projects
- /var/www
- Shared development and CI/CD directories
- Application data directories accessed by multiple users or services

They ensure that all files remain accessible to the intended group without
manual intervention.

## Key Takeaways

- setgid enforces group ownership inheritance on directories
- It prevents permission drift in shared environments
- Numeric permissions help identify special bits (2 for setgid)
- setgid is a foundational tool for multi-user collaboration

## Common Mistake Addressed

Incorrect assumption:
“Group ownership will remain consistent automatically.”

Correct understanding:
“setgid must be explicitly enabled on shared directories to enforce group
inheritance.”
