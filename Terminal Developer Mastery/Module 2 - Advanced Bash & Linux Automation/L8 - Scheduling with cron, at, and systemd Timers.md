> **"The best automation is the one you don't have to remember to run."**

Scheduling is one of the most valuable Linux skills.

Instead of manually running:

- Backups
- Log cleanup
- Health checks
- Database dumps
- SSL renewal
- Deployment reports

Linux can do it automatically.

As a backend engineer, you'll frequently schedule recurring maintenance and monitoring tasks.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Schedule recurring jobs with `cron`
- Schedule one-time jobs with `at`
- Understand `systemd` timers
- Read and debug scheduled jobs
- Write reliable scheduled scripts
- Avoid common scheduling mistakes

**Estimated Time:** 7–9 hours

**Difficulty:** ⭐⭐⭐⭐☆

---

# Three Scheduling Tools

Linux offers three common approaches:

|Tool|Best For|Modern?|
|---|---|---|
|`cron`|Repeating tasks|✅|
|`at`|One-time future tasks|✅|
|`systemd timers`|Advanced scheduling|⭐ Recommended|

---

# Part 1 — Cron

## What is Cron?

Cron is a background service that executes commands according to a schedule.

Example jobs:

- Every hour
- Every midnight
- Every Monday
- Every 5 minutes

---

# Cron Service

Check whether cron is running:

```bash
systemctl status cron
```

On some distributions (such as Fedora), the service is named `crond`.

Start it:

```bash
sudo systemctl start cron
```

Enable it at boot:

```bash
sudo systemctl enable cron
```

---

# Edit Your Crontab

```bash
crontab -e
```

View jobs:

```bash
crontab -l
```

Remove all jobs:

```bash
crontab -r
```

---

# Cron Format

```
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of week (0–7, Sunday is 0 or 7)
│ │ │ └──── Month (1–12)
│ │ └────── Day of month (1–31)
│ └──────── Hour (0–23)
└────────── Minute (0–59)
```

---

# Every Minute

```
* * * * * echo "Hello"
```

---

# Every Hour

```
0 * * * * script.sh
```

---

# Every Day at Midnight

```
0 0 * * * backup.sh
```

---

# Every Day at 3:30 AM

```
30 3 * * * backup.sh
```

---

# Every Monday

```
0 9 * * 1 report.sh
```

9:00 AM every Monday.

---

# Every 5 Minutes

```
*/5 * * * * health-check.sh
```

---

# Every 15 Minutes

```
*/15 * * * * monitor.sh
```

---

# Every Month

```
0 0 1 * * cleanup.sh
```

Runs on the first day of every month.

---

# Use Absolute Paths

Wrong:

```
0 * * * * backup.sh
```

Correct:

```
0 * * * * /home/rahul/scripts/backup.sh
```

Cron runs with a minimal environment, so always use absolute paths.

---

# Redirect Output

Without redirection:

Cron emails output to the user (if mail is configured).

Instead:

```
0 * * * * /home/rahul/backup.sh >> /home/rahul/logs/backup.log 2>&1
```

Explanation:

- `>>` appends standard output.
- `2>&1` redirects standard error to the same file.

---

# Environment Variables

Cron doesn't load your interactive shell configuration.

If your script needs something like `PATH` or `NODE_ENV`, define it explicitly:

```
PATH=/usr/local/bin:/usr/bin:/bin
NODE_ENV=production
```

or export the variables inside the script.

---

# Part 2 — `at`

Schedule a task **once**.

Install if needed (varies by distribution):

```bash
sudo apt install at
```

Start the service:

```bash
sudo systemctl enable --now atd
```

---

# Schedule a Job

```bash
at 5pm
```

Then type:

```bash
echo "Reminder"
```

Finish with:

```
Ctrl+D
```

---

# Schedule Tomorrow

```bash
at 10am tomorrow
```

---

# Schedule in One Hour

```bash
at now + 1 hour
```

---

# View Jobs

```bash
atq
```

Example:

```
2  Sat Jul 25 17:00
```

---

# Remove a Job

```bash
atrm 2
```

---

# Part 3 — `systemd` Timers

Modern Linux distributions increasingly prefer `systemd` timers over cron for system services.

Advantages:

- Better logging with `journalctl`
- Dependency management
- Missed-job handling (`Persistent=true`)
- Easier integration with services

---

# Service File

Example:

```
backup.service
```

```
[Unit]
Description=Daily Backup

[Service]
Type=oneshot
ExecStart=/home/rahul/scripts/backup.sh
```

---

# Timer File

```
backup.timer
```

```
[Unit]
Description=Run Backup Daily

[Timer]
OnCalendar=daily
Persistent=true

[Install]
WantedBy=timers.target
```

---

# Enable Timer

```bash
sudo systemctl enable --now backup.timer
```

---

# List Timers

```bash
systemctl list-timers
```

---

# Check Logs

```bash
journalctl -u backup.service
```

This is much easier than hunting through log files.

---

# Backend Example — Daily Database Backup

Cron:

```
0 2 * * * /home/rahul/scripts/db-backup.sh
```

Runs every day at 2:00 AM.

---

# Backend Example — SSL Renewal

Many servers schedule:

```bash
certbot renew
```

daily or twice a day.

