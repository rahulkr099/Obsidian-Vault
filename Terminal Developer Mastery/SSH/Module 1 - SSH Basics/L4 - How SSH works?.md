# SSH Mastery — Module 1, Lesson 4

# How SSH Works (Behind the Scenes)

Now we'll answer a question that many beginners have:

> **What actually happens after I press Enter?**

For example:

```bash
ssh rahul@192.168.1.100
```

It may look like one simple command, but several important steps happen in just a fraction of a second.

---

# The Complete Journey

```
┌─────────────┐
│ You press   │
│ Enter       │
└──────┬──────┘
       │
       ▼
Find the server
       │
       ▼
Connect to port 22
       │
       ▼
Verify the server
       │
       ▼
Encrypt the connection
       │
       ▼
Authenticate yourself
       │
       ▼
Open a remote shell
```

Let's look at each step.

---

# Step 1 — Find the Server

You type:

```bash
ssh rahul@192.168.1.100
```

SSH extracts:

- Username: `rahul`
- Server IP: `192.168.1.100`

If you use a hostname instead:

```bash
ssh rahul@example.com
```

SSH first converts the hostname into an IP address using **DNS (Domain Name System)**.

Think of DNS as the internet's phonebook.

```
example.com
      │
      ▼
192.168.1.100
```

---

# Step 2 — Connect to Port 22

Every network service listens on a **port**.

SSH uses:

```
Port 22
```

Imagine an apartment building.

```
Apartment Building
│
├── Door 22 → SSH
├── Door 80 → HTTP
├── Door 443 → HTTPS
```

SSH knocks on **door 22**.

If the SSH server is listening there, it answers.

---

# Step 3 — The Server Introduces Itself

The SSH server says something like:

> "Hello, I'm the server."

But how do you know it's really your server?

The server sends its **host key**.

Think of it like a digital fingerprint.

When you connect for the first time, you'll often see:

```
The authenticity of host '192.168.1.100' can't be established.
ED25519 key fingerprint is:
SHA256:xxxxxxxxxxxxxxxx

Are you sure you want to continue connecting (yes/no)?
```

If you type:

```
yes
```

SSH saves the server's fingerprint.

Later, if the fingerprint changes unexpectedly, SSH warns you because it could indicate:

- the server was reinstalled,
- the SSH configuration changed, or
- someone is attempting a **man-in-the-middle attack**.

---

# Step 4 — Create an Encrypted Tunnel

Now both computers agree on encryption.

From this point onward:

- Your commands are encrypted.
- Passwords are encrypted.
- Server responses are encrypted.

Think of it like sending messages through a locked tunnel.

```
Laptop
   │
Encrypted Tunnel
   │
Server
```

Anyone watching the network can see that data is flowing, but they can't read its contents.

---

# Step 5 — Authentication

The server now asks:

> "Who are you?"

There are two common ways to prove your identity.

## Method 1 — Password

```
Username: rahul
Password: ********
```

If the password is correct:

✅ Login succeeds.

---

## Method 2 — SSH Key (Preferred)

Instead of typing a password every time, your computer proves it owns a matching private key.

This is:

- faster,
- more secure,
- and the standard approach in professional environments.

We'll learn SSH keys in depth in a later module.

---

# Step 6 — The Server Starts Your Shell

After successful authentication, the server starts your default shell, such as:

```
bash
```

or

```
zsh
```

Now every command runs **on the remote server**, not on your laptop.

For example:

```bash
pwd
```

Output:

```
/home/rahul
```

This path belongs to the **remote** machine.

---

# A Visual Overview

```
Laptop                         Remote Server
------------------------------------------------------
ssh command
      │
      │──────────────► Find server
      │──────────────► Connect to port 22
      │◄────────────── Receive host key
      │──────────────► Trust the server
      │◄────────────── Create encrypted session
      │──────────────► Authenticate
      │◄────────────── Login successful
      │
Remote shell opens
```

---

# What If Something Goes Wrong?

### Server is Offline

```
ssh: connect to host ... Connection refused
```

or

```
No route to host
```

---

### Wrong Password

```
Permission denied
```

---

### Wrong Username

```
Permission denied
```

---

### SSH Server Not Running

```
Connection refused
```

We'll learn how to diagnose these errors in a later lesson.

---

# What Happens After Login?

Suppose you run:

```bash
ls
```

Here's the flow:

```
Laptop
    │
Type: ls
    │
Encrypted
    │
Server
Runs: ls
    │
Encrypted Output
    │
Laptop
Displays result
```

The command is executed on the server, and only the output comes back to your terminal.

---

# Key Takeaways

- SSH first finds the server (using an IP or DNS).
- It connects to **port 22** by default.
- The server proves its identity with a **host key**.
- An encrypted connection is established.
- You authenticate with a password or, preferably, an SSH key.
- A remote shell starts, allowing you to work on the remote machine.

---

# Mini Challenge

Suppose you type:

```bash
ssh rahul@example.com
```

Put these steps in the correct order:

1. Authenticate the user
2. Connect to port 22
3. Open a remote shell
4. Verify the server's identity
5. Create an encrypted connection
6. Find the server (DNS/IP)

**Answer:**

```
6 → 2 → 4 → 5 → 1 → 3
```

---

## Practice (No Remote Server Needed)

Run these commands on your Linux Mint machine:

```bash
ssh -V
```

This shows your SSH client version.

Then try:

```bash
ssh localhost
```

If an SSH server is running on your own computer, you'll connect to yourself. If it isn't, you'll likely see:

```
ssh: connect to host localhost port 22: Connection refused
```

That's perfectly fine—it simply means no SSH server is listening yet.

When you're ready, say **"Lesson 5"** to learn **How SSH Encryption Works (without heavy cryptography)**, where you'll understand why SSH is trusted for securely managing servers over the internet.