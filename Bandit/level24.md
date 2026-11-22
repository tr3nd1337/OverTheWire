# OverTheWire Bandit: Level 24 → 25

## Objective

The objective of this level is to retrieve the password for the next level by interacting with a service running on port `30002`.

The service requires two pieces of information:
- The current Bandit password.
- A four-digit PIN.

Since the PIN is unknown, we need to automate the process of testing all possible combinations.

## 1. Understanding the challenge

A four-digit PIN has 10,000 possible combinations:

```text
0000
0001
0002
...
9999
```

Manually testing every combination would be impractical. Instead, we can use a Bash loop to generate the combinations automatically.

## 2. Generating the PIN combinations

We can use `seq -w` to generate numbers from `0000` to `9999`, preserving leading zeros.

```bash
seq -w 0000 9999
```

The `-w` option ensures that all generated numbers have the same width.

## 3. Automating the attempts

We can create a simple Bash script:

```bash
#!/bin/bash

for pin in $(seq -w 0000 9999); do
    echo "CURRENT_PASSWORD $pin"
done | nc localhost 30002
```

Replace `CURRENT_PASSWORD` with the password obtained from the previous level.

### Explanation

- `for pin in`: Iterates through each generated PIN.
- `seq -w 0000 9999`: Generates all 10,000 four-digit combinations.
- `echo`: Sends the password and PIN together.
- `nc localhost 30002`: Connects to the service on port 30002.
- `|`: Pipes the generated input into Netcat.

We use one Netcat connection for the sequence of attempts.

## 4. Retrieving the password

The service processes the combinations and eventually returns the password for Bandit Level 25 when the correct PIN is supplied.

The important part of this challenge is understanding how to automate repetitive tasks rather than attempting them manually.

## Key takeaways

- Bash loops can automate repetitive operations.
- `seq -w` is useful when generating fixed-width numerical combinations.
- Netcat can interact with TCP services.
- Pipes allow us to send generated input directly into another program.

**What I learned:** A simple Bash script can automate thousands of authentication attempts, making repetitive manual tasks significantly more efficient.
