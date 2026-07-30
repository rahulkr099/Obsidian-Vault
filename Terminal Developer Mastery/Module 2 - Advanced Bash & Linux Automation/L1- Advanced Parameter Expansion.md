> **"This is where Bash starts feeling like a real programming language."**

If Module 1 taught you how to write Bash scripts, Module 2 starts teaching you how to write **professional** Bash scripts.

One feature you'll see repeatedly in high-quality Bash code is **parameter expansion**.

Instead of writing multiple `if` statements, loops, or helper functions, you'll often solve problems with a single expression.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Use advanced parameter expansion
- Set default values
- Enforce required variables
- Replace text inside variables
- Remove prefixes and suffixes
- Extract substrings
- Calculate string lengths
- Change case
- Build cleaner and faster Bash scripts

**Estimated Time:** 5–6 hours

**Difficulty:** ⭐⭐⭐⭐☆

---

# What is Parameter Expansion?

Whenever you write:

```bash
echo "$USER"
```

you're already using **parameter expansion**.

But Bash offers far more powerful forms than just `$variable`.

General syntax:

```bash
${parameter}
```

The braces allow Bash to perform additional operations on the variable.

---

# Why Use `${}` Instead of `$`

Simple:

```bash
name="Rahul"

echo "$name"
```

Works.

But suppose:

```bash
file="project"
```

Wrong:

```bash
echo "$file.txt"
```

Bash looks for a variable named:

```
file.txt
```

Correct:

```bash
echo "${file}.txt"
```

Output:

```
project.txt
```

**Rule:** When concatenating variables with text, prefer `${}`.

---

# Default Values — `${VAR:-default}`

Probably the most useful expansion in Bash.

Example:

```bash
PORT="${PORT:-3000}"

echo "$PORT"
```

If:

```bash
PORT=5000
```

Output:

```
5000
```

If `PORT` isn't set:

Output:

```
3000
```

---

## Why This Is Better

Instead of:

```bash
if [ -z "$PORT" ]
then
    PORT=3000
fi
```

Use:

```bash
PORT="${PORT:-3000}"
```

Cleaner and easier to read.

---

# Assign Default Value — `${VAR:=default}`

Difference:

`:-`

Only **uses** the default.

`:=`

**Assigns** the default.

Example:

```bash
unset PORT

echo "${PORT:=3000}"

echo "$PORT"
```

Output:

```
3000
3000
```

Now `PORT` actually exists.

---

# Required Variables — `${VAR:?message}`

Very useful in production scripts.

Example:

```bash
echo "${DATABASE_URL:?DATABASE_URL is required}"
```

If missing:

```
bash: DATABASE_URL: DATABASE_URL is required
```

The script exits immediately.

Backend example:

```bash
echo "${JWT_SECRET:?Missing JWT_SECRET}"
```

This prevents your application from starting with incomplete configuration.

---

# Alternative Value — `${VAR:+value}`

If the variable exists:

Return another value.

Example:

```bash
export DEBUG=true

echo "${DEBUG:+Debug mode enabled}"
```

Output:

```
Debug mode enabled
```

If `DEBUG` isn't set:

Nothing is printed.

Useful for optional features.

---

# String Length

Example:

```bash
name="Rahul"

echo "${#name}"
```

Output:

```
5
```

Another:

```bash
path="/home/rahul/projects"

echo "${#path}"
```

Useful for validation.

---

# Substrings

Syntax:

```bash
${variable:start:length}
```

Example:

```bash
name="JavaScript"

echo "${name:0:4}"
```

Output:

```
Java
```

Another:

```bash
echo "${name:4}"
```

Output:

```
Script
```

---

# Remove Shortest Prefix

Example:

```bash
path="/home/rahul/project"

echo "${path#*/}"
```

Output:

```
home/rahul/project
```

Removes the shortest match from the beginning.

---

# Remove Longest Prefix

Example:

```bash
path="/home/rahul/project"

echo "${path##*/}"
```

Output:

```
project
```

Very common for extracting filenames.

Equivalent to:

```bash
basename "$path"
```

but without launching another program.

---

# Remove Shortest Suffix

Example:

```bash
file="archive.tar.gz"

echo "${file%.*}"
```

Output:

```
archive.tar
```

Removes only the last extension.

---

# Remove Longest Suffix

```bash
echo "${file%%.*}"
```

Output:

```
archive
```

Useful for generating output filenames.

---

# Replace Text

Example:

```bash
text="Hello World"

echo "${text/World/Linux}"
```

Output:

```
Hello Linux
```

---

# Replace Every Match

```bash
text="cat cat cat"

echo "${text//cat/dog}"
```

Output:

```
dog dog dog
```

---

# Remove Text

Example:

```bash
filename="report.txt"

echo "${filename/.txt/}"
```

Output:

```
report
```

---

# Convert to Uppercase

```bash
language="bash"

echo "${language^^}"
```

Output:

```
BASH
```

---

# Convert to Lowercase

```bash
language="BASH"

echo "${language,,}"
```

Output:

```
bash
```

---

# Capitalize First Letter

```bash
word="linux"

echo "${word^}"
```

Output:

```
Linux
```

---

# Lowercase First Letter

```bash
word="Linux"

echo "${word,}"
```

Output:

```
linux
```

---

# Backend Example — Environment Variables

Instead of:

```bash
if [ -z "$PORT" ]
then
    PORT=3000
fi
```

Use:

