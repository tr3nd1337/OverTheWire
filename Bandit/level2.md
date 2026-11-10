# Bandit Level 2 → Level 3

This level took me longer than expected because I misunderstood how `cat` handles options and filenames.

The file had a name containing spaces and leading dashes. Initially, I was putting the dashes inside the quotes, which caused problems.

The correct syntax was:

```bash
cat -- "--name of the file--"
```

The important lesson here was understanding the `--` separator. It tells the command that everything following it should be treated as an argument rather than an option.

A humbling experience, but a useful one!

## Key takeaway

- Understand how command-line options work.
- Remember that `--` separates options from arguments.
- Quotation marks preserve filenames containing spaces.
