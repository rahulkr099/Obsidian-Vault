# Linux `find` Command 🔎🔥

The `find` command is one of the most important Linux commands.

It searches for **files and directories** based on conditions like:

- Name
    
- Type
    
- Extension
    
- Size
    
- Permissions
    
- Modification time
    
- Empty files
    
- Ownership
    

For a developer, `find` is incredibly useful for navigating and maintaining projects.

---

# Basic Syntax

```bash
find [starting-directory] [conditions]
```

Example:

```bash
find . -name "*.js"
```

Meaning:

```text
find
 ↓
Start from current directory (.)
 ↓
Find files/directories
 ↓
Matching *.js
```

---

# 1. Find by Exact Name

```bash
find . -name "package.json"
```

This searches recursively from the current directory.

Example output:

```text
./package.json
./frontend/package.json
./backend/package.json
```

---

# 2. Case-Insensitive Search

Normal `-name` is case-sensitive.

```bash
find . -name "README.md"
```

For case-insensitive search:

```bash
find . -iname "readme.md"
```

This can match:

```text
README.md
Readme.md
readme.md
```

---

# 3. Find by Extension 🔥

Find JavaScript files:

```bash
find . -name "*.js"
```

Find Python files:

```bash
find . -name "*.py"
```

Find JSON files:

```bash
find . -name "*.json"
```

For a MERN project:

```bash
find src -name "*.jsx"
```

---

# ⚠️ Why Quotes Matter?

Always prefer:

```bash
find . -name "*.js"
```

instead of:

```bash
find . -name *.js
```

Why?

Without quotes, the shell may expand `*.js` **before `find` receives it**.

So quotes protect the pattern.

---

# 4. Find Only Files

```bash
find . -type f
```

`f` means:

```text
f → File
```

Example:

```bash
find src -type f -name "*.js"
```

Finds only JavaScript files.

---

# 5. Find Only Directories

```bash
find . -type d
```

`d` means directory.

Example:

```bash
find . -type d -name "node_modules"
```

---

# 6. Find Multiple Extensions

Find JavaScript OR TypeScript files:

```bash
find . \( -name "*.js" -o -name "*.ts" \)
```

Better with type restriction:

```bash
find src -type f \( -name "*.js" -o -name "*.ts" \)
```

Meaning:

```text
Find files
     ↓
.js OR .ts
```

---

# 7. Exclude Directories 🔥

Suppose you don't want to search inside `node_modules`.

```bash
find . -path "./node_modules" -prune -o -name "*.js" -print
```

This looks complicated, so let's understand it.

```text
-prune → Don't enter this directory
```

For a project:

```bash
find . \
  -path "./node_modules" -prune -o \
  -type f -name "*.js" -print
```

This is useful because `node_modules` can contain thousands of files.

---

# 8. Find Files by Size

Find files larger than 100 MB:

```bash
find . -type f -size +100M
```

Find files smaller than 10 KB:

```bash
find . -type f -size -10k
```

Exactly 10 MB:

```bash
find . -type f -size 10M
```

Symbols:

```text
+ → Greater than
- → Less than
```

Examples:

```bash
find . -type f -size +1G
```

Find files larger than 1 GB.

---

# 9. Find Empty Files

```bash
find . -type f -empty
```

Find empty directories:

```bash
find . -type d -empty
```

Very useful for cleanup.

---

# 10. Find Files by Modification Time 🔥

This is extremely useful.

### Modified in last 24 hours

```bash
find . -type f -mtime -1
```

### Modified more than 7 days ago

```bash
find . -type f -mtime +7
```

### Modified exactly around 7 days ago

```bash
find . -type f -mtime 7
```

Mental model:

```text
-mtime -1 → Recently modified
-mtime +7 → Old files
```

---

# More Precise Time: `-mmin`

Find files modified within the last 30 minutes:

```bash
find . -type f -mmin -30
```

Very useful for development.

---

# 11. Find Files by Permissions

Find executable files:

```bash
find . -type f -executable
```

Find files with permission `777`:

```bash
find . -type f -perm 777
```

Be careful with exact permission searches.

---

# 12. Find and Execute Commands 🔥

This is where `find` becomes extremely powerful.

Basic syntax:

```bash
find . condition -exec command {} \;
```

`{}` represents the found file.

---

## Example: Delete `.log` files

⚠️ First, always inspect:

```bash
find . -type f -name "*.log"
```

Then:

```bash
find . -type f -name "*.log" -exec rm {} \;
```

Meaning:

```text
Find file
    ↓
Run rm individually
```

---

# `\;` vs `+` ⚡

### Run command once per file

```bash
find . -type f -name "*.txt" -exec echo {} \;
```

Conceptually:

```bash
echo file1.txt
echo file2.txt
echo file3.txt
```

### Run command with multiple files together

```bash
find . -type f -name "*.txt" -exec echo {} +
```

Conceptually:

```bash
echo file1.txt file2.txt file3.txt
```

Usually prefer:

```bash
-exec command {} +
```

