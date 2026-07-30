> **Theory teaches you syntax. Projects teach you engineering.**

Up to this point, you've learned all the core Bash concepts. Now it's time to use them to solve real problems.

These projects are inspired by tasks that backend developers, DevOps engineers, and Linux administrators perform regularly.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Combine multiple Bash concepts into complete tools
- Organize larger scripts using functions
- Handle errors gracefully
- Build reusable command-line utilities
- Write scripts that are practical in real development workflows

**Estimated Time:** 8–12 hours

**Difficulty:** ⭐⭐⭐⭐☆

---

# Project 1 — MERN Environment Doctor ⭐

## Goal

Check whether a machine is ready for MERN development.

---

## Requirements

Check:

- Git
- Node.js
- npm
- Neovim
- Docker
- curl

Also verify:

- `.git`
- `package.json`
- `.env`

Display:

```
========== MERN Doctor ==========

Tools
✓ Git
✓ Node
✓ npm
✗ Docker

Files
✓ package.json
✓ .env

Git
✓ Repository initialized

Summary

Passed: 8
Failed: 1
```

Exit:

- `0` if everything passes
- `1` otherwise

---

## Concepts Used

- Arrays
- Loops
- Functions
- Exit codes
- Conditions
- Error handling

---

# Project 2 — Project Generator ⭐⭐

Run:

```bash
./project-generator.sh blog-api
```

Automatically create:

```
blog-api/
│
├── src/
│   ├── controllers/
│   ├── routes/
│   ├── middleware/
│   ├── models/
│   ├── services/
│   ├── repositories/
│   ├── config/
│   ├── utils/
│   └── validators/
│
├── tests/
├── docs/
├── scripts/
├── public/
├── logs/
├── package.json
├── README.md
├── .gitignore
└── .env.example
```

Initialize:

```bash
git init
npm init -y
```

---

## Bonus

Automatically install:

```bash
npm install express dotenv cors helmet
```

---

# Project 3 — Automatic Backup Tool ⭐⭐

Run:

```bash
./backup.sh ~/Projects
```

Create:

```
backups/

↓

project-2026-07-25-103000.tar.gz
```

Requirements:

- Timestamp filename
- Compress with `tar`
- Verify backup succeeded
- Delete backups older than 30 days

---

## New Command

```bash
find backups -mtime +30 -delete
```

Very common in Linux administration.

---

# Project 4 — Log Analyzer ⭐⭐⭐

Given:

```
server.log
```

Count:

- Errors
- Warnings
- Requests
- 404 errors

Example:

```
ERROR Database failed
INFO User logged in
WARNING Memory high
ERROR Redis failed
```

Output:

```
Errors : 2
Warnings : 1
Info : 1
```

---

## Useful Commands

```bash
grep
```

```bash
wc -l
```

Example:

```bash
grep ERROR server.log | wc -l
```

---

# Project 5 — Directory Cleaner ⭐⭐

Remove:

```
*.tmp

*.log

node_modules
```

Ask:

```
Delete these files?

[y/N]
```

Only continue if confirmed.

Concepts:

- `find`
- `read`
- `case`
- loops

---

# Project 6 — Git Repository Manager ⭐⭐⭐

Suppose:

```
Projects/

blog/

todo/

chat/

portfolio/
```

Automatically:

For every repository:

```bash
git status
```

Optionally:

```bash
git pull
```

Print:

```
blog ✔

todo ✔

portfolio ✗
```

---

## Useful Command

```bash
find . -name ".git"
```

---

# Project 7 — Package Installer ⭐⭐

Read:

```
packages.txt
```

Example:

```
git

curl

jq

fzf

ripgrep
```

Automatically install each package.

Ubuntu:

```bash
sudo apt install
```

Linux Mint:

```bash
sudo apt install
```

Skip already installed packages.

---

# Project 8 — System Information ⭐⭐

Display:

```
Hostname

OS

Kernel

CPU

RAM

Disk

IP

Uptime

Shell
```

Useful commands:

```bash
hostname
```

```bash
uname -r
```

