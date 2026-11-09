# Level 1

## Objective
The objective was to read the contents of a file named `-`, which can be confusing because filenames beginning with a dash may be interpreted as command-line options.

## Method 1: Relative Path

One way to access the file is to prefix its name with `./`.

This tells Linux to look for the file in the current working directory rather than interpreting the filename as an option.

```bash
cat ./-
```

## Method 2: Double-Dash Operator

Another approach is to use the `--` operator.

This tells the command that all subsequent arguments should be treated as filenames rather than options.

```bash
cat -- -
```

Both methods successfully display the contents of the file.

## Key Takeaways

- `./` – Specifies a file or directory relative to the current working directory.
- `--` – Indicates the end of command-line options.
- `cat` – Displays file contents in the terminal.

## Result

Successfully retrieved the password required for Level 2.

**Password:** `[EMAIL IF YOU NEED HELP]`
