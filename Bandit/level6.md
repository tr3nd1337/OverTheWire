# Bandit Level 6 → Level 7

## Objective

Locate a file somewhere on the server that meets specific ownership, group and file-size requirements.

## Command

```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

## Command Breakdown

| Argument | Description |
|---|---|
| `find /` | Searches recursively from the root directory. |
| `-type f` | Returns regular files only. |
| `-user bandit7` | Matches files owned by `bandit7`. |
| `-group bandit6` | Matches files belonging to group `bandit6`. |
| `-size 33c` | Matches files exactly 33 bytes in size. |
| `2>/dev/null` | Redirects standard error to `/dev/null`, suppressing error messages. |

## Understanding File Types

The `-type` option allows us to filter results based on file type.

- `f` – Regular file
- `d` – Directory
- `l` – Symbolic link

Since the objective involves locating a file containing a password, `-type f` is appropriate.

## Understanding Output

Example:

```text
-rw-r--r-- 1 bandit7 bandit6 33
```

The relevant fields indicate:

- `bandit7` – File owner.
- `bandit6` – Group owner.
- `33` – File size in bytes.

## Additional Examples

Search for files owned by a specific user:

```bash
find / -user bandit7 2>/dev/null
```

Search for files with a specific size:

```bash
find / -type f -size 33c 2>/dev/null
```

Search within the current directory and its subdirectories:

```bash
find . -type f
```

## Key Takeaways

- `find` is a powerful utility for filesystem enumeration.
- File ownership and group permissions can help narrow down search results.
- `2>/dev/null` is useful when searching directories where permission restrictions generate errors.
- Combining multiple conditions makes file searches significantly more efficient.
