> **This lesson transforms your scripts from "it works on my machine" to "it's reliable in production."**

Many beginners write scripts like this:

```bash
#!/usr/bin/env bash

cd project

npm install

npm run build

git add .

git commit -m "Deploy"

git push
```

Looks fine...

But what happens if:

- `project` doesn't exist?
- `npm install` fails?
- `git commit` fails?
- Network disconnects during `git push`?

The script continues running, creating more problems.

Professional scripts **detect errors, stop safely, clean up, and provide useful messages**.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Handle errors correctly
- Stop scripts on failures
- Write cleanup code
- Display useful error messages
- Debug Bash scripts
- Build production-ready automation

**Estimated Time:** 5–6 hours

**Difficulty:** ⭐⭐⭐⭐☆

---

# Why Error Handling Matters

Imagine this deployment script:

```bash
git pull

npm install

npm run build

pm2 restart server
```

If `npm install` fails...

Should the server restart?

**Absolutely not.**

Error handling prevents situations like this.

---

# The Simplest Error Handler

Instead of:

```bash
cd project

npm install
```

Use:

```bash
cd project || exit 1

npm install
```

If `cd` fails...

The script immediately exits.

---

# `set -e`

One of Bash's most useful features.

```bash
#!/usr/bin/env bash

set -e
```

Meaning:

> Exit immediately if any command fails.

Example:

```bash
set -e

mkdir demo

cd demo

false

echo "You won't see this"
```

Output:

```
Script exited.
```

Because:

```bash
false
```

always returns:

```
1
```

---

# Why `set -e` Is Useful

Without it:

```bash
git pull

npm install

npm run build

pm2 restart server
```

Even if `npm install` fails...

The build continues.

With:

```bash
set -e
```

Everything stops immediately.

---

# `set -u`

Detect undefined variables.

Example:

```bash
#!/usr/bin/env bash

set -u

echo "$PORT"
```

If `PORT` doesn't exist:

Output:

```
bash: PORT: unbound variable
```

Instead of silently using an empty value.

---

# `set -x`

Debug mode.

Example:

```bash
set -x

name="Rahul"

echo "$name"
```

Output:

```
+ name=Rahul
+ echo Rahul
Rahul
```

Every command is displayed before execution.

Very useful for debugging.

---

# `set -o pipefail`

Suppose:

```bash
cat missing.txt | grep hello
```

Normally...

The pipeline might hide the original failure.

Use:

```bash
set -o pipefail
```

Now the pipeline fails if **any** command fails.

---

# The Professional Combination

Many production scripts begin with:

```bash
#!/usr/bin/env bash

set -euo pipefail
```

Meaning:

```
-e
Exit on errors

-u
Undefined variables are errors

-o pipefail
Pipelines fail correctly
```

This is considered a best practice for Bash automation.

---

# Writing Your Own Error Function

Instead of repeating:

```bash
echo "Error"

exit 1
```

Create:

```bash
error() {

    echo "ERROR: $1"

    exit 1

}
```

Use:

```bash
[ -f package.json ] || error "package.json not found"
```

Much cleaner.

---

# Logging Functions

```bash
info() {

    echo "[INFO] $1"

}

warn() {

    echo "[WARN] $1"

}

error() {

    echo "[ERROR] $1"

    exit 1

}
```

Example:

```bash
info "Installing packages"

warn "Docker not installed"

error "Git missing"
```

Output:

```
[INFO] Installing packages
[WARN] Docker not installed
[ERROR] Git missing
```

---

# Cleanup with `trap`

Sometimes your script creates temporary files.

If the script crashes...

Those files remain.

Example:

```bash
tmp=$(mktemp)
```

Remove automatically:

```bash
cleanup() {

    rm -f "$tmp"

}

trap cleanup EXIT
```

Now cleanup runs whether the script succeeds or fails.

---

# Catching Ctrl+C

Suppose the user presses:

```
Ctrl+C
```

Handle it:

```bash
cleanup() {

    echo "Interrupted."

}

trap cleanup INT
```

Instead of exiting abruptly.

---

# Backend Example — Safe Deployment

```bash
#!/usr/bin/env bash

set -euo pipefail

[ -f package.json ] || {
    echo "Not a Node project."
    exit 1
}

npm install

npm run build

echo "Deployment ready."
```

Notice how validation happens before expensive work.

---

# Backend Example — Safe Directory Changes

Wrong:

```bash
cd backend

npm install
```

If `backend` doesn't exist...

`npm install` runs in the wrong directory.

Correct:

```bash
cd backend || exit 1

npm install
```

