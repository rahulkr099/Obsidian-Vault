> **This lesson teaches you how to capture the output of commands and connect programs together like a professional Linux engineer.**

Almost every Bash script you write from now on will use **command substitution**.

It's how you:

- Read the current date
- Get the current Git branch
- Find files
- Read command output into variables
- Generate dynamic filenames
- Work with APIs
- Build deployment scripts

You'll also learn **process substitution**, a powerful Bash feature that replaces temporary files in many situations.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Capture command output
- Understand command substitution
- Use nested command substitution
- Understand process substitution
- Compare command outputs
- Replace temporary files
- Write cleaner automation scripts

**Estimated Time:** 5–6 hours

**Difficulty:** ⭐⭐⭐⭐☆

---

# What is Command Substitution?

Suppose you run:

```bash
date
```

Output:

```
Fri Jul 25 15:30:42 IST 2026
```

What if you want to store that output?

Command substitution lets you do exactly that.

```bash
today=$(date)

echo "$today"
```

Output:

```
Fri Jul 25 15:30:42 IST 2026
```

Instead of displaying output, it becomes a variable.

---

# Modern Syntax

Always use:

```bash
$(command)
```

Example:

```bash
current_user=$(whoami)

echo "$current_user"
```

Output:

```
rahul
```

---

# Old Syntax (Avoid)

You'll still see this:

```bash
current_user=`whoami`
```

This works...

But it is:

- Harder to read
- Difficult to nest
- Obsolete

Modern Bash uses:

```bash
$(...)
```

---

# Backend Example — Timestamped Backups

```bash
backup_name="backup-$(date +%F).tar.gz"

echo "$backup_name"
```

Output:

```
backup-2026-07-25.tar.gz
```

Every backup gets a unique filename.

---

# Backend Example — Git Branch

```bash
branch=$(git branch --show-current)

echo "$branch"
```

Output:

```
main
```

Useful for deployment scripts.

---

# Backend Example — Current Directory

```bash
project=$(basename "$PWD")

echo "$project"
```

Output:

```
blog-api
```

---

# Command Substitution Inside Strings

```bash
echo "Today is $(date)"
```

Output:

```
Today is Fri Jul 25...
```

Another:

```bash
echo "Current user: $(whoami)"
```

---

# Nested Command Substitution

Example:

```bash
echo "$(basename "$(pwd)")"
```

Flow:

```
pwd

↓

/home/rahul/blog-api

↓

basename

↓

blog-api
```

Nested substitutions are common in production scripts.

---

# Multiple Commands

You can capture multiple commands.

```bash
info=$(
    echo "User: $(whoami)"
    echo "Shell: $SHELL"
)

echo "$info"
```

Output:

```
User: rahul
Shell: /usr/bin/zsh
```

---

# Reading File Contents

Instead of:

```bash
cat version.txt
```

Store it:

```bash
version=$(<version.txt)

echo "$version"
```

This is faster than:

```bash
version=$(cat version.txt)
```

because it avoids launching `cat`.

---

# Counting Files

```bash
count=$(find . -type f | wc -l)

echo "$count"
```

Output:

```
42
```

---

# Capturing Exit Status

Remember:

```bash
output=$(git status)

status=$?
```

The command output and exit code are separate.

---

# Backend Example — Check Node Version

```bash
node_version=$(node --version)

echo "$node_version"
```

Output:

```
v22.10.0
```

Useful for environment validation.

---

# Backend Example — API Response

```bash
response=$(curl -s <https://api.github.com>)
```

Later in Module 2, we'll combine this with `jq` to parse JSON.

---

# What is Process Substitution?

Sometimes a command expects a **file**...

But you have command output.

Instead of creating temporary files...

Use process substitution.

Syntax:

```bash
<(command)
```

or

```bash
>(command)
```

---

# Example — Compare Two Directories

Without process substitution:

```bash
ls dir1 > file1.txt

ls dir2 > file2.txt

diff file1.txt file2.txt
```

Three commands.

Temporary files.

Cleanup required.

With process substitution:

```bash
diff <(ls dir1) <(ls dir2)
```

Done.

No temporary files.

---

# Another Example

Compare sorted files:

```bash
diff <(
    sort users1.txt
) <(
    sort users2.txt
)
```

Very common in Linux.

---

# Backend Example — Compare Dependencies

```bash
diff \
<(sort package1.txt) \
<(sort package2.txt)
```

Useful for checking dependency changes.

---

# Reading Process Output

Example:

```bash
while read -r line
do
    echo "$line"
done < <(ls)
```

Notice:

