## Objective

Understand what a shell script is and why backend engineers use them.

---

# What is a Shell?

When you type

```bash
ls
```

who runs it?

```
You
↓

Terminal

↓

Shell

↓

Linux Kernel

↓

Filesystem
```

The shell acts like an interpreter.

It reads your command and asks Linux to execute it.

Common shells:

```
bash

zsh

fish

sh
```

You use **Zsh**, but almost every script is written in **Bash** because Bash is available on nearly every Linux server.

---

# What is a Shell Script?

A shell script is simply a text file containing Linux commands.

Example:

```bash
pwd
date
whoami
```

Instead of typing these commands one by one, save them in a file.

Example:

```bash
hello.sh
```

Contents:

```bash
pwd
date
whoami
```

Run it once, and all commands execute automatically.

---

# Why Backend Engineers Use Shell Scripts

Imagine deploying a Node.js API.

Without a script:

```bash
git pull
npm install
npm run build
pm2 restart api
```

Every deployment means typing these commands again.

With a script:

```bash
deploy.sh
```

Run:

```bash
./deploy.sh
```

Done.

Automation saves time and reduces mistakes.

---

# Creating Your First Script

Create a new file:

```bash
touch hello.sh
```

Open it:

```bash
nvim hello.sh
```

Add:

```bash
echo "Hello Rahul!"
echo "Welcome to Shell Scripting."
```

Save the file.

---

# What is `echo`?

`echo` prints text to the terminal.

Example:

```bash
echo "Hello"
```

Output:

```
Hello
```

You can also print variables later.

---

# Shebang (`#!`)

Most scripts start with:

```bash
#!/usr/bin/env bash
```

or

```bash
#!/bin/bash
```

This tells Linux which program should execute the script.

Recommended:

```bash
#!/usr/bin/env bash
```

It works even if Bash is installed in a different location.

Your script becomes:

```bash
#!/usr/bin/env bash

echo "Hello Rahul!"
```

---

# Make the Script Executable

By default, it's just a text file.

Give it execute permission:

```bash
chmod +x hello.sh
```

Check permissions:

```bash
ls -l hello.sh
```

Example output:

```
-rwxr-xr-x
```

The `x` means it's executable.

---

# Run the Script

Method 1:

```bash
./hello.sh
```

Method 2:

```bash
bash hello.sh
```

Difference:

```bash
./hello.sh
```

Requires execute permission.

```bash
bash hello.sh
```

Doesn't require execute permission because you're explicitly asking Bash to interpret the file.

---

# Comments

Use comments to explain your code.

```bash
# This prints a greeting
echo "Hello"
```

Comments are ignored when the script runs.

---

# Multiple Commands

```bash
#!/usr/bin/env bash

echo "Current directory:"
pwd

echo

echo "Current user:"
whoami

echo

echo "Current date:"
date
```

---

# Variables Preview

```bash
name="Rahul"

echo "$name"
```

Output:

```
Rahul
```

We'll study variables in depth in Lesson 2.

---

# Real Backend Example

Check whether Node.js is installed:

```bash
#!/usr/bin/env bash

echo "Checking Node.js..."

node -v
```

Or:

```bash
#!/usr/bin/env bash

echo "Current Git version:"
git --version

echo "Current Node version:"
node --version

echo "Current npm version:"
npm --version
```

This is a simple environment verification script that many developers use after setting up a new machine.

---

# Internal Understanding

When you run:

```bash
./hello.sh
```

Linux roughly does this:

```
Open file

↓

Read first line

↓

Find Bash

↓

Pass the script to Bash

↓

Execute commands one by one

↓

Return an exit code
```

This explains why the shebang line is important.

---

# Hands-on Lab

Create a script named:

```
system-info.sh
```

It should display:

- Current user
- Home directory
- Current working directory
- Current date and time
- Linux kernel version
- Hostname
- Uptime

**Hint:** Explore commands such as `whoami`, `echo "$HOME"`, `pwd`, `date`, `uname -r`, `hostname`, and `uptime`.

---

# Mini Challenge

Create a script named:

```
welcome.sh
```

It should print something like:

```
==============================
Welcome Rahul!
Today is Friday.
Current time: 10:30 AM
Have a productive coding session!
==============================
```

Use only commands you've learned so far.

---

# Common Mistakes

### Forgetting execute permission

```bash
./hello.sh
```

Error:

```
Permission denied
```

Fix:

```bash
chmod +x hello.sh
```

---

### Missing shebang

The script may work when run with `bash script.sh`, but may fail or behave differently when executed directly.

Always include:

```bash
#!/usr/bin/env bash
```

---

### Using Windows line endings

If you edit scripts on Windows, you might see:

```
bad interpreter
```

Fix:

```bash
dos2unix script.sh
```

---

# Interview Questions

1. What is a shell?
2. What is a shell script?
3. What is the purpose of a shebang?
4. What is the difference between `bash script.sh` and `./script.sh`?
5. Why do we use `chmod +x`?
6. What does `echo` do?
7. Why are shell scripts useful in backend development?

---

# Cheat Sheet

```bash
# Create a script
touch hello.sh

# Edit
nvim hello.sh

# Shebang
#!/usr/bin/env bash

# Print text
echo "Hello"

# Make executable
chmod +x hello.sh

# Run
./hello.sh

# Or
bash hello.sh

# Check permissions
ls -l

# Current user
whoami

# Current directory
pwd

# Current date
date

# Hostname
hostname

# Kernel version
uname -r

# Uptime
uptime
```

---

# Weekly Challenge

Build a script called `dev-check.sh` that checks whether the following tools are installed and prints their versions if available:

- Git
- Node.js
- npm
- Python
- Docker
- Neovim

If a tool is missing, display a clear message instead of letting the script fail.

---

## What's Next?

**Lesson 2 — Variables and User Input**

You'll learn:

- Variables
- Command substitution
- User input with `read`
- Quoting (`" "` vs `' '`)
- Arithmetic operations
- Useful built-in variables
- Practical scripting examples

From Lesson 2 onward, we'll begin writing scripts that solve real backend development tasks instead of just printing information.