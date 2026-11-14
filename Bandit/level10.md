# Bandit Level 10 → Level 11

## Objective
The password for the next level is stored in `data.txt`, encoded using Base64.

## Approach

I started by checking the available help for the `base64` command:

```bash
base64 --help
```

After looking through the available options, I identified `-d` as the flag used for decoding Base64-encoded data.

I then decoded the contents of `data.txt`:

```bash
base64 -d data.txt
```

The command returned the decoded password.

## What I Learned

- Base64 is an encoding scheme used to represent binary data using ASCII characters.
- Encoding is not encryption; Base64 does not provide confidentiality.
- The `base64 -d` command can be used to decode Base64 data directly from a file.

## Key Takeaway

Sometimes the solution is much simpler than expected. Reading command documentation and understanding available flags can save a lot of time.
