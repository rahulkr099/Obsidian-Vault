> **One of the most important lessons for every backend developer.**

If I had to choose **only one Bash topic** that every backend developer must master, this would be in my top three.

Every modern backend application uses environment variables.

Examples:

- Express
- React (during builds)
- Next.js
- Docker
- Kubernetes
- GitHub Actions
- Vercel
- Render
- Railway
- AWS
- DigitalOcean

If you've built MERN applications before, you've already seen variables like:

```
PORT
MONGODB_URI
JWT_SECRET
NODE_ENV
```

Now you'll understand how they actually work.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Understand environment variables
- Create environment variables
- Export variables
- Read environment variables
- Work with `.env` files
- Understand `PATH`
- Configure Node.js applications
- Use environment variables securely

**Estimated Time:** 4–5 hours

**Difficulty:** ⭐⭐⭐⭐☆

---

# What is an Environment Variable?

A normal variable exists **only inside your current shell or script**.

Example:

```bash
name="Rahul"
```

Only your current shell knows about it.

An **environment variable** is different.

It is shared with child processes.

Think of it like this:

```
Terminal

↓

export PORT=3000

↓

Node

↓

npm

↓

Git

↓

Python

↓

Docker
```

Every child process can read it.

---

# Variable vs Environment Variable

Normal variable:

```bash
name="Rahul"
```

Environment variable:

```bash
export name="Rahul"
```

The keyword:

```bash
export
```

makes the variable available to child processes.

---

# Viewing Environment Variables

Show all environment variables:

```bash
printenv
```

or

```bash
env
```

Example output:

```
HOME=/home/rahul
USER=rahul
SHELL=/usr/bin/zsh
PATH=/usr/local/bin:...
LANG=en_US.UTF-8
```

---

# Reading an Environment Variable

Example:

```bash
echo "$HOME"
```

Output:

```
/home/rahul
```

Another:

```bash
echo "$USER"
```

Output:

```
rahul
```

---

# Common Environment Variables

|Variable|Purpose|
|---|---|
|`HOME`|Your home directory|
|`USER`|Current username|
|`PWD`|Current directory|
|`SHELL`|Current shell|
|`PATH`|Executable search path|
|`HOSTNAME`|Computer name|
|`LANG`|Language settings|

---

# Creating Environment Variables

Example:

```bash
export CITY="Bokaro"
```

Check:

```bash
echo "$CITY"
```

Output:

```
Bokaro
```

---

# Why `export` Matters

Without export:

```bash
name="Rahul"
```

Start a child shell:

```bash
bash
```

Now:

```bash
echo "$name"
```

Output:

(empty)

Now try:

```bash
export name="Rahul"
```

Start another shell:

```bash
bash
```

Now:

```bash
echo "$name"
```

Output:

```
Rahul
```

Because the variable was exported.

---

# Temporary Variables

Example:

```bash
export PORT=5000
```

Close the terminal.

Open it again.

The variable is gone.

Environment variables created this way are temporary.

---

# Permanent Variables

Add them to your shell configuration.

For Zsh:

```bash
~/.zshrc
```

Example:

```bash
export EDITOR="nvim"
export BROWSER="firefox"
```

Reload:

```bash
source ~/.zshrc
```

Now they're available every time you open a terminal.

---

# Unsetting Variables

Remove a variable:

```bash
unset PORT
```

Verify:

```bash
echo "$PORT"
```

Nothing is printed.

---

# The Most Important Environment Variable: `PATH`

Suppose you type:

```bash
git
```

How does Linux know where Git is?

It checks the directories listed in:

```bash
echo "$PATH"
```

Example:

```
/usr/local/bin
/usr/bin
/bin
```

Linux searches these directories in order until it finds the executable.

---

# Inspecting `PATH`

Print each directory on a new line:

```bash
echo "$PATH" | tr ':' '\n'
```

Example output:

```
/usr/local/bin
/usr/bin
/bin
/home/rahul/.local/bin
```

---

# Adding a Directory to `PATH`

Suppose you have your own scripts in:

```
~/bin
```

Add it:

```bash
export PATH="$HOME/bin:$PATH"
```

Now any executable in `~/bin` can be run directly.

Example:

Instead of:

```bash
./create-project
```

You can simply type:

```bash
create-project
```

---

# Real Backend Example — Node.js

Many Express applications use:

```jsx
const PORT = process.env.PORT || 3000;
```

If:

```bash
export PORT=5000
```

Then the server starts on:

```
5000
```

Otherwise:

```
3000
```

---

# Using `.env` Files

Most backend projects use a `.env` file.

Example:

```
PORT=3000
NODE_ENV=development
JWT_SECRET=my-secret-key
DATABASE_URL=mongodb://localhost:27017/blog
```

Node.js loads these values using packages such as `dotenv`.

In JavaScript:

