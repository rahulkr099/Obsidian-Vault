Welcome to one of the most practical lessons in Bash.

So far, your scripts have asked users for input like this:

```bash
read -p "Project name: " project
```

That works, but professional CLI tools usually work like this:

```bash
create-project blog-api
```

or

```bash
git commit -m "Initial commit"
```

Notice that **no questions are asked**. Everything is passed directly on the command line.

That's exactly what you'll learn in this lesson.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Use positional parameters (`$1`, `$2`, ...)
- Understand `$0`, `$#`, `"$@"`, and `$*`
- Validate the number of arguments
- Provide helpful usage messages
- Build professional command-line tools
- Handle arguments safely

**Estimated Time:** 3–4 hours

**Difficulty:** ⭐⭐⭐☆☆

---

# Why Command-Line Arguments?

Imagine you create a project every day.

Interactive version:

```bash
./create-project.sh
```

Output:

```
Project name:
```

You type:

```
blog-api
```

Now imagine doing this 20 times a week.

Instead:

```bash
./create-project.sh blog-api
```

Much faster.

This is how almost every Linux command works.

---

# What is `$0`?

`$0` contains the **script name**.

Example:

```bash
#!/usr/bin/env bash

echo "$0"
```

Run:

```bash
./hello.sh
```

Output:

```
./hello.sh
```

Useful in usage messages.

---

# What is `$1`?

The first argument.

Script:

```bash
#!/usr/bin/env bash

echo "Hello $1"
```

Run:

```bash
./hello.sh Rahul
```

Output:

```
Hello Rahul
```

---

# What is `$2`?

Second argument.

```bash
echo "$1"
echo "$2"
```

Run:

```bash
./info.sh Rahul JavaScript
```

Output:

```
Rahul
JavaScript
```

---

# Multiple Arguments

```bash
#!/usr/bin/env bash

echo "Name : $1"
echo "Language : $2"
echo "Editor : $3"
```

Run:

```bash
./developer.sh Rahul JavaScript nvim
```

Output:

```
Name : Rahul
Language : JavaScript
Editor : nvim
```

---

# What is `$#`?

Number of arguments.

Example:

```bash
echo "$#"
```

Run:

```bash
./script.sh one two three
```

Output:

```
3
```

---

# Validating Arguments

Suppose your script requires one argument.

```bash
#!/usr/bin/env bash

if [ "$#" -ne 1 ]
then
    echo "Usage: $0 <project-name>"
    exit 1
fi

echo "Creating $1"
```

Run:

```bash
./create-project.sh
```

Output:

```
Usage: ./create-project.sh <project-name>
```

Run:

```bash
./create-project.sh blog-api
```

Output:

```
Creating blog-api
```

This is how professional tools guide users.

---

# What is `"$@"`?

`"$@"` means:

> Every argument, preserved exactly as entered.

Example:

```bash
#!/usr/bin/env bash

for arg in "$@"
do
    echo "$arg"
done
```

Run:

```bash
./show.sh apple banana mango
```

Output:

```
apple
banana
mango
```

---

# Why `"$@"` Is Better Than `$*`

Suppose you run:

```bash
./script.sh "My Project" README.md
```

Using `"$@"`:

```
My Project
README.md
```

Using `$*` incorrectly can split `"My Project"` into two words.

**Rule:** In almost all scripts, prefer `"$@"`.

---

# Loop Through Arguments

```bash
#!/usr/bin/env bash

for tool in "$@"
do
    echo "Checking $tool"
done
```

Run:

```bash
./check.sh git node npm docker
```

Output:

```
Checking git
Checking node
Checking npm
Checking docker
```

---

# Backend Example — Tool Checker

```bash
#!/usr/bin/env bash

for tool in "$@"
do
    if command -v "$tool" >/dev/null 2>&1
    then
        echo "✓ $tool installed"
    else
        echo "✗ $tool missing"
    fi
done
```

Run:

```bash
./tool-check.sh git node docker
```

---

# Using Default Values

If no argument is provided:

```bash
project="${1:-demo-project}"

echo "$project"
```

Run:

```bash
./create.sh
```

Output:

```
demo-project
```

Run:

```bash
./create.sh blog-api
```

Output:

```
blog-api
```

---

# Combining Arguments and Functions

```bash
#!/usr/bin/env bash

create_project() {
    mkdir -p "$1"
    echo "Created $1"
}

main() {

    if [ "$#" -ne 1 ]
    then
        echo "Usage: $0 <project-name>"
        exit 1
    fi

    create_project "$1"
}

main "$@"
```

Notice:

```bash
main "$@"
```

passes all script arguments to the `main` function.

---

# Backend Example — Create Multiple Directories

