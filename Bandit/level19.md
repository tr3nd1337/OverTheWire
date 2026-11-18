# Bandit Level 19 → Level 20

## Today's Linux Lesson: SUID

### What is SUID?

SUID (Set User ID) is a special Linux file permission that allows an executable to run with the privileges of its file owner rather than the privileges of the user executing it.

For example, if a binary is owned by root and has the SUID permission enabled, it may execute with root privileges.

### Important Concepts

1. SUID allows an executable to run with the privileges of its file owner.
2. Shell builtins (such as `cd` and `export`) are handled by the shell rather than being standalone executable binaries.
3. SUID programs can execute external commands, depending on their implementation.
4. SUID permissions on scripts are generally ignored by Linux for security reasons.
5. What can be executed depends on how the SUID program is implemented.

**Most important takeaway:** SUID is a privilege mechanism, not a command restriction.

---

## Hunting for SUID Binaries

To enumerate files with the SUID permission across the filesystem:

```bash
find / -type f -perm -4000 2>/dev/null
```

### Understanding the command

| Argument | Description |
|---|---|
| `find /` | Search starting from the root directory |
| `-type f` | Search for regular files |
| `-perm -4000` | Find files with the SUID bit enabled |
| `2>/dev/null` | Suppress permission-denied errors |

---

## What Should You Investigate?

When identifying SUID binaries, consider the following:

- Is the binary legitimate?
- Is it a standard Linux utility?
- Does it have unusual permissions?
- Is it custom-made?
- Is its version vulnerable?
- Can it execute arbitrary commands?
- Does its implementation introduce a privilege escalation opportunity?

## Useful Resource

[GTFOBins](https://gtfobins.github.io/)

GTFOBins is a curated list of Unix binaries that can potentially be abused in security contexts, including privilege escalation.

It provides examples of how certain binaries can be leveraged when they have elevated permissions.

---

## Key Takeaways

- SUID is an important Linux privilege mechanism.
- Enumerating SUID binaries is a fundamental privilege escalation technique.
- Not every SUID binary is vulnerable.
- Understanding how a binary operates is more important than simply identifying its permissions.

**Lesson learned:** Always investigate unusual SUID binaries and understand their functionality before attempting exploitation.
