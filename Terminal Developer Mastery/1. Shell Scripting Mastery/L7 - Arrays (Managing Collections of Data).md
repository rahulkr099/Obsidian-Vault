Welcome to one of the most useful Bash features.

Until now, you've worked with **one value at a time**:

```bash
tool="git"
```

But what if you need to work with:

- Git
- Node.js
- npm
- Docker
- Neovim
- Python

Instead of creating six variables, you use **an array**.

Arrays make your scripts cleaner, shorter, and easier to maintain.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Create arrays
- Access array elements
- Loop through arrays
- Add and remove elements
- Get array length
- Use arrays in backend automation
- Avoid common array mistakes

**Estimated Time:** 3–4 hours

**Difficulty:** ⭐⭐⭐☆☆

---

# What is an Array?

An array stores **multiple values in one variable**.

Instead of:

```bash
tool1="git"
tool2="node"
tool3="npm"
tool4="docker"
```

Use:

```bash
tools=("git" "node" "npm" "docker")
```

Think of it like this:

```
tools

┌─────────┬──────────┐
│ Index   │ Value    │
├─────────┼──────────┤
│ 0       │ git      │
│ 1       │ node     │
│ 2       │ npm      │
│ 3       │ docker   │
└─────────┴──────────┘
```

Bash arrays start at **index 0**.

---

# Creating Arrays

```bash
languages=("JavaScript" "Python" "Go")
```

Another example:

```bash
projects=(
    "blog-api"
    "todo-app"
    "chat-server"
)
```

---

# Accessing Elements

```bash
echo "${languages[0]}"
```

Output:

```
JavaScript
```

```bash
echo "${languages[1]}"
```

Output:

```
Python
```

```bash
echo "${languages[2]}"
```

Output:

```
Go
```

Notice the syntax:

```bash
"${array[index]}"
```

---

# Print All Elements

```bash
echo "${languages[@]}"
```

Output:

```
JavaScript Python Go
```

---

# Difference Between `[@]` and `[*]`

Most of the time, use:

```bash
"${array[@]}"
```

It preserves each element correctly.

Think of it as the array equivalent of `"$@"`.

---

# Number of Elements

```bash
echo "${#languages[@]}"
```

Output:

```
3
```

Useful for validation.

---

# Loop Through an Array

```bash
for language in "${languages[@]}"
do
    echo "$language"
done
```

Output:

```
JavaScript
Python
Go
```

This is the most common way to use arrays.

---

# Loop Using Indexes

```bash
for i in "${!languages[@]}"
do
    echo "$i : ${languages[$i]}"
done
```

Output:

```
0 : JavaScript
1 : Python
2 : Go
```

Explanation:

```bash
"${!languages[@]}"
```

returns the array indexes.

---

# Adding Elements

```bash
tools=("git" "node")

tools+=("docker")
```

Now:

```bash
echo "${tools[@]}"
```

Output:

```
git node docker
```

---

# Replacing Elements

```bash
tools[1]="npm"
```

Now:

```
git npm docker
```

---

# Removing Elements

```bash
unset tools[1]
```

Now:

```
git docker
```

⚠️ Notice:

The index numbers are **not automatically reordered**.

---

# Checking if an Array is Empty

```bash
if [ "${#tools[@]}" -eq 0 ]
then
    echo "No tools found"
fi
```

---

# Backend Example 1 — Check Required Software

Instead of:

```bash
check_tool git
check_tool node
check_tool npm
check_tool docker
```

Use:

```bash
tools=("git" "node" "npm" "docker")

for tool in "${tools[@]}"
do
    check_tool "$tool"
done
```

Much cleaner.

---

# Backend Example 2 — Create Folder Structure

```bash
folders=(
    "src"
    "tests"
    "docs"
    "config"
    "scripts"
)
```

Loop:

```bash
for folder in "${folders[@]}"
do
    mkdir -p "$folder"
done
```

Professional scripts often work like this.

---

# Backend Example 3 — Install Packages

```bash
packages=(
    "curl"
    "git"
    "vim"
)
```

Loop:

```bash
for package in "${packages[@]}"
do
    echo "Installing $package..."
done
```

