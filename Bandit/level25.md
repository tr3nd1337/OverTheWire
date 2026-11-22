# OverTheWire Bandit: Level 25 → 26

## Objective

The objective of this level is to move from Bandit Level 25 to Level 26.

Unlike previous levels, this challenge focuses on understanding restricted login shells and exploiting the functionality of programs available within them.

## 1. Investigating the user account

After connecting as Bandit 25, we discover that the account uses a custom shell rather than a standard Bash shell.

We can inspect the configured login shell using:

```bash
cat /etc/passwd | grep bandit26
```

This helps identify the program executed when the user logs in.

## 2. Understanding the restricted environment

The challenge provides an SSH private key for the next account.

However, logging in as Bandit 26 does not immediately provide a normal shell.

Instead, the account launches a restricted environment.

The important observation is that the environment uses the `more` pager.

## 3. Understanding the terminal-size restriction

The challenge behaves differently depending on terminal dimensions.

If the terminal is sufficiently large, the pager may display the available content without providing an opportunity to interact with it.

By reducing the terminal height before connecting, we can force the pager to pause.

## 4. Escaping through the pager

Once the pager pauses, press:

```text
v
```

This opens the Vim editor.

Vim provides additional functionality beyond simply viewing text.

From Vim, enter:

```vim
:set shell=/bin/bash
```

Then:

```vim
:shell
```

This launches a Bash shell from within Vim.

We have now escaped the restricted environment.

## 5. Retrieving the next password

Once inside the shell, navigate to the relevant location and retrieve the password for the next level using the available challenge files.

The important part of this challenge is recognising that a restricted shell does not necessarily prevent access to other functionality exposed by programs it launches.

## Key takeaways

- Linux accounts can use custom login shells.
- Terminal dimensions can affect pager behaviour.
- `more` provides interactive functionality.
- Vim can execute shell commands.
- Restricted environments should be assessed for unintended functionality.

**What I learned:** A restricted shell is only as restrictive as the programs it allows users to access. Understanding the behaviour of those programs can reveal unexpected paths to command execution.
