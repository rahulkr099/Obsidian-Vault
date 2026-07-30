> **"If Bash is the language of Linux, text processing is its superpower."**

This is one of the **most important lessons** in the entire course.

Linux treats almost everything as text:

- Logs
- Configuration files
- JSON (before parsing)
- CSV files
- HTTP responses
- Process lists
- Git output
- Docker output
- Kubernetes output

Professional backend engineers spend a huge amount of time filtering, transforming, and analyzing text.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Search text efficiently
- Extract specific fields
- Transform data
- Analyze log files
- Remove duplicates
- Build powerful command pipelines
- Use Linux text-processing tools together

**Estimated Time:** 8–10 hours

**Difficulty:** ⭐⭐⭐⭐⭐

---

# The Unix Philosophy

Instead of one giant program, Linux provides many small tools.

Each does one job well.

```
Log File
    │
    ▼
grep
    │
    ▼
cut
    │
    ▼
sort
    │
    ▼
uniq
    │
    ▼
awk
    │
    ▼
Report
```

Learning to combine these tools is a hallmark of experienced Linux users.

---

# Tool 1 — `grep`

## Purpose

Search for matching text.

Example:

```bash
grep "ERROR" server.log
```

Output:

```
ERROR Database connection failed
ERROR Redis unavailable
```

---

## Ignore Case

```bash
grep -i "error" server.log
```

Matches:

```
ERROR
error
Error
```

---

## Show Line Numbers

```bash
grep -n "ERROR" server.log
```

Output:

```
12:ERROR Database failed

28:ERROR Redis failed
```

---

## Count Matches

```bash
grep -c "ERROR" server.log
```

Output:

```
18
```

---

## Recursive Search

Search every file:

```bash
grep -R "JWT_SECRET" .
```

Great for finding where configuration values are used.

---

## Invert Match

Show lines **not** matching:

```bash
grep -v INFO server.log
```

---

## Match Whole Words

```bash
grep -w user file.txt
```

Matches:

```
user
```

Not:

```
username
```

---

# Tool 2 — `cut`

Extract columns.

CSV:

```
Rahul,22,Bokaro
```

Extract first field:

```bash
cut -d',' -f1 users.csv
```

Output:

```
Rahul
```

---

Extract multiple fields:

```bash
cut -d',' -f1,3 users.csv
```

Output:

```
Rahul,Bokaro
```

---

Extract characters:

```bash
echo "Linux" | cut -c1-3
```

Output:

```
Lin
```

---

# Tool 3 — `sort`

Sort alphabetically.

```bash
sort names.txt
```

---

Reverse:

```bash
sort -r names.txt
```

---

Numeric:

```bash
sort -n scores.txt
```

---

Sort by column:

```bash
sort -k2 marks.csv
```

---

# Tool 4 — `uniq`

Removes adjacent duplicates.

Example:

Input:

```
apple
apple
banana
banana
banana
orange
```

```bash
uniq fruits.txt
```

Output:

```
apple
banana
orange
```

---

Count duplicates:

```bash
uniq -c fruits.txt
```

Output:

```
2 apple
3 banana
1 orange
```

---

⚠️ Important:

`uniq` only removes **adjacent** duplicates.

Always combine with:

```bash
sort file.txt | uniq
```

---

# Tool 5 — `tr`

Translate or delete characters.

Uppercase:

```bash
echo "linux" | tr 'a-z' 'A-Z'
```

Output:

```
LINUX
```

---

Lowercase:

```bash
echo "LINUX" | tr 'A-Z' 'a-z'
```

---

Delete spaces:

```bash
echo "Hello World" | tr -d ' '
```

Output:

```
HelloWorld
```

---

Replace commas:

```bash
echo "a,b,c" | tr ',' '\n'
```

Output:

```
a
b
c
```

---

# Tool 6 — `xargs`

Convert input into command arguments.

Without `xargs`:

```bash
rm file1 file2 file3
```

With a list:

```bash
cat files.txt | xargs rm
```

---

Delete every `.log` file:

```bash
find . -name "*.log" | xargs rm
```

Safer version:

```bash
find . -name "*.log" -print0 | xargs -0 rm
```

The `-print0`/`-0` combination handles filenames containing spaces or special characters.

---

# Tool 7 — `awk`

`awk` is a powerful text processing language.

Input:

```
Rahul 22 Bokaro
```

Print first column:

```bash
awk '{print $1}' users.txt
```

Output:

```
Rahul
```

---

Print second column:

```bash
awk '{print $2}'
```

---

Print multiple:

```bash
awk '{print $1,$3}'
```

Output:

```
Rahul Bokaro
```

---

Sum numbers:

```
10
20
30
```

```bash
awk '{sum+=$1} END {print sum}'
```

Output:

```
60
```

---

Custom delimiter:

CSV:

```
Rahul,22,Bokaro
```

```bash
awk -F',' '{print $1}'
```

---

# Tool 8 — `sed`

Stream editor.

Replace text:

```bash
sed 's/Linux/Bash/' file.txt
```

Replace first occurrence on each line.

---

Replace all:

```bash
sed 's/Linux/Bash/g'
```

---

Delete line 5:

```bash
sed '5d' file.txt
```

---

Print line 10:

```bash
sed -n '10p' file.txt
```

---

Edit file in place:

```bash
sed -i 's/localhost/db.example.com/g' .env
```

Very common during deployments.

---

# Powerful Pipelines

Example:

Top error count:

```bash
grep ERROR server.log | wc -l
```

---

Most common IP:

```bash
awk '{print $1}' access.log \
| sort \
| uniq -c \
| sort -nr \
| head
```

Flow:

```
access.log
     │
     ▼
awk
     │
     ▼
sort
     │
     ▼
uniq -c
     │
     ▼
sort -nr
     │
     ▼
head
```

