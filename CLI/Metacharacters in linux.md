# Metacharacters in Linux

**Metacharacters** are special characters that have a special meaning to the Linux shell (like Bash). They allow you to perform powerful operations without writing long commands.

For example:

```bash
*
?
>
|
$
```

These characters are interpreted by the shell before a command runs.

---

## 1. `*` — Wildcard

Matches **zero or more characters**.

Suppose you have:

```text
file.txt
data.txt
notes.txt
image.png
```

Command:

```bash
ls *.txt
```

Output:

```text
data.txt
file.txt
notes.txt
```

`*.txt` means:

> Match anything ending with `.txt`

Another example:

```bash
rm *.log
```

Deletes all `.log` files.

⚠️ Be careful with `rm *`.

---

# 2. `?` — Single Character Wildcard

Matches **exactly one character**.

Suppose:

```text
file1.txt
file2.txt
file10.txt
```

Command:

```bash
ls file?.txt
```

Matches:

```text
file1.txt
file2.txt
```

But not:

```text
file10.txt
```

Because `?` matches only one character.

---

# 3. `[]` — Character Set

Matches **one character from a set**.

```bash
ls file[123].txt
```

Matches:

```text
file1.txt
file2.txt
file3.txt
```

### Range

```bash
ls file[1-5].txt
```

Matches:

```text
file1.txt
file2.txt
file3.txt
file4.txt
file5.txt
```

### Letters

```bash
ls file[a-z].txt
```

Matches files containing lowercase letters.

---

# 4. `{}` — Brace Expansion

Used to generate multiple strings.

```bash
echo file{1,2,3}.txt
```

Output:

```text
file1.txt file2.txt file3.txt
```

You can also create multiple files:

```bash
touch file{1,2,3}.txt
```

### Range expansion

```bash
echo {1..10}
```

Output:

```text
1 2 3 4 5 6 7 8 9 10
```

Letters:

```bash
echo {a..z}
```

Very useful:

```bash
mkdir project/{frontend,backend,database}
```

Creates:

```text
project/
├── frontend
├── backend
└── database
```

---

# 5. `~` — Home Directory

Represents your home directory.

```bash
cd ~
```

Equivalent to:

```bash
cd /home/rahul
```

You can also use:

```bash
ls ~/Documents
```

---

# 6. `$` — Variable Expansion

Used to access environment or shell variables.

```bash
name="Rahul"

echo $name
```

Output:

```text
Rahul
```

Example:

```bash
echo $HOME
```

Output:

```text
/home/rahul
```

Other useful variables:

```bash
echo $USER
echo $PATH
echo $PWD
echo $SHELL
```

---

# 7. `>` — Output Redirection

Redirects output to a file.

```bash
echo "Hello" > file.txt
```

Creates or overwrites `file.txt`.

```bash
ls > files.txt
```

Saves output into `files.txt`.

⚠️ `>` overwrites existing content.

---

# 8. `>>` — Append Output

Adds output to the end of a file.

```bash
echo "Hello" >> file.txt
```

If the file contains:

```text
Hi
```

After the command:

```text
Hi
Hello
```

---

# 9. `<` — Input Redirection

Takes input from a file.

```bash
sort < names.txt
```

Equivalent idea:

```text
names.txt → sort command
```

---

# 10. `|` — Pipe

Sends output of one command as input to another.

```bash
ls | grep ".txt"
```

Flow:

```text
ls → grep
```

Another example:

```bash
cat file.txt | sort | uniq
```

Pipeline:

```text
file → sort → uniq
```

This is one of the most important Linux concepts.

---

# 11. `;` — Command Separator

Runs multiple commands sequentially.

```bash
pwd ; ls ; date
```

All commands execute regardless of whether previous commands succeed.

---

# 12. `&&` — Logical AND

Runs the next command **only if the previous command succeeds**.

```bash
mkdir project && cd project
```

Meaning:

```text
mkdir succeeds?
       │
      YES
       ↓
cd project
```

Useful for safe command chaining.

---

# 13. `||` — Logical OR

Runs the next command **only if the previous command fails**.

```bash
mkdir project || echo "Directory already exists"
```

---

# 14. `&` — Run in Background

Runs a command in the background.

```bash
sleep 100 &
```

Your terminal remains available.

Check background jobs:

```bash
jobs
```

Bring a job to foreground:

```bash
fg
```

---

# 15. `()` — Subshell

Runs commands inside a separate shell environment.

```bash
(cd /tmp && ls)
```

After execution, your current directory remains unchanged.

Example:

```bash
pwd

(cd /tmp)

pwd
```

You remain in your original directory.

---

# 16. `\` — Escape Character

Removes the special meaning of the next character.

Example:

```bash
echo \$HOME
```

Output:

```text
$HOME
```

Without escape:

```bash
echo $HOME
```

Output:

```text
/home/rahul
```

---

# 17. `' '` — Single Quotes

Preserves everything literally.

```bash
echo '$HOME'
```

Output:

```text
$HOME
```

No variable expansion happens.

---

# 18. `" "` — Double Quotes

Allows variable expansion but preserves spaces.

```bash
name="Rahul"

echo "Hello $name"
```

Output:

```text
Hello Rahul
```

Difference:

```bash
echo '$HOME'
```

Output:

```text
$HOME
```

vs

```bash
echo "$HOME"
```

Output:

```text
/home/rahul
```

---

# 19. `` ` ` `` — Command Substitution (Old Style)

Executes a command and substitutes its output.

```bash
echo "Today is `date`"
```

Modern alternative is preferred:

```bash
echo "Today is $(date)"
```

---

# 20. `$()` — Command Substitution

Executes a command and uses its output.

```bash
current_date=$(date)

echo "$current_date"
```

Very useful in shell scripting:

```bash
files=$(ls *.txt)

echo "$files"
```

---

# 21. `#` — Comment

Everything after `#` is ignored.

```bash
# This is a comment

echo "Hello"
```

In shell scripts:

```bash
#!/bin/bash

# Print a message
echo "Hello"
```

---

# Quick Summary

|Metacharacter|Meaning|
|---|---|
|`*`|Match zero or more characters|
|`?`|Match exactly one character|
|`[]`|Character set/range|
|`{}`|Brace expansion|
|`~`|Home directory|
|`$`|Variable expansion|
|`>`|Redirect output (overwrite)|
|`>>`|Append output|
|`<`|Redirect input|
|`\|`|Pipe output to another command|
|`;`|Command separator|
|`&&`|Run next command if previous succeeds|
|`\|`|Run next command if previous fails|
|`&`|Run command in background|
|`()`|Subshell|
|`\`|Escape character|
|`' '`|Literal text|
|`" "`|Expand variables|
|`$()`|Command substitution|
|`#`|Comment|

---

## Important Concept: Shell Expansion Order

When you type:

```bash
echo ~/project/{frontend,backend}/*.js
```

The shell processes special characters and expands them.

Conceptually:

```text
~
↓
/home/rahul

{frontend,backend}
↓
frontend backend

*.js
↓
all matching JavaScript files
```

This is why understanding metacharacters makes you much faster in Linux and terminal-based development.

### My recommendation for your Linux journey

Focus especially on mastering these first:

```text
*  ?  []  {}  ~
$  $()  >  >>  <
|  &&  ||  ;  &
'  "  \
```

These are the metacharacters you'll use constantly as a **terminal-first MERN developer**.

**Next natural topic:** **Shell expansions in Linux** — pathname expansion, brace expansion, parameter expansion, command substitution, arithmetic expansion, and quote removal.