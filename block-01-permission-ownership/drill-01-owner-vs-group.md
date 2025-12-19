# Drill 01 — Owner vs Group Permission Evaluation

## Objective

This drill demonstrates how Linux evaluates permissions when a user is both
the **owner** of a file and a member of its **group**, and why group permissions
do **not** act as a fallback for the owner.

The goal is to correct a common misconception about permission evaluation order.

---

## Scenario

A file is configured such that:
- The **owner** does not have execute permission
- The **group** does have execute permission

Intuitively, it may appear that the owner should still be able to execute the
file via group permissions. This drill proves that assumption incorrect.

---

## Setup

A simple executable script is created and inspected:

```bash
echo -e '#!/bin/bash\necho "Script executed"' > test_script.sh
chmod 750 test_script.sh
ls -l test_script.sh
```


## Expected State (Before Misconfiguration)

At this stage:

- Owner has execute permission
- Group has execute permission
- Script executes successfully

## Misconfiguration (Intentional)

Owner execute permission is removed, while group execute permission is preserved:

```
chmod u-x,g+x test_script.sh
ls -l test_script.sh
```

Resulting permission resembles:
-rw-r-x--- 1 emmanuel emmanuel ...


## Observation
Attempting to execute the script:
```
./test_script.sh
```

Results in:
'Permission denied'
This occurs even though the group has execute permission.


## Explanation

Linux evaluates permissions in a strict order:

- Owner
- Group
- Others

If the user is the owner, Linux evaluates only the owner permission bits
and stops immediately.

Linux does not fall back to group permissions when the user matches the file
owner.

Therefore:

- Owner without execute permission → execution denied
- Group permissions are ignored in this case

This behavior is intentional and ensures deterministic permission enforcement.


## Real-World Relevance

This scenario commonly appears in environments where:

- Files are owned by service or deployment accounts
- Group permissions are intended to control execution
- Owner permissions are accidentally misconfigured

Administrators may incorrectly assume group permissions will compensate,
leading to unexpected execution failures.

## Key Takeaways

- Permission evaluation stops at the first matching category
- Group permissions are not a fallback for the owner
- Owners can lock themselves out of executing their own files
- Understanding evaluation order is critical for troubleshooting access issues

##Common Mistake Addressed

Incorrect assumption:
“If the group has execute permission, the owner should still be able to execute.”

Correct understanding:
“If you are the owner, only owner permissions are evaluated.”
