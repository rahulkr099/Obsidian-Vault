# SSH Mastery — Module 1, Lesson 12

# Common SSH Errors and How to Fix Them

Every developer sees SSH errors.

The difference between a beginner and an experienced developer is **not that experienced developers never get errors—they know how to diagnose them quickly.**

In this lesson, you'll learn the most common SSH errors and exactly what they mean.

---

# Debugging Rule #1 ⭐

Whenever SSH fails, don't guess.

Run:

```bash
ssh -v user@server
```

If needed:

```bash
ssh -vv user@server
```

or

```bash
ssh -vvv user@server
```

Verbose mode often tells you exactly where the connection is failing.

---

# Error 1 — Connection Refused

Example:

```
ssh: connect to host 203.0.113.10 port 22:
Connection refused
```

## What It Means

Your computer **reached the server**, but **nothing is listening on that port**.

Think of it like calling someone's phone number.

The phone exists.

But it's switched off.

---

## Common Causes

- SSH server isn't running
- Wrong port
- SSH server isn't installed
- Firewall blocking the service

---

## How to Fix

On the server:

Check SSH service:

```bash
sudo systemctl status ssh
```

Start it:

```bash
sudo systemctl start ssh
```

If using another port:

```bash
ssh -p 2222 user@server
```

---

# Error 2 — Permission Denied

Example:

```
Permission denied (publickey,password).
```

or

```
Permission denied, please try again.
```

---

## What It Means

The server rejected your authentication.

---

## Possible Causes

Wrong username

Example:

```bash
ssh rahul@server
```

But the real username is:

```
ubuntu
```

---

Wrong password

Wrong SSH key

Public key missing on the server

Private key has incorrect permissions

---

## Fix

Double-check:

- Username
- Password
- SSH key

Use verbose mode:

```bash
ssh -v user@server
```

It often shows which authentication methods were attempted.

---

# Error 3 — Host Key Verification Failed

Example:

```
Host key verification failed.
```

or

```
WARNING:
REMOTE HOST IDENTIFICATION HAS CHANGED!
```

---

## What It Means

SSH remembers the server's fingerprint.

The fingerprint has changed.

---

## Possible Reasons

✅ Server reinstalled

✅ SSH keys regenerated

❌ Someone may be impersonating the server

---

## Fix

Only if you're sure the change is expected:

Remove the old entry:

```bash
ssh-keygen -R server
```

or

```bash
ssh-keygen -R 203.0.113.10
```

Then reconnect.

SSH will ask you to trust the new fingerprint.

---

# Error 4 — No Route to Host

Example:

```
No route to host
```

---

## What It Means

Your computer cannot reach the server at all.

It's like trying to drive to a city where the road is closed.

---

## Causes

- Wrong IP
- Server offline
- Network outage
- Firewall
- VPN issues

---

## Check

Try:

```bash
ping server
```

or

```bash
ping 203.0.113.10
```

If the server doesn't respond, it may be unreachable.

> **Note:** Some servers intentionally block `ping`, so a failed ping doesn't always mean the server is down.

---

# Error 5 — Could Not Resolve Hostname

Example:

```
ssh: Could not resolve hostname myservr.com
```

---

## What It Means

DNS couldn't find the hostname.

---

## Causes

Misspelled hostname

Example:

```
github.con
```

instead of

```
github.com
```

---

DNS problem

Internet disconnected

---

## Fix

Check spelling.

Try:

```bash
ping hostname
```

or

```bash
getent hosts hostname
```

---

# Error 6 — Connection Timed Out

Example:

```
Connection timed out
```

---

## Meaning

SSH waited.

Nobody answered.

---

## Causes

- Firewall
- Wrong IP
- Server offline
- Wrong port

---

## Difference

|Error|Meaning|
|---|---|
|Connection Refused|Server reached, service unavailable|
|Connection Timed Out|No response received|

---

# Error 7 — Broken Pipe

Example:

```
client_loop:
send disconnect:
Broken pipe
```

---

## Meaning

The SSH connection was dropped.

---

## Causes

- Internet disconnected
- Wi-Fi changed
- Server rebooted
- Idle timeout

---

## Fix

Reconnect.

For long-running sessions, tools like **tmux** help because your work continues even if SSH disconnects.

