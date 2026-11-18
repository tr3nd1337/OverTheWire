# Bandit Level 18 → Level 19

## Objective

The challenge demonstrates that SSH can execute commands directly on a remote machine without opening an interactive shell.

## My Approach

Initially, I assumed I needed to establish a normal SSH session. However, the solution was much simpler.

Instead of requesting an interactive shell, I passed the command directly through SSH.

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
```

This executed `cat readme` on the remote machine and returned the file contents directly to my terminal.

## Key Takeaways

- SSH supports remote command execution.
- You don't always need an interactive shell to interact with a remote system.
- Commands can be passed directly as arguments to SSH.
- This technique is useful for remote administration and automation.

## What I Learned

An SSH connection can be used for both interactive sessions and direct command execution.

Sometimes the simplest solution is to execute exactly what you need remotely rather than trying to establish a full shell session.

## References

- [OpenSSH Manual](https://man.openbsd.org/ssh)
