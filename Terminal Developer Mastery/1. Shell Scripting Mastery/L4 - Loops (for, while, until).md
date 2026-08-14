Welcome to one of the most powerful features in Bash.

Conditions let your script **make decisions**.

Loops let your script **repeat work automatically**.

Instead of writing the same command 100 times, you write it once.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Use `for`, `while`, and `until` loops
- Iterate over numbers, files, and arrays
- Read files line by line
- Use `break` and `continue`
- Build automation scripts for backend development
- Avoid common loop mistakes

**Estimated Time:** 4–5 hours

**Difficulty:** ⭐⭐⭐☆☆

---

# Why Do We Need Loops?

Imagine you have 50 MERN projects.

Without a loop:

```bash
cd project1
git pull

cd ../project2
git pull

cd ../project3
git pull
```

...

Repeat 50 times.

With a loop:

```bash
for dir in */
do
    echo "$dir"
done
```

Much simpler.

---

# Types of Loops

Bash provides three main loops:

|Loop|Best For|
|---|---|
|`for`|Fixed number of iterations or lists|
|`while`|Continue while a condition is true|
|`until`|Continue until a condition becomes true|

For backend work, you'll mostly use:

- ⭐⭐⭐⭐⭐ `for`
- ⭐⭐⭐⭐☆ `while`
- ⭐⭐☆☆☆ `until` (less common)

---

# Part 1 — `for` Loop

## Basic Syntax

```bash
for variable in list
do
    commands
done
```

Example:

```bash
for fruit in apple banana mango
do
    echo "$fruit"
done
```

Output:

```
apple
banana
mango
```

---

# Loop Through Numbers

```bash
for num in 1 2 3 4 5
do
    echo "$num"
done
```

Output:

```
1
2
3
4
5
```

---

# Brace Expansion

Much cleaner.

```bash
for i in {1..5}
do
    echo "$i"
done
```

Output:

```
1
2
3
4
5
```

---

# Step Values

```bash
for i in {10..50..10}
do
    echo "$i"
done
```

Output:

```
10
20
30
40
50
```

---

# C-Style `for` Loop

Looks similar to C, Java, or JavaScript.

```bash
for ((i=1; i<=5; i++))
do
    echo "$i"
done
```

Output:

```
1
2
3
4
5
```

This style is common when you need more control.

---

# Loop Through Files

Suppose your directory contains:

```
logs/
    app.log
    error.log
    access.log
```

Script:

```bash
for file in logs/*
do
    echo "$file"
done
```

Output:

```
logs/app.log
logs/error.log
logs/access.log
```

---

# Backend Example — Check All JavaScript Files

```bash
for file in src/*.js
do
    echo "Checking $file"
done
```

---

# Loop Through Directories

```bash
for dir in */
do
    echo "$dir"
done
```

Useful for managing multiple Git repositories.

---

# Backend Example — Pull Every Git Repository

```bash
for dir in */
do
    if [ -d "$dir/.git" ]
    then
        echo "Updating $dir"

        (
            cd "$dir" || exit
            git pull
        )
    fi
done
```

Notice the parentheses. They create a **subshell**, so changing directories inside the loop doesn't affect the main script.

---

# Part 2 — `while` Loop

A `while` loop runs as long as the condition is true.

Syntax:

```bash
while condition
do
    commands
done
```

Example:

```bash
count=1

while [ "$count" -le 5 ]
do
    echo "$count"
    count=$((count+1))
done
```

Output:

```
1
2
3
4
5
```

---

# Reading a File Line by Line

Suppose:

```
users.txt

Rahul
Aman
Neha
```

Script:

```bash
while read -r user
do
    echo "Hello $user"
done < users.txt
```

Output:

```
Hello Rahul
Hello Aman
Hello Neha
```

This is extremely common.

---

# Backend Example — Process `.env`

Imagine reading configuration entries one by one.

```bash
while read -r line
do
    echo "$line"
done < .env
```

---

# Part 3 — `until`

Runs until the condition becomes true.

```bash
count=1

until [ "$count" -gt 5 ]
do
    echo "$count"
    count=$((count+1))
done
```

Output:

```
1
2
3
4
5
```

You'll rarely need this compared to `for` and `while`.

