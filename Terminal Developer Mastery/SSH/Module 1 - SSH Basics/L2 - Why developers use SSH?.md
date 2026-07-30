# SSH Mastery — Module 1, Lesson 2

# Why Developers Use SSH

Now that you know **what SSH is**, let's answer the next question:

> **Why do almost all backend developers use SSH every day?**

The short answer: **Because your code usually runs on another computer, not your own.**

---

# Imagine this workflow

You build a MERN application on your laptop.

```
Your Laptop
├── React Frontend
├── Express Backend
└── MongoDB (local)
```

Everything works perfectly.

But users around the world can't access your laptop.

So you deploy your app to a cloud server.

```
Your Laptop
      │
      │ SSH
      ▼
Cloud Server
├── Ubuntu
├── Node.js
├── Docker
└── Your Backend
```

Whenever something needs to change, you connect with SSH.

---

# Real-Life Examples

## Example 1 — Deploying Your App

You finish a new feature.

You SSH into your server:

```bash
ssh rahul@your-server-ip
```

Then:

```bash
git pull
npm install
npm run build
pm2 restart backend
```

Your new version is live.

---

## Example 2 — Fixing a Bug

A user reports:

> Login isn't working.

You connect:

```bash
ssh rahul@your-server-ip
```

Check logs:

```bash
pm2 logs
```

Find the error.

Fix it.

Restart the app.

Problem solved.

---

## Example 3 — Checking Server Health

Want to know if your server is overloaded?

```bash
top
```

or

```bash
htop
```

Need disk usage?

```bash
df -h
```

Need memory?

```bash
free -h
```

All of these commands are run after connecting through SSH.

---

## Example 4 — Managing Docker

Many backend apps run inside Docker.

SSH into the server:

```bash
docker ps
```

Restart a container:

```bash
docker restart my-api
```

Check logs:

```bash
docker logs my-api
```

---

## Example 5 — Updating Linux

```bash
sudo apt update
sudo apt upgrade
```

SSH lets you manage the operating system itself.

---

# Where You'll Use SSH in Your Career

### As a Student

- Raspberry Pi
- Virtual Machines
- College Linux servers

---

### During an Internship

- Development servers
- Testing servers
- Internal company machines

---

### As a Backend Developer

- AWS EC2
- DigitalOcean
- Hetzner
- Azure
- Google Cloud

---

### As a DevOps Engineer

- Hundreds of Linux servers
- Kubernetes nodes
- Build servers
- CI/CD systems

SSH is a core skill in all of these environments.

---

# SSH Isn't Just for Logging In

SSH can also:

### Copy files

```bash
scp report.pdf user@server:/home/user/
```

---

### Synchronize projects

```bash
rsync -av project/ user@server:/var/www/
```

---

### Run a single remote command

```bash
ssh user@server uptime
```

Output:

```
15:42:01 up 32 days, 3 users, load average: 0.25
```

Your computer sends the command, the server runs it, and returns the output.

---

### Use GitHub Securely

Instead of entering your username and password every time:

```bash
git push
```

Git can authenticate using your SSH key.

We'll learn this in a later module.

---

# Why Companies Prefer SSH

SSH provides:

- 🔒 Encrypted communication
- 🔑 Strong authentication with SSH keys
- 📜 Logging and auditing capabilities
- ⚡ Fast remote administration
- 🌍 Access from almost anywhere with network connectivity

That's why it's the standard way to manage Linux servers.

---

# Skills You'll Gain

By mastering SSH, you'll be able to:

- Deploy web applications
- Fix production issues
- Restart services
- Transfer files securely
- Manage Docker containers
- Configure servers
- Connect to GitHub without passwords
- Work on cloud infrastructure confidently

---

# Key Takeaways

- Your application usually runs on a **remote server**, not your laptop.
- SSH is the primary tool to securely manage that server.
- It's used for deployment, troubleshooting, maintenance, file transfer, and automation.
- Almost every backend and DevOps role expects you to know SSH.

---

# Mini Challenge

Think about your own MERN projects.

Suppose you deploy your backend to a Linux VPS. Which tasks would require SSH?

1. Restarting the backend server
2. Viewing application logs
3. Copying updated files to the server
4. All of the above

**4. All of the above.**

When you're ready, say **"Lesson 3"** to learn about **SSH Client vs SSH Server**, one of the most important concepts for understanding how SSH connections work.