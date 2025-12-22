# Drill 01 — Visualizing ACL Structure (Base ACL Only)

## Goal

To observe how ACLs exist even when no extended ACL entries are defined, and to
understand how base ACL entries map directly to traditional POSIX permissions.

This drill establishes the baseline before introducing named users, masks, or
inheritance.

---

## Setup

Create a clean working directory and file:

```bash
mkdir ~/acl-lab
cd ~/acl-lab
touch sample.txt
```


## Commands

```bash
ls -l sample.txt
getfacl sample.txt
```

## Observation

- getfacl displays the following entries:
	- user::
	- group::
	- other::
- No mask:: entry is present
- ls -l does not show a + indicator

## Explanation

Even when no extended ACLs exist, every file has an ACL structure.

At this stage:
- The ACL mirrors traditional permissions exactly
- No named users or named groups exist
- No mask is required because no group-class extensions exist
- The ACL is present but not extended

ACLs do not replace POSIX permissions; they extend them only when needed.


## Verification

- Confirm that ls -l output matches getfacl base entries
- Confirm that no mask:: entry exists
- Confirm that no + appears in ls -l

## Key Takeaways

- Base ACL entries always exist on Linux files
- The absence of a mask indicates no extended ACL entries
- The + indicator appears only when extended ACLs are present
- getfacl is the authoritative view of permissions when ACLs are involved
