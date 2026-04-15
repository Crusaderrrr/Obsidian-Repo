**Secure Shell** is a cryptographic network protocol that lets you *securely communicate with remote machines* over an unsecured network. It encrypts all traffic, meaning no one can intercept what's being sent between your machine and the server.

## Common uses
- Remote Server access (aws ec2 instances)
- Remote command execution
- File transfer (secure one)
- Automated scripts - ci/cd, backup systems, etc.

## How it works
There are two keys:
- **Private key** - stays on local machine, never shared
- **Public key** - is uploaded to e.g. Bitbucket

When you try to connect, Bitbucket sends a challenge encrypted with your public key. Only your private key can decrypt it and prove your identity — no password ever travels over the network.