# SSH Mastery — Module 1, Lesson 13

# Basic SSH Security

Congratulations! 🎉

You've learned how SSH works and how to troubleshoot common problems.

Now it's time to learn **how to use SSH safely**.

Many successful cyberattacks happen because of simple mistakes, not because SSH itself is insecure.

---

# Security Rule #1 ⭐

# Never Share Your Private Key

When you create an SSH key pair, you'll have two files:

```
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
```

|File|Share?|
|---|---|
|`id_ed25519` (Private Key)|❌ Never|
|`id_ed25519.pub` (Public Key)|✅ Yes|

Think of it like this:

```
House Key
│
├── Private Key → Your real house key
│                 Never give it away.
│
└── Public Key → A copy of your lock
                  Safe to share.
```

---

# Security Rule #2 ⭐⭐⭐⭐⭐

# Never Log In as `root`

Many Linux servers have a special user:

```
root
```

`root` has unlimited power.

It can:

- Delete every file
- Stop every service
- Create users
- Install software
- Change passwords

If someone gets root access, they control the entire server.

---

## Better Practice

Instead of:

```bash
ssh root@server
```

Use:

```bash
ssh rahul@server
```

Then only become root when necessary:

```bash
sudo apt update
```

or

```bash
sudo systemctl restart nginx
```

This follows the **principle of least privilege**: use only the permissions you need.

---

# Security Rule #3

# Use SSH Keys Instead of Passwords

Password login:

```
Password
```

SSH key login:

```
Private Key
```

SSH keys are:

- More secure
- Faster
- Easier for automation

Most production servers disable password login after SSH keys are configured.

---

# Security Rule #4

# Use a Passphrase

A passphrase protects your private key.

Without one:

```
Laptop stolen

↓

Private key copied

↓

Attacker can use it
```

With a passphrase:

```
Laptop stolen

↓

Private key copied

↓

Still needs passphrase
```

Think of it like a PIN on your ATM card.

Someone might steal the card, but they still need the PIN.

---

# Security Rule #5

# Protect the `.ssh` Directory

Correct permissions matter.

Your `.ssh` folder:

```bash
chmod 700 ~/.ssh
```

Private key:

```bash
chmod 600 ~/.ssh/id_ed25519
```

Public key:

```bash
chmod 644 ~/.ssh/id_ed25519.pub
```

Meaning:

|Permission|Purpose|
|---|---|
|`700`|Only you can access the `.ssh` folder|
|`600`|Only you can read/write the private key|
|`644`|Everyone can read the public key|

SSH will often refuse to use a private key if it's too accessible.

---

# Security Rule #6

# Verify Host Keys

The first time you connect:

```
The authenticity of host ...
can't be established.
```

Always make sure you're connecting to the correct server.

After accepting it:

SSH stores the fingerprint in:

```
~/.ssh/known_hosts
```

If the fingerprint changes later:

```
WARNING:
REMOTE HOST IDENTIFICATION HAS CHANGED!
```

Don't ignore it.

Find out why it changed before accepting the new fingerprint.

---

# Security Rule #7

# Keep OpenSSH Updated

Updates fix bugs and security issues.

On Ubuntu or Linux Mint:

```bash
sudo apt update
sudo apt upgrade
```

You don't need to update every day, but installing security updates regularly is a good habit.

---

# Security Rule #8

# Don't Upload Private Keys

Never commit this:

```
~/.ssh/id_ed25519
```

to:

- GitHub
- GitLab
- Google Drive
- Discord
- Slack
- Email

If you accidentally expose a private key:

1. Generate a new key pair.
2. Replace the public key on every server.
3. Delete the old key from all servers.

Treat it as compromised.

---

# Security Rule #9

# Lock Your Computer

Even the strongest SSH setup can't help if someone walks up to your unlocked laptop.

Good habits:

- Lock your screen when away.
- Use a strong login password.
- Enable full-disk encryption when installing Linux if possible.

---

# Security Rule #10

# Disconnect When Finished

After completing your work:

```bash
exit
```

or

Press:

```
Ctrl + D
```

Closing unused sessions reduces the chance of accidental commands or misuse.

---

# A Typical Secure Workflow

```
Laptop
│
├── Private key (protected)
├── Passphrase enabled
├── Screen locked when away
│
▼
SSH
│
▼
Server
│
├── Login as normal user
├── Use sudo when needed
├── Verify host key
└── Logout when finished
```

This is how many professional developers work every day.

---

# Real Backend Example

Imagine you've deployed your Express application.

You connect:

```bash
ssh rahul@api.example.com
```

Your private key authenticates you.

You update your application:

```bash
git pull
npm install
pm2 restart backend
```

Need administrative privileges?

```bash
sudo systemctl restart nginx
```

When you're done:

```bash
exit
```

Simple, secure, and professional.

---

# Common Beginner Mistakes

❌ Saving the private key in cloud storage.

---

❌ Sharing the private key with teammates.

Instead, each teammate should have **their own SSH key pair**, and their **public key** should be added to the server.

---

❌ Logging in as `root` for everything.

Use a regular user and `sudo` when required.

---

❌ Ignoring SSH warnings.

Read them carefully. They often prevent security problems.

---

# Security Checklist

Before connecting to a production server:

- ✅ Private key is secure.
- ✅ `.ssh` permissions are correct.
- ✅ Server hostname is correct.
- ✅ Host fingerprint is verified.
- ✅ Use a normal user account.
- ✅ Use `sudo` only when needed.
- ✅ Logout when finished.

---

# Key Takeaways

- Never share your **private key**.
- Sharing your **public key** is safe.
- Prefer SSH keys over passwords.
- Use a passphrase to protect your private key.
- Avoid logging in directly as `root`.
- Keep your SSH client and server updated.
- Treat SSH warnings seriously.

---

# Mini Challenge

### Question 1

Which file should **never** be shared?

A.

```
id_ed25519
```

B.

```
id_ed25519.pub
```

✅ **Answer:** **A**

---

### Question 2

What command sets the correct permissions for your private key?

```bash
chmod 600 ~/.ssh/id_ed25519
```

✅ **Correct!**

---

### Question 3

Why is using `sudo` from a normal user better than logging in directly as `root`?

A. It follows the principle of least privilege and reduces the impact of mistakes.

B. It makes the server faster.

C. It changes the SSH port.

✅ **Answer:** **A**

---

# Practice on Your Linux Mint

Check your SSH directory permissions:

```bash
ls -ld ~/.ssh
```

Check your SSH files:

```bash
ls -l ~/.ssh
```

If you already have a private key, verify its permissions:

```bash
stat -c "%a %n" ~/.ssh/id_ed25519
```

A secure setup should look similar to:

```
700 ~/.ssh
600 ~/.ssh/id_ed25519
644 ~/.ssh/id_ed25519.pub
```

---

## Pro Tip ⭐

A good habit is to **create a separate SSH key for different purposes**. For example:

```
~/.ssh/id_ed25519_github
~/.ssh/id_ed25519_personal_vps
~/.ssh/id_ed25519_work
```

This way, if one key is ever compromised, you only need to replace that specific key instead of updating every server and service that uses SSH.

---

## Looking Ahead

In **Lesson 14**, you'll complete a **hands-on mini project** where you'll:

- Generate your first SSH key pair.
- Understand each file in `~/.ssh`.
- Add a key to an SSH agent.
- Practice connecting locally (or to a test server if available).

This will be your first practical SSH workflow and will prepare you for Module 2, where you'll start connecting to real servers.