---

# Error 8 — Too Many Authentication Failures

Example:

```
Received disconnect:
Too many authentication failures
```

---

## Meaning

Your SSH client tried many keys.

The server gave up.

---

## Fix

Specify the correct key:

```bash
ssh -i ~/.ssh/id_ed25519 user@server
```

Later, you'll learn how to manage this cleanly with `~/.ssh/config`.

---

# Error 9 — Bad Permissions

Example:

```
Permissions 0644 for 'id_ed25519'
are too open.
```

---

## Meaning

Your private key can be read by other users.

SSH refuses to use it.

---

## Fix

```bash
chmod 600 ~/.ssh/id_ed25519
```

Also ensure:

```bash
chmod 700 ~/.ssh
```

---

# The SSH Troubleshooting Flow ⭐

When SSH fails, follow this order:

```
SSH Failed
     │
     ▼
1. Internet working?
     │
     ▼
2. Hostname/IP correct?
     │
     ▼
3. Correct port?
     │
     ▼
4. SSH server running?
     │
     ▼
5. Username correct?
     │
     ▼
6. Authentication working?
     │
     ▼
7. Run ssh -vvv
```

Following this sequence saves time and avoids random guessing.

---

# Real Backend Example

Suppose you deploy your API to a VPS.

You try:

```bash
ssh ubuntu@203.0.113.10
```

You get:

```
Connection refused
```

Your thought process should be:

✅ Is the IP correct?

↓

✅ Is SSH listening on port 22?

↓

✅ Is the SSH service running?

↓

✅ Is a firewall blocking the port?

Instead of randomly reinstalling software, you narrow down the cause.

---

# Most Useful Debugging Commands

Check SSH version:

```bash
ssh -V
```

Verbose mode:

```bash
ssh -vvv user@server
```

Check hostname:

```bash
hostname
```

Check local IP:

```bash
hostname -I
```

See listening ports:

```bash
ss -tln
```

Check SSH service:

```bash
systemctl status ssh
```

---

# Key Takeaways

- Read the full error message carefully—SSH errors are usually descriptive.
- Start troubleshooting with `ssh -v`, `vv`, or `vvv`.
- Identify **where** the failure occurs: network, hostname, port, service, or authentication.
- Fix one issue at a time instead of changing multiple things at once.

---

# Cheat Sheet

|Error|Most Likely Cause|First Thing to Check|
|---|---|---|
|Connection refused|SSH service not listening|`systemctl status ssh`|
|Permission denied|Authentication failed|Username, password, SSH key|
|Host key verification failed|Stored fingerprint mismatch|`ssh-keygen -R host`|
|Could not resolve hostname|DNS or typo|Check hostname spelling|
|No route to host|Network issue|IP address and connectivity|
|Connection timed out|Firewall or unreachable server|Port and firewall|
|Broken pipe|Connection dropped|Network stability|
|Bad permissions|Private key permissions|`chmod 600 ~/.ssh/id_ed25519`|

---

# Mini Challenge

## Question 1

You run:

```bash
ssh user@server
```

and get:

```
Connection refused
```

What should you check first?

A. Whether the SSH server is running.

B. Whether your password is correct.

C. Whether Git is installed.

✅ **Answer:** **A**

---

## Question 2

Which command gives the most detailed SSH debugging output?

A.

```bash
ssh -v user@server
```

B.

```bash
ssh -vvv user@server
```

C.

```bash
ssh --debug user@server
```

✅ **Answer:** **B**

---

## Question 3

Your private key has permissions that are too open. Which command fixes it?

```bash
chmod 600 ~/.ssh/id_ed25519
```

✅ **Correct!**

---

## Practice Exercise

On your Linux Mint machine, try:

```bash
ssh -vvv localhost
```

If your SSH server isn't running, read the verbose output and identify **at which stage** the connection fails (DNS, port connection, authentication, etc.). This is excellent practice for learning how to interpret SSH debug messages.

---

## Looking Ahead

In **Lesson 13**, you'll learn **Basic SSH Security**, including:

- Why you should avoid logging in as `root`
- Keeping your private key safe
- Using strong passphrases
- File permissions in `~/.ssh`
- Best security habits for developers

These are the habits that help keep your servers and accounts secure from day one.