```bash
< <(...)
```

There is a space.

This is one of Bash's unusual syntaxes.

---

# Why Use Process Substitution?

Without it:

```
Temporary files

↓

Extra cleanup

↓

Slower
```

With it:

```
Command output

↓

Virtual file

↓

Done
```

---

# Real Backend Example — Compare Environments

Development:

```bash
printenv | sort
```

Production:

```bash
ssh server printenv | sort
```

Compare:

```bash
diff \
<(printenv | sort) \
<(ssh server printenv | sort)
```

Very useful for debugging deployment issues.

---

# Real Backend Example — Compare Routes

```bash
diff \
<(find routes1 -type f | sort) \
<(find routes2 -type f | sort)
```

Instant comparison.

---

# Performance Tip

Avoid:

```bash
temp=$(mktemp)

ls > "$temp"

cat "$temp"

rm "$temp"
```

Instead:

```bash
ls | while read -r line
do
    echo "$line"
done
```

Or use process substitution.

---

# Hands-on Lab

Create:

```
system-report.sh
```

Display:

- Date
- User
- Hostname
- Current Directory
- Kernel Version
- Shell
- Uptime

Store every command result in variables before printing.

---

# Mini Project

Create:

```
git-summary.sh
```

Display:

```
Repository

Current Branch

Last Commit

Number of Commits

Remote URL
```

Hints:

```bash
git branch --show-current

git log -1

git rev-list --count HEAD

git remote get-url origin
```

Store each value using command substitution.

---

# Common Mistakes

## Using Backticks

Wrong:

```bash
`date`
```

Correct:

```bash
$(date)
```

---

## Forgetting Quotes

Wrong:

```bash
echo $output
```

Correct:

```bash
echo "$output"
```

Especially important when output contains spaces or newlines.

---

## Using `cat` Unnecessarily

Instead of:

```bash
version=$(cat VERSION)
```

Prefer:

```bash
version=$(<VERSION)
```

This is a Bash optimization.

---

## Confusing `<(...)` With `$(...)`

```bash
$(...)
```

Returns text.

```bash
<(...)
```

Returns a temporary file-like object.

They solve different problems.

---

# Interview Questions

1. What is command substitution?
2. Why is `$(...)` preferred over backticks?
3. How do you store command output in a variable?
4. What is process substitution?
5. When should you use `<(...)`?
6. What's the difference between command substitution and process substitution?
7. Why is `$(<file)` faster than `$(cat file)`?

---

# Cheat Sheet

```bash
# Command substitution
today=$(date)

# Nested
echo "$(basename "$(pwd)")"

# Read file
content=$(<README.md)

# Process substitution
diff <(ls dir1) <(ls dir2)

# While loop
while read -r line
do
    echo "$line"
done < <(ls)

# Multiple commands
info=$(
    date
    whoami
)
```

---

# Weekly Challenge 🚀

Build a tool named **`project-report.sh`**.

Run:

```bash
./project-report.sh
```

Output:

```
========== Project Report ==========

Project Name : blog-api
Current User : rahul
Current Branch : main
Last Commit :
Fix authentication middleware

Total Commits : 52

Node Version : v22.10.0

npm Version : 11.x.x

Current Date :
2026-07-25

Directory Size :
24M

Files :
142

Directories :
18
```

### Rules

- Store every value using **command substitution**.
- Do **not** hardcode any values.
- Use at least **10** command substitutions.
- Use `$(<file)` at least once.
- Format the report neatly.

---

# ⭐ Pro Challenge (Backend Engineer)

Create a script called **`deploy-check.sh`**.

It should:

1. Read the current Git branch.
2. Ensure it's `main`.
3. Read the latest commit message.
4. Check that `package.json` exists.
5. Read the project version from `package.json` (you'll improve this with `jq` in Lesson 10).
6. Display a deployment summary.
7. Exit with status `0` if all checks pass, otherwise `1`.

This is very similar to pre-deployment validation scripts used in real CI/CD pipelines.

---

# ⭐ Module 2 Progress

```
✅ Lesson 1 — Advanced Parameter Expansion
✅ Lesson 2 — Command Substitution & Process Substitution

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

## 💡 Professional Tip

If there's one Bash feature you'll use **every single day** as a backend engineer, it's **command substitution**. You'll use it to:

- Read Git information.
- Capture API responses.
- Generate timestamps.
- Inspect system state.
- Build dynamic filenames.
- Feed data into deployment scripts.

Mastering it now will make the remaining lessons—especially **text processing**, **API automation**, and **deployment scripting**—much more natural.