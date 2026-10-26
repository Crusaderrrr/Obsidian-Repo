**Secure Shell** is a cryptographic network protocol that lets you *securely communicate with remote machines* over an unsecured network. It encrypts all traffic, meaning no one can intercept what's being sent between your machine and the server.

## Common uses
- Remote Server access (AWS ec2 instances)
- Remote command execution
- File transfer (secure one)
- Automated scripts - ci/cd, backup systems, etc.

## How it works
There are two keys:
- **Private key** - stays on local machine, never shared
- **Public key** - is uploaded to e.g. Bitbucket or to the remote machine

When you try to connect, Bitbucket sends a challenge encrypted with your public key. Only your private key can decrypt it and prove your identity — no password ever travels over the network.

## Basic example (home server)
- I **generate** both *private and public* keys on my pc
- **put the public one on remote**, two ways:  
	- create it 
	- `ssh-copy-id -i ~/.ssh/[PKN].pub user@[RI]`
		- *PKN* - public key name
		- *RI* - remote IP
- **connect** `ssh user@[RI]`

## Configuration
All the config is stored in the `.ssh` folder, specific to each user (on Windows)

A file with `.pub` is a public key and without it is private.

There is a file `known_hosts`, which has host names and IPs

Also a `config` file can be created to specify short names for hosts like that:
```txt
Host hs
    HostName 192.168.1.142
    User nikita
```
and connect with `ssh hs`.