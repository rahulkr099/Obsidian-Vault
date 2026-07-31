# SSH Mastery — Module 2

# Using SSH in the Real World

Welcome to **Module 2**.

Module 1 taught you **what SSH is**.

Module 2 is about **actually using SSH**.

By the end of this module, you'll be comfortable connecting to Linux machines, running commands remotely, transferring files, and working like a backend developer.

---

# Module 2 Roadmap

## Lesson 1 — Connecting to Localhost

Practice SSH safely on your own computer.

**You'll learn:**

- What `localhost` means
- `127.0.0.1` vs `localhost`
- Testing your SSH client
- First local SSH session
- Why developers practice locally first

**Practice:**

```bash
ssh localhost
```

---

## Lesson 2 — Installing and Configuring an SSH Server

**You'll learn:**

- Install `openssh-server`
- Start and stop the SSH service
- Enable it on boot
- Verify it's listening
- Check logs

**Commands:**

```bash
sudo apt install openssh-server
sudo systemctl enable ssh
sudo systemctl start ssh
```

---

## Lesson 3 — Understanding `known_hosts`

You'll learn:

- What `known_hosts` is
- Why SSH remembers servers
- Host fingerprints
- Preventing man-in-the-middle attacks
- Viewing and editing `known_hosts`

---

## Lesson 4 — Managing Host Keys

Topics:

- First connection
- Accepting fingerprints
- Removing old fingerprints
- When host keys legitimately change
- Common warnings

Commands:

```bash
ssh-keygen -R hostname
```

---

## Lesson 5 — Connecting to a Remote VPS

You'll learn how developers connect to cloud servers.

Examples:

```bash
ssh ubuntu@203.0.113.10
```

Topics:

- VPS providers
- Public IP
- Authentication
- First login

---

## Lesson 6 — Running Remote Commands

Instead of opening a shell:

```bash
ssh server uptime
```

or

```bash
ssh server hostname
```

You'll automate small tasks from your local machine.

---

## Lesson 7 — Logging Out & Session Management

Topics:

- `exit`
- `logout`
- `Ctrl + D`
- What happens when a session ends
- Avoiding accidental disconnects

---

## Lesson 8 — Useful SSH Options

You'll master options like:

```bash
-p
-l
-v
-C
-i
```

These appear in real documentation and production environments.

---

## Lesson 9 — Timeouts & Keep-Alives

Learn why SSH disconnects unexpectedly and how to reduce idle disconnects.

Topics:

- ServerAliveInterval
- ClientAliveInterval
- ConnectionTimeout
- Long-running sessions

---

## Lesson 10 — SSH Configuration File

Introduction to:

```
~/.ssh/config
```

You'll create shortcuts like:

```bash
ssh myserver
```

instead of:

```bash
ssh -p 2222 ubuntu@203.0.113.10
```

---

## Lesson 11 — Useful Developer Workflows

Real examples:

```bash
ssh production

git pull

npm install

pm2 restart backend

exit
```

Also:

- Checking logs
- Monitoring memory
- Restarting services

---

## Lesson 12 — SSH and Docker

Manage Docker remotely:

```bash
ssh server docker ps
```

Run:

```bash
docker logs
docker exec
docker restart
```

without leaving your laptop.

---

## Lesson 13 — Troubleshooting Real Servers

Practice diagnosing:

- SSH won't connect
- Wrong key
- Firewall issues
- Wrong user
- DNS problems
- Permission denied

You'll follow a structured debugging workflow.

---

## Lesson 14 — Mini Project

You'll:

- Connect to localhost
- Configure SSH
- Run remote commands
- Practice key authentication
- Build confidence before using a VPS

---

## Lesson 15 — Module Review

You'll complete:

- Practical exercises
- Command recap
- Troubleshooting quiz
- Readiness checklist for Module 3

---

# Skills You'll Gain

By the end of Module 2, you'll be able to:

- ✅ Connect to Linux servers confidently
- ✅ Run commands remotely
- ✅ Understand SSH fingerprints
- ✅ Troubleshoot common connection issues
- ✅ Configure SSH for daily use
- ✅ Use SSH in real backend workflows

---

# Prerequisites Check

Before starting Lesson 1, make sure your Linux Mint system has:

```bash
ssh -V
```

and, if you want to SSH into your own machine for practice:

```bash
systemctl status ssh
```

If the SSH server isn't installed yet, don't worry—Lesson 2 will walk you through it step by step.

---

# Ready for Lesson 1

In **Lesson 1: Connecting to Localhost**, you'll learn:

- Why `localhost` is the safest place to practice SSH.
- The difference between `localhost`, `127.0.0.1`, and your computer's hostname.
- How to open your first real SSH session to your own machine.
- How backend developers use localhost to test SSH configurations before touching production servers.

This is the point where your SSH knowledge starts becoming practical.

Just say **"Lesson 1"** when you're ready.