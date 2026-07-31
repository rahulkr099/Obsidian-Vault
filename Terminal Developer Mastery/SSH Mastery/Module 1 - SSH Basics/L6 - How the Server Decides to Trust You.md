# SSH Mastery — Module 1, Lesson 6

# Authentication — How the Server Decides to Trust You

In the previous lesson, we learned how SSH creates a secure, encrypted connection.

Now comes the next question:

> **How does the server know that you are really you?**

The answer is **authentication**.

---

# What is Authentication?

Authentication means:

> **Proving your identity.**

Think of entering your college.

The security guard asks for your ID card.

If the ID matches:

✅ You enter.

If it doesn't:

❌ You stay outside.

SSH works the same way.

---

# Authentication vs Authorization

Many beginners confuse these two terms.

|Authentication|Authorization|
|---|---|
|Who are you?|What are you allowed to do?|
|Login|Permissions|
|Verify identity|Verify access|

Example:

You log in as `rahul`.

Authentication:

✔ Are you really Rahul?

Authorization:

✔ Can Rahul restart services?

✔ Can Rahul delete files?

✔ Can Rahul use `sudo`?

First comes **authentication**, then **authorization**.

---

# The Login Process

Suppose you type:

```bash
ssh rahul@192.168.1.100
```

The process looks like this:

```
Laptop
   │
   │ Connect
   ▼
Server
   │
"Who are you?"
   │
Username = rahul
   │
"Prove it."
   │
Password or SSH Key
   │
Verified?
   │
 ┌───────┴────────┐
 │                │
Yes              No
 │                │
Login         Permission Denied
```

---

# Method 1 — Password Authentication

The oldest method.

Example:

```bash
ssh rahul@server
```

SSH asks:

```
rahul@server's password:
```

You type:

```
********
```

If the password matches:

✅ Login succeeds.

Otherwise:

```
Permission denied
```

---

# Why Passwords Have Problems

Passwords can be:

- guessed
- reused
- stolen
- leaked
- weak

Example of a weak password:

```
password123
```

Example of a stronger password:

```
T9#mQ7!Lp2@x
```

Even strong passwords have to travel through the authentication process each time you log in.

---

# Method 2 — SSH Key Authentication ⭐

This is the modern and preferred method.

Instead of remembering a password, you have two keys.

```
Private Key
```

and

```
Public Key
```

The private key stays on **your computer**.

The public key is copied to the **server**.

---

# Think of It Like a Lock

Imagine:

Your house has a lock.

```
Server
   │
Public Lock
```

You own the only key.

```
Laptop
   │
Private Key
```

Anyone can see the lock.

Only you can open it with the matching key.

---

# Login Using SSH Keys

```
Laptop
│
Private Key
│
▼
Server
│
Public Key
│
Match?
│
Yes
│
Login
```

Notice something important:

Your **private key never leaves your laptop**.

The server verifies it mathematically.

This is one reason SSH key authentication is so secure.

---

# Password vs SSH Keys

|Password|SSH Key|
|---|---|
|You type it|Usually automatic|
|Can be guessed|Extremely difficult to guess|
|Easy to reuse|Unique to you|
|Less secure|More secure|
|Common for beginners|Standard in production|

Most companies disable password login entirely and allow only SSH keys.

---

# Multiple Failed Attempts

Suppose someone tries:

```
password
```

Wrong.

```
123456
```

Wrong.

```
letmein
```

Wrong.

Many servers detect repeated failures and temporarily block further attempts to reduce brute-force attacks.

---

# What Happens After Authentication?

If authentication succeeds:

```
Authentication
      │
      ▼
Start your shell
      │
      ▼
bash
```

Now you can run commands like:

```bash
pwd
```

```bash
ls
```

```bash
cd /var/www
```

These commands run on the **remote server**.

---

# If Authentication Fails

You'll usually see:

```
Permission denied (publickey).
```

or

```
Permission denied, please try again.
```

This doesn't always mean the password is wrong. It can also mean:

- Wrong username
- Wrong SSH key
- Public key not installed on the server
- Incorrect file permissions on the SSH keys

We'll learn how to troubleshoot these later.

---

# Real Backend Example

Imagine your backend is deployed on a VPS.

You connect:

```bash
ssh rahul@203.0.113.10
```

The server checks:

- Is there a user named `rahul`?
- Is Rahul using a valid password or SSH key?

If everything checks out:

```
Welcome to Ubuntu
Last login: Wed Jul 29 16:45:12 IST 2026
rahul@server:~$
```

You're now logged into the remote server.

---

# Key Takeaways

- Authentication means **proving your identity**.
- SSH supports **password authentication** and **SSH key authentication**.
- SSH keys are the preferred method because they are more secure and more convenient.
- Your **private key must always stay private**.
- Authentication happens before you get access to the remote shell.

---

# Mini Challenge

### Question 1

Authentication answers which question?

A. What can you do?

B. Who are you?

C. Which port should be used?

✅ **Answer:** **B**

---

### Question 2

Which key should **never** be shared?

A. Public Key

B. Private Key

✅ **Answer:** **B**

---

### Question 3

Which authentication method is commonly used in production servers?

A. Password Authentication

B. SSH Key Authentication

✅ **Answer:** **B**

---

## Practice

Check your SSH configuration to see which authentication methods your client supports:

```bash
ssh -G localhost | grep -i preferredauthentications
```

You might see something like:

```
preferredauthentications gssapi-with-mic,hostbased,publickey,keyboard-interactive,password
```

Don't worry about all of these yet. Over the next lessons, we'll focus on the two methods you'll use most:

- **Password authentication**
- **SSH key authentication**

When you're ready, say **"Lesson 7"** to learn **Password Login vs SSH Key Login** in more detail, including why professional servers almost always prefer SSH keys.