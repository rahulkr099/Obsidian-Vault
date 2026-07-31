# SSH Mastery — Module 1, Lesson 14

# Mini Project — Your First SSH Setup

This is your first hands-on SSH project.

By the end of this lesson, you'll have:

- ✅ Explored your SSH directory
- ✅ Generated your first SSH key pair
- ✅ Understood every file
- ✅ Tested your setup
- ✅ Prepared for GitHub and remote servers

> **Don't worry if you don't have a VPS yet.** Everything here can be done on your Linux Mint laptop.

---

# Project Goal

We'll build this structure:

```
~/.ssh/
├── id_ed25519
├── id_ed25519.pub
├── known_hosts
└── config   (optional for now)
```

---

# Step 1 — Check Your SSH Directory

Run:

```bash
ls -la ~/.ssh
```

Possible output:

```
total 16
drwx------ 2 rahul rahul 4096 Jul 29 17:10 .
drwxr-x--- 8 rahul rahul 4096 Jul 29 17:08 ..
```

If the directory doesn't exist:

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

---

# Step 2 — Check if You Already Have SSH Keys

Run:

```bash
ls ~/.ssh
```

If you see:

```
id_ed25519
id_ed25519.pub
```

You already have a key pair.

If not, continue to Step 3.

---

# Step 3 — Generate Your First SSH Key

Run:

```bash
ssh-keygen -t ed25519 -C "rahul@example.com"
```

### What does this mean?

|Option|Meaning|
|---|---|
|`-t ed25519`|Create an Ed25519 key pair (recommended today)|
|`-C`|Add a comment to identify the key|

> The comment can be your email, your GitHub email, or a label like `"Rahul Linux Mint"`.

---

# Step 4 — Follow the Prompts

You'll see:

```
Generating public/private ed25519 key pair.
Enter file in which to save the key:
```

Press:

```
Enter
```

to accept:

```
~/.ssh/id_ed25519
```

---

Next:

```
Enter passphrase (empty for no passphrase):
```

### Recommendation

For learning:

You can leave it empty if you want to keep things simple.

For real-world use:

Use a **strong passphrase**.

Example:

```
Coffee&Code2026!
```

You won't see any characters while typing. That's normal.

---

# Step 5 — See What Was Created

Run:

```bash
ls -l ~/.ssh
```

Example:

```
id_ed25519
id_ed25519.pub
```

---

# Step 6 — Understand Each File

## Private Key

```
id_ed25519
```

- Secret
- Never share it
- Used to prove your identity

---

## Public Key

```
id_ed25519.pub
```

- Safe to share
- Upload to GitHub
- Copy to servers
- Used by the server to recognize you

---

# Step 7 — View Your Public Key

Run:

```bash
cat ~/.ssh/id_ed25519.pub
```

Example:

```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAI...
rahul@example.com
```

Sharing this public key is safe.

---

# Step 8 — Never View Your Private Key Publicly

Although you _can_ display it:

```bash
cat ~/.ssh/id_ed25519
```

**Don't make a habit of this**, and never paste the output into chat, email, GitHub, or screenshots.

Think of it as your house key.

---

# Step 9 — Verify File Permissions

Run:

```bash
ls -l ~/.ssh
```

Expected:

```
-rw------- id_ed25519
-rw-r--r-- id_ed25519.pub
```

Or check numerically:

```bash
stat -c "%a %n" ~/.ssh/*
```

Expected:

```
600 ~/.ssh/id_ed25519
644 ~/.ssh/id_ed25519.pub
```

---

# Step 10 — Fix Permissions (If Needed)

Private key:

```bash
chmod 600 ~/.ssh/id_ed25519
```

Public key:

```bash
chmod 644 ~/.ssh/id_ed25519.pub
```

Directory:

```bash
chmod 700 ~/.ssh
```

---

# Step 11 — Get the Fingerprint

Every SSH key has a fingerprint.

Run:

```bash
ssh-keygen -lf ~/.ssh/id_ed25519.pub
```

Example:

```
256 SHA256:abc123... rahul@example.com (ED25519)
```

Think of this as your key's unique fingerprint.

---

# Step 12 — Test the SSH Client

Run:

```bash
ssh -V
```

You should see your OpenSSH version.

---

# Bonus — Learn About the SSH Agent

Check if an SSH agent is running:

```bash
ssh-add -l
```

You might see:

```
The agent has no identities.
```

That's okay.

We'll learn about the SSH agent in detail in **Module 3**.

---

# Final Project Structure

Your `.ssh` directory should now look something like this:

```
~/.ssh
├── id_ed25519
├── id_ed25519.pub
├── known_hosts   (may not exist yet)
└── config        (optional)
```

---

# Real Backend Workflow

When you deploy your backend in the future:

1. Generate your SSH key.
2. Copy the **public key** to the server.
3. Connect:

```bash
ssh ubuntu@203.0.113.10
```

1. Deploy your application:

```bash
git pull
npm install
pm2 restart backend
```

This is a common workflow used by backend developers.

---

# Project Checklist

Mark each item when you complete it:

- ☐ Created `~/.ssh` (if needed)
- ☐ Generated an Ed25519 key pair
- ☐ Understood the difference between private and public keys
- ☐ Verified file permissions
- ☐ Viewed your public key
- ☐ Generated your key fingerprint
- ☐ Confirmed the SSH client is installed

---

# Mini Challenge

## Question 1

Which command generates a modern SSH key?

```bash
ssh-keygen -t ed25519
```

✅ Correct.

---

## Question 2

Which file is safe to upload to GitHub or copy to a server?

A.

```
id_ed25519
```

B.

```
id_ed25519.pub
```

✅ **Answer:** **B**

---

## Question 3

What permissions should a private key normally have?

A. `777`

B. `644`

C. `600`

✅ **Answer:** **C**

---

# Practical Assignment ⭐

Complete these commands on your Linux Mint machine:

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh

ssh-keygen -t ed25519 -C "your-email@example.com"

ls -l ~/.ssh

cat ~/.ssh/id_ed25519.pub

ssh-keygen -lf ~/.ssh/id_ed25519.pub

ssh -V
```

If you've already generated a key before, **don't overwrite it unless you're sure you no longer need it**. You can always create an additional key with a different filename using:

```bash
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519_github -C "your-email@example.com"
```

This is a common practice for separating personal, work, and GitHub keys.

---

# Looking Ahead

In **Lesson 15**, we'll review everything you've learned in Module 1 with:

- A complete concept recap
- A real-world SSH workflow
- A 15-question quiz
- A readiness checklist for **Module 2**, where you'll begin connecting to real SSH servers and working with host keys and `known_hosts` in more depth.

You're now very close to being ready for real SSH usage. 🚀