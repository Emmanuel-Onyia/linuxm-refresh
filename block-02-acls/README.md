# Block 02 — Access Control Lists (ACLs)

This block covers **Access Control Lists (ACLs)** as a controlled extension to
standard POSIX permissions.

Rather than treating ACLs as a set of commands, the focus is on understanding
**how Linux evaluates access when ACLs are present**, why permissions may appear
correct but still fail, and how ACLs are used safely in real system
administration scenarios.

---

## Objectives

By completing this block, the goal is to:

- Understand the limitations of traditional owner / group / other permissions
- Explain why ACLs are required in multi-user and service-based environments
- Interpret `getfacl` output accurately
- Understand the ACL **mask** and how it controls effective permissions
- Diagnose access failures caused by misleading ACL configurations
- Understand **default ACLs** and permission inheritance
- Distinguish between ACL masks and `umask`

---

## Why ACLs Matter

Standard Linux permissions are intentionally simple:
- One owner
- One group
- Everyone else

This model breaks down when:
- A single additional user needs access
- Multiple users or services require different permissions
- Ownership or group changes are undesirable
- Access must be granted without broadening permissions

ACLs solve these problems by allowing **explicit, identity-based access rules**
without changing ownership or primary group permissions.

---

## Topics Covered

### ACL Fundamentals
- Base ACLs vs extended ACLs
- Viewing ACLs with `getfacl`
- Modifying ACLs with `setfacl`
- Understanding the `+` indicator in `ls -l`

### ACL Mask and Effective Permissions
- The ACL mask as a **permission ceiling**
- Group-class entries (named users, owning group, named groups)
- Effective permissions as *ACL entry AND mask*
- Why `ls -l` displays the mask instead of group permissions
- Diagnosing access failures caused by the mask

### Intentional Failure Scenarios
- ACLs that appear correct but deny access
- Systematic troubleshooting using `getfacl`
- Understanding why ACLs are safer due to enforced boundaries

### Default ACLs and Inheritance
- Difference between **access ACLs** and **default ACLs**
- How default ACLs act as templates for new files and directories
- Why default ACLs apply only at creation time
- Why files inherit ACLs but cannot retain `default:` entries
- Separate masks for access ACLs and default ACLs

### ACLs vs umask
- `umask` as a process-level permission filter
- ACL masks as file-level permission ceilings
- When default ACLs are preferred over `umask`

---

## Key Takeaways

- ACLs extend POSIX permissions; they do not replace them
- The presence of a `+` indicates extended ACLs exist
- The ACL mask silently limits all group-class permissions
- Effective permissions must always be evaluated, not assumed
- `ls -l` alone is insufficient when ACLs are present
- Default ACLs provide predictable, directory-level inheritance
- ACL masks and `umask` serve different purposes and scopes

---

## Notes

This block emphasizes **interpretation, evaluation order, and diagnosis** rather
than memorization.

The drills intentionally include misconfigurations to mirror how ACL-related
issues present themselves in real production environments, where permissions
often appear correct but behave unexpectedly.
