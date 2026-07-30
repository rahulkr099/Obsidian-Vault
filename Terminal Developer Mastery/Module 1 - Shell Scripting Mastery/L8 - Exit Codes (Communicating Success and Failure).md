This is one of the most important concepts in Linux.

Many beginners write scripts that print messages like:

```
Everything completed successfully!
```

But Linux doesn't rely on printed messages. It relies on **exit codes**.

Every command, program, and script returns an exit code that tells the operating system whether it succeeded or failed.

This is how tools like **Git, Docker, npm, systemd, cron, GitHub Actions, Jenkins, and CI/CD pipelines** decide what to do next.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Understand what exit codes are
- Check the exit status of commands
- Return custom exit codes from scripts
- Use exit codes in functions
- Build scripts that integrate with automation tools
- Follow Linux exit code conventions

**Estimated Time:** 3–4 hours

**Difficulty:** ⭐⭐⭐☆☆

---

# What is an Exit Code?

Every Linux command returns a number when it finishes.

The shell stores this number in a special variable:

```bash
$?
```

Example:

```bash
echo "Hello"
```

Then immediately run:

```bash
echo $?
```

Output:

```
0
```

`0` means the command succeeded.

---

# Success vs Failure

|Exit Code|Meaning|
|---|---|
|`0`|Success|
|`1`|General error|
|`2`|Incorrect usage or misuse|
|`126`|Command found but not executable|
|`127`|Command not found|
|`130`|Interrupted with `Ctrl + C`|

You don't need to memorize every code, but you should remember:

- `0` = success
- Non-zero = failure

---

# Checking Exit Codes

Example:

```bash
mkdir demo
```

Check:

```bash
echo $?
```

Output:

```
0
```

Now try:

```bash
mkdir demo
```

again.

Output:

```
mkdir: cannot create directory 'demo': File exists
```

Check:

```bash
echo $?
```

Output:

```
1
```

The command failed.

---

# `$?` Must Be Checked Immediately

Wrong:

```bash
mkdir demo

echo "Done"

echo $?
```

The exit code now belongs to `echo`, not `mkdir`.

Correct:

```bash
mkdir demo

status=$?

echo "$status"
```

Always save it if you'll need it later.

---

# Exiting a Script

Use:

```bash
exit NUMBER
```

Success:

```bash
exit 0
```

Failure:

```bash
exit 1
```

Example:

```bash
#!/usr/bin/env bash

echo "Finished"

exit 0
```

---

# Returning Failure

```bash
#!/usr/bin/env bash

echo "Something went wrong."

exit 1
```

Other scripts and tools can now detect that something failed.

---

# Exit Codes in Conditions

Remember this script:

```bash
if command -v git >/dev/null 2>&1
then
    echo "Git installed"
fi
```

Why does it work?

Because:

```bash
command -v git
```

returns:

```
0
```

if Git exists.

Otherwise:

```
1
```

The `if` statement checks the exit code automatically.

---

# Real Backend Example

Check Node.js:

```bash
#!/usr/bin/env bash

if command -v node >/dev/null 2>&1
then
    echo "Node.js installed"
    exit 0
else
    echo "Node.js missing"
    exit 1
fi
```

This script can be used inside another automation.

---

# Returning Exit Codes from Functions

Functions also return exit codes.

Example:

```bash
is_git_installed() {

    if command -v git >/dev/null 2>&1
    then
        return 0
    else
        return 1
    fi

}
```

Use it:

```bash
if is_git_installed
then
    echo "Git OK"
else
    echo "Install Git"
fi
```

---

# Don't Return Strings

Wrong:

```bash
return "Rahul"
```

`return` only accepts numbers between `0` and `255`.

Correct:

```bash
echo "Rahul"
```

Use `echo` for data.

Use `return` for success or failure.

---

# Using Exit Codes with `&&`

```bash
mkdir project && echo "Created successfully"
```

Flow:

```
mkdir succeeds
        │
        ▼
echo runs
```

If `mkdir` fails, `echo` won't run.

---

# Using Exit Codes with `||`

```bash
mkdir project || echo "Creation failed"
```

Flow:

```
mkdir fails
      │
      ▼
echo runs
```

---

# Combining Both

```bash
command -v docker >/dev/null 2>&1 \
    && echo "Docker installed" \
    || echo "Docker missing"
```

This style is common in small scripts, but for larger scripts, `if` statements are usually easier to read.

---

# Backend Example — Deployment Check

