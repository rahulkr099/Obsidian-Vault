# Module 2 — Lesson 11: Production Automation Projects ⭐⭐⭐⭐⭐

Now it's time to combine everything you've learned in this module.

A backend engineer rarely writes a script just to learn Bash. They write scripts to automate repetitive work, reduce mistakes, and save time.

This lesson focuses on building production-style automation scripts similar to those used by DevOps engineers, backend developers, SREs, and system administrators.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Design automation workflows
    
- Build reusable production scripts
    
- Handle failures gracefully
    
- Generate logs and reports
    
- Validate user input
    
- Write maintainable automation
    
- Chain multiple Linux tools together
    

---

# What Makes a Script "Production Ready"?

A beginner script:

```bash
git pull
npm install
npm start
```

A production script:

- validates prerequisites
    
- logs everything
    
- handles errors
    
- supports options
    
- cleans temporary files
    
- sends notifications
    
- returns meaningful exit codes
    

Production scripts are designed for **reliability**, not just correctness.

---

# Project 1 — Smart Deployment Script

Imagine deploying your Node.js backend.

Instead of manually typing:

```
git pull
npm install
npm test
npm run build
pm2 restart api
```

Create one script.

```
deploy.sh

↓

Pull latest code

↓

Install packages

↓

Run tests

↓

Build

↓

Restart server

↓

Write deployment log
```

Example:

```bash
#!/bin/bash
set -e

echo "Pulling latest code..."
git pull

echo "Installing packages..."
npm install

echo "Running tests..."
npm test

echo "Building..."
npm run build

echo "Restarting..."
pm2 restart api

echo "Deployment completed."
```

`set -e` stops the script if any command fails.

---

# Improving the Deployment Script

Instead of:

```bash
echo "Running..."
```

Use timestamps.

```bash
log() {
    echo "[$(date '+%F %T')] $1"
}
```

Example:

```bash
log "Starting deployment"
```

Output:

```
[2026-07-30 22:10:01] Starting deployment
```

Professional scripts always include timestamps.

---

# Save Logs

```bash
LOG="deploy.log"

exec > >(tee -a "$LOG") 2>&1
```

Now every output goes to:

```
deploy.log
```

and

```
terminal
```

simultaneously.

---

# Project 2 — Server Health Checker

Collect system information automatically.

Information:

```
CPU

RAM

Disk

Uptime

Load Average

Top Memory Process
```

Example:

```bash
#!/bin/bash

echo "===== SERVER REPORT ====="

echo
echo "CPU"
lscpu | head

echo
echo "Memory"
free -h

echo
echo "Disk"
df -h

echo
echo "Uptime"
uptime
```

Save it:

```bash
./monitor.sh > report.txt
```

---

# Adding Color

```bash
GREEN="\e[32m"
RED="\e[31m"
RESET="\e[0m"

echo -e "${GREEN}Healthy${RESET}"
```

Useful for terminal dashboards.

---

# Disk Alert Example

```bash
usage=$(df / | awk 'NR==2 {print $5}' | tr -d '%')

if (( usage > 80 ))
then
    echo "Disk almost full!"
fi
```

---

# Project 3 — Backup Automation

Steps:

```
Choose directory

↓

Compress

↓

Timestamp filename

↓

Store backup

↓

Delete old backups
```

Example:

```bash
#!/bin/bash

SOURCE="$HOME/projects"

DEST="$HOME/backups"

DATE=$(date +%F-%H%M)

tar -czf "$DEST/backup-$DATE.tar.gz" "$SOURCE"
```

---

# Delete Old Backups

Older than 7 days:

```bash
find "$DEST" -name "*.tar.gz" -mtime +7 -delete
```

Very common in production.

---

# Project 4 — Automatic Log Analyzer

Input:

```
access.log
```

Output:

```
Top IPs

404 errors

500 errors

Most visited endpoint

Requests per minute
```

Top IPs:

```bash
awk '{print $1}' access.log |
sort |
uniq -c |
sort -nr |
head
```

404 count:

```bash
grep ' 404 ' access.log | wc -l
```

500 count:

```bash
grep ' 500 ' access.log | wc -l
```

Most requested URL:

```bash
awk '{print $7}' access.log |
sort |
uniq -c |
sort -nr |
head
```

---

# Project 5 — Docker Cleanup

List containers:

```bash
docker ps
```

Remove stopped:

```bash
docker container prune -f
```

Remove dangling images:

```bash
docker image prune -f
```

Combined:

```bash
docker system prune -f
```

Great for CI servers.

---

# Project 6 — API Health Monitor

Check:

- response time
    
- HTTP status
    
- JSON response
    

Example:

```bash
status=$(curl -o /dev/null -s -w "%{http_code}" https://example.com)

if [[ "$status" == "200" ]]
then
    echo "Healthy"
else
    echo "Down"
fi
```

Response time:

```bash
curl -o /dev/null \
-s \
-w "%{time_total}\n" \
https://example.com
```

---

# Project 7 — Automatic Service Restarter

Suppose nginx crashes.

```bash
if ! systemctl is-active --quiet nginx
then
    systemctl restart nginx
fi
```

This is common in monitoring systems.

---

# Project 8 — Git Automation

Show repository status:

```bash
git fetch

git status

git log --oneline -5
```

Automatic commit:

