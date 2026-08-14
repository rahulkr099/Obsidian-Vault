> **"Small scripts solve problems. Modular scripts build systems."**

Most beginners write Bash like this:

```bash
#!/usr/bin/env bash

# 500+ lines...

function1() { ... }
function2() { ... }
function3() { ... }
function4() { ... }

# ...
```

It works... until it doesn't.

Professional Bash projects are organized like Node.js, Python, or Go projects:

```
project/
├── main.sh
├── lib/
│   ├── log.sh
│   ├── file.sh
│   ├── network.sh
│   └── validate.sh
├── config/
├── tests/
└── README.md
```

This lesson teaches you how to write maintainable, reusable Bash code.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Split Bash into modules
- Import reusable libraries
- Write clean functions
- Organize project directories
- Handle errors consistently
- Share common utilities
- Build production-quality Bash projects

**Estimated Time:** 8–10 hours

**Difficulty:** ⭐⭐⭐⭐☆

---

# Why Modularize?

Instead of repeating:

```bash
echo "[INFO] Starting..."
```

in every script, create one reusable logging function.

Benefits:

- Less duplication
- Easier maintenance
- Better testing
- Cleaner code
- Reusability

---

# Project Structure

A professional Bash project might look like:

```
project/
├── main.sh
├── lib/
│   ├── colors.sh
│   ├── log.sh
│   ├── file.sh
│   ├── network.sh
│   ├── string.sh
│   └── validate.sh
├── config/
│   └── config.sh
├── scripts/
├── tests/
├── docs/
└── README.md
```

---

# Importing Libraries

Use:

```bash
source lib/log.sh
```

or

```bash
. lib/log.sh
```

Both do the same thing.

---

# Example Library

`lib/log.sh`

```bash
#!/usr/bin/env bash

log_info() {
    echo "[INFO] $*"
}

log_error() {
    echo "[ERROR] $*" >&2
}

log_warn() {
    echo "[WARN] $*"
}
```

---

Main script:

```bash
#!/usr/bin/env bash

source lib/log.sh

log_info "Application started"

log_warn "Cache almost full"

log_error "Database unavailable"
```

Output:

```
[INFO] Application started
[WARN] Cache almost full
[ERROR] Database unavailable
```

---

# Colors Library

`lib/colors.sh`

```bash
RED="\033[31m"
GREEN="\033[32m"
YELLOW="\033[33m"
BLUE="\033[34m"
RESET="\033[0m"
```

Usage:

```bash
source lib/colors.sh

echo -e "${GREEN}Success${RESET}"
```

---

# Validation Library

`lib/validate.sh`

```bash
require_command() {
    command -v "$1" >/dev/null ||
    {
        echo "$1 not installed"
        exit 1
    }
}
```

Usage:

```bash
source lib/validate.sh

require_command git

require_command curl
```

---

# File Library

```bash
copy_file() {
    cp "$1" "$2"
}

move_file() {
    mv "$1" "$2"
}

delete_file() {
    rm -f "$1"
}
```

---

# String Library

Uppercase:

```bash
to_upper() {
    echo "${1^^}"
}
```

Lowercase:

```bash
to_lower() {
    echo "${1,,}"
}
```

Trim spaces (simple example):

```bash
trim() {
    local s="$1"
    s="${s#"${s%%[![:space:]]*}"}"
    s="${s%"${s##*[![:space:]]}"}"
    printf '%s\n' "$s"
}
```

---

# Network Library

```bash
check_internet() {
    ping -c 1 8.8.8.8 >/dev/null 2>&1
}
```

Usage:

```bash
if check_internet
then
    echo "Online"
else
    echo "Offline"
fi
```

---

# Configuration File

`config/config.sh`

```bash
APP_NAME="MyTool"

LOG_DIR="$HOME/logs"

BACKUP_DIR="$HOME/backups"
```

Main:

```bash
source config/config.sh

echo "$APP_NAME"
```

---

# Returning Values

Wrong:

```bash
my_func() {
    return "Hello"
}
```

`return` is only for numeric exit codes (0–255).

Correct:

```bash
my_func() {
    echo "Hello"
}
```

Capture it:

```bash
value=$(my_func)
```

---

# Exit Codes

Success:

```bash
return 0
```

Failure:

```bash
return 1
```

Example:

```bash
file_exists() {
    [[ -f "$1" ]]
}
```

Usage:

```bash
if file_exists config.json
then
    echo "Found"
fi
```

---

# Local Variables

Always prefer:

```bash
my_function() {
    local name="$1"

    echo "$name"
}
```

instead of:

```bash
name="$1"
```

Local variables avoid accidental conflicts.

---

# Function Naming

Good:

```
log_info
validate_email
backup_database
copy_directory
```

Poor:

```
a
func
run
test
```

Choose descriptive names.

---

# Error Handling

Create:

```bash
die() {
    echo "[ERROR] $*" >&2
    exit 1
}
```

Usage:

```bash
[[ -f config.sh ]] ||
die "Missing configuration."
```

---

# Logging Library (Improved)

```bash
timestamp() {
    date +"%F %T"
}

log_info() {
    echo "$(timestamp) [INFO] $*"
}

log_error() {
    echo "$(timestamp) [ERROR] $*" >&2
}
```

