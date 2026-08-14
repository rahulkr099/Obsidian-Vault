# SSH Mastery — Module 1, Lesson 10

# Your First SSH Connection

Congratulations! 🎉

This is the lesson where you'll see what a **real SSH login** looks like.

Even if you don't have a remote server yet, you'll understand exactly what happens.

---

# The Basic Command

The simplest SSH command is:

```bash
ssh USER@HOST
```

Example:

```bash
ssh rahul@192.168.1.100
```

Here:

- `ssh` → Start the SSH client
- `rahul` → Remote username
- `192.168.1.100` → Remote server's IP address

---

# Real Examples

Using an IP address:

```bash
ssh rahul@203.0.113.10
```

Using a domain name:

```bash
ssh rahul@myserver.com
```

Using a custom port:

```bash
ssh -p 2222 rahul@myserver.com
```

---

# What Happens After You Press Enter?

```
You
 │
 ▼
Type SSH command
 │
 ▼
Connect to server
 │
 ▼
Verify server identity
 │
 ▼
Authenticate
 │
 ▼
Remote shell opens
```

Most of this happens in just a few seconds.

---

# The First-Time Connection

The first time you connect to a server, you may see:

```
The authenticity of host '203.0.113.10' can't be established.
ED25519 key fingerprint is:
SHA256:AbCdEfGhIjKlMnOpQrStUvWxYz1234567890

Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

This surprises many beginners.

It's **normal**.

---

# Why Does SSH Ask This?

SSH has never seen this server before.

It wants you to confirm:

> "Is this really the server you intended to connect to?"

If you trust the server, type:

```
yes
```

SSH then saves the server's fingerprint.

---

# Where Is It Saved?

In this file:

```
~/.ssh/known_hosts
```

You can inspect it:

```bash
cat ~/.ssh/known_hosts
```

You'll see lines that represent trusted servers.

---

# The Second Connection

The next time you connect:

```bash
ssh rahul@203.0.113.10
```

SSH compares the current server fingerprint with the one stored in `known_hosts`.

If they match:

✅ It connects without asking again.

---

# What If the Fingerprint Changes?

You may see a warning like:

```
WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!
```

This can happen if:

- The server was reinstalled.
- The SSH server was reconfigured.
- The server's SSH keys were regenerated.
- Someone is attempting a man-in-the-middle attack.

**Never ignore this warning.** Investigate why it changed before trusting the new key.

---

# Authentication Begins

After the server is trusted, SSH asks you to authenticate.

### Password Login

```
rahul@203.0.113.10's password:
```

Type your password.

> **Note:** Nothing appears on the screen while typing—not even `*`. This is normal.

Press **Enter** when you're done.

---

### SSH Key Login

If you've configured SSH keys, the login may happen automatically:

```
Welcome to Ubuntu 26.04 LTS
```

No password prompt is needed.

---

# Successful Login

You'll usually see a welcome message:

```
Welcome to Ubuntu 26.04 LTS

Last login: Wed Jul 29 16:30:11 IST 2026

rahul@server:~$
```

Notice the prompt:

```
rahul@server:~$
```

You're now working **on the remote server**.

---

# How Can You Tell You're Remote?

Run:

```bash
hostname
```

Example output:

```
web-server
```

If your laptop's hostname is `mint-laptop` but `hostname` returns `web-server`, you're definitely connected to the remote machine.

---

# Useful First Commands

Once connected, try these:

Show current directory:

```bash
pwd
```

List files:

```bash
ls
```

Show current user:

```bash
whoami
```

Show server name:

```bash
hostname
```

Check system uptime:

```bash
uptime
```

Check operating system:

```bash
cat /etc/os-release
```

These commands help you understand the environment you've logged into.

---

# Leaving the Remote Server

When you're finished:

```bash
exit
```

or press:

```
Ctrl + D
```

You'll return to your local terminal.

Example:

```
logout
Connection to 203.0.113.10 closed.
```

---

# Complete Connection Flow

```
Laptop
   │
   ▼
ssh rahul@server
   │
   ▼
Server identity check
   │
   ▼
Type "yes" (first connection only)
   │
   ▼
Authenticate
   │
   ▼
Remote shell
   │
   ▼
Run commands
   │
   ▼
exit
   │
   ▼
Back to local terminal
```

---

# Common Beginner Mistakes

### Mistake 1

Typing:

```
Yes
```

instead of:

```
yes
```

SSH expects the word **`yes`** in lowercase.

---

### Mistake 2

Thinking the keyboard is broken because no password characters appear.

This is expected behavior.

---

### Mistake 3

Forgetting to type `exit` after finishing.

Always close your SSH session when you're done.

---

### Mistake 4

Ignoring a host key warning.

If SSH reports that the server's identity has changed, verify the reason before proceeding.

---

# Practice (No Remote Server Needed)

You can still explore your SSH setup.

Check whether you already trust any hosts:

```bash
ls ~/.ssh
```

If `known_hosts` exists:

```bash
cat ~/.ssh/known_hosts
```

If you've never connected to an SSH server before, the file may not exist yet.

---

# Real Backend Example

Imagine you've deployed your Express backend to a VPS.

You connect:

```bash
ssh rahul@203.0.113.10
```

Then verify you're on the server:

```bash
hostname
whoami
pwd
```

Finally, restart your application:

```bash
pm2 restart backend
```

When finished:

```bash
exit
```

This is a common workflow for backend developers.

---

# Key Takeaways

- Use `ssh USER@HOST` to connect.
- The first connection asks you to verify the server's identity.
- Trusted server fingerprints are stored in `~/.ssh/known_hosts`.
- Your password won't be displayed while typing.
- Use `hostname`, `whoami`, and `pwd` to confirm where you are.
- End the session with `exit` or **Ctrl + D**.

---

# Mini Challenge

### Question 1

Where does SSH store trusted server fingerprints?

A. `~/.ssh/config`

B. `~/.ssh/known_hosts`

C. `~/.ssh/id_ed25519`

✅ **Answer:** **B**

---

### Question 2

How do you leave an SSH session?

A.

```bash
quit
```

B.

```bash
exit
```

C.

```bash
logout now
```

✅ **Answer:** **B**

---

### Question 3

Why doesn't your password appear while typing?

A. Your keyboard is broken.

B. SSH hides all password input for security.

C. SSH is frozen.

✅ **Answer:** **B**

---

## Practice Exercise

If you don't have a remote server yet, you can prepare your environment:

```bash
mkdir -p ~/.ssh
ls -la ~/.ssh
```

This creates the `.ssh` directory if it doesn't already exist and shows its contents.

### Looking Ahead

In **Lesson 11**, you'll learn about **hostnames, IP addresses, and ports**—how SSH finds the correct machine on a network and why port **22** is the default. Understanding these concepts will make troubleshooting SSH connections much easier.