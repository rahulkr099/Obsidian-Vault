> **"This is no longer a Bash script. This is a real software project."**

Congratulations!

By reaching Lesson 12, you've learned enough Bash to build tools that many junior DevOps engineers and backend developers use in production.

This capstone brings **everything** from Module 2 together into one portfolio-quality project.

---

# 🎯 Goal

Build a production-ready CLI application called:

```
devops-toolkit
```

The toolkit should be modular, extensible, and easy to maintain.

Think of it as your own mini version of tools like:

- GitHub CLI (`gh`)
- Docker CLI
- Kubernetes (`kubectl`)
- npm
- pnpm

---

# Project Architecture

```
devops-toolkit/
│
├── toolkit.sh               # Entry point
│
├── config/
│   ├── config.sh
│   └── env.sh
│
├── lib/
│   ├── api.sh
│   ├── backup.sh
│   ├── cleanup.sh
│   ├── colors.sh
│   ├── doctor.sh
│   ├── file.sh
│   ├── git.sh
│   ├── health.sh
│   ├── log.sh
│   ├── network.sh
│   ├── process.sh
│   ├── string.sh
│   ├── system.sh
│   ├── ui.sh
│   └── validate.sh
│
├── commands/
│   ├── doctor.sh
│   ├── backup.sh
│   ├── monitor.sh
│   ├── cleanup.sh
│   ├── analyze.sh
│   ├── repo.sh
│   ├── api.sh
│   ├── health.sh
│   ├── stats.sh
│   └── version.sh
│
├── reports/
│
├── backups/
│
├── logs/
│
├── tmp/
│
├── tests/
│
├── docs/
│
├── README.md
│
└── LICENSE
```

---

# Command Line Interface

The toolkit should behave like:

```bash
toolkit doctor
toolkit backup
toolkit monitor
toolkit cleanup
toolkit analyze
toolkit repo
toolkit api
toolkit health
toolkit stats
toolkit version
toolkit help
```

---

# Dispatcher

Main file:

```bash
case "$1" in

doctor)

    source commands/doctor.sh
    ;;

backup)

    source commands/backup.sh
    ;;

monitor)

    source commands/monitor.sh
    ;;

cleanup)

    source commands/cleanup.sh
    ;;

*)

    help
    ;;
esac
```

Exactly like:

- git
- npm
- docker
- gh

---

# Feature 1 — Linux Doctor

Check:

```
Git
Node
npm
Docker
curl
jq
ripgrep
fd
fzf
bat
tmux
lazygit
yazi
```

Output:

```
✓ Git

✓ Node

✓ npm

✓ jq

✗ Docker

✓ fzf

✓ yazi
```

Bonus:

Show versions.

---

# Feature 2 — Backup Manager

```bash
toolkit backup ~/Projects
```

Creates

```
Projects-2026-07-25.tar.gz
```

Features:

- compression
- timestamp
- checksum
- rotation
- logging

---

# Feature 3 — Repository Manager

Inside:

```
Projects/

App1/

App2/

App3/
```

Run

```
git status

git fetch

git pull
```

in parallel.

---

# Feature 4 — Health Monitor

Check

```
CPU

RAM

Disk

Internet

API

Node Server

Docker
```

Produce report.

---

# Feature 5 — API Client

```bash
toolkit api GET users
```

Example:

```bash
toolkit api GET <https://dummyjson.com/users>
```

Support:

GET

POST

PUT

PATCH

DELETE

---

# Feature 6 — Log Analyzer

Input:

```
access.log
```

Generate:

```
Top IPs

Top URLs

404

500

Average Size

Largest Response

Requests/hour
```

---

# Feature 7 — Project Statistics

Inside a project:

Generate:

```
JS Files

TS Files

CSS Files

HTML Files

Markdown Files

JSON Files

TODO

FIXME

Total LOC
```

---

# Feature 8 — Cleanup

Remove:

```
node_modules

tmp

cache

old logs

old backups
```

Safely.

Support

```bash
--dry-run
```

---

# Feature 9 — Monitoring Dashboard

Print:

```
==========================

System

==========================

CPU

Memory

Disk

Processes

Network

Node

Docker

==========================
```

Refresh every:

```
5 seconds
```

until

```
Ctrl+C
```

---

# Feature 10 — Report Generator

Generate

```
reports/

daily-report.txt
```

Include:

System

Projects

Repositories

Disk

Health

Logs

Backups

---

# Libraries

Everything reusable belongs in:

```
lib/
```

Examples

```
log.sh

colors.sh

validate.sh

network.sh

file.sh
```

---

