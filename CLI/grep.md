# Linux `grep` Command 🔍

`grep` is one of the **most important Linux commands** for developers.

It is used to **search for text or patterns** inside files or command output.

> Think of `grep` as **Ctrl + F for the terminal**.

---

# Basic Syntax

```bash
grep [OPTIONS] PATTERN FILE
```

Example:

```bash
grep "error" server.log
```

This prints every line containing `error`.

---

## 1. Basic Text Search

Suppose `server.log` contains:

```text
Server started
Database connected
ERROR: Invalid token
User logged in
ERROR: Database timeout
```

Run:

```bash
grep "ERROR" server.log
```

Output:

```text
ERROR: Invalid token
ERROR: Database timeout
```

---

# 2. Case-Insensitive Search

Normally `grep` is case-sensitive.

```bash
grep "error" server.log
```

This won't necessarily match:

```text
ERROR
Error
```

Use `-i`:

```bash
grep -i "error" server.log
```

Now it matches:

```text
error
ERROR
Error
eRrOr
```

---

# 3. Show Line Numbers

Use `-n`:

```bash
grep -n "ERROR" server.log
```

Output:

```text
15:ERROR: Invalid token
42:ERROR: Database timeout
```

Very useful when debugging files.

---

# 4. Search Multiple Files

```bash
grep "MongoDB" file1.txt file2.txt
```

Example for a project:

```bash
grep "JWT_SECRET" .env config.txt
```

---

# 5. Search Recursively in a Directory 🔥

This is extremely useful for developers.

```bash
grep -r "useState" .
```

Meaning:

> Search for `useState` recursively inside the current directory.

Example:

```bash
grep -r "console.log" src/
```

This searches every file inside `src/`.

### Better version with line numbers:

```bash
grep -rn "console.log" src/
```

---

# 6. Show Only Matching File Names

Use `-l`.

```bash
grep -rl "useState" src/
```

Output:

```text
src/components/Login.jsx
src/components/Profile.jsx
src/pages/Home.jsx
```

Useful when asking:

> "Which files contain this code?"

---

# 7. Invert Search (Exclude Matches)

Use `-v`.

```bash
grep -v "ERROR" server.log
```

This displays every line **except** lines containing `ERROR`.

Example:

```text
Server started
Database connected
User logged in
```

---

# 8. Count Matches

Use `-c`.

```bash
grep -c "ERROR" server.log
```

Output:

```text
2
```

This counts matching **lines**.

⚠️ Important: `grep -c` counts matching lines, not necessarily every occurrence of the word.

---

# 9. Search Whole Words

Suppose you search:

```bash
grep "user" file.txt
```

It might match:

```text
user
username
superuser
```

To match only the complete word `user`:

```bash
grep -w "user" file.txt
```

---

# 10. Show Context Around Matches

Very useful for debugging logs.

### Show 2 lines after match

```bash
grep -A 2 "ERROR" server.log
```

### Show 2 lines before match

```bash
grep -B 2 "ERROR" server.log
```

### Show 2 lines before and after

```bash
grep -C 2 "ERROR" server.log
```

Example:

```bash
grep -C 3 "Unhandled" server.log
```

This gives you context around the error.

---

# 11. Use `grep` with Pipes 🔥

`grep` becomes very powerful with `|`.

### Find Node processes

```bash
ps aux | grep node
```

### Find a package

```bash
npm list | grep express
```

### Search errors from logs

```bash
tail -f server.log | grep ERROR
```

### Search environment variables

```bash
env | grep PATH
```

---

# 12. Developer Example: Find a Specific API Route

Suppose you're working on a large MERN project.

Search for:

```bash
grep -rn "/api/users" src/
```

Output:

```text
src/routes/userRoutes.js:12:router.get("/api/users", getUsers)
src/api/userApi.js:8:fetch("/api/users")
```

Now you immediately know where that route is used.

---

# 13. Exclude Directories

When searching recursively, you often don't want `node_modules`.

```bash
grep -rn --exclude-dir=node_modules "console.log" .
```

This is a **very practical command** for MERN development.

You can exclude multiple directories:

```bash
grep -rn \
  --exclude-dir=node_modules \
  --exclude-dir=.git \
  "TODO" .
```

---

# 14. Highlight Matches

Usually modern `grep` already highlights matches when used interactively.

You can explicitly enable it:

```bash
grep --color=auto "ERROR" server.log
```

---

# Useful `grep` Options Cheat Sheet

|Command|Meaning|
|---|---|
|`grep "text" file`|Search text|
|`grep -i`|Ignore case|
|`grep -n`|Show line numbers|
|`grep -r`|Recursive search|
|`grep -l`|Show matching filenames|
|`grep -v`|Exclude matches|
|`grep -c`|Count matching lines|
|`grep -w`|Match whole word|
|`grep -A 3`|Show 3 lines after|
|`grep -B 3`|Show 3 lines before|
|`grep -C 3`|Show context|
|`grep -E`|Extended regex|

---

# My Most Recommended Commands for You 🚀

As a MERN developer, remember these:

```bash
# Find console.log statements
grep -rn "console.log" src/

# Find TODO comments
grep -rn "TODO" .

# Find a function
grep -rn "functionName" src/

# Search while excluding node_modules
grep -rn --exclude-dir=node_modules "searchTerm" .

# Watch live errors
tail -f logs/app.log | grep ERROR

# Find running Node processes
ps aux | grep node
```

## Important Developer Upgrade

In modern development, you'll eventually use `rg` (**ripgrep**) more often than `grep` for searching code:

```bash
rg "console.log"
```

It's generally faster and automatically respects `.gitignore` in many common workflows.

But learning `grep` first is absolutely worth it because it is available on almost every Linux system.

### Your toolkit now

```text
cat    → Print files
less   → Read large files
head   → Beginning of files
tail   → End/follow logs
grep   → Search text 🔍
```

**Next command I recommend: `sort`** — then `uniq`, because together they teach you a very important Linux concept: processing and cleaning text data through pipes.