```bash
PORT="${PORT:-3000}"
```

---

# Backend Example — File Extension

Input:

```
image.png
```

```bash
file="image.png"

echo "${file%.*}"
```

Output:

```
image
```

---

# Backend Example — Validate Secrets

```bash
: "${DATABASE_URL:?DATABASE_URL missing}"

: "${JWT_SECRET:?JWT_SECRET missing}"
```

Notice:

```bash
:
```

is the **null command**.

It does nothing except trigger parameter expansion.

This is a common Bash idiom in production scripts.

---

# Backend Example — Docker Tags

```bash
tag="node:20-alpine"

echo "${tag%%:*}"
```

Output:

```
node
```

---

# Backend Example — API Version

```bash
url="/api/v1/users"

echo "${url#*/}"
```

Output:

```
api/v1/users
```

---

# Performance Tip

Compare:

```bash
basename "$file"
```

vs

```bash
"${file##*/}"
```

The second version is faster because Bash performs the work internally without starting an external program.

For scripts that process thousands of files, this difference matters.

---

# Hands-on Lab

Create:

```
string-tools.sh
```

The script should:

1. Read a filename.
2. Print:
    - Original name
    - Name without extension
    - Length
    - Uppercase
    - Lowercase
3. Add `.backup` to the filename.

---

# Mini Project

Create:

```
env-validator.sh
```

Requirements:

Required variables:

```
DATABASE_URL
JWT_SECRET
PORT
NODE_ENV
```

Behavior:

- Fail if `DATABASE_URL` is missing.
- Fail if `JWT_SECRET` is missing.
- Default:

```
PORT=3000

NODE_ENV=development
```

Finally print:

```
Environment Ready
```

---

# Common Mistakes

## Forgetting Braces

Wrong:

```bash
echo "$file.txt"
```

Correct:

```bash
echo "${file}.txt"
```

---

## Confusing `:-` and `:=`

```bash
${VAR:-default}
```

Uses a default value.

```bash
${VAR:=default}
```

Creates the variable if it doesn't exist.

---

## Using External Commands Unnecessarily

Instead of:

```bash
basename "$file"
```

Use:

```bash
${file##*/}
```

Instead of:

```bash
dirname "$file"
```

You can often use:

```bash
${file%/*}
```

These expansions avoid launching extra processes.

---

# Interview Questions

1. What is parameter expansion?
2. What's the difference between `$var` and `${var}`?
3. Explain `:-`, `:=`, `:?`, and `:+`.
4. How do you remove a file extension?
5. How do you extract a substring?
6. How do you convert text to uppercase?
7. Why is parameter expansion generally faster than external commands?

---

# Cheat Sheet

```bash
# Default value
${VAR:-default}

# Assign default
${VAR:=default}

# Required
${VAR:?message}

# Alternate value
${VAR:+value}

# Length
${#VAR}

# Substring
${VAR:2:4}

# Remove shortest prefix
${VAR#pattern}

# Remove longest prefix
${VAR##pattern}

# Remove shortest suffix
${VAR%pattern}

# Remove longest suffix
${VAR%%pattern}

# Replace first
${VAR/old/new}

# Replace all
${VAR//old/new}

# Uppercase
${VAR^^}

# Lowercase
${VAR,,}

# Capitalize
${VAR^}
```

---

# Weekly Challenge 🚀

Build a tool called **`filename-manager.sh`**.

### Example

Run:

```bash
./filename-manager.sh archive.tar.gz
```

Output:

```
Original        : archive.tar.gz
Filename        : archive
Last Extension  : gz
Extension Chain : tar.gz
Length          : 14
Uppercase       : ARCHIVE.TAR.GZ
Lowercase       : archive.tar.gz
Backup Name     : archive.tar.gz.backup
Compressed Name : archive.zip
```

### Bonus Challenge ⭐⭐⭐⭐⭐

Support an optional second argument:

```bash
./filename-manager.sh archive.tar.gz zip
```

Output:

```
Converted Name: archive.zip
```

Without using:

- `sed`
- `awk`
- `cut`
- `basename`
- `dirname`

Use **only Bash parameter expansion**.

---

# ⭐ Module 2 Progress

```
✅ Lesson 1 — Advanced Parameter Expansion

⬜ Lesson 2 — Command Substitution & Process Substitution
⬜ Lesson 3 — Here Documents & Here Strings
⬜ Lesson 4 — Advanced Text Processing
⬜ Lesson 5 — Regular Expressions
⬜ Lesson 6 — Signals, Traps & Process Control
⬜ Lesson 7 — Background Jobs & Parallel Processing
⬜ Lesson 8 — Scheduling (cron, at, systemd timers)
⬜ Lesson 9 — Writing Reusable Bash Libraries
⬜ Lesson 10 — API Automation with curl & JSON
⬜ Lesson 11 — Production Automation Projects
⬜ Lesson 12 — Final DevOps Toolkit Capstone
```

## 💡 Backend Engineer Insight

If you browse mature Bash projects—such as package installers, Docker helper scripts, or Linux provisioning tools—you'll see parameter expansion everywhere. It's one of the biggest differences between beginner and professional Bash code because it makes scripts:

- **Shorter** (fewer `if` statements)
- **Faster** (less reliance on external programs)
- **More expressive** (complex logic in concise forms)

Mastering this lesson will make the rest of Module 2 much easier, especially when we begin processing files, automating deployments, and interacting with APIs.