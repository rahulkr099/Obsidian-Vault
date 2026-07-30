This is where your scripts become **intelligent**.

Until now, every script executed every command in order.

Now your script can **make decisions**.

This is one of the most used features in shell scripting.

**Estimated Time:** 3–4 hours

**Difficulty:** ⭐⭐⭐☆☆

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Write `if`, `elif`, and `else` statements.
- Compare numbers and strings.
- Check whether files and directories exist.
- Test command success or failure.
- Validate user input.
- Use logical operators (`&&`, `||`, `!`).
- Write backend-friendly validation scripts.

---

# Why Do We Need Conditions?

Imagine this deployment script:

```bash
git pull
npm install
npm run build
npm start
```

What if `git pull` fails because there's no internet?

The script should stop instead of continuing.

Or imagine:

```bash
if Docker is installed
    start container
else
    show installation message
```

Conditions allow your script to **react** instead of blindly executing commands.

---

# Basic `if` Statement

Syntax:

```bash
if condition
then
    commands
fi
```

Example:

```bash
age=20

if [ "$age" -ge 18 ]
then
    echo "Adult"
fi
```

Output:

```
Adult
```

---

# `if...else`

```bash
age=16

if [ "$age" -ge 18 ]
then
    echo "Adult"
else
    echo "Minor"
fi
```

Output:

```
Minor
```

---

# `if...elif...else`

```bash
marks=75

if [ "$marks" -ge 90 ]
then
    echo "Grade A"

elif [ "$marks" -ge 70 ]
then
    echo "Grade B"

elif [ "$marks" -ge 50 ]
then
    echo "Grade C"

else
    echo "Failed"
fi
```

Output:

```
Grade B
```

---

# Comparison Operators

## Numbers

|Operator|Meaning|
|---|---|
|`-eq`|Equal|
|`-ne`|Not equal|
|`-gt`|Greater than|
|`-lt`|Less than|
|`-ge`|Greater than or equal|
|`-le`|Less than or equal|

Example:

```bash
num=50

if [ "$num" -gt 30 ]
then
    echo "Greater"
fi
```

---

# String Comparisons

```bash
name="Rahul"

if [ "$name" = "Rahul" ]
then
    echo "Welcome!"
fi
```

Not equal:

```bash
if [ "$name" != "Admin" ]
then
    echo "Normal user"
fi
```

---

# Why Double Quotes Matter

Always write:

```bash
if [ "$name" = "Rahul" ]
```

Not:

```bash
if [ $name = Rahul ]
```

If `name` is empty, the second version may produce errors.

---

# File Tests

One of the most useful features for backend developers.

## Check if a file exists

```bash
if [ -f "package.json" ]
then
    echo "Node project detected"
fi
```

---

## Check if a directory exists

```bash
if [ -d "src" ]
then
    echo "Source folder exists"
fi
```

---

## Check if a file is executable

```bash
if [ -x "./deploy.sh" ]
then
    echo "Deployment script ready"
fi
```

---

## Check if a file is readable

```bash
if [ -r "config.env" ]
then
    echo "Configuration can be read"
fi
```

---

## Check if a file is writable

```bash
if [ -w "README.md" ]
then
    echo "README can be edited"
fi
```

---

# Useful File Test Operators

|Test|Meaning|
|---|---|
|`-f`|Regular file exists|
|`-d`|Directory exists|
|`-e`|File or directory exists|
|`-x`|Executable|
|`-r`|Readable|
|`-w`|Writable|
|`-s`|File is not empty|

---

# Checking Command Success

Every Linux command returns an **exit status**.

Success:

```
0
```

Failure:

```
non-zero
```

Example:

```bash
mkdir demo

if mkdir project
then
    echo "Folder created"
else
    echo "Creation failed"
fi
```

---

# Checking Installed Software

Example:

```bash
if command -v node >/dev/null 2>&1
then
    echo "Node.js installed"
else
    echo "Node.js missing"
fi
```

This is how many installation scripts work.

The command:

```bash
command -v git >/dev/null 2>&1
```

checks whether the `git` command is available, while suppressing all output.

### Breakdown

- `command -v git`
    - `command` is a shell builtin.
        
    - `v` asks the shell where it would find the `git` command.
        
    - If Git exists, it prints something like:
        
        ```bash
        /usr/bin/git
        ```
        
        or
        
        ```bash
        git
        ```
        
    - If Git does not exist, it prints nothing and returns a non-zero exit status.
        
- `>/dev/null`
    - Redirects standard output (`stdout`) to `/dev/null` (the "black hole"), so nothing is displayed.
- `2>&1`
    - Redirects standard error (`stderr`) to the same place as standard output.
    - Since stdout is already going to `/dev/null`, stderr also goes there.

### What the command does

It silently checks whether Git is installed.

### How to use it

In shell scripts:

```bash
if command -v git >/dev/null 2>&1; then
    echo "Git is installed."
else
    echo "Git is not installed."
fi
```

### Why use `command -v` instead of `which`?

`command -v` is generally preferred because:

- ✅ It's a POSIX-standard shell builtin.
- ✅ Works in almost all POSIX shells (`bash`, `zsh`, `dash`, etc.).
- ✅ Doesn't rely on an external `which` program.
- ✅ Correctly identifies aliases, shell functions, builtins, and executables.