The renewal only occurs if needed.

---

# Backend Example — Log Cleanup

```
0 1 * * 0 find /var/log/myapp -type f -mtime +30 -delete
```

Deletes log files older than 30 days every Sunday at 1:00 AM.

---

# Backend Example — Health Check

Every 5 minutes:

```
*/5 * * * * /home/rahul/scripts/health-check.sh
```

---

# Backend Example — Docker Cleanup

Weekly:

```
0 4 * * 6 docker system prune -f
```

Removes unused Docker resources every Saturday at 4:00 AM.

---

# Best Practices

## Use Lock Files

Prevent duplicate runs.

Example:

```bash
LOCK="/tmp/backup.lock"

if [ -e "$LOCK" ]
then
    echo "Already running."
    exit 1
fi

touch "$LOCK"

trap 'rm -f "$LOCK"' EXIT
```

---

## Log Everything

```bash
echo "$(date): Backup completed." >> backup.log
```

Logs make scheduled jobs much easier to troubleshoot.

---

## Test Scripts Manually

Before scheduling:

```bash
./backup.sh
```

Never assume cron will fix a broken script.

---

## Use Absolute Paths

Instead of:

```bash
node app.js
```

Prefer:

```bash
/opt/node/bin/node /home/rahul/app.js
```

or ensure `PATH` is correctly configured.

---

# Hands-on Lab

Create:

```
daily-report.sh
```

Requirements:

- Display date
- CPU usage
- Memory usage
- Disk usage
- Uptime

Save the report to:

```
reports/YYYY-MM-DD.txt
```

Then create a cron entry to run it every morning at 8:00 AM.

---

# Mini Project

Create:

```
backup-manager.sh
```

Requirements:

- Compress a chosen directory.
- Save it with today's date.
- Delete backups older than 14 days.
- Log each backup.
- Schedule it to run daily.

---

# Common Mistakes

## Relative Paths

Wrong:

```
backup.sh
```

Correct:

```
/home/rahul/scripts/backup.sh
```

---

## Assuming `.zshrc` Loads

Cron does **not** automatically load your shell configuration.

Load required variables explicitly.

---

## Forgetting Execute Permission

```bash
chmod +x backup.sh
```

Without execute permission, cron cannot run the script directly.

---

## Ignoring Logs

Always capture output:

```
>> backup.log 2>&1
```

Otherwise, debugging becomes much harder.

---

# Interview Questions

1. What is cron?
2. Explain the five cron fields.
3. What is the difference between `cron` and `at`?
4. Why should cron jobs use absolute paths?
5. What are `systemd` timers?
6. Why is `Persistent=true` useful?
7. How do you prevent overlapping scheduled jobs?

---

# Cheat Sheet

```bash
# Edit crontab
crontab -e

# List cron jobs
crontab -l

# Remove cron jobs
crontab -r

# Every 5 minutes
*/5 * * * *

# Every day at midnight
0 0 * * *

# Queue one-time job
at now + 1 hour

# View at jobs
atq

# Remove at job
atrm <job_id>

# List timers
systemctl list-timers

# View logs
journalctl -u backup.service
```

---

# Weekly Challenge 🚀

Build:

```
maintenance-suite.sh
```

Features:

- Backup project directory
- Rotate logs
- Remove temporary files older than 7 days
- Generate a system report
- Write everything to a log file

Then:

- Create a cron job to run daily.
- Create a `systemd` timer version of the same automation.

---

# ⭐ Pro Challenge (Backend Engineer)

Create:

```
server-maintenance.sh
```

Tasks:

1. Check available disk space.
2. Archive logs older than 14 days.
3. Remove backups older than 60 days.
4. Verify that a Node.js application is running.
5. Restart it if necessary.
6. Record every action in a timestamped log.

Design it so it can be executed by either **cron** or a **systemd timer** without modification.

---

# ⭐ Module 2 Progress

```
✅ Lesson 1 — Advanced Parameter Expansion
✅ Lesson 2 — Command Substitution & Process Substitution
✅ Lesson 3 — Here Documents & Here Strings
✅ Lesson 4 — Advanced Text Processing
✅ Lesson 5 — Regular Expressions
✅ Lesson 6 — Signals, Traps & Process Control
✅ Lesson 7 — Background Jobs & Parallel Processing
✅ Lesson 8 — Scheduling (cron, at, systemd timers)

⬜ Lesson 9 — Writing Reusable Bash Libraries
⬜ Lesson 10 — API Automation with curl & JSON
⬜ Lesson 11 — Production Automation Projects
⬜ Lesson 12 — Final DevOps Toolkit Capstone
```

---

# 💡 Backend Engineer Insight

Scheduling is a foundational skill for backend operations.

In production environments, scheduled tasks commonly include:

- Database backups
- Cache cleanup
- SSL certificate renewal
- Log rotation
- Health reports
- Metrics collection
- Temporary file cleanup
- Batch data processing

While `cron` is still widely used, many modern Linux servers rely on **`systemd` timers** because they provide better logging, dependency handling, and recovery from missed executions.

In **Lesson 9**, we'll build **Reusable Bash Libraries**, learning how to organize large Bash projects into modular, maintainable codebases instead of placing everything in a single script. This is the same approach used by many mature open-source shell projects.