Welcome to one of the most important lessons in shell scripting. Almost every Bash script you write will use variables and user input.

**Estimated time:** 2–3 hours

**Difficulty:** ⭐⭐☆☆☆

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Create and use variables
- Read input from users
- Perform arithmetic
- Store command output
- Understand quoting
- Use built-in shell variables
- Build interactive scripts

---

# 1. What is a Variable?

A variable stores a value that you can use later.

Instead of writing the same value repeatedly, you save it once.

Example:

```bash
name="Rahul"

echo "$name"
```

Output:

```
Rahul
```

Think of a variable like a labeled box:

```
+------------------+
| name             |
|------------------|
| Rahul            |
+------------------+
```

---

# 2. Creating Variables

Syntax:

```bash
variable_name="value"
```

Example:

```bash
language="JavaScript"
framework="Express"
database="MongoDB"
```

Print them:

```bash
echo "$language"
echo "$framework"
echo "$database"
```

Output:

```
JavaScript
Express
MongoDB
```

---

# 3. Variable Naming Rules

✅ Valid:

```bash
user_name="Rahul"
project="BlogAPI"
port=3000
```

❌ Invalid:

```bash
2name="Rahul"
my-project="Blog"
user name="Rahul"
```

Rules:

- Start with a letter or `_`
- No spaces
- Avoid special characters
- Use meaningful names

Good:

```bash
database_url=""
server_port=5000
```

Bad:

```bash
x=5000
a=1
```

---

# 4. No Spaces Around `=`

Correct:

```bash
name="Rahul"
```

Wrong:

```bash
name = "Rahul"
```

Bash interprets this as a command and you'll get an error.

---

# 5. Accessing Variables

Always use `$` when reading a variable.

```bash
name="Rahul"

echo "$name"
```

Without `$`:

```bash
echo "name"
```

Output:

```
name
```

With `$`:

```bash
echo "$name"
```

Output:

```
Rahul
```

---

# 6. Double Quotes vs Single Quotes

### Double Quotes (`"`)

Variables are expanded.

```bash
name="Rahul"

echo "Hello $name"
```

Output:

```
Hello Rahul
```

---

### Single Quotes (`'`)

Variables are **not** expanded.

```bash
echo 'Hello $name'
```

Output:

```
Hello $name
```

---

### Rule of Thumb

Almost always use **double quotes** when printing variables.

---

# 7. Reading User Input

Use `read`.

Example:

```bash
#!/usr/bin/env bash

echo "What is your name?"
read name

echo "Welcome $name!"
```

Run:

```
What is your name?
Rahul

Welcome Rahul!
```

---

# 8. Reading Input with a Prompt

Instead of two lines:

```bash
echo "Enter name:"
read name
```

Use:

```bash
read -p "Enter your name: " name
```

Cleaner.

---

# 9. Reading Multiple Values

```bash
read -p "Enter first and last name: " first last

echo "$first"
echo "$last"
```

Input:

```
Rahul Kumar
```

Output:

```
Rahul
Kumar
```

---

# 10. Read Password Securely

Hide typed characters.

```bash
read -sp "Password: " password

echo
echo "Password received."
```

Useful for deployment scripts.

---

# 11. Command Substitution

Store command output.

Example:

```bash
today=$(date)

echo "$today"
```

Another example:

```bash
current_user=$(whoami)

echo "$current_user"
```

This is extremely common.

---

# 12. Practical Example

```bash
#!/usr/bin/env bash

user=$(whoami)
directory=$(pwd)
today=$(date)

echo "User: $user"
echo "Directory: $directory"
echo "Date: $today"
```

---

# 13. Arithmetic

Using `$(( ))`

```bash
a=10
b=20

sum=$((a+b))

echo "$sum"
```

Output:

```
30
```

More examples:

```bash
echo $((10+5))
echo $((20-7))
echo $((5*8))
echo $((40/5))
echo $((10%3))
```

---

# 14. Increment

