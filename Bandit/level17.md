# Bandit Level 17 → 18

A relatively straightforward level, but an introduction to another useful Linux command: `diff`.

## 1. Comparing Files with diff

This level introduced us to comparing two files to identify their differences.

The command:

```bash
diff file.txt file2.txt
```

The output indicates which lines differ between the two files.

### Understanding the Output

- `<` indicates a line present in the first file.
- `>` indicates a line present in the second file.

For example:

```text
< old content
> new content
```

This makes it easy to identify changes without manually comparing files line by line.

## What I Learned

- Using `diff` to compare files.
- Understanding differences between two files.
- Interpreting `<` and `>` in diff output.

### Key Takeaway

`diff` is a simple but extremely useful command, especially when comparing configuration files, scripts, logs or other files during Linux enumeration.

One more level completed. Onwards!
