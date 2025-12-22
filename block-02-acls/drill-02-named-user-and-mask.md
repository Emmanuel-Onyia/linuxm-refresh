# Drill 02 — Introducing a Named User and the ACL Mask

## Goal

To observe how adding a named user ACL entry extends the ACL, introduces the
ACL mask automatically, and changes how permissions are displayed and evaluated.

This drill establishes the relationship between **named ACL entries**, the
**mask**, and misleading output from `ls -l`.

---

## Setup

Ensure you are working with the file created in Drill 01:

```bash
cd ~/acl-lab
```

Create a secondary user if one does not already exist:
```bash
sudo useradd acluser
```

## Commands

Add a named user ACL entry:
```bash
setfacl -m u:acluser:rw sample.txt
```

Inspect the ACL and permissions:
```bash
getfacl sample.txt
ls -l sample.txt
```

## Observation

- A user:acluser entry appears in the ACL
- A mask:: entry is created automatically
- ls -l now displays a + indicator
- The group permission field in ls -l reflects the mask, not the group:: ACL entry

## Explanation

Adding a named user converts the ACL from base to extended.

Once extended ACL entries exist:

- Linux introduces a mask to define the maximum effective permissions for all group-class entries
- The mask applies to:
	-Named users
	-The owning group
	-Named groups
- ls -l displays the mask value in the group permission field

This behavior is intentional and often leads to confusion if ACLs are not
examined using getfacl.

## Verification

- Confirm that user:acluser appears in getfacl output
- Confirm that a mask:: entry exists
- Confirm that ls -l shows a +
- Confirm that the group permissions shown by ls -l match the mask value

## Key Takeaways

- Adding a named user creates an extended ACL
- Extended ACLs require a mask
- The mask limits effective permissions for all group-class entries
- ls -l displays the mask, not the owning group permissions, when ACLs exist
