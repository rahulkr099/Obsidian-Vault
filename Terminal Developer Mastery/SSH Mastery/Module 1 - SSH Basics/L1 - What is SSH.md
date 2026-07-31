# Lesson 1 — What is SSH?

## Imagine this situation

You have two computers:

- Your laptop (Linux Mint)
- A cloud server running Ubuntu

The server is in another city or even another country.

You want to:

- open the terminal
- edit files
- run Node.js
- restart your backend
- check logs

How do you control that remote computer?

**Answer: SSH.**

---

# What does SSH stand for?

**SSH = Secure Shell**

It lets you safely control another computer over a network.

Think of it as opening a terminal on another machine while sitting at your own computer.

Example:

```
Your Laptop  -------------------->  Remote Linux Server
        SSH Connection
```

Once connected, every command you type runs on the **remote** computer, not on your laptop.

---

# Why not just use the internet directly?

Imagine logging into your bank.

Would you want your password to travel across the internet as plain text?

Of course not.

SSH encrypts everything:

- your password
- your commands
- the server's responses
- transferred files

Even if someone intercepts the traffic, they shouldn't be able to read it.

---

# What can SSH do?

SSH is much more than remote login.

You can:

- Manage remote Linux servers
- Deploy websites
- Run Docker containers
- Restart services
- Copy files securely
- Tunnel network traffic
- Use GitHub with SSH keys

---

# A real backend developer's day

Suppose you've deployed your MERN backend to a VPS.

You receive a message:

> "The API is down."

Instead of driving to the server (which could be thousands of kilometers away), you simply run:

```
ssh rahul@203.0.113.10
```

Now you're working directly on that server.

You can:

```
pm2restart backend
```

or

```
dockerps
```

or

```
journalctl-u backend.service
```

All without leaving your desk.

---

# SSH vs Terminal

Many beginners think SSH and Terminal are the same.

They're different.

**Terminal**

A program where you type commands.

Examples:

- Kitty
- GNOME Terminal
- Windows Terminal

**SSH**

A program that connects your terminal to another computer securely.

Think of it like this:

```
Keyboard
    ↓
Terminal
    ↓
SSH
    ↓
Remote Linux Server
```

---

# Is SSH only for Linux?

No.

SSH clients exist for:

- Linux ✅
- macOS ✅
- Windows ✅

Most servers you'll connect to are Linux servers.

---

# When will you use SSH?

As a backend developer, you'll use it for:

- Deploying Node.js applications
- Connecting to cloud servers
- Managing Docker containers
- Viewing application logs
- Running database backups
- Fixing production issues
- Configuring Nginx or Apache
- Updating software
- Using Git over SSH

---

# Key takeaways

- SSH stands for **Secure Shell**.
- It lets you securely control another computer from your terminal.
- All communication is encrypted.
- It's one of the most important tools for backend developers, DevOps engineers, and system administrators.

---

# Mini Challenge

Answer these three questions without looking back:

1. What does SSH stand for?
2. Why is SSH considered secure?
3. Name three tasks you can perform using SSH.

Reply with your answers, or simply say **"Lesson 2"** when you're ready to continue.