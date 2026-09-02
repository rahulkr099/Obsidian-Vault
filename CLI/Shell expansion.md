# Shell Expansion in Linux 🔥

Shell expansion means:

> **Before executing your command, Bash transforms certain special patterns into actual values.**

For example:

```bash
echo ~
```

You type `~`, but Bash expands it to something like:

```text
/home/rahul
```

Then `echo` receives:

```bash
echo /home/rahul
```

Understanding expansion helps you become much faster in the terminal.

---

# The Big Picture 🧠

Bash performs several types of expansion:

```text
Shell Expansion
│
├── Brace Expansion       {}
├── Tilde Expansion       ~
├── Parameter Expansion   $VAR
├── Command Substitution  $(command)
├── Arithmetic Expansion  $(( ))
├── Word Splitting
└── Filename Expansion    * ? []
```

Let's learn the most useful ones.

---

# 1. Brace Expansion `{}` 🔥

Brace expansion generates combinations of text.

Example:

```bash
echo {a,b,c}
```

Output:

```text
a b c
```

Bash expands the command before `echo` runs.

Conceptually:

```bash
echo {a,b,c}
```

becomes:

```bash
echo a b c
```

---

## Create Multiple Directories

```bash
mkdir project-{frontend,backend,database}
```

This creates:

```text
project-frontend
project-backend
project-database
```

Very useful!

---

## Multiple Files

```bash
touch file-{1,2,3}.txt
```

Creates:

```text
file-1.txt
file-2.txt
file-3.txt
```

---

# 2. Range Expansion `{1..10}` 🔥

Generate numbers:

```bash
echo {1..10}
```

Output:

```text
1 2 3 4 5 6 7 8 9 10
```

---

## Create Files

```bash
touch file{1..10}.txt
```

Creates:

```text
file1.txt
file2.txt
file3.txt
...
file10.txt
```

---

## Range with Step

```bash
echo {1..10..2}
```

Output:

```text
1 3 5 7 9
```

Syntax:

```text
{start..end..step}
```

---

# 3. Alphabet Range

```bash
echo {a..z}
```

Output:

```text
a b c d e f ... z
```

Uppercase:

```bash
echo {A..Z}
```

---

# 4. Practical MERN Project Example 🚀

You can quickly create a project structure:

```bash
mkdir -p myapp/{frontend,backend}/{src,tests}
```

This creates:

```text
myapp
├── frontend
│   ├── src
│   └── tests
│
└── backend
    ├── src
    └── tests
```

Very powerful.

You can verify:

```bash
tree myapp
```

If `tree` isn't installed:

```bash
find myapp -type d
```

---

# 5. Tilde Expansion `~` 🏠

The tilde represents your home directory.

```bash
echo ~
```

Example:

```text
/home/rahul
```

Equivalent:

```bash
echo "$HOME"
```

---

## Navigate Home

```bash
cd ~
```

or simply:

```bash
cd
```

---

## Access Files in Home

Instead of:

```bash
cd /home/rahul/projects
```

you can write:

```bash
cd ~/projects
```

Much faster.

---

# 6. Parameter Expansion `$VARIABLE`

You've already seen this.

```bash
name="Rahul"

echo "$name"
```

Bash expands:

```text
$name
 ↓
Rahul
```

Then executes:

```bash
echo Rahul
```

---

## Curly Braces

```bash
name="Rahul"

echo "${name}_developer"
```

Output:

```text
Rahul_developer
```

Without braces:

```bash
echo "$name_developer"
```

Bash thinks `name_developer` is the variable name.

---

# 7. Command Substitution `$(command)` 🔥

You can put command output inside another command.

Example:

```bash
echo "Today is $(date)"
```

Bash first runs:

```bash
date
```

Then substitutes the result.

Conceptually:

```bash
echo "Today is $(date)"
```

becomes:

```bash
echo "Today is Wed Sep 2 ..."
```

---

## Store Command Output

```bash
current_dir=$(pwd)

echo "$current_dir"
```

---

## Developer Example

Get the current Git branch:

```bash
branch=$(git branch --show-current)

echo "Current branch: $branch"
```

Very useful in shell scripts.

---

# 8. Arithmetic Expansion `$(( ))`

Perform calculations directly in Bash.

```bash
echo $((10 + 5))
```