```bash
git add .

git commit -m "Daily backup"

git push
```

---

# Project 9 — Project Generator

Instead of creating folders manually:

```
mkdir project

mkdir src

mkdir tests

touch README.md
```

Automate:

```bash
mkdir -p "$1"/{src,tests,docs}

touch "$1"/README.md
```

Run:

```bash
./new-project.sh blog-api
```

Result:

```
blog-api/

src/

tests/

docs/

README.md
```

---

# Project 10 — CI/CD Helper

Pipeline:

```
Lint

↓

Test

↓

Build

↓

Deploy
```

Example:

```bash
npm run lint &&
npm test &&
npm run build &&
./deploy.sh
```

If lint fails:

```
↓

Stop immediately
```

No deployment happens.

---

# Using Functions

Instead of:

```bash
echo "Testing"

npm test

echo "Done"
```

Create:

```bash
run_step() {
    echo
    echo "== $1 =="

    shift

    "$@"
}
```

Use:

```bash
run_step "Installing" npm install

run_step "Testing" npm test

run_step "Building" npm run build
```

Cleaner and reusable.

---

# Progress Indicator

```bash
echo "[1/5] Pull"

echo "[2/5] Install"

echo "[3/5] Test"

echo "[4/5] Build"

echo "[5/5] Deploy"
```

Users know what is happening.

---

# Error Handler

```bash
trap 'echo "Deployment failed."' ERR
```

Useful with:

```bash
set -e
```

---

# Configuration File

Instead of hardcoding:

```bash
PORT=3000
```

Read:

```bash
source config.env
```

Example:

```
PORT=8080

HOST=localhost
```

---

# Notifications

Terminal:

```bash
echo "Deployment finished."
```

Desktop notification (Linux):

```bash
notify-send "Deployment Complete"
```

---

# Script Structure

A good production script often looks like this:

```
Configuration

↓

Functions

↓

Validation

↓

Main Logic

↓

Cleanup

↓

Exit
```

Example:

```text
deploy.sh

├── variables
├── functions
├── checks
├── deployment
├── cleanup
└── exit
```

This structure makes scripts easier to maintain.

---

# Production Practices

- Use `#!/bin/bash` (or `#!/usr/bin/env bash` for portability).
    
- Enable strict mode where appropriate:
    

```bash
set -euo pipefail
```

- Quote variable expansions:
    

```bash
"$file"
```

- Validate required commands:
    

```bash
command -v git >/dev/null || {
    echo "git not installed"
    exit 1
}
```

- Keep configuration separate from code.
    
- Break large scripts into functions.
    
- Use meaningful exit codes.
    
- Log important actions with timestamps.
    
- Test scripts in a safe environment before running them on production servers.
    

---

# Common Mistakes

❌ Hardcoding paths

```bash
/home/user/project
```

✔ Better:

```bash
PROJECT_DIR="${PROJECT_DIR:-$HOME/project}"
```

---

❌ Ignoring failures

```bash
git pull
npm install
npm run build
```

If `git pull` fails, the script still continues.

✔ Better:

```bash
set -e
```

or check exit codes explicitly.

---

❌ Running destructive commands without confirmation

```bash
rm -rf "$TARGET"
```

For interactive tools, confirm first or provide a `--force` option.

---

❌ Not quoting variables

```bash
rm $file
```

✔ Better:

```bash
rm "$file"
```

---

# Mini Project

Build a **Developer Maintenance Toolkit** called `dev-maintenance.sh`.

It should:

1. Check if Git is installed.
    
2. Check available disk space.
    
3. Show memory usage.
    
4. Run `git status` in the current repository (if applicable).
    
5. Create a timestamped backup of a chosen directory.
    
6. Save everything into `maintenance.log`.
    
7. Print a final summary with success or failure.
    

---

# Interview Questions

**1. Why use `set -euo pipefail`?**

To make scripts fail early on errors, catch unset variables, and detect failures inside pipelines.

---

**2. Why are logs important?**

They help debug failures, audit actions, and understand what happened during automation.

---

**3. Why use functions?**

They improve readability, reduce duplication, and make scripts easier to test and maintain.

---

**4. What is idempotency?**

An idempotent script can be run multiple times and still produce the same desired state without causing unintended side effects. This is a key concept in deployment and infrastructure automation.

---

# Cheat Sheet

|Task|Command/Technique|
|---|---|
|Stop on errors|`set -e` or `set -euo pipefail`|
|Timestamp|`date '+%F %T'`|
|Log to file and terminal|`exec > >(tee -a logfile) 2>&1`|
|Backup|`tar -czf archive.tar.gz dir/`|
|Delete old backups|`find dir -mtime +7 -delete`|
|Check service|`systemctl is-active --quiet service`|
|Check HTTP status|`curl -w "%{http_code}"`|
|Disk usage|`df -h`|
|Memory usage|`free -h`|
|Uptime|`uptime`|
|Docker cleanup|`docker system prune -f`|

---

# What's Next?

In **Lesson 12**, you'll build a **Linux DevOps Toolkit** as a capstone project.

You'll combine everything from Modules 1 and 2 into a professional command-line toolkit with multiple subcommands, reusable libraries, configuration files, logging, error handling, and real-world automation features. This project will resemble the kind of internal tools used by backend and DevOps teams in production.