```bash
free -h
```

```bash
df -h
```

```bash
uptime
```

```bash
ip addr
```

---

# Project 9 — Environment Loader ⭐⭐⭐

Read:

```
.env
```

Export every variable automatically.

Example:

```
PORT=5000

DATABASE_URL=...

JWT_SECRET=...
```

Then:

```bash
source .env
```

Or:

```bash
set -a
source .env
set +a
```

This is similar to how `dotenv` works.

---

# Project 10 — Simple Deployment Script ⭐⭐⭐⭐

Workflow:

```
Check Git

↓

Git Pull

↓

npm install

↓

npm run build

↓

Restart PM2

↓

Success
```

Stop immediately if anything fails.

---

# Recommended Folder Structure

```
bash-projects/

├── project-generator/
├── backup-tool/
├── doctor/
├── deployment/
├── git-manager/
├── cleaner/
├── log-analyzer/
├── package-installer/
├── env-loader/
└── system-info/
```

This makes a great GitHub repository.

---

# Professional Script Template

Most of your future scripts should follow this layout:

```bash
#!/usr/bin/env bash

set -euo pipefail

# -------------------------
# Configuration
# -------------------------

readonly VERSION="1.0.0"

# -------------------------
# Functions
# -------------------------

error() {
    echo "[ERROR] $1"
    exit 1
}

info() {
    echo "[INFO] $1"
}

main() {
    info "Starting..."
}

main "$@"
```

---

# Best Practices Checklist

Every script should aim for:

- ✅ `#!/usr/bin/env bash`
- ✅ `set -euo pipefail`
- ✅ Quote variables (`"$var"`)
- ✅ Use functions
- ✅ Validate arguments
- ✅ Return proper exit codes
- ✅ Use arrays instead of repetition
- ✅ Print useful error messages
- ✅ Clean up temporary files
- ✅ Include a `main()` function

---

# Interview Challenge

Write a script that:

1. Accepts a project name.
2. Creates a Node.js project.
3. Initializes Git.
4. Creates:

```
src/

tests/

README.md
```

1. Checks every command for success.
2. Prints a summary.

This is a common take-home assignment for junior backend roles.

---

# Final Practice Challenge ⭐⭐⭐⭐⭐

Create a tool named:

```
dev-manager
```

Supported commands:

```bash
dev-manager create blog-api

dev-manager doctor

dev-manager backup

dev-manager deploy

dev-manager clean

dev-manager info
```

Example implementation:

```bash
case "$1" in
    create)
        create_project "$2"
        ;;
    doctor)
        run_doctor
        ;;
    backup)
        backup_projects
        ;;
    deploy)
        deploy_project
        ;;
    clean)
        clean_project
        ;;
    info)
        system_info
        ;;
    *)
        usage
        ;;
esac
```

This introduces the idea of building a single CLI with subcommands, similar to tools like `git`, `docker`, and `npm`.

---

# ⭐ Capstone Preparation Checklist

Before moving to Lesson 12, make sure you can confidently:

|Skill|Status|
|---|---|
|Variables|✅|
|User Input|✅|
|Conditions|✅|
|Loops|✅|
|Functions|✅|
|Command-Line Arguments|✅|
|Arrays|✅|
|Exit Codes|✅|
|Environment Variables|✅|
|Error Handling|✅|
|Project Structure|✅|
|Script Organization|✅|

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
✅ Lesson 10 — Error Handling
✅ Lesson 11 — Mini Projects

⬜ Lesson 12 — Final Capstone Project
```

---

# 🎯 Before We Start Lesson 12

The final lesson is not just another script.

You'll build a **production-quality CLI application** called something like **`devtool`**, bringing together everything from Module 1.

It will include:

- Professional directory structure
- Modular functions
- Colored output
- Configuration
- Logging
- Help system (`-help`)
- Version information (`-version`)
- Multiple subcommands
- Robust error handling
- Clean, maintainable code
- Patterns inspired by real open-source command-line tools

This capstone will be something you can genuinely showcase on your GitHub profile as evidence of your Bash and Linux automation skills.