Output:

```text
15
```

---

## With Variables

```bash
a=10
b=20

echo $((a + b))
```

Output:

```text
30
```

---

## Useful Operations

```bash
$((10 + 5))
$((10 - 5))
$((10 * 5))
$((10 / 5))
$((10 % 3))
```

---

# 9. Filename Expansion (Globbing) 🔥🔥

This is extremely important.

Globbing lets you match filenames.

Main symbols:

```text
*     Any number of characters
?     Exactly one character
[]    One character from a set
```

---

# 10. `*` — Match Anything

Suppose:

```text
src/
├── app.js
├── server.js
├── utils.js
└── config.json
```

Run:

```bash
echo *.js
```

Bash expands:

```text
*.js
```

into:

```text
app.js server.js utils.js
```

Then executes:

```bash
echo app.js server.js utils.js
```

---

## Delete Matching Files ⚠️

```bash
rm *.log
```

This means Bash first finds all `.log` files:

```text
error.log
server.log
debug.log
```

Then effectively runs:

```bash
rm error.log server.log debug.log
```

Always be careful with `rm` + glob patterns.

---

# 11. `?` — Exactly One Character

Suppose:

```text
file1.txt
file2.txt
fileA.txt
file10.txt
```

Run:

```bash
echo file?.txt
```

Matches:

```text
file1.txt
file2.txt
fileA.txt
```

But NOT:

```text
file10.txt
```

Because `?` matches exactly one character.

---

# 12. `[]` — Match Character Sets

Suppose:

```text
file1.txt
file2.txt
file3.txt
fileA.txt
```

Run:

```bash
echo file[123].txt
```

Matches:

```text
file1.txt
file2.txt
file3.txt
```

---

## Range

```bash
echo file[1-5].txt
```

Matches:

```text
file1.txt
file2.txt
file3.txt
file4.txt
file5.txt
```

---

# 13. Negation

You can match characters NOT in a set:

```bash
echo file[!0-9].txt
```

Matches files where that character is not a digit.

For example:

```text
fileA.txt
fileB.txt
```

---

# 14. Hidden Files ⚠️

A very important Linux behavior:

```bash
echo *
```

does NOT normally show hidden files.

Files beginning with `.` are hidden:

```text
.git
.env
.bashrc
```

To match hidden files:

```bash
echo .*
```

But be careful: this can include `.` and `..` in some contexts.

A safer Bash option exists:

```bash
shopt -s dotglob
```

Now:

```bash
echo *
```

can include hidden files.

Turn it off:

```bash
shopt -u dotglob
```

---

# 15. Recursive Globbing `**` 🔥

Bash supports recursive globbing with `globstar`.

Enable:

```bash
shopt -s globstar
```

Now:

```bash
echo **/*.js
```

Finds `.js` files recursively.

Example structure:

```text
project/
├── app.js
├── src/
│   ├── server.js
│   └── utils/
│       └── helper.js
```

Then:

```bash
echo **/*.js
```

can match:

```text
app.js
src/server.js
src/utils/helper.js
```

This can sometimes be more convenient than `find`.

---

# 16. Globbing vs Regex ⚠️

These are NOT the same.

### Glob

```bash
*.js
```

Used for filenames.

### Regex

```text
.*\.js$
```

Used for text pattern matching.

Comparison:

| Feature | Glob | Regex |  
|---|---|  
| Main purpose | Filename matching | Text pattern matching |  
| Any characters | `*` | `.*` |  
| One character | `?` | `.` |  
| Examples | `*.js` | `.*\.js$` |

This is a common beginner confusion.

---

# 17. Expansion Order 🧠🔥

Bash performs expansions in a specific order.

Simplified:

```text
1. Brace Expansion
        ↓
2. Tilde Expansion
        ↓
3. Parameter Expansion
        ↓
4. Command Substitution
        ↓
5. Arithmetic Expansion
        ↓
6. Word Splitting
        ↓
7. Filename Expansion (Globbing)
```

You don't need to memorize this immediately.

But knowing that:

> **Bash expands things before executing the command**

is extremely important.

---

# 18. Quoting Changes Expansion 🔥

Consider:

```bash
echo *.js
```

Bash expands `*.js`.

But:

```bash
echo "*.js"
```

Output:

```text
*.js
```