Output:

```
2026-07-25 09:20:11 [INFO] Starting backup
```

---

# Real Backend Example

Instead of repeating:

```bash
curl
jq
grep
```

in every script...

Create:

```
lib/api.sh
```

```bash
api_get() {
    curl -fsSL "$1"
}
```

Now every project can reuse it.

---

# Main Script

```bash
#!/usr/bin/env bash

source lib/log.sh
source lib/colors.sh
source lib/validate.sh
source config/config.sh

require_command curl

log_info "Starting"

echo "$APP_NAME"

echo -e "${GREEN}Done${RESET}"
```

---

# Hands-on Lab

Create:

```
project/
```

Inside:

```
lib/log.sh

lib/file.sh

config/config.sh

main.sh
```

Use every library.

---

# Mini Project

Build:

```
backup-tool/
```

Structure:

```
backup-tool/
├── backup.sh
├── config/
│   └── config.sh
├── lib/
│   ├── log.sh
│   ├── file.sh
│   └── validate.sh
└── backups/
```

Features:

- Read configuration
- Validate dependencies
- Backup directory
- Log progress
- Handle errors

---

# Best Practices

## Use `#!/usr/bin/env bash`

Instead of hardcoding:

```bash
#!/bin/bash
```

This is more portable across systems.

---

## Quote Variables

Wrong:

```bash
cp $src $dst
```

Correct:

```bash
cp "$src" "$dst"
```

---

## Keep Functions Small

Prefer:

```
20–40 lines
```

rather than one giant function.

---

## One Responsibility Per Function

Good:

```
backup_database()
```

Bad:

```
backup_database_and_send_email_and_cleanup_and_restart_server()
```

Split complex work into focused functions.

---

## Separate Configuration

Don't hardcode values inside functions.

Use configuration files.

---

# Common Mistakes

## Global Variables Everywhere

Wrong:

```bash
user="Rahul"
```

inside many functions.

Prefer:

```bash
local user="$1"
```

---

## Duplicating Code

If you copy the same function into multiple scripts, move it into a shared library.

---

## Huge Files

Avoid 1,000-line Bash scripts.

Split them into logical modules.

---

## Mixing Output and Errors

Use:

```bash
echo "Error" >&2
```

for error messages so they go to standard error.

---

# Interview Questions

1. What does `source` do?
2. Why use Bash libraries?
3. What is the difference between `return` and `echo`?
4. Why use `local` variables?
5. Why separate configuration?
6. What makes a good Bash function?
7. How do you organize a large Bash project?

---

# Cheat Sheet

```bash
# Import library
source lib/log.sh

# Local variable
local name="$1"

# Exit success
return 0

# Exit failure
return 1

# Capture output
value=$(my_function)

# Error output
echo "Error" >&2

# Portable shebang
#!/usr/bin/env bash
```

---

# Weekly Challenge 🚀

Build a reusable library called:

```
lib/common.sh
```

It should include:

- Colored logging
- Timestamped logging
- Dependency checking
- File existence validation
- Internet connectivity check
- Confirmation prompt (`yes/no`)
- Temporary directory creation
- Cleanup helper
- Error handling (`die`)
- Progress bar (simple implementation)

Then write three separate scripts that all reuse `common.sh`.

---

# ⭐ Pro Challenge (Backend Engineer)

Build a complete CLI toolkit:

```
devtools/
├── devtools.sh
├── config/
│   └── config.sh
├── lib/
│   ├── api.sh
│   ├── colors.sh
│   ├── file.sh
│   ├── git.sh
│   ├── log.sh
│   ├── network.sh
│   ├── process.sh
│   ├── string.sh
│   └── validate.sh
├── tests/
└── README.md
```

Commands:

```bash
./devtools.sh doctor
./devtools.sh backup
./devtools.sh cleanup
./devtools.sh git-status
./devtools.sh health-check
```

Requirements:

- Each command should use shared libraries instead of duplicating code.
- Configuration should be centralized.
- Logging should be consistent.
- Every function should have a single responsibility.

This mirrors the structure of many mature open-source shell projects.

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
✅ Lesson 9 — Writing Reusable Bash Libraries

⬜ Lesson 10 — API Automation with curl & JSON
⬜ Lesson 11 — Production Automation Projects
⬜ Lesson 12 — Final DevOps Toolkit Capstone
```

---

# 💡 Backend Engineer Insight

As your automation grows, organization becomes just as important as functionality.

This lesson's principles are the same ones you'll see in larger software projects:

- **Node.js** uses modules and packages.
- **Python** organizes code into packages and modules.
- **Go** groups functionality into packages.
- **Bash** achieves similar maintainability with `source`, reusable libraries, and configuration files.

Treat your shell scripts like production code:

- Keep them modular.
- Reuse common functionality.
- Separate configuration from logic.
- Make functions small and focused.

In **Lesson 10**, you'll learn **API Automation with `curl` & JSON**, where you'll interact with REST APIs, send authenticated requests, parse JSON responses with `jq`, automate deployments, monitor services, and integrate Bash with modern backend systems.