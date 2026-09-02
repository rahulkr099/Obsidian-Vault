# Linux `wc` Command 🔢

`wc` stands for **Word Count**.

But it can do more than count words. It can count:

- Lines
    
- Words
    
- Characters
    
- Bytes
    
- Maximum line length
    

It is a very useful Linux filter command.

## Basic Syntax

```bash
wc [OPTIONS] FILE
```

---

# 1. Basic `wc`

Suppose `file.txt` contains:

```text
Hello World
I am learning Linux
MERN Stack Developer
```

Run:

```bash
wc file.txt
```

Output might look like:

```text
3 9 56 file.txt
```

The order is:

```text
Lines  Words  Bytes  Filename
```

So:

- `3` → lines
    
- `9` → words
    
- `56` → bytes
    

⚠️ The exact byte count depends on spaces and newline characters.

---

# 2. Count Lines with `-l`

```bash
wc -l file.txt
```

Output:

```text
3 file.txt
```

This is one of the most commonly used forms of `wc`.

### Developer example

Count JavaScript files:

```bash
find src -name "*.js" | wc -l
```

---

# 3. Count Words with `-w`

```bash
wc -w file.txt
```

Example output:

```text
9 file.txt
```

---

# 4. Count Characters with `-m`

```bash
wc -m file.txt
```

Useful when dealing with text length.

For example:

```bash
echo "Hello Rahul" | wc -m
```

---

# 5. Count Bytes with `-c`

```bash
wc -c file.txt
```

Difference:

```text
-m → characters
-c → bytes
```

For normal English text, they are often similar.

For Unicode characters like Hindi:

```text
नमस्ते
```

the byte count and character count can be different.

---

# 6. Count Maximum Line Length

Use `-L`:

```bash
wc -L file.txt
```

This returns the length of the longest line.

Example:

```text
42 file.txt
```

Meaning the longest line contains 42 characters.

---

# Using `wc` with Pipes 🔥

This is where `wc` becomes more useful.

## Count files

```bash
ls | wc -l
```

This counts how many lines `ls` outputs.

But a better approach for scripting is usually `find`:

```bash
find . -maxdepth 1 -type f | wc -l
```

---

## Count search results

How many `console.log` statements exist?

```bash
grep -r "console.log" src/ | wc -l
```

Or:

```bash
grep -rn "console.log" src/ | wc -l
```

---

## Count running Node processes

```bash
ps aux | grep node | wc -l
```

⚠️ This can count the `grep node` command itself too. A cleaner pattern is:

```bash
pgrep -c node
```

Nice example of how Linux often has a specialized command for common tasks.

---

# Count Unique Items

Suppose `languages.txt` contains:

```text
JavaScript
Python
JavaScript
React
Python
```

Count unique technologies:

```bash
sort -u languages.txt | wc -l
```

Output:

```text
3
```

---

# Real Developer Examples 🚀

### Count lines of code

For JavaScript files:

```bash
find src -name "*.js" -type f -exec cat {} + | wc -l
```

For React projects:

```bash
find src -type f \( -name "*.js" -o -name "*.jsx" \) -exec cat {} + | wc -l
```

### Count API routes

```bash
grep -r "router.get" src/ | wc -l
```

### Count errors in logs

```bash
grep "ERROR" server.log | wc -l
```

### Count unique errors

```bash
grep "ERROR" server.log | sort -u | wc -l
```

---

# Useful Options Cheat Sheet

|Option|Meaning|
|---|---|
|`wc file.txt`|Lines, words, bytes|
|`wc -l`|Count lines|
|`wc -w`|Count words|
|`wc -m`|Count characters|
|`wc -c`|Count bytes|
|`wc -L`|Longest line length|

---

# A Powerful Pipeline

Suppose you want to know how many unique error messages exist:

```bash
grep "ERROR" server.log | sort -u | wc -l
```

Pipeline:

```text
server.log
   ↓
grep ERROR
   ↓
sort -u
   ↓
wc -l
   ↓
Number of unique errors
```

---

## Mental Model 🧠

```text
wc = Count things

-l → Lines
-w → Words
-m → Characters
-c → Bytes
-L → Longest line
```

### Your Linux filter toolkit so far

```text
cat    → Display files
less   → Navigate files
head   → First lines
tail   → Last lines / live logs
grep   → Search patterns
sort   → Sort lines
uniq   → Handle duplicates
wc     → Count
```

### Next command recommendation: `cut` ✂️

`cut` is very useful for extracting specific columns from text, CSV files, `/etc/passwd`, logs, and command output. It will introduce you to **field-based text processing**, which is an important terminal skill.