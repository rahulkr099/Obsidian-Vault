Congratulations! 🎉

You're now learning a feature that separates beginner scripts from professional ones.

Until now, your scripts looked like this:

```bash
echo "Checking Git..."
command -v git

echo "Checking Node..."
command -v node

echo "Checking npm..."
command -v npm
```

Notice how the same logic is repeated.

A better approach is to write the logic **once** and reuse it.

That's exactly what **functions** do.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Create functions
- Pass arguments to functions
- Return success or failure
- Use local variables
- Organize large scripts
- Build reusable utilities
- Write cleaner, maintainable Bash code

**Estimated Time:** 4–5 hours

**Difficulty:** ⭐⭐⭐☆☆

---

# What is a Function?

A function is a **named block of code which can be reused multiple times.**

Instead of copying code multiple times, you call the function whenever you need it.

Think of it like this:

```
Function

↓

Small machine

↓

Input

↓

Processing

↓

Output
```

---

# Why Functions Matter

Without functions:

```bash
echo "Checking Git..."
command -v git

echo "Checking Node..."
command -v node

echo "Checking Docker..."
command -v docker
```

Lots of repeated code.

With functions:

```bash
check_tool git
check_tool node
check_tool docker
```

Much cleaner.

---

# Creating Your First Function

Syntax:

```bash
function_name() {
    commands
}
```

Example:

```bash
greet() {
    echo "Hello Rahul!"
}
```

Call it:

```bash
greet
```

Output:

```
Hello Rahul!
```

---

# Another Example

```bash
welcome() {
    echo "Welcome"
    echo "Happy Coding!"
}

welcome
```

Output:

```
Welcome
Happy Coding!
```

---

# Functions Can Be Called Many Times

```bash
hello() {
    echo "Hello!"
}

hello
hello
hello
```

Output

```
Hello!
Hello!
Hello!
```

---

# Function Parameters

Functions can receive arguments.

Example:

```bash
greet() {
    echo "Hello $1"
}

greet Rahul
```

Output

```
Hello Rahul
```

---

# Multiple Parameters

```bash
developer() {
    echo "Name : $1"
    echo "Language : $2"
}

developer Rahul JavaScript
```

Output

```
Name : Rahul
Language : JavaScript
```

---

# Understanding `$1`, `$2`, `$3`

Suppose:

```bash
deploy production main
```

Inside the function

```
$1 → production

$2 → main
```

---

# All Arguments

```bash
show() {
    echo "$@"
}

show git node npm docker
```

Output

```
git node npm docker
```

`"$@"` means:

> Every argument separately.

This is preferred over `$*` in most cases.

---

# Number of Arguments

```bash
count() {
    echo "Arguments: $#"
}

count a b c
```

Output

```
Arguments: 3
```

---

# Local Variables

Avoid modifying global variables accidentally.

```bash
name="Rahul"

show() {
    local name="Aman"
    echo "$name"
}

show

echo "$name"
```

Output

```
Aman
Rahul
```

Without `local`, both would become `Aman`.

---

# Returning Success or Failure

Functions don't return strings like Python or JavaScript.

Instead, they return an **exit status**.

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
is_node_installed() {

    if command -v node >/dev/null 2>&1
    then
        return 0
    else
        return 1
    fi

}
```

Use it:

```bash
if is_node_installed
then
    echo "Node found"
else
    echo "Install Node"
fi
```

---

# Returning Data

Instead of `return`, print the value.

Example:

```bash
current_user() {
    echo "$USER"
}

user=$(current_user)

echo "$user"
```

Output

```
Rahul
```

---

# Backend Example 1 — Check Installed Software

```bash
check_tool() {

    if command -v "$1" >/dev/null 2>&1
    then
        echo "✓ $1 installed"
    else
        echo "✗ $1 missing"
    fi

}
```

Use

```bash
check_tool git
check_tool node
check_tool docker
check_tool npm
```

Output

```
✓ git installed
✓ node installed
✗ docker missing
✓ npm installed
```

---

# Backend Example 2 — Create Project Folder

```bash
create_folder() {

    mkdir -p "$1"

    echo "$1 created"

}
```

Use

```bash
create_folder src
create_folder tests
create_folder config
```

---

# Backend Example 3 — Print Heading

```bash
heading() {

    echo
    echo "===================="
    echo "$1"
    echo "===================="

}
```

Use

```bash
heading "Checking Environment"
```

Output

```
====================
Checking Environment
====================
```

---

# Combining Functions

```bash
heading() {
    echo
    echo "==== $1 ===="
}

check_tool() {

    if command -v "$1" >/dev/null
    then
        echo "✓ $1"
    else
        echo "✗ $1"
    fi

}