```bash
count=1

count=$((count+1))

echo "$count"
```

Output:

```
2
```

---

# 15. String Concatenation

```bash
first="Rahul"
last="Kumar"

full="$first $last"

echo "$full"
```

Output:

```
Rahul Kumar
```

---

# 16. Useful Built-in Variables

### Current Script

```bash
echo "$0"
```

---

### Current User

```bash
echo "$USER"
```

---

### Home Directory

```bash
echo "$HOME"
```

---

### Current Shell

```bash
echo "$SHELL"
```

---

### Current Working Directory

```bash
echo "$PWD"
```

---

### Previous Directory

```bash
echo "$OLDPWD"
```

---

# 17. Default Values

Useful when variables might be empty.

```bash
echo "${name:-Guest}"
```

If:

```bash
name=""
```

Output:

```
Guest
```

---

# 18. Exporting Variables

Make variables available to child processes.

```bash
export PORT=5000
```

Verify:

```bash
printenv PORT
```

You'll learn environment variables in more detail in Lesson 9.

---

# Real Backend Example

Suppose you're creating a new Express project.

```bash
#!/usr/bin/env bash

read -p "Project name: " project

mkdir "$project"

cd "$project" || exit

npm init -y

echo "Project created!"
```

Instead of typing every command manually, the script automates the setup.

---

# Hands-on Lab

Create a script named `developer-info.sh`.

It should:

1. Ask for your name.
2. Ask for your favorite programming language.
3. Ask for your editor.
4. Display a summary like:

```
Developer Profile
-----------------
Name: Rahul
Language: JavaScript
Editor: Neovim
```

---

# Mini Project

Create a simple calculator.

Requirements:

```
Enter first number:
10

Enter second number:
5
```

Display:

```
Addition: 15
Subtraction: 5
Multiplication: 50
Division: 2
Remainder: 0
```

---

# Common Mistakes

### Forgetting Quotes

Bad:

```bash
mkdir $project
```

If the project name contains spaces:

```
My Project
```

It becomes:

```
mkdir My Project
```

This creates two directories.

Correct:

```bash
mkdir "$project"
```

Always quote variables unless you specifically need word splitting.

---

### Forgetting `$`

Wrong:

```bash
echo "name"
```

Correct:

```bash
echo "$name"
```

---

### Using `=` Incorrectly

Wrong:

```bash
port = 3000
```

Correct:

```bash
port=3000
```

---

# Interview Questions

1. What is a variable in Bash?
2. Why should variables usually be enclosed in double quotes?
3. What is the difference between single and double quotes?
4. How do you read user input?
5. What does `$(command)` do?
6. How do you perform arithmetic in Bash?
7. What is the purpose of `export`?

---

# Cheat Sheet

```bash
# Variables
name="Rahul"

# Print
echo "$name"

# Read input
read name

# Prompt
read -p "Name: " name

# Hidden input
read -sp "Password: " password

# Command substitution
today=$(date)

# Arithmetic
sum=$((10+20))

# Export
export PORT=5000

# Default value
echo "${name:-Guest}"

# Useful variables
echo "$USER"
echo "$HOME"
echo "$PWD"
echo "$SHELL"
echo "$0"
```

---

# Weekly Challenge 🚀

Create a script called `project-info.sh` that:

- Asks for:
    - Project name
    - Author name
    - Version
    - License
- Creates a directory with the project name.
- Generates a `README.md` containing:

```
# <Project Name>

Author: <Author Name>

Version: <Version>

License: <License>
```

- Prints a success message showing where the project was created.

---

## Coming Next: Lesson 3 — Conditions (`if`, `elif`, `else`)

In the next lesson, you'll learn how to make your scripts **think and make decisions**. You'll build scripts that can:

- Check if a file exists.
- Verify whether Node.js or Docker is installed.
- Validate user input.
- Exit with meaningful error messages.
- Decide different actions based on conditions.

This is where your shell scripts start becoming genuinely useful for backend development.