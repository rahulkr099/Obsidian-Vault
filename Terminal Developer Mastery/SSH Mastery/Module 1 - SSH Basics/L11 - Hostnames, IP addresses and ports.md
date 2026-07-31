# SSH Mastery — Module 1, Lesson 11

# Hostnames, IP Addresses, and Ports

Before SSH can connect to a server, it needs to answer **three questions**:

1. **Which computer?** → IP Address or Hostname
2. **Which service?** → Port
3. **Which user?** → Username

Today we'll focus on the first two.

---

# Think of Delivering a Letter 📬

Suppose you want to send a letter.

You need:

- City
- Street
- House Number
- Person's Name

Similarly, SSH needs:

```
Username
IP Address (or Hostname)
Port
```

Example:

```bash
ssh rahul@203.0.113.10
```

Here:

- Username → `rahul`
- IP Address → `203.0.113.10`
- Port → `22` (default)

---

# What is an IP Address?

An **IP address** is the unique address of a device on a network.

Think of it as the **house address** of a computer.

Example:

```
192.168.1.100
```

or

```
203.0.113.10
```

Without an IP address, your computer doesn't know where to connect.

---

# Public vs Private IP

There are two common types.

## Private IP

Used inside your home, office, or college network.

Examples:

```
192.168.1.10
192.168.0.25
10.0.0.5
172.16.1.50
```

These **cannot** be reached directly from the internet.

Example:

```
Laptop
192.168.1.5
      │
Wi-Fi Router
      │
Internet
```

---

## Public IP

Assigned by your Internet Service Provider (ISP).

Example:

```
203.0.113.10
```

This is the address other computers on the internet use to reach your server.

Example:

```
Laptop
      │
Internet
      │
203.0.113.10
```

Cloud servers (AWS, DigitalOcean, Azure, etc.) usually have a public IP.

---

# What is a Hostname?

Humans remember names better than numbers.

Instead of:

```
203.0.113.10
```

we use:

```
myserver.com
```

or

```
github.com
```

These names are called **hostnames**.

---

# How Does a Hostname Become an IP Address?

SSH asks **DNS (Domain Name System)**.

Think of DNS as the internet's phonebook.

```
myserver.com
        │
        ▼
DNS Server
        │
        ▼
203.0.113.10
```

Then SSH connects to that IP.

---

# IP vs Hostname

|IP Address|Hostname|
|---|---|
|Numeric|Human-readable|
|`203.0.113.10`|`myserver.com`|
|Doesn't require DNS|Requires DNS lookup|

Both work with SSH.

---

# What is a Port?

A computer can run many network services at the same time.

How does it know which service you want?

**Ports.**

Think of a hotel.

```
Hotel
│
├── Room 22
├── Room 80
├── Room 443
├── Room 3306
```

The hotel is the computer.

The room number is the port.

---

# Common Ports

|Port|Service|
|---|---|
|22|SSH|
|80|HTTP|
|443|HTTPS|
|21|FTP|
|25|SMTP (Email)|
|3306|MySQL|
|5432|PostgreSQL|
|6379|Redis|
|27017|MongoDB|

As a backend developer, you'll see many of these regularly.

---

# Why Does SSH Use Port 22?

By convention, SSH listens on **port 22**.

So this command:

```bash
ssh rahul@server
```

is actually interpreted as:

```bash
ssh -p 22 rahul@server
```

---

# Custom SSH Ports

Some servers use another port, such as **2222**.

Example:

```bash
ssh -p 2222 rahul@server
```

SSH now connects to port **2222** instead of **22**.

---

# Real Connection Example

Suppose your company gives you:

```
Host: api.company.com
Port: 2222
User: deploy
```

You connect like this:

```bash
ssh -p 2222 deploy@api.company.com
```

---

# How SSH Finds the Server

Let's trace the full process.

```
ssh rahul@myserver.com
        │
        ▼
DNS
        │
        ▼
203.0.113.10
        │
        ▼
Port 22
        │
        ▼
SSH Server
```

---

# What Happens If the Port Is Wrong?

Suppose the server listens on **2222**, but you type:

```bash
ssh rahul@server
```

SSH tries port **22**.

Possible output:

```
ssh: connect to host server port 22: Connection refused
```

The server exists, but nothing is listening on that port.

---

# What Happens If the Hostname Is Wrong?

Example:

```bash
ssh rahul@myservr.com
```

Notice the typo.

You might see:

```
Could not resolve hostname myservr.com:
Name or service not known
```

SSH couldn't find the server because DNS couldn't resolve the hostname.

---

# Check Your Own Hostname

Run:

```bash
hostname
```

Example:

```
mint-laptop
```

This is your computer's hostname.

---

# Check Your Local IP

Run:

```bash
hostname -I
```

Example:

```
192.168.1.5
```

This is usually your local (private) IP address.

---

# See Listening Ports

Want to know which services are listening?

Run:

```bash
ss -tln
```

Example:

```
State   Local Address:Port
LISTEN  0.0.0.0:22
LISTEN  0.0.0.0:80
LISTEN  0.0.0.0:443
```

If SSH is running, you'll usually see port **22**.

---

# Real Backend Example

Suppose you've deployed your Node.js app.

Your hosting provider sends:

```
Server: api.myapp.com
Port: 22
Username: ubuntu
```

You connect:

```bash
ssh ubuntu@api.myapp.com
```

SSH:

1. Resolves `api.myapp.com` to an IP.
2. Connects to port **22**.
3. Authenticates you.
4. Opens a remote shell.

---

# Key Takeaways

- Every computer has an **IP address**.
- A **hostname** is a human-friendly name that maps to an IP using DNS.
- A **port** identifies a specific network service.
- SSH uses **port 22** by default.
- If the server uses a different port, use `p`.

---

# Mini Challenge

### Question 1

What does DNS do?

A. Encrypts SSH traffic

B. Converts a hostname into an IP address

C. Starts the SSH server

✅ **Answer:** **B**

---

### Question 2

Which port does SSH use by default?

A. 21

B. 22

C. 80

D. 443

✅ **Answer:** **B**

---

### Question 3

How do you connect to a server on port **2222**?

```bash
ssh -p 2222 rahul@server
```

✅ Correct.

---

# Practice on Your Linux Mint

Run these commands:

Check your hostname:

```bash
hostname
```

Check your private IP:

```bash
hostname -I
```

See listening TCP ports:

```bash
ss -tln
```

Check if SSH is listening:

```bash
ss -tln | grep :22
```

If you don't see any output, your SSH server probably isn't running yet, which is completely fine if you've only installed the SSH client.

---

## Pro Tip ⭐

As a backend developer, one of the first questions you'll ask when SSH fails is:

- **Am I connecting to the correct hostname?**
- **Is it resolving to the right IP?**
- **Is the SSH server listening on the expected port?**

Checking those three things solves a large percentage of SSH connection problems.

When you're ready, say **"Lesson 12"** to learn **Common SSH Errors and How to Fix Them**, where we'll troubleshoot real-world connection issues like `Connection refused`, `Permission denied`, `Host key verification failed`, and `No route to host`.