heading "Environment"

check_tool git
check_tool node
check_tool npm
```

Notice how small functions work together.

---

# Function Call Order

Functions should usually be defined before they're called.

```bash
hello() {
    echo "Hello"
}

hello
```

---

# Organizing Scripts

Professional scripts often look like this:

```
Functions

↓

Variables

↓

Main Logic
```

Example

```bash
#!/usr/bin/env bash

check_tool() {
    ...
}

create_project() {
    ...
}

main() {

    check_tool git
    create_project blog-api

}

main
```

This makes scripts much easier to read and maintain.

---

# Hands-on Lab

Create a script named:

```
tool-check.sh
```

Requirements:

Create a function

```bash
check()
```

It should

- Accept a tool name
- Check whether it's installed
- Print

```
✓ Installed
```

or

```
✗ Missing
```

Then call it for:

- Git
- Node
- npm
- Docker
- Neovim

---

# Mini Project

Create

```
project-generator.sh
```

Functions:

```
create_structure()

create_readme()

create_gitignore()

initialize_git()
```

Workflow:

```
Ask project name

↓

Create folders

↓

Create README

↓

Create .gitignore

↓

git init

↓

Done
```

---

# Common Mistakes

## Forgetting Parentheses

Wrong

```bash
hello {
}
```

Correct

```bash
hello() {
}
```

---

## Forgetting to Call the Function

Creating

```bash
hello() {
    echo "Hi"
}
```

does nothing until you call

```bash
hello
```

---

## Using `return` for Text

Wrong

```bash
return "Rahul"
```

`return` only supports numeric exit codes (0–255).

Correct

```bash
echo "Rahul"
```

Capture it:

```bash
name=$(current_user)
```

---

## Not Using `local`

Wrong

```bash
count=0

increase() {
    count=10
}
```

This changes the global variable.

Better

```bash
increase() {
    local count=10
}
```

---

# Interview Questions

1. What is a Bash function?
2. Why use functions instead of repeating code?
3. What is the difference between `return` and `echo` in a function?
4. What does `local` do?
5. What are `$1`, `$2`, and `"$@"`?
6. How do you check if a function succeeded?
7. Why do many Bash scripts include a `main()` function?

---

# Cheat Sheet

```bash
# Function
hello() {
    echo "Hello"
}

# Call
hello

# Argument
greet() {
    echo "Hello $1"
}

greet Rahul

# All arguments
"$@"

# Number of arguments
$#

# Local variable
local name="Rahul"

# Success
return 0

# Failure
return 1

# Return data
echo "value"

result=$(function_name)
```

---

# Weekly Challenge 🚀

Build a **`dev-setup.sh`** script using functions.

### Requirements

Create these functions:

```
print_banner()
check_tool()
create_project()
create_readme()
create_gitignore()
initialize_git()
main()
```

### Workflow

1. Display a welcome banner.
2. Check if Git, Node.js, npm, and Neovim are installed.
3. Ask the user for a project name.
4. Create this structure:

```
project-name/
├── src/
├── tests/
├── docs/
├── config/
├── scripts/
├── README.md
└── .gitignore
```

1. Initialize a Git repository.
2. Print a success message with the project path.

---

# ⭐ Module 1 Progress

You've completed **5 of 12 lessons**.

```
✅ Lesson 1 — Introduction
✅ Lesson 2 — Variables & User Input
✅ Lesson 3 — Conditions
✅ Lesson 4 — Loops
✅ Lesson 5 — Functions

⬜ Lesson 6 — Command-Line Arguments ($1, $2, "$@", $#)
⬜ Lesson 7 — Arrays
⬜ Lesson 8 — Exit Codes
⬜ Lesson 9 — Environment Variables
⬜ Lesson 10 — Error Handling
⬜ Lesson 11 — Mini Projects
⬜ Lesson 12 — Final Capstone Project
```

## 💡 Extra Practice (Recommended)

Before moving to Lesson 6, try combining everything you've learned so far into one script:

`new-node-project.sh`

Features:

- Uses **functions** to organize the code.
- Accepts a project name (or prompts the user if not provided).
- Checks if `git`, `node`, and `npm` are installed.
- Creates the project structure.
- Generates a `README.md` and `.gitignore`.
- Initializes Git.
- Prints a colored success message.

This single project will reinforce **variables, input, conditions, loops, and functions**—the core building blocks of shell scripting.

In **Lesson 6**, we'll make this even better by accepting the project name directly from the command line, allowing you to run:

```bash
./new-node-project.sh blog-api
```

instead of answering prompts. That's how professional command-line tools are typically designed.