> **Welcome to the final lesson of Module 1.**

Everything you've learned now comes together.

This isn't just another Bash script.

You'll build a real command-line application that looks and feels like professional tools such as:

- `git`
- `npm`
- `docker`
- `gh`
- `pnpm`
- `cargo`

While it won't be as feature-rich, it will follow many of the same engineering principles.

---

# 🎯 Project Overview

You'll build a CLI called:

```
devtool
```

Example usage:

```bash
devtool create blog-api

devtool doctor

devtool info

devtool backup ~/Projects

devtool clean

devtool version

devtool help
```

This single tool will automate many common backend development tasks.

---

# Learning Objectives

By completing this project, you'll learn how to:

- Design a CLI application
- Organize large Bash projects
- Split logic into reusable functions
- Handle multiple commands
- Display colored output
- Write logs
- Validate arguments
- Produce user-friendly help messages
- Follow open-source project conventions

**Estimated Time:** 12–20 hours

**Difficulty:** ⭐⭐⭐⭐⭐

---

# Final Project Structure

```
devtool/

├── devtool
├── lib/
│   ├── create.sh
│   ├── doctor.sh
│   ├── backup.sh
│   ├── clean.sh
│   ├── info.sh
│   ├── utils.sh
│   └── config.sh
│
├── logs/
│
├── README.md
│
├── LICENSE
│
└── install.sh
```

Professional projects separate functionality into modules instead of placing everything in one file.

---

# Main Script

```
devtool
```

Responsibilities:

- Parse command-line arguments
- Load libraries
- Dispatch commands
- Handle errors
- Show help

Think of it as the application's entry point.

---

# Utilities Module

`lib/utils.sh`

Contains reusable functions.

Example:

```bash
info()
warn()
error()
success()

check_command()

confirm()

timestamp()

log()
```

Every other module uses these functions.

---

# Configuration Module

```
lib/config.sh
```

Contains:

```bash
readonly VERSION="1.0.0"

readonly LOG_DIR="$HOME/.devtool"

readonly BACKUP_DIR="$HOME/backups"
```

Keeping configuration separate makes maintenance easier.

---

# Command 1 — `create`

Example:

```bash
devtool create blog-api
```

Creates:

```
blog-api/

├── src/
├── tests/
├── docs/
├── config/
├── public/
├── scripts/
├── README.md
├── .gitignore
├── .env.example
└── package.json
```

Also:

```bash
git init

npm init -y
```

Optional:

```bash
npm install express dotenv cors helmet
```

---

# Command 2 — `doctor`

Checks:

```
Git

Node

npm

Docker

Neovim

curl

jq

fzf

ripgrep
```

Checks project files:

```
package.json

.env

.git
```

Displays:

```
=========================
Development Environment
=========================

✓ Git

✓ Node

✓ npm

✗ Docker

Summary

Passed : 7

Failed : 1
```

---

# Command 3 — `backup`

Run:

```bash
devtool backup ~/Projects
```

Creates:

```
backups/

↓

Projects-2026-07-25-103012.tar.gz
```

Requirements:

- Timestamp filename
- Verify archive creation
- Keep latest backups
- Delete backups older than 30 days

---

# Command 4 — `clean`

Delete:

```
node_modules

dist

coverage

*.log

*.tmp
```

Ask:

```
Delete these files?

[y/N]
```

Never delete automatically without confirmation.

---

# Command 5 — `info`

Display:

```
Hostname

Operating System

Kernel

CPU

Memory

Disk

Shell

IP

Current User

Current Directory

Uptime
```

Bonus:

Show battery level (if available) and load average.

---

# Command 6 — `version`

Display:

```
devtool 1.0.0
```

---

# Command 7 — `help`

Print:

```
Usage:

devtool COMMAND

Commands

create

doctor

backup

clean

info

version

help
```

This is expected for every professional CLI.

---

# Command Dispatcher

Instead of many `if` statements:

```bash
case "$1" in

create)

    create_project "$2"

    ;;

doctor)

    doctor

    ;;

backup)

    backup "$2"

    ;;

clean)

    clean

    ;;

info)

    info_command

    ;;

version)

    version

    ;;

help)

    help

    ;;

*)

    usage

    exit 1

    ;;

esac
```

