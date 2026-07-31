# SSH Mastery — Module 1, Lesson 15

# Module 1 Review & Final Assessment

🎉 **Congratulations! You've completed Module 1.**

You now understand the **fundamentals of SSH**. You may not have connected to a real server yet, but you have built the knowledge needed to do so confidently.

---

# What You Learned

## Lesson 1 — What is SSH?

You learned:

- SSH = **Secure Shell**
- Securely control another computer from your terminal
- All communication is encrypted

---

## Lesson 2 — Why Developers Use SSH

You learned SSH is used for:

- Deploying applications
- Managing Linux servers
- Viewing logs
- Restarting services
- Managing Docker
- Connecting to cloud servers

---

## Lesson 3 — Client vs Server

```
Laptop (SSH Client)
        │
        ▼
Ubuntu Server (SSH Server)
```

Remember:

> **Client initiates. Server listens.**

---

## Lesson 4 — How SSH Works

Connection flow:

```
Find Server
      ↓
Connect Port 22
      ↓
Verify Server
      ↓
Encrypt
      ↓
Authenticate
      ↓
Open Shell
```

---

## Lesson 5 — Encryption

You learned:

- Encryption protects data
- SSH uses:
    - Asymmetric encryption → Handshake
    - Symmetric encryption → Fast communication

---

## Lesson 6 — Authentication

Two common methods:

- Password
- SSH Key

SSH keys are the professional standard.

---

## Lesson 7 — Password vs SSH Key

|Password|SSH Key|
|---|---|
|Easy|Better|
|Manual|Automatic|
|Less secure|More secure|
|Good for beginners|Used in production|

---

## Lesson 8 — SSH Tools

You learned these commands:

```bash
ssh
scp
sftp
ssh-keygen
ssh-agent
ssh-add
```

---

## Lesson 9 — SSH Client

Useful commands:

```bash
ssh -V
```

```bash
ssh --help
```

```bash
man ssh
```

```bash
ssh -G localhost
```

---

## Lesson 10 — First SSH Connection

Connection syntax:

```bash
ssh user@server
```

You learned about:

- First connection warning
- Host fingerprint
- `known_hosts`
- `exit`

---

## Lesson 11 — Hostnames & Ports

You learned:

Hostname:

```
github.com
```

↓

DNS

↓

IP

↓

Port 22

↓

SSH

---

## Lesson 12 — Common Errors

You can now recognize:

- Connection refused
- Permission denied
- No route to host
- Host key verification failed
- Connection timed out
- Broken pipe

Most important debugging command:

```bash
ssh -vvv user@server
```

---

## Lesson 13 — Security

Golden rules:

✅ Never share private keys

✅ Use SSH keys

✅ Use `sudo`

✅ Don't login as root

✅ Verify host keys

---

## Lesson 14 — Mini Project

You learned to:

Generate keys

```bash
ssh-keygen -t ed25519
```

Check permissions

```bash
chmod 600 ~/.ssh/id_ed25519
```

View public key

```bash
cat ~/.ssh/id_ed25519.pub
```

---

# Commands You Should Know

## Basic

```bash
ssh user@server
```

```bash
ssh -p 2222 user@server
```

```bash
exit
```

---

## Debugging

```bash
ssh -v user@server
```

```bash
ssh -vv
```

```bash
ssh -vvv
```

---

## Key Generation

```bash
ssh-keygen
```

---

## Information

```bash
ssh -V
```

```bash
hostname
```

```bash
hostname -I
```

---

## Permissions

```bash
chmod 700 ~/.ssh
```

```bash
chmod 600 ~/.ssh/id_ed25519
```

```bash
chmod 644 ~/.ssh/id_ed25519.pub
```

---

# Complete SSH Flow

```
Laptop
   │
Type ssh user@server
   │
   ▼
DNS Lookup
   │
   ▼
IP Address
   │
   ▼
Port 22
   │
   ▼
SSH Server
   │
   ▼
Host Verification
   │
   ▼
Encryption
   │
   ▼
Authentication
   │
   ▼
Remote Shell
```

---

# Final Quiz (15 Questions)

Try answering these without looking back.

### 1. What does SSH stand for?

✅ Secure Shell

---

### 2. Which program starts the connection?

A. Client

B. Server

✅ A

---

### 3. Which daemon accepts SSH connections?

✅ `sshd`

---

### 4. Default SSH port?

✅ `22`

---

### 5. Which file should never be shared?

✅ `id_ed25519`

---

### 6. Which file is safe to share?

✅ `id_ed25519.pub`

---

### 7. Where are trusted server fingerprints stored?

✅ `~/.ssh/known_hosts`

---

### 8. Which command creates SSH keys?

✅

```bash
ssh-keygen
```

---

### 9. Which option enables maximum debugging?

✅

```bash
-vvv
```

---

### 10. Which command exits SSH?

✅

```bash
exit
```

---

### 11. What does DNS do?

✅ Converts hostnames into IP addresses.

---

### 12. Which encryption is faster?

A. Symmetric

B. Asymmetric

✅ A

---

### 13. Which authentication method do companies prefer?

✅ SSH Keys

---

### 14. Which command shows your SSH version?

✅

```bash
ssh -V
```

---

### 15. What should you check first when SSH fails?

✅ Run:

```bash
ssh -vvv user@server
```

and identify whether the issue is:

- Network
- Hostname
- Port
- Authentication
- Host verification

---

# Readiness Checklist

Can you confidently answer **yes** to these?

- ✅ I know what SSH is.
- ✅ I know the difference between client and server.
- ✅ I know how SSH creates a secure connection.
- ✅ I understand password and key authentication.
- ✅ I know why SSH keys are preferred.
- ✅ I know how to generate an SSH key.
- ✅ I understand `known_hosts`.
- ✅ I know common SSH errors.
- ✅ I know basic SSH security practices.
- ✅ I know the commands needed to start using SSH.

If you answered **yes** to most of these, you're ready for Module 2.

---

# What's Coming in Module 2

Module 2 is where SSH becomes practical. You'll start using it in realistic scenarios.

### Lesson Plan

1. Connecting to Localhost
2. Installing and Configuring an SSH Server
3. Understanding `known_hosts`
4. Accepting and Removing Host Keys
5. Connecting to a Remote VPS
6. Running Commands Remotely
7. Logging Out Cleanly
8. SSH Session Options
9. Connection Timeouts
10. Keep-Alive Settings
11. Useful SSH Options
12. SSH Command Shortcuts
13. Real Developer Workflows
14. Hands-on Lab
15. Module Review

---

## A Note for You

Since you've already learned:

- Linux terminal
- Git
- Docker
- Shell scripting
- Neovim
- CLI tools

SSH is the skill that ties all of them together. You'll use it whenever you deploy a MERN application, troubleshoot a Linux server, or manage cloud infrastructure.

When you're ready, just say:

> **"SSH Module 2"**

and we'll start connecting to real systems and using SSH the way backend developers do every day.