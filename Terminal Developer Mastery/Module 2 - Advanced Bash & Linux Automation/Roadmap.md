> **Goal:** Move from writing useful Bash scripts to building professional-grade Linux automation used in backend engineering, DevOps, CI/CD, and system administration.

---

# 🎯 What You'll Build in Module 2

By the end of this module, you'll be able to build tools like:

- 🚀 Deployment automation
- 📦 Backup systems
- 🔍 Log analyzers
- 📊 System monitoring tools
- 🛠️ Server provisioning scripts
- 🔄 CI/CD helper scripts
- 📁 Project scaffolding tools
- 🌐 API automation using `curl`
- 🐳 Docker automation scripts

---

# 📖 Module Overview

|Lesson|Topic|Difficulty|
|---|---|---|
|1|Advanced Parameter Expansion|⭐⭐⭐⭐☆|
|2|Command Substitution & Process Substitution|⭐⭐⭐☆☆|
|3|Here Documents & Here Strings|⭐⭐⭐☆☆|
|4|Advanced Text Processing (`grep`, `sed`, `awk`, `cut`, `sort`, `uniq`, `tr`, `xargs`)|⭐⭐⭐⭐⭐|
|5|Regular Expressions|⭐⭐⭐⭐☆|
|6|Signals, Traps & Process Control|⭐⭐⭐⭐☆|
|7|Background Jobs & Parallel Processing|⭐⭐⭐⭐☆|
|8|Scheduling (`cron`, `at`, `systemd timers`)|⭐⭐⭐⭐☆|
|9|Writing Reusable Bash Libraries|⭐⭐⭐⭐☆|
|10|API Automation with `curl` & JSON|⭐⭐⭐⭐⭐|
|11|Production Automation Projects|⭐⭐⭐⭐⭐|
|12|Final Capstone: Build a Linux DevOps Toolkit|⭐⭐⭐⭐⭐|

---

# 📅 Estimated Duration

- **4–6 weeks**
- Around **45–60 hours**
- **12 lessons**
- **20+ projects**
- **100+ exercises**

---

# Prerequisites

You should already know:

- ✅ Variables
- ✅ Loops
- ✅ Functions
- ✅ Arrays
- ✅ Exit Codes
- ✅ Environment Variables
- ✅ Error Handling

(Completed in Module 1.)

---

# Learning Style

Every lesson follows this structure:

1. Theory
2. Linux internals
3. Syntax
4. Examples
5. Backend use cases
6. Mini projects
7. Common mistakes
8. Interview questions
9. Cheat sheet
10. Weekly challenge

---

# Projects You'll Build

Throughout Module 2, you'll build progressively more advanced tools.

### Project 1 — API Health Checker

```
Check

↓

API Status

↓

Response Time

↓

Status Code

↓

Save Report
```

---

### Project 2 — Docker Manager

```
docker-manager

↓

List Containers

↓

Stop Containers

↓

Restart Containers

↓

Cleanup Images
```

---

### Project 3 — Automatic Log Analyzer

Input:

```
access.log
```

Output:

```
Top IPs

404 Count

500 Errors

Slow Requests

Most Requested Endpoint
```

---

### Project 4 — Deployment Tool

```
Git Pull

↓

npm install

↓

Tests

↓

Build

↓

Restart Server
```

---

### Project 5 — Server Monitor

Checks:

- CPU
- RAM
- Disk
- Network
- Services

Produces:

```
server-report.txt
```

---

### Project 6 — Backup Manager

Supports:

- Full backups
- Incremental backups
- Compression
- Automatic cleanup

---

# Skills You'll Gain

After Module 2 you'll understand:

- Professional Bash scripting
- Linux process management
- Linux scheduling
- Log analysis
- Text processing
- API automation
- Monitoring
- Deployment
- Server maintenance

These are daily tasks for backend and DevOps engineers.

---

# Before We Begin

This module assumes you're using a modern Linux distribution. Based on our previous conversations, your Linux Mint setup with tools like `git`, `curl`, `jq`, `ripgrep`, `fzf`, `zoxide`, `tmux`, and `Neovim` is a great environment for these exercises. You'll get even more value by trying every example directly in your terminal.

---

# ⭐ Lesson 1 Preview

The first lesson is **Advanced Parameter Expansion**.

This is one of Bash's most powerful features.

Instead of writing:

```bash
if [ -z "$PORT" ]
then
    PORT=3000
fi
```

You'll learn to write:

```bash
PORT="${PORT:-3000}"
```

You'll also learn how to:

- Remove prefixes and suffixes
- Replace text inside variables
- Calculate string length
- Extract substrings
- Change letter case
- Validate required variables
- Build cleaner and faster scripts

Mastering parameter expansion will significantly reduce the amount of code you write while making your scripts more expressive.

---

# 🏁 Module 2 Starts Here

In **Lesson 1**, we'll dive deep into **Advanced Parameter Expansion**, one of the most powerful and frequently used features in professional Bash scripting. It's a feature you'll encounter in many open-source shell scripts and production automation tools.