This is the standard approach for Bash CLIs.

---

# Logging

Create:

```
~/.devtool/devtool.log
```

Log entries:

```
2026-07-25 10:15:21 Created project blog-api

2026-07-25 10:17:01 Backup completed

2026-07-25 10:20:18 Doctor finished
```

Logging makes troubleshooting easier.

---

# Colored Output

```bash
GREEN="\033[32m"
RED="\033[31m"
YELLOW="\033[33m"
BLUE="\033[34m"
RESET="\033[0m"
```

Example:

```bash
echo -e "${GREEN}Success${RESET}"
```

Suggested meanings:

- Green → Success
- Yellow → Warning
- Red → Error
- Blue → Information

---

# Argument Validation

Example:

```bash
devtool create
```

Output:

```
Missing project name.

Usage:

devtool create <project-name>
```

Always validate user input.

---

# Error Handling

Every script:

```bash
#!/usr/bin/env bash

set -euo pipefail
```

Validate commands:

```bash
command -v git >/dev/null 2>&1 || error "Git not installed"
```

---

# Installation Script

Provide:

```bash
./install.sh
```

Responsibilities:

- Make `devtool` executable.
- Create `~/.local/bin` if it doesn't exist.
- Copy `devtool` there.
- Ensure `~/.local/bin` is on the user's `PATH`.
- Print installation instructions.

This gives you a real command-line tool you can run from anywhere.

---

# README

Your README should include:

- Introduction
- Features
- Installation
- Usage
- Commands
- Screenshots (optional)
- Requirements
- License
- Future Improvements

This is excellent practice for GitHub projects.

---

# Stretch Goals ⭐⭐⭐⭐⭐

If you finish early, add these features:

### Configuration File

```
~/.config/devtool/config
```

Store default settings like backup location.

---

### Auto Update Check

Display:

```
A newer version of devtool is available.
```

(You can simulate this by comparing a local version string.)

---

### Progress Indicators

Example:

```
[1/5] Checking Git...

[2/5] Checking Node...

[3/5] Creating folders...
```

This improves user experience for longer-running tasks.

---

### Quiet Mode

```bash
devtool doctor --quiet
```

Only print errors.

---

### Verbose Mode

```bash
devtool doctor --verbose
```

Show every command being executed.

---

### Dry Run

```bash
devtool clean --dry-run
```

Display what would be deleted without actually deleting anything.

---

# Final Challenge

Create **Version 2** of `devtool` with these commands:

```
create

doctor

deploy

backup

restore

clean

logs

update

info

help

version
```

You're now approaching the structure of a real CLI application.

---

# 🎓 Module 1 Graduation Checklist

Before moving on, make sure you can confidently explain and use:

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
|Project Organization|✅|
|CLI Design|✅|

---

# 🏆 What You've Achieved

You can now write Bash scripts that:

- Automate repetitive tasks.
- Validate system requirements.
- Create project scaffolding.
- Perform backups.
- Analyze logs.
- Manage Git repositories.
- Handle errors correctly.
- Use environment variables securely.
- Follow professional Bash coding practices.
- Form the foundation for DevOps and backend automation.

---

# 🚀 What's Next? Module 2 — Advanced Bash & Linux Automation

Module 2 takes your scripting skills to the next level with topics such as:

1. Advanced parameter expansion
2. Command substitution in depth
3. Process substitution
4. Here documents (`<<EOF`) and here strings (`<<<`)
5. Advanced text processing (`grep`, `sed`, `awk`, `cut`, `sort`, `uniq`, `xargs`)
6. Regular expressions
7. Signals and traps in depth
8. Background jobs and job control
9. Process management
10. Scheduling with `cron` and `systemd` timers
11. Writing reusable Bash libraries
12. Building production-grade automation pipelines

---

# 📚 A Recommendation for Your Journey

Since your goal is to become a strong **backend engineer**, don't stop at learning syntax.

For every new Linux concept you learn, ask yourself:

- **Where would I use this in a real backend project?**
- **How could this automate part of my development workflow?**
- **How would this help in deployment, monitoring, or debugging?**

That mindset will help you move beyond "knowing Bash" to becoming an engineer who solves real problems with it.

Congratulations on completing **Module 1: Bash Scripting Fundamentals**! 🎉