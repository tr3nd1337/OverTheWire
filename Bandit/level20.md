# Bandit Level 20 → 21

## Objective

Retrieve the password for Bandit Level 21 by exploiting a SUID binary that communicates with a user-specified TCP port on localhost.

## 1. Understanding the SUID Binary

The level provides a SUID executable that:

- Connects to a specified TCP port on localhost.
- Waits to receive a line of text.
- Compares the received input against the password of the previous level.
- Returns the next level's password if the comparison succeeds.

The important detail is that we control the TCP endpoint the binary connects to.

## 2. Creating a TCP Listener

Instead of connecting to an existing service, we create our own listener using Netcat.

```bash
nc -lvnp PORT
```

Breaking down the command:

| Argument | Explanation |
|---|---|
| `-l` | Listen for incoming connections |
| `-v` | Enable verbose output |
| `-n` | Disable DNS resolution |
| `-p` | Specify the listening port |

Our listener acts as the service that the SUID executable expects to communicate with.

## 3. Exploiting the Binary

The process:

1. Start the Netcat listener on the chosen port.
2. Execute the SUID binary and specify the same port.
3. Wait for the binary to establish a connection.
4. Supply the Bandit 20 password through the Netcat listener.
5. Observe the response returned through the connection.

Once the supplied password matches the expected value, the binary returns the password for Bandit 21.

## 4. Technical Concepts Learned

| Concept | Explanation |
|---|---|
| SUID | Allows an executable to run with the privileges of its file owner. |
| TCP Listener | Waits for incoming network connections on a specified port. |
| Localhost | Refers to the machine on which the connection is initiated. |
| Service Impersonation | Creating an endpoint that behaves like an expected service. |
| Netcat | A networking utility used to establish connections, listen for incoming traffic and exchange data. |

## 5. Security Implications

This level demonstrates how a privileged application can communicate with an endpoint controlled by an unprivileged user.

Poorly secured local service communication can introduce opportunities for service impersonation and potentially privilege escalation or