---

# `break`

Stops the loop immediately.

Example:

```bash
for i in {1..10}
do
    if [ "$i" -eq 5 ]
    then
        break
    fi

    echo "$i"
done
```

Output:

```
1
2
3
4
```

---

# `continue`

Skips the current iteration.

```bash
for i in {1..5}
do
    if [ "$i" -eq 3 ]
    then
        continue
    fi

    echo "$i"
done
```

Output:

```
1
2
4
5
```

---

# Loop Over Command Output

```bash
for user in $(who)
do
    echo "$user"
done
```

⚠️ This can break when output contains spaces.

A safer approach is often:

```bash
while read -r line
do
    echo "$line"
done < <(who)
```

---

# Nested Loops

```bash
for row in {1..3}
do
    for col in {1..3}
    do
        echo "Row $row, Column $col"
    done
done
```

Output:

```
Row 1, Column 1
Row 1, Column 2
...
Row 3, Column 3
```

---

# Real Backend Example 1 — Create Multiple Directories

```bash
for dir in src tests docs config scripts
do
    mkdir -p "$dir"
done
```

---

# Real Backend Example 2 — Backup Logs

```bash
mkdir -p backup

for file in logs/*.log
do
    cp "$file" backup/
done
```

---

# Real Backend Example 3 — Check Multiple Commands

```bash
for tool in git node npm docker nvim
do
    if command -v "$tool" >/dev/null 2>&1
    then
        echo "✓ $tool installed"
    else
        echo "✗ $tool missing"
    fi
done
```

---

# Hands-on Lab

Create a script named `create-folders.sh`.

Requirements:

- Create directories:

```
src
tests
controllers
routes
models
config
middlewares
```

- Print a message after creating each one.

---

# Mini Project

Create a script called `backup-projects.sh`.

Requirements:

- Loop through every folder in `~/Projects`.
- If the folder contains a `.git` directory:
    - Compress it into a `.tar.gz` archive.
    - Save it in `~/Backups`.

This is a practical backup automation task.

---

# Common Mistakes

## Forgetting to Update the Counter

```bash
count=1

while [ "$count" -le 5 ]
do
    echo "$count"
done
```

This creates an infinite loop because `count` never changes.

Correct:

```bash
count=$((count+1))
```

---

## Not Quoting Variables

Wrong:

```bash
mkdir $folder
```

Correct:

```bash
mkdir "$folder"
```

---

## Using `for` for File Input

Avoid:

```bash
for line in $(cat file.txt)
```

This splits lines on spaces.

Prefer:

```bash
while read -r line
do
    echo "$line"
done < file.txt
```

---

# Interview Questions

1. What is the difference between `for` and `while` loops?
2. When would you use an `until` loop?
3. What do `break` and `continue` do?
4. Why is `while read -r` preferred for reading files?
5. What is a subshell, and why is it useful?
6. How do you iterate over all directories in the current folder?

---

# Cheat Sheet

```bash
# For loop
for item in list
do
    echo "$item"
done

# Number loop
for i in {1..10}
do
    echo "$i"
done

# C-style loop
for ((i=1; i<=5; i++))
do
    echo "$i"
done

# While loop
count=1
while [ "$count" -le 5 ]
do
    echo "$count"
    count=$((count+1))
done

# Read a file
while read -r line
do
    echo "$line"
done < file.txt

# Break
break

# Continue
continue
```

---

# Weekly Challenge 🚀

Build a script called **`project-maintenance.sh`**.

The script should:

1. Scan every folder inside `~/Projects`.
2. Check if it is a Git repository.
3. For each Git repository:
    - Show the repository name.
        
    - Display the current Git branch.
        
    - Run `git status --short`.
        
    - Ask:
        
        ```
        Pull latest changes? (y/n):
        ```
        
    - If the user enters `y`, run `git pull`.
        
    - If the user enters `n`, skip it.
        
4. At the end, print a summary showing:
    - Total folders scanned
    - Git repositories found
    - Repositories updated
    - Repositories skipped

This combines **loops, conditions, variables, command substitution, and user input**, making it an excellent practice project before moving on to **Lesson 5: Functions**, where you'll learn how to organize scripts into reusable, professional-quality code.