because it is more efficient.

---

# 13. Find + Delete

You can use:

```bash
find . -type f -name "*.tmp" -delete
```

⚠️ Be careful.

Good practice:

### Step 1: Preview

```bash
find . -type f -name "*.tmp"
```

### Step 2: Delete

```bash
find . -type f -name "*.tmp" -delete
```

Never blindly run destructive `find` commands.

---

# 14. Find + `xargs`

You just learned `xargs`.

Classic combination:

```bash
find . -type f -name "*.txt" -print0 | xargs -0 wc -l
```

But `find -exec` can often do this more simply:

```bash
find . -type f -name "*.txt" -exec wc -l {} +
```

Both are useful.

---

# 15. Find Duplicate `package.json` Files

Inside a project:

```bash
find . -name "package.json"
```

Example:

```text
./package.json
./frontend/package.json
./backend/package.json
```

Very useful in monorepos.

---

# 16. Find Large Files in a Project 🔥

```bash
find . -type f -size +50M
```

Want them sorted by size?

```bash
find . -type f -size +10M -printf "%s %p\n" | sort -nr
```

Here:

```text
%s → File size
%p → File path
```

Example output:

```text
250000000 ./video.mp4
120000000 ./backup.zip
```

---

# 17. Find Recently Modified Source Files

For JavaScript:

```bash
find src -type f -name "*.js" -mtime -1
```

Or files changed in the last hour:

```bash
find src -type f -name "*.js" -mmin -60
```

This is useful when debugging:

> "Which files did I recently modify?"

---

# 18. Find `node_modules` Directories

```bash
find . -type d -name "node_modules"
```

You can check their size:

```bash
find . -type d -name "node_modules" -exec du -sh {} +
```

Example:

```text
250M ./frontend/node_modules
180M ./backend/node_modules
```

Useful when cleaning disk space.

---

# 19. Find and Run `grep` 🔥

Search for `console.log` inside JavaScript files:

```bash
find src -type f -name "*.js" -exec grep -n "console.log" {} +
```

This combines:

```text
find → Locate files
grep → Search inside files
```

---

# 20. `find` + Pipes + `awk`

Let's create a powerful pipeline.

Find large files:

```bash
find . -type f -printf "%s %p\n" \
  | sort -nr \
  | head
```

Flow:

```text
find
 ↓
file size + path
 ↓
sort largest first
 ↓
head
 ↓
Top 10 largest files
```

This is a real Linux power-user command.

---

# 21. Practical MERN Examples 🚀

### Find all React components

```bash
find src -type f -name "*.jsx"
```

---

### Find all environment files

```bash
find . -type f -name ".env*"
```

---

### Find all test files

```bash
find . -type f \( -name "*.test.js" -o -name "*.spec.js" \)
```

---

### Find empty JavaScript files

```bash
find src -type f -name "*.js" -empty
```

---

### Find recently changed files

```bash
find src -type f -mmin -60
```

---

### Find all `.log` files but don't delete yet

```bash
find . -type f -name "*.log"
```

---

# Quick Cheat Sheet 🧠

|Command|Meaning|
|---|---|
|`find . -name "file.txt"`|Find by name|
|`find . -iname "file.txt"`|Case-insensitive|
|`find . -type f`|Files only|
|`find . -type d`|Directories only|
|`find . -name "*.js"`|Find extension|
|`find . -size +100M`|Larger than 100 MB|
|`find . -empty`|Empty files/dirs|
|`find . -mtime -1`|Modified recently|
|`find . -mmin -30`|Modified last 30 min|
|`find . -executable`|Executable files|
|`-exec command {} +`|Execute command|
|`-delete`|Delete matches|

---

# Important Safety Rule ⚠️

Before using:

```bash
-delete
```

or:

```bash
-exec rm {} +
```

Always first run:

```bash
find . [your conditions]
```

Inspect the output.

Then add the destructive action.

---

# Mental Model 🧠

```text
find = Search Engine for Your Filesystem

Starting location
       ↓
Conditions
       ↓
Matching files
       ↓
Optional action
```

Example:

```bash
find src -type f -name "*.js" -mtime -7
```

Read it naturally:

> Starting from `src`, find regular files ending in `.js` modified within the last 7 days.

---

## Your Linux Toolkit So Far 🚀

```text
Text Processing
├── grep
├── sort
├── uniq
├── wc
├── cut
├── tr
├── sed
└── awk

Shell Operations
├── Pipes
├── Redirection
├── Command chaining
├── xargs
└── find 🔥
```

### Next Topic: Regular Expressions (Regex) 🔥

This is the **perfect next step** because Regex will make commands like `grep`, `sed`, and `awk` dramatically more powerful.

You'll learn patterns such as:

```text
^hello      → Starts with hello
world$      → Ends with world
[0-9]       → Any digit
[a-z]       → Any lowercase letter
.           → Any character
*           → Zero or more
+           → One or more
```

Once you understand Regex, Linux text processing becomes much easier and more powerful.