# Linux `head` Command

`head` is the opposite of `tail`.

It displays the **beginning of a file**. By default, it shows the **first 10 lines**.

## Basic Syntax

```bash
head [OPTIONS] FILE
```

---

## 1. Display the first 10 lines

```bash
head file.txt
```

Example:

```bash
head server.log
```

Output:

```text
Server started
Connected to MongoDB
Environment: development
Port: 5000
...
```

---

## 2. Display a specific number of lines

Use `-n`.

### First 5 lines

```bash
head -n 5 file.txt
```

Example:

```bash
head -n 20 package.json
```

This is useful when you just want a quick preview.

---

## 3. Quick preview of large files

Suppose you have a huge CSV file:

```bash
users.csv
```

Instead of opening the entire file:

```bash
less users.csv
```

You can quickly check its structure:

```bash
head users.csv
```

Example output:

```text
id,name,email,role
1,Rahul,rahul@example.com,admin
2,John,john@example.com,user
3,Ali,ali@example.com,user
```

Very useful for checking:

- CSV files
    
- Log files
    
- JSON files
    
- Configuration files
    
- Database exports
    

---

# 4. Display everything except the last N lines

This is a slightly advanced use.

```bash
head -n -5 file.txt
```

This means:

> Display everything except the last 5 lines.

Example:

```bash
head -n -2 file.txt
```

Useful occasionally in shell scripting.

---

# 5. Combine `head` with other commands

### First 20 lines containing "error"

```bash
head -n 100 server.log | grep ERROR
```

This:

1. Takes the first 100 lines.
    
2. Searches for `ERROR`.
    

---

### Preview directory output

```bash
ls -la | head
```

Show only the first few entries.

Or:

```bash
ps aux | head
```

Quickly inspect running processes.

---

# Real Developer Examples

### Check the beginning of `.env.example`

```bash
head .env.example
```

### Check the beginning of a Docker log

```bash
docker logs container_name | head
```

### Check the first API records in a CSV

```bash
head -n 5 users.csv
```

### Check the first lines of a system log

```bash
head -n 50 /var/log/syslog
```

---

# `head` vs `tail`

|Command|Purpose|
|---|---|
|`head file.txt`|First 10 lines|
|`tail file.txt`|Last 10 lines|
|`head -n 5 file.txt`|First 5 lines|
|`tail -n 5 file.txt`|Last 5 lines|
|`tail -f file.txt`|Watch new lines live|

---

## A useful combination: View a specific range of lines

Suppose you want to see **lines 10 to 20**:

```bash
head -n 20 file.txt | tail -n 11
```

How it works:

```text
head -n 20
     ↓
Gets lines 1–20
     ↓
tail -n 11
     ↓
Gets the last 11 lines
     ↓
Lines 10–20
```

Although for this purpose, later you'll learn better tools like `sed` and `awk`.

---

## Quick memory trick 🧠

```text
head → beginning of file
tail → end of file
less → navigate large file
cat  → print/concatenate file
```

### Your Linux command toolkit so far

```text
cat   → Display entire small file
less  → Read large file interactively
head  → Display beginning
tail  → Display end / follow logs
```

**Next command I recommend: `grep` 🔥**

This is one of the most important commands for a developer because it lets you **search text, logs, source code, and command output directly from the terminal**.