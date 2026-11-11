# Bandit Level 5 → Level 6

## Approach

This level introduced the use of the `find` command to identify a specific file based on its properties.

The objective was to locate a regular file with an exact size of 1,033 bytes while excluding executable files.

## Command Used

```bash
find . -type f -size 1033c ! -executable
```

## Command Breakdown

| Argument | Description |
|---|---|
| `find .` | Searches recursively from the current directory. |
| `-type f` | Restricts the search to regular files. |
| `-size 1033c` | Matches files that are exactly 1,033 bytes in size. |
| `! -executable` | Excludes executable files. |

**Note:** The `c` suffix specifies that the file size is measured in bytes.

## Key Takeaways

- `find` can locate files based on specific attributes.
- File type, size and permissions can be combined to narrow down search results.
- Understanding command-line arguments is essential when navigating Linux environments.

This level provided additional practice with Linux file discovery and command syntax.
