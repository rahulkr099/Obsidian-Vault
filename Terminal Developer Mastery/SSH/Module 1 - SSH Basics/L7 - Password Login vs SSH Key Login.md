# SSH Mastery — Module 1, Lesson 7

# Password Login vs SSH Key Login

In the previous lesson, you learned that SSH supports two common authentication methods:

1. Password Login
2. SSH Key Login

Now let's compare them in detail.

---

# The Big Picture

```
                SSH Authentication
                      │
         ┌────────────┴────────────┐
         │                         │
         ▼                         ▼
   Password Login           SSH Key Login
```

Both methods let you log in to a server.

The difference is **how you prove your identity**.

---

# Password Login

Suppose you connect:

```bash
ssh rahul@server
```

The server asks:

```
rahul@server's password:
```

You type:

```
MySecretPassword
```

The server checks whether it matches the stored password.

If yes:

✅ Login successful

---

## How Password Login Works

```
Laptop                     Server

Username ───────────────►
Password ───────────────►
                    Check Password
                          │
                     Match?
                   Yes / No
```

Simple and easy to understand.

---

# Advantages of Password Login

- Easy for beginners
- No setup required
- Works on almost every SSH server
- Good for learning

---

# Disadvantages of Password Login

You must remember the password.

You type it every time.

Weak passwords can be guessed.

Passwords can be leaked or reused.

Not ideal for automation.

---

# SSH Key Login

Instead of a password, you have a **key pair**.

```
Laptop

Private Key
```

↓

```
Server

Public Key
```

The server verifies that your private key matches the public key.

If it matches:

✅ Login successful

---

## How SSH Key Login Works

```
Laptop                     Server

Private Key
      │
      ├──────────────► Public Key
      │
      └──────────────► Verification
                          │
                     Match?
                     Yes / No
```

Notice:

The **private key never leaves your laptop**.

---

# Real-World Analogy

## Password Login

Imagine entering a building.

The guard asks:

> "Tell me the secret password."

You answer:

> "BlueTiger123"

If correct, you're allowed in.

---

## SSH Key Login

Instead, imagine you have a special key.

The guard doesn't ask for a password.

He checks whether your key fits the lock.

If it fits:

Welcome inside.

---

# Which One is Faster?

## Password

```
Connect

↓

Type password

↓

Login
```

---

## SSH Key

```
Connect

↓

Automatic verification

↓

Login
```

SSH keys are usually much faster because you don't type a password every time.

---

# Which One is More Secure?

### Password

Can be:

- guessed
- stolen
- reused
- leaked

---

### SSH Keys

A modern Ed25519 private key contains an enormous amount of randomness.

Guessing it by brute force is not considered practical with current technology.

That's why SSH keys are trusted across the industry.

---

# Can Someone Copy My Private Key?

Only if they gain access to your computer or you accidentally share it.

That's why you should:

- Never email your private key.
- Never upload it to GitHub.
- Never send it in chat messages.
- Never copy it to another person's computer.

Treat it like the key to your house.

---

# What if I Lose My Private Key?

If it's lost and you don't have a backup:

❌ You can't use it to log in anymore.

The solution is to:

1. Generate a new key pair.
2. Add the new public key to the server.
3. Remove the old public key.

We'll practice this later.

---

# Why Companies Disable Password Login

Many production servers are configured like this:

```
Password Login

❌ Disabled
```

Only SSH keys are accepted.

Why?

Because attackers constantly scan the internet and try common usernames and passwords.

Example:

```
root / root

admin / admin

test / test

ubuntu / ubuntu
```

Disabling password authentication removes that attack path.

---

# Which Should You Use?

|Situation|Recommended Method|
|---|---|
|Learning SSH|Password or SSH Key|
|Personal VPS|SSH Key|
|Company Server|SSH Key|
|GitHub Authentication|SSH Key|
|Automated Scripts|SSH Key|

---

# Your Future Workflow

As a backend developer, your login will usually look like this:

```bash
ssh rahul@my-server
```

No password prompt.

Your SSH key authenticates you automatically.

Then you can run:

```bash
git pull
```

```bash
docker compose up -d
```

```bash
pm2 restart backend
```

This is the workflow you'll use frequently in professional environments.

---

# Quick Comparison

|Feature|Password|SSH Key|
|---|---|---|
|Easy to start|✅|Needs initial setup|
|Type every login|✅|Usually no|
|Secure|Good|Excellent|
|Automation|Poor|Excellent|
|Used in companies|Sometimes|Very common|

---

# Key Takeaways

- Both methods authenticate you to the server.
- Passwords are easier to start with but less convenient and generally less secure.
- SSH keys are the preferred method for professional development and server administration.
- **Never share your private key.**
- SSH keys are the standard for GitHub, cloud servers, and automation.

---

# Mini Challenge

### Question 1

Which file should stay only on your computer?

A. Public Key

B. Private Key

✅ **Answer:** **B**

---

### Question 2

Which authentication method is best for automated deployments?

A. Password

B. SSH Key

✅ **Answer:** **B**

---

### Question 3

Why do many companies disable password login?

A. Passwords are too slow.

B. Passwords are a common target for guessing and brute-force attacks.

C. SSH doesn't support passwords.

✅ **Answer:** **B**

---

## Practice

Check whether you already have SSH keys on your Linux Mint system:

```bash
ls -la ~/.ssh
```

You may see files like:

```
id_ed25519
id_ed25519.pub
known_hosts
config
```

Don't worry if you don't have `id_ed25519` yet. In the next modules, you'll learn how to generate an SSH key pair, understand what each file does, and use it with GitHub and remote servers.

When you're ready, say **"Lesson 8"** to learn how to **install SSH tools and understand what is already available on your Linux Mint system**.