```jsx
import dotenv from "dotenv";

dotenv.config();

console.log(process.env.PORT);
```

Output:

```
3000
```

---

# Why `.env` Files?

Instead of changing your code:

```jsx
const password = "123456";
```

Use:

```jsx
const password = process.env.DB_PASSWORD;
```

Benefits:

- Different values for development and production.
- Secrets stay out of source code.
- Easier deployments.

---

# Never Commit Secrets

Bad:

```
JWT_SECRET=my-super-secret
```

inside Git.

Instead:

`.gitignore`

```
.env
```

Always ignore `.env` files containing secrets.

---

# Backend Example — Database Connection

Development:

```
DATABASE_URL=mongodb://localhost/blog
```

Production:

```
DATABASE_URL=mongodb+srv://...
```

No code changes are required.

Only the environment variable changes.

---

# Backend Example — Multiple Environments

Development:

```
NODE_ENV=development
```

Testing:

```
NODE_ENV=test
```

Production:

```
NODE_ENV=production
```

Many frameworks automatically change behavior based on this variable.

---

# Checking If a Variable Exists

```bash
if [ -z "$PORT" ]
then
    echo "PORT is not set."
fi
```

Provide a default:

```bash
PORT="${PORT:-3000}"
```

This uses `3000` only if `PORT` is unset or empty.

---

# Hands-on Lab

Create a script named `show-env.sh`.

Requirements:

Display:

- `USER`
- `HOME`
- `SHELL`
- `PWD`
- `HOSTNAME`
- `PATH`

Format the output clearly.

---

# Mini Project

Create `start-server.sh`.

Requirements:

1. Check whether `PORT` exists.
2. If not:

```bash
export PORT=3000
```

1. Print:

```
Starting server on port 3000
```

(You don't need to start a real server yet.)

---

# Common Mistakes

## Forgetting `export`

Wrong:

```bash
PORT=3000
```

If a child process needs the variable, it won't see it.

Correct:

```bash
export PORT=3000
```

---

## Overwriting `PATH`

Wrong:

```bash
export PATH="$HOME/bin"
```

You've removed all the standard system paths.

Commands like `ls` or `git` may stop working.

Correct:

```bash
export PATH="$HOME/bin:$PATH"
```

Always append or prepend to the existing `PATH`.

---

## Committing `.env`

Never commit:

```
JWT_SECRET
DATABASE_PASSWORD
API_KEYS
```

Keep `.env` in `.gitignore`.

---

# Interview Questions

1. What is an environment variable?
2. What does `export` do?
3. What is the difference between a normal variable and an environment variable?
4. What is the purpose of the `PATH` variable?
5. Why are `.env` files used in backend development?
6. Why should `.env` files usually be ignored by Git?
7. How do you provide a default value for an environment variable?

---

# Cheat Sheet

```bash
# Show environment variables
printenv
env

# Read a variable
echo "$HOME"

# Create
export PORT=3000

# Remove
unset PORT

# Reload Zsh config
source ~/.zshrc

# Show PATH
echo "$PATH"

# PATH line by line
echo "$PATH" | tr ':' '\n'

# Add to PATH
export PATH="$HOME/bin:$PATH"

# Default value
PORT="${PORT:-3000}"
```

---

# Weekly Challenge 🚀

Build a script named **`env-doctor.sh`**.

### Requirements

Check that these environment variables exist:

```
HOME
USER
SHELL
PATH
EDITOR
```

If `EDITOR` is missing, automatically set it to:

```
nvim
```

Then display a report:

```
========== Environment Report ==========
✓ HOME
✓ USER
✓ SHELL
✓ PATH
✓ EDITOR (nvim)

PATH Directories:
1. /home/rahul/bin
2. /usr/local/bin
3. /usr/bin
...
```

Finally, verify that these commands can be found through `PATH`:

- `git`
- `node`
- `npm`
- `nvim`

Print whether each one is available.

---

# ⭐ Module 1 Progress

```
✅ Lesson 1 — Introduction
✅ Lesson 2 — Variables & User Input
✅ Lesson 3 — Conditions
✅ Lesson 4 — Loops
✅ Lesson 5 — Functions
✅ Lesson 6 — Command-Line Arguments
✅ Lesson 7 — Arrays
✅ Lesson 8 — Exit Codes
✅ Lesson 9 — Environment Variables

⬜ Lesson 10 — Error Handling
⬜ Lesson 11 — Mini Projects
⬜ Lesson 12 — Final Capstone Project
```

## 💡 Backend Tip

Since you're a **MERN backend developer**, make it a habit to **validate all required environment variables before your application starts**. For example, check that `PORT`, `DATABASE_URL`, and `JWT_SECRET` are present. If any are missing, exit immediately with a clear error message.

Failing fast at startup is much better than discovering configuration problems after your server has already begun handling requests.