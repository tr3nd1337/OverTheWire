# Bandit Level 9 → Level 10

## Objective

Find the password stored in `data.txt`.

The password is stored among other data and is preceded by several `=` characters.

## Approach

Initially, I attempted to inspect the file by sorting its contents and using `strings`.

However, manually scrolling through the output was inefficient.

After looking into the available options, I found a much better approach using `grep`.

### Understanding strings

The `strings` utility extracts sequences of printable characters from binary files or other data.

This is particularly useful when investigating files containing binary data mixed with readable text.

The `-a` option instructs `strings` to scan the entire file.

### Exploitation

Instead of manually inspecting the output, we can pipe it directly into `grep`:

```bash
strings -a data.txt | grep "==="
```

### Command breakdown

- `strings` — Extracts readable character sequences.
- `-a` — Scans the entire file.
- `data.txt` — Specifies the file being investigated.
- `|` — Pipes the extracted strings into the next command.
- `grep "==="` — Filters the output to display lines containing three consecutive equals signs.

The resulting output reveals the relevant string containing the password.

## Key Takeaways

- Understanding how binary files can contain readable strings.
- Using `strings` for basic file analysis.
- Filtering command output with `grep`.
- Combining Linux utilities using pipes.
- Improving enumeration efficiency instead of manually inspecting large outputs.

## Reflection

My initial approach involved manually scrolling through the output to locate the relevant string.

Although it worked, it wasn't particularly efficient.

The better solution was:

```bash
strings -a data.txt | grep "==="
```

This immediately filters the output and makes identifying the relevant information significantly easier.

**Lesson learned:** Whenever possible, automate filtering instead of manually searching through large amounts of output.
