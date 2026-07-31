# SSH Mastery — Module 1, Lesson 3

# SSH Client vs SSH Server

This lesson explains **who starts the connection** and **who receives it**. Once you understand this, SSH becomes much easier.

---

# Think of a Phone Call 📞

Imagine you call your friend.

- **You** dial the number.
- **Your friend** answers the call.

SSH works the same way.

```
Your Laptop ─────────────► Remote Server
     Client                  Server
```

- The **client** starts the connection.
- The **server** accepts the connection.

---

# What is an SSH Client?

An **SSH client** is the program you use to connect to another computer.

On Linux Mint, you already have one installed.

When you type:

```bash
ssh rahul@192.168.1.10
```

The `ssh` command is the **SSH client**.

Its job is to:

- Start the connection
- Encrypt communication
- Verify the server's identity
- Send your commands
- Display the server's output

---

# What is an SSH Server?

The **SSH server** is software running on the remote machine.

Its job is to:

- Listen for incoming SSH connections
- Check your username and authentication
- Verify your password or SSH key
- Allow or deny access
- Execute your commands

The SSH server program on most Linux systems is called **OpenSSH Server**.

---

# A Simple Diagram

```
           Internet / Network
                  │
                  │
      ┌─────────────────────┐
      │                     │
      ▼                     ▼
+----------------+    +----------------------+
| Your Laptop    |    | Ubuntu Server        |
|                |    |                      |
| SSH Client     |───►| SSH Server           |
| (ssh command)  |    | (sshd service)       |
+----------------+    +----------------------+
```

---

# Real Example

Suppose you have:

**Laptop**

```
IP: 192.168.1.5
```

**Server**

```
IP: 192.168.1.100
```

You run:

```bash
ssh rahul@192.168.1.100
```

What happens?

1. Your SSH client starts.
2. It contacts `192.168.1.100`.
3. The SSH server receives the request.
4. Authentication begins.
5. If successful, you get a remote shell.

---

# Who Runs Which?

|Machine|Software|
|---|---|
|Your laptop|SSH Client|
|Remote server|SSH Server|

Remember:

> **Client connects. Server accepts.**

---

# The SSH Server is Always Waiting

The SSH server is like a receptionist waiting for visitors.

It keeps listening for new connections.

On Linux, this is done by a background service called:

```
sshd
```

The **`d`** stands for **daemon**, which is a program that runs in the background.

---

# What is a Daemon?

A **daemon** is a program that runs continuously in the background and waits for work.

Examples:

|Daemon|Purpose|
|---|---|
|`sshd`|Accept SSH connections|
|`cron`|Run scheduled jobs|
|`systemd`|Manage system services|
|`cupsd`|Handle printing|

You don't usually start these manually—they run as services.

---

# Why Doesn't Every Computer Accept SSH?

For security.

Many personal computers don't have an SSH server running because they don't need to accept remote logins.

For example:

- Your Linux Mint laptop has an SSH **client** by default.
- It may **not** have an SSH **server** installed or enabled.

That means:

- ✅ You can connect to other machines.
- ❌ Other machines can't SSH into yours unless you install and enable an SSH server.

---

# Client vs Server Analogy

Think of a restaurant.

```
Customer  ─────►  Restaurant

Client            Server
```

- Customer places the order.
- Restaurant receives the order.
- Restaurant prepares the food.
- Customer gets the result.

SSH works similarly:

```
Client  ─────►  Server

Command         Executes command
```

---

# Everyday Example

Imagine you deploy your backend to a VPS.

You type:

```bash
ssh rahul@203.0.113.10
```

Here's what happens:

```
Laptop
│
├── SSH Client starts
│
▼
Internet
│
▼
Ubuntu VPS
│
├── sshd receives the request
├── Verifies your identity
├── Starts your shell
│
▼
You control the server
```

---

# Key Takeaways

- **SSH Client**: The program that starts the connection (`ssh` command).
- **SSH Server**: The program that accepts SSH connections (`sshd` service).
- The client initiates communication; the server listens for it.
- Your laptop is usually the **client**.
- The remote Linux machine is usually the **server**.

---

# Quick Quiz

**1. Which machine starts an SSH connection?**

A. Server

B. Client

✅ **Answer:** **B. Client**

---

**2. What is the name of the SSH server service on Linux?**

A. `ssh`

B. `sshd`

C. `ssh-server`

✅ **Answer:** **B. `sshd`**

---

**3. Your Linux Mint laptop can SSH into a VPS, but the VPS can't SSH into your laptop. What is the most likely reason?**

A. Your laptop has no SSH client.

B. The VPS has no internet.

C. Your laptop doesn't have an SSH server installed or running.

✅ **Answer:** **C. Your laptop doesn't have an SSH server installed or running.**

---

## Practice (on your Linux Mint)

Check whether the SSH client is installed:

```bash
ssh -V
```

Example output:

```
OpenSSH_9.xp1, OpenSSL 3.x.x
```

Check whether the SSH server (`sshd`) is installed and running:

```bash
systemctl status ssh
```

or, on some systems:

```bash
systemctl status sshd
```

If the service isn't found, don't worry—we'll learn how to install and configure the SSH server in upcoming lessons.

When you're ready, say **"Lesson 4"** to learn **How SSH Works Behind the Scenes**, including what happens from the moment you press Enter until you get a remote shell.