---

# Backend Example — Count HTTP Status Codes

Apache/Nginx logs:

```
200
404
500
```

```bash
awk '{print $9}' access.log \
| sort \
| uniq -c
```

---

# Backend Example — Find Large Files

```bash
find . -type f \
| xargs du -h \
| sort -hr \
| head
```

Shows the largest files in the current directory tree.

---

# Backend Example — Extract Environment Variables

```bash
grep '^export' ~/.zshrc
```

---

# Backend Example — Find TODO Comments

```bash
grep -R "TODO" src/
```

Useful before releases.

---

# Backend Example — Rename Files

Suppose filenames contain spaces.

```bash
find . -type f -name "* *"
```

You could combine `find`, `xargs`, and a shell loop to rename them safely.

---

# Hands-on Lab

Create:

```
log-summary.sh
```

Given:

```
server.log
```

Print:

- Total lines
- ERROR count
- WARNING count
- INFO count
- First ERROR
- Last ERROR

Use at least:

- `grep`
- `wc`
- `head`
- `tail`

---

# Mini Project

Create:

```
access-analyzer.sh
```

Given:

```
access.log
```

Generate:

```
Top 10 IPs

Top Endpoints

404 Count

500 Count

Total Requests
```

Recommended tools:

- `awk`
- `sort`
- `uniq`
- `grep`
- `head`

---

# Common Mistakes

## Using `cat` Unnecessarily

Avoid:

```bash
cat file | grep ERROR
```

Prefer:

```bash
grep ERROR file
```

This is known as the **Useless Use of `cat` (UUOC)**.

---

## Forgetting to Sort Before `uniq`

Wrong:

```bash
uniq names.txt
```

Correct:

```bash
sort names.txt | uniq
```

---

## Editing Files Without Backup

Instead of:

```bash
sed -i 's/foo/bar/g' file
```

Safer:

```bash
sed -i.bak 's/foo/bar/g' file
```

This creates `file.bak` before modifying the original.

---

## Not Handling Spaces in Filenames

Avoid:

```bash
find . -name "*.txt" | xargs rm
```

Safer:

```bash
find . -name "*.txt" -print0 | xargs -0 rm
```

---

# Interview Questions

1. What's the difference between `grep` and `sed`?
2. When would you use `awk` instead of `cut`?
3. Why does `uniq` usually require `sort`?
4. What's the purpose of `xargs`?
5. How do you replace text in a file?
6. How do you count occurrences of a word?
7. Explain a command pipeline you've built.

---

# Cheat Sheet

```bash
# Search
grep ERROR file

# Ignore case
grep -i error file

# Count
grep -c ERROR file

# Extract CSV column
cut -d',' -f2 file.csv

# Sort numerically
sort -n numbers.txt

# Remove duplicates
sort file | uniq

# Count duplicates
sort file | uniq -c

# Uppercase
tr 'a-z' 'A-Z'

# First column
awk '{print $1}'

# CSV first field
awk -F',' '{print $1}'

# Replace text
sed 's/old/new/g'

# In-place edit
sed -i 's/foo/bar/g' file

# Execute command on input
xargs
```

---

# Weekly Challenge 🚀

Build a tool named:

```
repo-inspector.sh
```

Run it inside a Node.js project.

Generate a report containing:

```
Project Name

Number of JavaScript files

Number of TypeScript files

Number of TODO comments

Number of console.log statements

Number of package.json files

Largest 10 files

Top 10 biggest directories

Total lines of JavaScript
```

Use:

- `find`
- `grep`
- `awk`
- `sort`
- `head`
- `xargs`
- `wc`

---

# ⭐ Pro Challenge (Backend Engineer)

Build:

```
nginx-log-dashboard.sh
```

Input:

```
access.log
```

Generate:

```
========= Daily Report =========

Total Requests : 58213

Unique Visitors : 3278

Top 10 IPs

Top 10 URLs

404 Errors

500 Errors

Most Requested File

Largest Response Size

Average Response Size
```

Use only standard Linux tools—no Python or Node.js.

This mirrors the kind of log analysis many operations teams perform.

---

# ⭐ Module 2 Progress

```
✅ Lesson 1 — Advanced Parameter Expansion
✅ Lesson 2 — Command Substitution & Process Substitution
✅ Lesson 3 — Here Documents & Here Strings
✅ Lesson 4 — Advanced Text Processing

⬜ Lesson 5 — Regular Expressions
⬜ Lesson 6 — Signals, Traps & Process Control
⬜ Lesson 7 — Background Jobs & Parallel Processing
⬜ Lesson 8 — Scheduling (cron, at, systemd timers)
⬜ Lesson 9 — Writing Reusable Bash Libraries
⬜ Lesson 10 — API Automation with curl & JSON
⬜ Lesson 11 — Production Automation Projects
⬜ Lesson 12 — Final DevOps Toolkit Capstone
```

---

## 💡 Backend Engineer Insight

This lesson is arguably the **highest return on investment** in the entire Linux course.

The tools you learned today are used daily to:

- Analyze application and server logs
- Inspect Docker and Kubernetes output
- Parse CI/CD logs
- Search codebases
- Refactor configuration files
- Build monitoring dashboards
- Generate deployment reports

If you're aiming for **backend engineering**, become especially comfortable with:

- ⭐ `grep`
- ⭐ `awk`
- ⭐ `sed`
- ⭐ `sort`
- ⭐ `xargs`

These four tools alone can solve an enormous range of real-world automation tasks.

In **Lesson 5**, we'll dive into **Regular Expressions (Regex)**—the foundation that powers advanced searching with `grep`, text transformation with `sed`, parsing with `awk`, input validation, log filtering, and many backend applications.