(Replace `echo` with your package manager command when you're ready.)

---

# Reading Input into an Array

```bash
read -ra names
```

Example:

```
Rahul Aman Neha
```

Now:

```bash
echo "${names[@]}"
```

Output:

```
Rahul Aman Neha
```

---

# Splitting a String

```bash
path="/usr/local/bin"

IFS="/" read -ra parts <<< "$path"

echo "${parts[@]}"
```

Output:

```
usr local bin
```

You'll encounter `IFS` in more advanced scripting.

---

# Associative Arrays (Bonus)

Normal arrays use numbers:

```
0
1
2
```

Associative arrays use keys.

```bash
declare -A ports

ports[http]=80
ports[https]=443
ports[ssh]=22
```

Access:

```bash
echo "${ports[https]}"
```

Output:

```
443
```

This requires Bash 4 or newer (available on modern Linux systems).

---

# Real Backend Example — Project Generator

```bash
folders=(
    src
    tests
    routes
    controllers
    models
    config
    middleware
)
```

Loop:

```bash
for folder in "${folders[@]}"
do
    mkdir -p "$folder"
done
```

Instead of writing seven `mkdir` commands.

---

# Hands-on Lab

Create:

```
create-structure.sh
```

Requirements:

Store these folders in an array:

```
src
controllers
routes
models
middlewares
config
utils
tests
docs
```

Create each directory.

Print:

```
✓ src created
✓ controllers created
...
```

---

# Mini Project

Create:

```
tool-installer.sh
```

Store:

```
git
node
npm
docker
nvim
curl
wget
```

Loop through them.

For each tool:

- Check if it's installed.
- Print:

```
✓ Installed
```

or

```
✗ Missing
```

---

# Common Mistakes

## Forgetting Quotes

Wrong:

```bash
for tool in ${tools[@]}
```

Correct:

```bash
for tool in "${tools[@]}"
```

This prevents problems with elements containing spaces.

---

## Missing Braces

Wrong:

```bash
echo "$tools[0]"
```

Correct:

```bash
echo "${tools[0]}"
```

---

## Using Indexes Incorrectly

Remember:

```
0
1
2
```

Not:

```
1
2
3
```

Arrays start at **0**.

---

# Interview Questions

1. What is an array in Bash?
2. How do you create an array?
3. How do you access the first element?
4. What does `"${array[@]}"` do?
5. How do you find the number of elements?
6. What is an associative array?
7. Why are arrays useful in automation scripts?

---

# Cheat Sheet

```bash
# Create array
tools=("git" "node" "docker")

# First element
echo "${tools[0]}"

# All elements
echo "${tools[@]}"

# Length
echo "${#tools[@]}"

# Loop
for tool in "${tools[@]}"
do
    echo "$tool"
done

# Add
tools+=("npm")

# Replace
tools[0]="curl"

# Remove
unset tools[1]

# Read into array
read -ra names

# Associative array
declare -A ports

ports[http]=80
ports[https]=443
```

---

# Weekly Challenge 🚀

Build a script named **`backend-health-check.sh`**.

### Requirements

Create three arrays:

```
Tools:
git
node
npm
docker
nvim
curl

Directories:
src
tests
config
docs

Files:
package.json
README.md
.gitignore
```

### The script should:

1. Check every tool using a loop.
2. Check every directory exists.
3. Check every file exists.
4. Print a report like:

```
========== Backend Health Check ==========
Tools
✓ git
✓ node
✗ docker

Directories
✓ src
✓ tests
✗ docs

Files
✓ package.json
✓ README.md
✗ .gitignore

Summary
Tools Passed: 5/6
Directories Passed: 3/4
Files Passed: 2/3
```

This is a realistic diagnostic utility similar to the checks performed by many development toolchains.

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

⬜ Lesson 8 — Exit Codes
⬜ Lesson 9 — Environment Variables
⬜ Lesson 10 — Error Handling
⬜ Lesson 11 — Mini Projects
⬜ Lesson 12 — Final Capstone Project
```

## Before Lesson 8

At this point, you've learned enough Bash to build useful automation scripts.

From the next lesson onward, you'll move into topics that make scripts **production-ready**:

- Returning meaningful success or failure statuses.
- Integrating scripts with other commands and CI/CD pipelines.
- Writing automation that behaves like professional Linux tools.

These are the skills that distinguish a simple script from a robust command-line utility.