# Configuration

Never hardcode

```bash
BACKUP_DIR="$HOME/backups"

LOG_DIR="$HOME/logs"

REPORT_DIR="$HOME/reports"

MAX_BACKUPS=20
```

Keep them inside

```
config/config.sh
```

---

# Logging

Every action:

```
2026-07-25 10:15:21

[INFO]

Backup Started
```

Errors:

```
[ERROR]
```

Warnings:

```
[WARN]
```

---

# Error Handling

Every script begins with

```bash
set -euo pipefail
```

Every cleanup

```bash
trap cleanup EXIT
```

Every variable

```bash
"$variable"
```

Every function

```bash
local variable
```

---

# Scheduling

Support:

Cron

Example

```
Daily backup

Weekly cleanup

Hourly monitor
```

Systemd timer version.

---

# Parallel Processing

Whenever possible

```
Git

API

Repositories

Monitoring
```

Run simultaneously.

---

# ShellCheck

Every script

```bash
shellcheck
```

No warnings.

---

# shfmt

Entire project

```bash
shfmt -w .
```

---

# GitHub Repository

Recommended:

```
devops-toolkit/
```

README includes

Installation

Features

Usage

Commands

Examples

Directory Structure

Screenshots

Roadmap

License

---

# Resume Project

You can honestly write:

```
DevOps Toolkit CLI

• Built a modular Linux CLI toolkit using Bash.

• Implemented reusable libraries, logging,
error handling and configuration.

• Added backup management, API automation,
health monitoring, repository management,
parallel execution and scheduling.

• Used curl, jq, grep, awk, sed, cron,
systemd timers, ShellCheck and shfmt.

• Designed production-ready CLI architecture
with modular command system.
```

---

# Interview Questions

Expect questions like

- Why Bash?
- Why modular libraries?
- Why use trap?
- Explain set -euo pipefail
- Why jq over grep?
- Why ShellCheck?
- Explain cron vs systemd timers
- Explain parallel processing

---

# Final Mega Challenge ⭐⭐⭐⭐⭐

Build version **1.0**

Then extend it to

## Version 2

Add

```
Docker Support

Docker Compose

Kubernetes

GitHub API

Slack Notifications

Discord Notifications

Email Reports
```

---

## Version 3

Interactive TUI

Use

```
gum

fzf

whiptail

dialog
```

Menus

Progress bars

Search

Interactive reports

---

## Version 4

Plugin System

Example

```
toolkit plugins install docker

toolkit plugins install aws

toolkit plugins install postgres
```

---

## Version 5

Package Manager

Install

```bash
sudo make install
```

Run globally

```bash
toolkit doctor
```

instead of

```bash
./toolkit.sh doctor
```

---

# 🎉 Module 2 Graduation

```
████████████████████████████

        MODULE 2

          COMPLETE

████████████████████████████

Advanced Bash ✔

Regex ✔

Text Processing ✔

Signals ✔

Parallel Processing ✔

Scheduling ✔

Libraries ✔

API Automation ✔

Production Projects ✔

Capstone ✔
```

---

# 🏆 Skills You've Gained

By completing Module 2, you can now confidently:

### Bash & Linux

- Write advanced Bash scripts
- Build modular CLI applications
- Handle errors and signals
- Schedule recurring tasks
- Run parallel jobs
- Create reusable libraries

### Backend Automation

- Automate REST APIs with `curl`
- Parse JSON using `jq`
- Monitor application health
- Generate system and project reports
- Build backup and maintenance utilities

### Production Practices

- Organize large Bash projects
- Use `ShellCheck` and `shfmt`
- Separate configuration from logic
- Implement logging and cleanup
- Write scripts suitable for real-world environments

---

# 🚀 What Comes Next?

Based on everything we've discussed over the last few weeks—your goal of becoming a strong **MERN backend engineer**, your Linux setup, Neovim, terminal workflow, Git, Docker interest, and Bash skills—the next module I'd recommend is:

# **Module 3 — Docker & Containerization for Backend Engineers**

You'll learn:

1. Docker fundamentals
2. Images vs Containers
3. Writing production Dockerfiles
4. Docker Compose
5. Networking
6. Volumes
7. Multi-stage builds
8. Containerizing Node.js & Express apps
9. MongoDB with Docker
10. Debugging containers
11. Docker security
12. Production deployment with Docker

This naturally builds on Module 2 and prepares you for modern backend development and DevOps workflows.

🎉 Congratulations on completing **Module 2**! This gives you a solid foundation in advanced Bash and Linux automation that will continue to pay dividends throughout your backend engineering journey.