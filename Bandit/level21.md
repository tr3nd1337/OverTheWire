# Bandit Level 21 → 22

## Objective

Retrieve the password for Bandit Level 22 by investigating a scheduled cronjob.

## 1. Locate the Cron Configuration

First, navigate to the cron configuration directory:

```bash
cd /etc/cron.d/
```

List its contents:

```bash
ls -la
```

We are looking for a configuration file called:

```bash
cronjob_bandit22
```

Read its contents:

```bash
cat cronjob_bandit22
```

### Output

```bash
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

### Understanding the Configuration

| Component | Explanation |
|---|---|
| `@reboot` | Executes the command when the system starts. |
| `* * * * *` | Executes the command every minute. |
| `bandit22` | Specifies the user executing the command. |
| `/usr/bin/cronjob_bandit22.sh` | Script being executed. |
| `&> /dev/null` | Discards standard output and standard error. |

**Important:** The script executes as `bandit22`, not our current user (`bandit21`).

## 2. Investigate the Shell Script

The cron configuration tells us exactly where the script is located.

Read it:

```bash
cat /usr/bin/cronjob_bandit22.sh
```

### Output

```bash
#!/bin/bash

chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv

cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

There are two important commands here.

### Command 1: chmod 644

```bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

This changes the permissions of the temporary file.

Permission `644` translates to:

| User | Permissions |
|---|---|
| Owner | Read and write |
| Group | Read |
| Others | Read |

This means other users, including `bandit21`, can read the file.

### Command 2: Password Redirection

```bash
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

Breaking it down:

- `cat` reads the contents of a file.
- `/etc/bandit_pass/bandit22` contains the password for Bandit 22.
- `>` redirects the output into another file.
- `/tmp/...` is the destination where the password is stored.

Essentially, the cronjob copies the Bandit 22 password into a temporary file that other users can read.

## 3. Retrieve the Password

Since the cronjob executes every minute, we simply need to read the temporary file it creates.

Execute:

```bash
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

This displays the password for Bandit 22.

**Important:** The filename contains a capital `O`, not a zero (`0`).

## 4. Connect to Bandit 22

Use the retrieved password to connect:

```bash
ssh bandit22@bandit.labs.overthewire.org -p 2220
```

Level completed!

## 5. Technical Concepts Learned

| Concept | Explanation |
|---|---|
| Cron | Linux task scheduler that executes commands automatically. |
| Crontab | Defines when scheduled commands execute. |
| chmod | Changes file permissions. |
| 644 | Owner can read/write; everyone else can read. |
| Redirection (`>`) | Sends command output into a file. |
| File Ownership | Determines who owns and can modify a file. |
| Shell Scripts (`.sh`) | Files containing commands executed by a shell. |

## 6. Security Implications

This level demonstrates how scheduled tasks can unintentionally expose sensitive information.

The cronjob executes with the permissions of `bandit22`, allowing it to access the Bandit 22 password file.

It then copies that password into a temporary file with permissions that allow other users to read it.

As a security analyst, always investigate:

1. What scheduled tasks are running?
2. Which user executes them?
3. What scripts are being executed?
4. What files do those scripts access?
5. Where is their output stored?
6. Are the resulting files accessible to unauthorised users?

## Key Takeaway

Scheduled tasks running with elevated or different user permissions can introduce serious security risks when their output is exposed to unauthorised users.

Always inspect cronjobs, their execution context, the scripts they invoke and the permissions of files they create.