---

# Backend Example — Verify Commands

Instead of:

```bash
npm install
```

Check first:

```bash
command -v npm >/dev/null 2>&1 || {

    echo "npm not installed"

    exit 1

}
```

---

# Backend Example — Temporary Build Folder

```bash
tmp=$(mktemp -d)

cleanup() {

    rm -rf "$tmp"

}

trap cleanup EXIT
```

Even if the script fails...

The temporary directory is removed.

---

# Building a `main()` Function

Professional Bash scripts often look like this:

```bash
#!/usr/bin/env bash

set -euo pipefail

check_tools() {
    :
}

create_project() {
    :
}

main() {

    check_tools

    create_project

}

main "$@"
```

Benefits:

- Easier to read
- Easier to test
- Easier to extend

---

# Hands-on Lab

Create:

```
safe-copy.sh
```

Requirements:

- Accept:

```bash
./safe-copy.sh source.txt destination.txt
```

- Validate:
    - Source exists
    - Two arguments provided
- Copy the file
- Print success
- Exit correctly

---

# Mini Project

Create:

```
mern-deploy-check.sh
```

Requirements:

Check:

- Git
- Node
- npm
- package.json
- .git
- `.env`

If any fail:

```
Deployment aborted.
```

Exit:

```
1
```

Otherwise:

```
Environment verified.
```

Exit:

```
0
```

Use:

- `set -euo pipefail`
- functions
- error handler
- `main()`

---

# Common Mistakes

## Ignoring Command Failures

Bad:

```bash
git pull

npm install

npm run build
```

Good:

```bash
set -e
```

---

## Not Quoting Variables

Wrong:

```bash
rm -rf $folder
```

Correct:

```bash
rm -rf "$folder"
```

Always quote variables unless you specifically need word splitting.

---

## No Cleanup

Bad:

```bash
tmp=$(mktemp)
```

If the script crashes...

The temporary file remains.

Better:

```bash
trap cleanup EXIT
```

---

## Hiding Errors

Avoid this:

```bash
command >/dev/null 2>&1
```

unless you intentionally want to suppress output.

During development, it's often better to let errors be visible.

---

# Interview Questions

1. What does `set -e` do?
2. What does `set -u` do?
3. What is `pipefail`?
4. Why is `trap` useful?
5. What is the purpose of a `main()` function?
6. Why should you check `cd` with `|| exit 1`?
7. Why should temporary files be cleaned up?

---

# Cheat Sheet

```bash
# Exit on errors
set -e

# Undefined variables
set -u

# Debug mode
set -x

# Pipeline failures
set -o pipefail

# Best practice
set -euo pipefail

# Cleanup
trap cleanup EXIT

# Ctrl+C
trap cleanup INT

# Error function
error() {

    echo "$1"

    exit 1

}

# Safe directory change
cd project || exit 1

# Main
main() {

}

main "$@"
```

---

# Weekly Challenge 🚀

Build a production-quality script called **`mern-project-init.sh`**.

### Features

Accept:

```bash
./mern-project-init.sh my-api
```

### Requirements

- Use:

```bash
set -euo pipefail
```

- Validate:
    - Exactly one argument.
    - Git installed.
    - Node installed.
    - npm installed.
- Create:

```
my-api/
├── src/
├── routes/
├── controllers/
├── middleware/
├── models/
├── config/
├── tests/
├── docs/
├── public/
├── package.json
├── README.md
└── .gitignore
```

- Initialize Git.
- Run `npm init -y`.
- Use:
    - `main()`
    - helper functions
    - arrays
    - exit codes
    - error handling
- Print a final summary showing:
    - Project path
    - Number of directories created
    - Number of files created
    - Whether Git initialization succeeded
    - Whether npm initialization succeeded

This challenge combines **everything you've learned in Module 1** into a realistic backend automation tool.

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

⬜ Lesson 11 — Mini Projects
⬜ Lesson 12 — Final Capstone Project
```

---

# 🎓 End of the Core Bash Curriculum

Congratulations! You now understand the core concepts that professional Bash scripts are built on:

- Variables
- User input
- Conditions
- Loops
- Functions
- Command-line arguments
- Arrays
- Exit codes
- Environment variables
- Error handling

The next two lessons are where you'll put all of these concepts together in increasingly realistic projects.

- **Lesson 11** will contain a series of practical mini-projects inspired by real backend development and Linux administration tasks.
- **Lesson 12** will culminate in a full capstone project that resembles a production-ready command-line tool, using the same design patterns found in professional Bash automation.