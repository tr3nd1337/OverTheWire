# Bandit Level 15 → Level 16

## Objective
Retrieve the password for the next level by connecting to a service that requires SSL/TLS encryption.

## Methodology

Unlike the previous challenge, this service requires an encrypted connection.

Instead of using Netcat, we can use OpenSSL's `s_client` utility to establish an SSL/TLS connection.

Execute:

```bash
openssl s_client -connect localhost:30001
```

Once the connection is established:

1. Wait for the SSL/TLS handshake to complete.
2. Submit the current level's password.
3. The server validates the credentials.
4. Retrieve the password for the next level.

## Key Takeaways

- **OpenSSL:** A toolkit for implementing SSL/TLS protocols.
- **SSL/TLS:** Protocols used to establish encrypted communication.
- **s_client:** An OpenSSL utility that acts as a diagnostic SSL/TLS client.
- **Encrypted connections:** Some services require encrypted communication rather than standard TCP connections.

## Credentials

- Previous level: `bandit15`
- Next level: `bandit16`

> Passwords intentionally excluded from this repository.