### Common examples

```bash
command -v python3 >/dev/null 2>&1
command -v docker >/dev/null 2>&1
command -v node >/dev/null 2>&1
command -v nvim >/dev/null 2>&1
```

This is a very common pattern in installation scripts to check whether a required program is available before continuing.

---

# Logical AND (`&&`)

Both conditions must be true.

```bash
age=20
country="India"

if [ "$age" -ge 18 ] && [ "$country" = "India" ]
then
    echo "Eligible"
fi
```

---

# Logical OR (`||`)

At least one condition must be true.

```bash
if [ "$age" -ge 18 ] || [ "$country" = "India" ]
then
    echo "Allowed"
fi
```

---

# Logical NOT (`!`)

Reverse the condition.

```bash
if ! command -v docker >/dev/null 2>&1
then
    echo "Install Docker first"
fi
```

---

# Nested `if`

```bash
age=25

if [ "$age" -ge 18 ]
then
    if [ "$age" -lt 60 ]
    then
        echo "Working age"
    fi
fi
```

---

# Backend Example 1 — Check for `package.json`

```bash
#!/usr/bin/env bash

if [ -f "package.json" ]
then
    echo "Node project found"
else
    echo "Not a Node project"
fi
```

---

# Backend Example 2 — Verify Required Tools

```bash
#!/usr/bin/env bash

if command -v git >/dev/null 2>&1
then
    echo "Git installed"
else
    echo "Git missing"
fi

if command -v node >/dev/null 2>&1
then
    echo "Node installed"
else
    echo "Node missing"
fi

if command -v npm >/dev/null 2>&1
then
    echo "npm installed"
else
    echo "npm missing"
fi
```

---

# Backend Example 3 — Validate User Input

```bash
#!/usr/bin/env bash

read -p "Project name: " project

if [ -z "$project" ]
then
    echo "Project name cannot be empty."
else
    echo "Creating project: $project"
fi
```

Here, `-z` checks whether the string is empty.

---

# Useful String Tests

|Test|Meaning|
|---|---|
|`-z`|String is empty|
|`-n`|String is not empty|

Example:

```bash
name=""

if [ -z "$name" ]
then
    echo "Name is required"
fi
```

---

# Hands-on Lab

Create a script called `environment-check.sh`.

It should:

1. Check if `git` is installed.
2. Check if `node` is installed.
3. Check if `npm` is installed.
4. Check if `docker` is installed.
5. Display a summary like:

```
✓ Git installed
✓ Node installed
✓ npm installed
✗ Docker missing
```

---

# Mini Project — Smart Project Creator

Requirements:

- Ask for a project name.
- If the directory already exists, show:

```
Project already exists.
```

- Otherwise:
    - Create the directory.
    - Create `src`, `tests`, and `README.md`.
    - Print:

```
Project created successfully!
```

---

# Common Mistakes

### Missing Spaces

❌ Wrong:

```bash
if["$age"-gt18]
```

✅ Correct:

```bash
if [ "$age" -gt 18 ]
```

The spaces around `[` and `]` are required.

---

### Forgetting `fi`

Every `if` block must end with:

```bash
fi
```

---

### Comparing Numbers with `=`

❌ Wrong:

```bash
if [ "$age" = 18 ]
```

For numeric comparisons, use:

```bash
if [ "$age" -eq 18 ]
```

---

# Interview Questions

1. What is the difference between `if`, `elif`, and `else`?
2. What does an exit status of `0` mean?
3. How do you check if a directory exists?
4. What is the difference between `f` and `d`?
5. How do you check if a command is installed?
6. What do `z` and `n` do?
7. Why should variables be enclosed in double quotes?

---

# Cheat Sheet

```bash
# Basic if
if [ condition ]
then
    commands
fi

# if...else
if [ condition ]
then
    commands
else
    commands
fi

# Number comparison
-eq
-ne
-gt
-lt
-ge
-le

# String comparison
=
!=

# Empty string
-z

# Non-empty string
-n

# File tests
-f
-d
-e
-r
-w
-x
-s

# Command exists
command -v git >/dev/null 2>&1

# Logical operators
&&
||
!

# Current exit status
echo $?
```

---

# Weekly Challenge 🚀

Build a script named `mern-doctor.sh`.

The script should:

- Check for:
    - Git
    - Node.js
    - npm
    - Docker
    - Neovim
- Verify that the current directory contains:
    - `package.json`
    - `src/`
    - `.git/`
- Display a color-coded summary:
    - 🟢 Passed
    - 🟡 Warning
    - 🔴 Failed
- Exit with a non-zero status if any required dependency is missing.

This is similar to the diagnostic tools many development frameworks provide and is a great real-world scripting exercise.

---

## Next Lesson: Lesson 4 — Loops (`for`, `while`, `until`)

You'll learn how to repeat tasks automatically, such as:

- Creating 100 project folders.
- Renaming hundreds of files.
- Processing log files line by line.
- Backing up multiple directories.
- Running commands over many Git repositories.

This is where shell scripting starts saving you hours of repetitive work.