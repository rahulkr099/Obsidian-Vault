# SSH Mastery — Module 1, Lesson 8

# Installing SSH Tools

In the previous lessons, we learned the concepts behind SSH.

Now let's see what is **actually installed on your Linux Mint system**.

Good news: **you probably already have the SSH client installed.**

---

# SSH Tools You'll Use

The OpenSSH package provides several commands.

|Command|Purpose|
|---|---|
|`ssh`|Connect to a remote server|
|`sshd`|SSH server (accepts connections)|
|`scp`|Copy files securely|
|`sftp`|Secure file transfer|
|`ssh-keygen`|Generate SSH keys|
|`ssh-agent`|Store SSH keys in memory|
|`ssh-add`|Add keys to the SSH agent|

Don't worry if some of these aren't installed yet. We'll verify them.

---

# Step 1 — Check the SSH Client

Run:

```bash
ssh -V
```

Example output:

```
OpenSSH_9.9p2 Ubuntu-2ubuntu0.1, OpenSSL 3.3.2
```

> **Note:** Your version number may be different, and that's perfectly normal.

If you see a version, your SSH client is installed.

---

# Step 2 — Find the SSH Client

Run:

```bash
which ssh
```

Example:

```
/usr/bin/ssh
```

This tells you where the `ssh` program is located.

You can also use:

```bash
command -v ssh
```

This is a more portable command that works in most shells.

---

# Step 3 — Check Other SSH Tools

Let's see what else is available.

```bash
which ssh-keygen
```

```bash
which scp
```

```bash
which sftp
```

Example:

```
/usr/bin/ssh-keygen
/usr/bin/scp
/usr/bin/sftp
```

---

# Step 4 — Check the SSH Server

The SSH server is different from the SSH client.

Check whether the service exists:

```bash
systemctl status ssh
```

or

```bash
systemctl status sshd
```

Possible outcomes:

### Running

```
Active: active (running)
```

Great! Your computer can accept SSH connections.

---

### Installed but Stopped

```
Active: inactive (dead)
```

The server is installed but not currently running.

---

### Not Installed

```
Unit ssh.service could not be found.
```

This means your machine has no SSH server yet.

That's completely fine for most desktop users.

---

# Step 5 — Install the SSH Client (If Needed)

Most Linux Mint installations already include it.

If not:

```bash
sudo apt update
sudo apt install openssh-client
```

---

# Step 6 — Install the SSH Server

If you want **other computers to SSH into your Linux Mint machine**, install the server:

```bash
sudo apt update
sudo apt install openssh-server
```

---

# Step 7 — Start the SSH Server

Start it:

```bash
sudo systemctl start ssh
```

Enable it at boot:

```bash
sudo systemctl enable ssh
```

Check its status:

```bash
systemctl status ssh
```

---

# Step 8 — Verify That SSH Is Listening

Run:

```bash
ss -tln
```

Example output:

```
LISTEN 0 128 0.0.0.0:22
```

This means SSH is listening on **port 22**.

You can also filter the output:

```bash
ss -tln | grep :22
```

---

# Step 9 — Test Local SSH

If the server is running:

```bash
ssh localhost
```

or

```bash
ssh 127.0.0.1
```

You'll be connecting **to your own computer**.

This is a great way to practice without needing another machine.

---

# Understanding the Packages

Think of it like this:

```
OpenSSH
│
├── SSH Client
│     ├── ssh
│     ├── scp
│     ├── sftp
│     └── ssh-keygen
│
└── SSH Server
      └── sshd
```

The client and server are separate components.

---

# Which Do You Need?

### If you only want to connect to servers:

✅ SSH Client only

---

### If you want other computers to connect to your Linux Mint PC:

✅ SSH Server

---

### As a Backend Developer

You'll almost always need:

- SSH Client ✅

You'll occasionally need:

- SSH Server (for testing or learning)

---

# Common Mistakes

### Mistake 1

Trying to connect to another server before confirming the SSH client is installed.

Check first:

```bash
ssh -V
```

---

### Mistake 2

Installing the server when you only need the client.

Remember:

- **Client** → Connect **to** other machines.
- **Server** → Accept connections **from** other machines.

---

### Mistake 3

Forgetting to start the SSH server after installing it.

Install:

```bash
sudo apt install openssh-server
```

Start:

```bash
sudo systemctl start ssh
```

Enable at boot:

```bash
sudo systemctl enable ssh
```

---

# Real Backend Example

Imagine you've rented an Ubuntu VPS.

From your Linux Mint laptop:

```bash
ssh rahul@203.0.113.10
```

You only need the **SSH client**.

The VPS already has the **SSH server** running, ready to accept your connection.

---

# Key Takeaways

- The `ssh` command is the SSH **client**.
- `sshd` is the SSH **server**.
- Most Linux Mint installations already include the SSH client.
- Install `openssh-server` only if you want your computer to accept SSH connections.
- You can test your setup using `ssh localhost`.

---

# Mini Challenge

### Question 1

Which package lets your computer **accept** SSH connections?

A. `openssh-client`

B. `openssh-server`

✅ **Answer:** **B**

---

### Question 2

Which command generates SSH keys?

A. `ssh-keygen`

B. `ssh-add`

C. `scp`

✅ **Answer:** **A**

---

### Question 3

What does this command do?

```bash
ssh localhost
```

A. Connects to your own computer via SSH

B. Downloads SSH

C. Restarts the SSH server

✅ **Answer:** **A**

---

# Practice on Your Linux Mint

Run these commands one by one:

```bash
ssh -V
```

```bash
command -v ssh
```

```bash
command -v ssh-keygen
```

```bash
command -v scp
```

```bash
command -v sftp
```

```bash
systemctl status ssh
```

If the SSH server is installed and running:

```bash
ssh localhost
```

If you get a prompt asking about the host's authenticity or for your password, that's expected. If you get "Connection refused," it simply means the SSH server isn't running yet.

---

## Looking Ahead

From **Lesson 9 onward**, we'll stop just learning about SSH and start **using it**. You'll learn how to inspect your SSH client configuration, understand default behavior, and prepare for making your first real SSH connection.

When you're ready, say **"Lesson 9"**.