```bash
#!/usr/bin/env bash

if ! command -v docker >/dev/null 2>&1
then
    echo "Docker is required."
    exit 1
fi

echo "Starting deployment..."
```

If Docker isn't installed, the deployment stops immediately.

---

# Backend Example — Validate Project

```bash
#!/usr/bin/env bash

if [ ! -f package.json ]
then
    echo "Not a Node.js project."
    exit 1
fi

echo "Project looks valid."
exit 0
```

---

# Backend Example — Script Chaining

Suppose:

```bash
./check-env.sh
```

returns:

```
0
```

Then:

```bash
./check-env.sh && ./deploy.sh
```

Deployment only happens if the environment check succeeds.

This is a common pattern in CI/CD pipelines.

---

# Exit Codes in Loops

```bash
tools=("git" "node" "docker")

for tool in "${tools[@]}"
do
    if command -v "$tool" >/dev/null 2>&1
    then
        echo "✓ $tool"
    else
        echo "✗ $tool"
    fi
done
```

Notice that the loop checks exit codes on each iteration.

---

# Hands-on Lab

Create a script named:

```
check-node.sh
```

Requirements:

- Check if `node` exists.
- If yes:
    - Print:

```
Node.js installed.
```

- Exit with `0`.
- Otherwise:
    - Print:

```
Node.js not installed.
```

- Exit with `1`.

Test it:

```bash
./check-node.sh

echo $?
```

---

# Mini Project

Create:

```
mern-validator.sh
```

Requirements:

Check for:

- Git
- Node.js
- npm
- package.json

If any requirement is missing:

```
Validation failed.
```

Exit:

```
1
```

Otherwise:

```
Environment ready.
```

Exit:

```
0
```

---

# Common Mistakes

## Using `return` Outside a Function

Wrong:

```bash
return 1
```

This only works inside functions.

At the script level, use:

```bash
exit 1
```

---

## Checking `$?` Too Late

Wrong:

```bash
git status

echo "Checking..."

echo $?
```

Correct:

```bash
git status

status=$?

echo "$status"
```

---

## Ignoring Failures

Bad:

```bash
cd project

npm install
```

If `cd` fails, `npm install` runs in the wrong directory.

Better:

```bash
cd project || exit 1

npm install
```

---

# Interview Questions

1. What does an exit code of `0` mean?
2. What is stored in `$?`?
3. What's the difference between `return` and `exit`?
4. Why should scripts return meaningful exit codes?
5. How do `&&` and `||` use exit codes?
6. Why is checking `$?` immediately important?
7. How do CI/CD tools use exit codes?

---

# Cheat Sheet

```bash
# Previous command exit status
echo $?

# Success
exit 0

# Failure
exit 1

# Function success
return 0

# Function failure
return 1

# Stop if command fails
cd project || exit 1

# Run next command only if previous succeeded
command && another_command

# Run next command only if previous failed
command || recovery_command
```

---

# Weekly Challenge 🚀

Build a script called **`dev-ready.sh`**.

### Requirements

The script should:

1. Check for:
    - Git
    - Node.js
    - npm
    - Docker
    - Neovim
2. Verify:
    - `package.json`
    - `.git`
    - `src/`
3. Count how many checks pass.
4. If **all** checks pass:
    - Print:

```
✅ Development environment is ready.
```

- Exit with:

```
0
```

1. Otherwise:
    - Print:

```
❌ Development environment is incomplete.
```

- Show which checks failed.
- Exit with:

```
1
```

This script is very similar to the environment validation steps used before deployments or automated tests.

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

⬜ Lesson 9 — Environment Variables
⬜ Lesson 10 — Error Handling
⬜ Lesson 11 — Mini Projects
⬜ Lesson 12 — Final Capstone Project
```

## 💡 Pro Tip

Exit codes are one of the most important ideas in Linux. You'll see them everywhere:

- `git clone && npm install`
- Docker health checks
- GitHub Actions workflows
- `systemd` service monitoring
- Cron jobs
- Deployment scripts
- Shell pipelines

Understanding exit codes makes it much easier to understand how Linux automation works.

---

## Next Lesson: Lesson 9 — Environment Variables

This lesson is especially valuable for backend developers. You'll learn how to manage configuration securely using variables like:

- `PORT`
- `DATABASE_URL`
- `JWT_SECRET`
- `NODE_ENV`
- `PATH`

You'll also see how `.env` files work with Node.js applications and why environment variables are essential for building secure, deployable backend services.