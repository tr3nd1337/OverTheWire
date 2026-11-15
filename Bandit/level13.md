# Bandit Level 13 → Level 14

## Objective

Understand SSH public-key authentication and use a provided private key to authenticate to another account.

## Key Concepts

This level introduces SSH key-based authentication and the relationship between public and private keys.

SSH authentication typically relies on a key pair:

- **Private key:** Kept securely by the client. Used to prove ownership of the identity.
- **Public key:** Stored on the remote server in the user's `~/.ssh/authorized_keys` file.

During authentication, the client uses its private key to sign authentication data. The server verifies the signature using the corresponding authorised public key.

### Security Implications

If an attacker compromises a workstation and obtains an SSH private key, they may be able to impersonate its owner.

However, successful authentication also depends on several conditions:

1. The attacker must satisfy any passphrase protection on the stolen private key.
2. The attacker must be able to reach the target SSH service over the network.
3. The corresponding public key must be authorised for an account on the target server.

## Practical Approach

The level provides an SSH private key that needs to be transferred to your own machine.

Use the `-i` option to specify the private key when connecting:

```bash
ssh -i <private_key> bandit14@<hostname>
```

Ensure the private key has appropriate permissions before using it:

```bash
chmod 600 <private_key>
```

## Key Takeaways

- Understand the difference between public and private SSH keys.
- Learn how SSH key-based authentication works.
- Understand the security implications of compromised private keys.
- Use `ssh -i` to authenticate with a specific private key.
- Understand the purpose of `authorized_keys`.

## Password

Not applicable. The objective is to use the provided private SSH key to authenticate to the next account.
