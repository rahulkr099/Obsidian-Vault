# SSH Mastery — Module 1, Lesson 9

# Understanding Your SSH Client

So far you've learned **what SSH is** and **how it works**.

Now it's time to get familiar with the SSH client that's already on your Linux Mint system.

Think of this lesson as getting to know your tools before using them.

---

# Meet the SSH Client

The SSH client is simply the `ssh` command.

Whenever you type:

```bash
ssh
```

you're running the OpenSSH client.

You can see where it lives:

```bash
which ssh
```

Example:

```
/usr/bin/ssh
```

---

# Getting Help

Every Linux command has documentation.

Start with:

```bash
ssh --help
```

or

```bash
ssh -h
```

You'll see many options.

Don't worry—you won't memorize them.

Professionals look them up too.

---

# The Manual Page

Linux has built-in documentation called **man pages**.

Open the SSH manual:

```bash
man ssh
```

You'll see something like:

```
NAME
     ssh — OpenSSH remote login client
```

Navigation inside `man`:

|Key|Action|
|---|---|
|↑ ↓|Move one line|
|Space|Next page|
|b|Previous page|
|/word|Search|
|n|Next search result|
|q|Quit|

Since you've already learned **`vim`** and terminal navigation, using `man` will feel familiar.

---

# Check Your SSH Version

```bash
ssh -V
```

Example:

```
OpenSSH_9.9p2 Ubuntu-2ubuntu0.1
```

The version helps when:

- Reporting bugs
- Following tutorials
- Checking feature support

---

# Understanding SSH Syntax

The basic format is:

```bash
ssh [OPTIONS] USER@HOST
```

Let's break it down.

### USER

The account you want to log in as.

Example:

```
rahul
```

---

### HOST

The destination computer.

It can be:

An IP address:

```
192.168.1.100
```

or

A domain name:

```
example.com
```

---

### OPTIONS

Options change SSH's behavior.

Example:

```bash
ssh -v rahul@example.com
```

Here:

```
-v
```

means **verbose mode**.

---

# Some Useful Options

## `v` (Verbose)

```bash
ssh -v localhost
```

Shows connection details.

---

## `vv`

```bash
ssh -vv localhost
```

Shows even more information.

---

## `vvv`

```bash
ssh -vvv localhost
```

Maximum debugging output.

This is one of the most useful commands when troubleshooting SSH.

---

## `p`

Connect to a different port.

Default:

```
22
```

Example:

```bash
ssh -p 2222 rahul@server
```

Now SSH connects to port **2222** instead of **22**.

---

## `l`

Specify the username separately.

Instead of:

```bash
ssh rahul@server
```

you can write:

```bash
ssh -l rahul server
```

Both commands do exactly the same thing.

---

# Viewing the Effective Configuration

This is one of the most useful but least-known commands.

```bash
ssh -G localhost
```

It prints the configuration that SSH will actually use.

Example:

```
hostname localhost
user rahul
port 22
```

This is very helpful for debugging.

---

# Searching the Configuration

Instead of reading hundreds of lines:

```bash
ssh -G localhost | grep port
```

Output:

```
port 22
```

Or:

```bash
ssh -G localhost | grep user
```

Output:

```
user rahul
```

---

# Where Does SSH Get Its Settings?

SSH checks configuration files.

There are two main ones.

### System-wide

```
/etc/ssh/ssh_config
```

Affects all users.

---

### Personal

```
~/.ssh/config
```

Only affects your user account.

We'll learn how to create and use this file in a later module.

---

# Example Connection

Suppose you type:

```bash
ssh rahul@example.com
```

SSH does roughly this:

```
Read configuration
       │
Resolve hostname
       │
Connect to port 22
       │
Authenticate
       │
Open shell
```

Many defaults (like port 22) come from the configuration.

---

# Common Beginner Mistakes

### Mistake 1

Typing only:

```bash
ssh
```

Result:

```
usage: ssh ...
```

SSH needs a destination.

---

### Mistake 2

Forgetting the username.

```bash
ssh example.com
```

SSH will try your current local username.

Sometimes that's fine.

Sometimes it fails because the remote username is different.

---

### Mistake 3

Using the wrong port.

If the server uses port **2222** but you connect to **22**, you'll get a connection error.

Always check the correct port.

---

# Real Backend Example

Your company gives you:

```
Host: api.company.com
User: deploy
Port: 2222
```

You connect like this:

```bash
ssh -p 2222 deploy@api.company.com
```

That's a very common real-world scenario.

---

# Key Takeaways

- The SSH client is the `ssh` command.
- The general syntax is:

```bash
ssh [OPTIONS] USER@HOST
```

- `v`, `vv`, and `vvv` help with debugging.
- `p` specifies a custom port.
- `G` displays the effective SSH configuration.
- SSH settings come from system and user configuration files.

---

# Mini Challenge

### Question 1

Which command shows your SSH version?

A.

```bash
ssh -V
```

B.

```bash
ssh version
```

✅ **Answer:** **A**

---

### Question 2

Which option enables verbose output?

A.

```
-d
```

B.

```
-v
```

✅ **Answer:** **B**

---

### Question 3

How do you connect to a server on port **2222**?

A.

```bash
ssh user@server:2222
```

B.

```bash
ssh -p 2222 user@server
```

✅ **Answer:** **B**

---

# Practice on Your Linux Mint

Run these commands:

```bash
ssh -V
```

```bash
ssh --help
```

```bash
man ssh
```

```bash
ssh -G localhost | grep user
```

```bash
ssh -G localhost | grep port
```

```bash
ssh -v localhost
```

If `localhost` isn't running an SSH server, you'll likely see a connection error after the client attempts to connect. That's okay—the goal here is to observe the client's behavior.

---

## Pro Tip ⭐

As a backend developer, you'll often debug SSH issues with:

```bash
ssh -vvv user@server
```

Whenever an SSH connection fails, **increase the verbosity first**. The detailed output usually points directly to the problem, whether it's DNS resolution, port connectivity, authentication, or key selection.

When you're ready, say **"Lesson 10"** to make your **first real SSH connection** and understand the prompts you'll see the first time you connect to a server.