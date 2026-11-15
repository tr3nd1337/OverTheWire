# Bandit Level 12 → Level 13

## Objective

Recover the password hidden inside a repeatedly compressed file.

## Approach

This level was quite a journey. The first step was reconstructing the original binary file from a hexdump using `xxd -r`.

```bash
xxd -r <input_file> <output_file>
```

Once the binary file was reconstructed, I used the `file` command to identify its format and determine which decompression utility was required.

The file had been compressed multiple times using a combination of:

- Gzip
- Bzip2
- Tar

The process involved repeatedly identifying the file format, renaming files where necessary, and extracting each compression layer until the original password was recovered.

## Key Takeaways

- `xxd -r` – Reconstructs binary data from a hexdump.
- `file` – Identifies file types and formats.
- `gzip` / `gunzip` – Handles Gzip compression.
- `bzip2` / `bunzip2` – Handles Bzip2 compression.
- `tar` – Extracts archived files.
