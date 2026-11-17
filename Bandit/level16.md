# Bandit Level 16 → 17

This one was interesting! We had to scan ports between 31000 and 32000 and identify which services were using SSL/TLS.

## 1. Port Scanning with Nmap

First, we scanned the target's port range:

```bash
nmap -p 31000-32000 localhost
```

This identified the open ports within the specified range.

Next, we enabled service detection using `-sV`:

```bash
nmap -p 31000-32000 -sV 127.0.0.1
```

This helped us identify the services running on the open ports.

We discovered several echo services and two services supporting SSL/TLS.

## 2. Connecting with OpenSSL

We had already worked with OpenSSL in the previous level, but this time things got a little confusing.

I kept receiving `KEYUPDATE` messages when trying to submit the password.

After some digging around, I used:

```bash
openssl s_client -connect localhost:31790 -quiet
```

The `-quiet` option suppresses session and certificate information, making the application-level communication easier to work with.

After submitting the password, BOOM! Instead of another password, we received an SSH private key.

## 3. SSH Private Key Authentication

Now we needed to save the private key locally.

Created a file:

```bash
nano ~/bandit17.key
```

Pasted the private key and saved it.

Next, we restricted its permissions:

```bash
chmod 600 ~/bandit17.key
```

SSH requires private keys to have appropriately restrictive permissions. Otherwise, it may refuse to use them.

Finally, we authenticated using the private key:

```bash
ssh -i ~/bandit17.key bandit17@bandit.labs.overthewire.org -p 2220
```

And we're in!

## What I Learned

- Nmap port scanning using `-p`.
- Service and version detection using `-sV`.
- Establishing SSL/TLS connections with OpenSSL.
- Understanding the `-quiet` option.
- SSH private key authentication.
- File permissions and why `chmod 600` matters.

Another level down. Onwards!
