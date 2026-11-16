# Bandit Level 14 → Level 15

## Objective
Retrieve the password for the next level by communicating with a service listening on localhost.

## Methodology

First, retrieve the current level's password from:

```bash
cat /etc/bandit_pass/bandit14
```

Next, establish a connection to the service using Netcat:

```bash
nc localhost 30000
```

Once connected, submit the password obtained from the previous step.

The service will validate the password and return the credentials for the next level.

## Key Takeaways

- **Netcat (`nc`):** A networking utility used to establish TCP and UDP connections.
- **Localhost:** Refers to the local machine (127.0.0.1).
- **Ports:** Identify specific services running on a host.
- **TCP communication:** Netcat allows direct interaction with services over TCP connections.

## Credentials

- Previous level: `bandit14`
- Next level: `bandit15`

> Passwords intentionally excluded from this repository.