Why?

Double quotes prevent filename expansion.

---

## Single Quotes

```bash
name="Rahul"

echo '$name'
```

Output:

```text
$name
```

Nothing expands inside single quotes.

---

## Double Quotes

```bash
echo "$name"
```

Output:

```text
Rahul
```

Variables expand inside double quotes.

---

# Important Quoting Table 🧠

|Syntax|Variable Expansion|Globbing|
|---|---|---|
|`$name`|✅|✅ possible|
|`"$name"`|✅|❌|
|`'$name'`|❌|❌|

Example:

```bash
name="Rahul"
```

```bash
echo "$name"
```

→ `Rahul`

```bash
echo '$name'
```

→ `$name`

---

# 19. Combining Expansions 🚀

This is where Bash becomes fun.

```bash
mkdir -p project/{frontend,backend}/src
```

Creates:

```text
project
├── frontend
│   └── src
│
└── backend
    └── src
```

Another example:

```bash
touch file{1..5}.txt
```

Then:

```bash
echo *.txt
```

Bash finds them.

You can combine commands:

```bash
wc -l *.js
```

Conceptually Bash converts:

```bash
wc -l *.js
```

into:

```bash
wc -l app.js server.js utils.js
```

---

# 20. A Powerful Developer Example 🔥

Suppose you want to create a backend structure quickly:

```bash
mkdir -p backend/src/{controllers,models,routes,middleware,services,utils}
```

Then:

```bash
touch backend/src/{app.js,server.js}
```

Result:

```text
backend/
└── src/
    ├── controllers/
    ├── middleware/
    ├── models/
    ├── routes/
    ├── services/
    ├── utils/
    ├── app.js
    └── server.js
```

That's terminal-first development. 🚀

---

# 21. Useful Practice Commands 💪

Try these safely in a temporary directory:

```bash
mkdir ~/shell-practice
cd ~/shell-practice
```

### Brace expansion

```bash
echo {1..10}
```

### Create directories

```bash
mkdir {frontend,backend,database}
```

### Create files

```bash
touch file{1..5}.txt
```

### Glob

```bash
echo *.txt
```

### One-character matching

```bash
echo file?.txt
```

### Character range

```bash
echo file[1-3].txt
```

### Command substitution

```bash
echo "Current directory: $(pwd)"
```

### Arithmetic

```bash
echo $((10 * 5))
```

---

# Quick Cheat Sheet 📌

```bash
# Brace expansion
echo {a,b,c}

# Number range
echo {1..10}

# Step
echo {1..10..2}

# Tilde/home
echo ~

# Variable
echo "$HOME"

# Command substitution
echo "$(date)"

# Arithmetic
echo $((10 + 20))

# All .js files
echo *.js

# Exactly one character
echo file?.txt

# Character range
echo file[1-5].txt

# Recursive globbing
shopt -s globstar
echo **/*.js
```

---

# The Core Mental Model 🧠

When you type:

```bash
mkdir project-{frontend,backend}
```

Bash doesn't give this literal text directly to `mkdir`.

First:

```text
Bash Expansion
      ↓
project-frontend project-backend
      ↓
mkdir
```

So:

> **The shell prepares and transforms your command before the command actually runs.**

This understanding becomes very important when writing shell scripts.

---

## Your Linux Learning Journey So Far 🚀

```text
Linux Terminal Mastery
│
├── Navigation & Files
├── Text Processing
│   ├── grep
│   ├── sed
│   ├── awk
│   └── Regex
│
├── Shell Power
│   ├── Pipes
│   ├── Redirection
│   ├── Chaining
│   ├── xargs
│   └── find
│
├── Process Streams
│   └── stdin / stdout / stderr
│
├── Environment
│   ├── Variables
│   ├── PATH
│   └── export
│
└── Shell Expansion 🔥
    ├── {}
    ├── ~
    ├── $VAR
    ├── $(command)
    ├── $((math))
    └── Globbing
```

# Next Topic: Permissions & Ownership 🔐

This is the next essential Linux topic.

You'll learn:

```bash
chmod
chown
chgrp
```

And understand this mysterious output:

```text
-rwxr-xr--
```

Including:

```text
r → read
w → write
x → execute
```

This is essential for Linux, servers, Docker, deployment, SSH, and backend development.