```bash
#!/usr/bin/env bash

for folder in "$@"
do
    mkdir -p "$folder"
    echo "Created $folder"
done
```

Run:

```bash
./mkdirs.sh src tests docs config
```

Output:

```
Created src
Created tests
Created docs
Created config
```

---

# Backend Example — Batch Git Status

```bash
#!/usr/bin/env bash

for repo in "$@"
do
    echo "===== $repo ====="

    if [ -d "$repo/.git" ]
    then
        (
            cd "$repo" || exit
            git status
        )
    else
        echo "Not a Git repository"
    fi
done
```

---

# Special Positional Variables

|Variable|Meaning|
|---|---|
|`$0`|Script name|
|`$1`|First argument|
|`$2`|Second argument|
|`$3`|Third argument|
|`$#`|Number of arguments|
|`"$@"`|All arguments (recommended)|
|`$?`|Exit status of the previous command|
|`$$`|Current script's process ID|

Example:

```bash
echo "PID: $$"
```

---

# Hands-on Lab

Create a script named `greet.sh`.

Requirements:

- Accept one or more names as arguments.
- Greet each person.

Example:

```bash
./greet.sh Rahul Aman Neha
```

Output:

```
Hello Rahul!
Hello Aman!
Hello Neha!
```

---

# Mini Project

Create `project-maker.sh`.

Requirements:

Run:

```bash
./project-maker.sh blog-api
```

Automatically create:

```
blog-api/
├── src/
├── tests/
├── docs/
├── config/
├── scripts/
├── README.md
├── .gitignore
└── package.json
```

If no project name is provided:

```
Usage: ./project-maker.sh <project-name>
```

---

# Common Mistakes

## Forgetting Quotes

❌ Wrong:

```bash
mkdir $1
```

If the argument is:

```
"My Project"
```

it becomes:

```bash
mkdir My Project
```

creating two directories.

✅ Correct:

```bash
mkdir "$1"
```

---

## Forgetting to Validate Arguments

Bad:

```bash
mkdir "$1"
```

If `$1` is empty, unexpected behavior can occur.

Better:

```bash
if [ "$#" -eq 0 ]
then
    echo "Usage: $0 <directory>"
    exit 1
fi
```

---

## Using `$*` Instead of `"$@"`

Prefer:

```bash
for arg in "$@"
```

rather than:

```bash
for arg in $*
```

because `"$@"` preserves each argument correctly.

---

# Interview Questions

1. What is the difference between `$0` and `$1`?
2. What does `$#` represent?
3. Why is `"$@"` preferred over `$*`?
4. How do you display a usage message?
5. How do you check whether a required argument is missing?
6. What does `$$` represent?
7. Why should command-line arguments usually be enclosed in double quotes?

---

# Cheat Sheet

```bash
# Script name
echo "$0"

# First argument
echo "$1"

# Second argument
echo "$2"

# Number of arguments
echo "$#"

# All arguments
echo "$@"

# Process ID
echo "$$"

# Previous command exit status
echo "$?"

# Default value
name="${1:-Guest}"

# Validate argument count
if [ "$#" -ne 1 ]
then
    echo "Usage: $0 <argument>"
    exit 1
fi
```

---

# Weekly Challenge 🚀

Build a command-line tool called `create-node-app.sh`.

It should support:

```bash
./create-node-app.sh my-api
```

### Features

- Validate that exactly one project name is provided.
- Check that `node`, `npm`, and `git` are installed.
- Create the following structure:

```
my-api/
├── src/
├── tests/
├── docs/
├── config/
├── scripts/
├── public/
├── README.md
├── .gitignore
└── package.json
```

- Run:
    - `npm init -y`
    - `git init`
- Print a success summary with the project path.

This project combines everything you've learned so far: **variables, conditions, loops, functions, and command-line arguments**.

---

# ⭐ Module 1 Progress

```
✅ Lesson 1 — Introduction
✅ Lesson 2 — Variables & User Input
✅ Lesson 3 — Conditions
✅ Lesson 4 — Loops
✅ Lesson 5 — Functions
✅ Lesson 6 — Command-Line Arguments

⬜ Lesson 7 — Arrays
⬜ Lesson 8 — Exit Codes
⬜ Lesson 9 — Environment Variables
⬜ Lesson 10 — Error Handling
⬜ Lesson 11 — Mini Projects
⬜ Lesson 12 — Final Capstone Project
```

## Looking Ahead

In **Lesson 7: Arrays**, you'll learn how to work with collections of values. Arrays are extremely useful for tasks like:

- Checking multiple tools (`git`, `node`, `docker`, `nvim`) without repeating code.
- Processing lists of files or directories.
- Managing deployment targets.
- Building more flexible automation scripts.

Arrays will make your Bash code shorter, cleaner, and much easier to extend.