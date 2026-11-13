# Bandit Level 8 → Level 9

## Objective
Find the password stored in `data.txt`. The password is the only line of text that occurs exactly once.

## Approach

Initially, I needed to figure out how to identify a line that appeared only once in a large file.

After some research, I came across the `uniq` command.

### Understanding uniq

The `uniq` command is used to detect or filter repeated adjacent lines in a file.

An important detail is that `uniq` only detects consecutive duplicate lines. If identical lines are separated by other content, they will not be recognised as duplicates.

This is why we need to combine it with `sort`.

### Exploitation

First, sort the contents of the file:

```bash
sort data.txt
```

This places identical lines next to each other.

Next, we can combine `sort` with `uniq -u`:

```bash
sort data.txt | uniq -u
```

### Command breakdown

- `sort data.txt` — Sorts the contents of the file.
- `|` — Pipes the output into another command.
- `uniq -u` — Displays only lines that occur exactly once.

The resulting output contains the unique line, which is the password for the next level.

## Key Takeaways

- Understanding Linux text-processing utilities.
- Using pipes to combine commands.
- Understanding the difference between `uniq` and `uniq -u`.
- Why sorting data before using `uniq` is important.

## Reflection

This level took a little longer than expected because I initially struggled to identify the correct command.

After researching the available utilities, I discovered that combining `sort` and `uniq -u` provides a straightforward solution.

**Lesson learned:** Understanding individual Linux commands is useful, but knowing how to combine them is where their real power becomes apparent.
