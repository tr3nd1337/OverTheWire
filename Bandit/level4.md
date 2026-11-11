# Bandit Level 4 → Level 5

## Approach

Initially, I attempted to inspect the files individually using `cat`, working through them one by one.

After inspecting several files, I decided to combine their contents into a single output to make the process more efficient.

However, combining the contents made it difficult to identify which file contained the correct password.

The password was eventually located in `-file07`.

## Commands Used

```bash
ls
cat *
```

- `ls` – Lists the contents of the current directory.
- `cat *` – Displays the contents of files in the current directory.

## Verification

After reviewing the combined output, I used the following command to inspect the suspected file individually:

```bash
cat ./-file07
```

This confirmed that the file contained the correct password.

## Key Takeaways

- Wildcards (`*`) can be used to reference multiple files.
- Combining file contents can make output difficult to interpret.
- When working with multiple files, verify the exact source of the required information.
- Files beginning with a hyphen should be referenced using an appropriate path, such as `./-file07`.
