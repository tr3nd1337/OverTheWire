# Bandit Level 7 → Level 8

## Objective

Locate the password inside the `data.txt` file.

The password is stored next to the word `millionth`.

## Command

```bash
grep "millionth" data.txt
```

## Command Breakdown

| Argument | Description |
|---|---|
| `grep` | Searches text for lines matching a specified pattern. |
| `"millionth"` | The search pattern. |
| `data.txt` | The file being searched. |

## Understanding Grep

`grep` is a command-line utility used to search files for specific strings or patterns.

Its basic syntax is:

```bash
grep "pattern" filename
```

For this level, we know that the password is located on the same line as the word `millionth`.

Instead of manually inspecting the entire file, we can use `grep` to locate the relevant line.

## Additional Examples

Search for a specific word:

```bash
grep "millionth" data.txt
```

Perform a case-insensitive search:

```bash
grep -i "millionth" data.txt
```

Display matching lines with their line numbers:

```bash
grep -n "millionth" data.txt
```

## Key Takeaways

- `grep` allows efficient searching through files.
- You can search for specific words, strings or regular expressions.
- It is particularly useful when analysing large text files.
- Combining `grep` with other Linux utilities can make enumeration more efficient.
