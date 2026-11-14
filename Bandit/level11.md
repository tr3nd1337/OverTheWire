# Bandit Level 11 → Level 12

## Objective
The password for the next level is stored in `data.txt`.

However, the contents have been encrypted using a ROT13 cipher.

## Approach

This level was considerably more challenging for me, so I used ChatGPT to help me understand the underlying concept and work through the solution.

The file contained the following encoded text:

```text
Gur cnffjbeq vf TEBbmJCB8DlA0zTewHxVQ0JPLxMvDkeA
```

The encryption method used here is ROT13.

ROT13 is a simple substitution cipher that shifts each letter 13 positions through the alphabet.

For example:

- A becomes N.
- B becomes O.
- C becomes P.
- G becomes T.

Since the English alphabet contains 26 letters, applying ROT13 twice returns the original text.

I used the following command to decode the contents:

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

The decoded output revealed the password for the next level.

## What I Learned

- ROT13 is a substitution cipher.
- Each alphabetical character is shifted 13 positions.
- ROT13 is reversible and does not provide real security.
- Linux `tr` can be used to perform character translation directly in the terminal.

## Additional Resources

[Wikipedia — ROT13](https://en.wikipedia.org/wiki/ROT13)

## Key Takeaway

This level introduced me to substitution ciphers and demonstrated how Linux text-processing utilities can be used to decode information efficiently.
