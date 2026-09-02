# Next Topic: Linux Pipes (`|`) 🔥

Now that you know commands like `grep`, `sort`, `uniq`, `wc`, `cut`, `tr`, `sed`, and `awk`, it's time to learn how to **connect them together**.

The pipe operator is:

```bash
|
```

## What is a Pipe?

A pipe sends the **output of one command** directly as the **input of another command**.

### Basic idea

```text
Command 1 → output → Command 2
```

Using a pipe:

```bash
command1 | command2
```

---

# 1. Simple Example

Suppose you want to search for "ERROR" inside a log:

```bash
grep "ERROR" server.log
```

Now suppose you want to count those errors:

```bash
grep "ERROR" server.log | wc -l
```

Flow:

```text
server.log
    ↓
grep "ERROR"
    ↓
Matching lines
    ↓
wc -l
    ↓
Number of errors
```

---

# 2. Pipe with `sort` and `uniq`

Suppose `languages.txt` contains:

```text
React
Node
React
MongoDB
Node
React
```

Run:

```bash
sort languages.txt | uniq -c
```

Output:

```text
      1 MongoDB
      2 Node
      3 React
```

Flow:

```text
File
 ↓
sort
 ↓
React
React
React
Node
Node
MongoDB
 ↓
uniq -c
 ↓
Count occurrences
```

---

# 3. Multiple Pipes 🔥

You can chain many commands:

```bash
command1 | command2 | command3 | command4
```

Example:

```bash
grep "ERROR" server.log | sort | uniq -c | sort -nr
```

Flow:

```text
server.log
     │
     ▼
grep ERROR
     │
     ▼
sort
     │
     ▼
uniq -c
     │
     ▼
sort -nr
     │
     ▼
Most common errors
```

This is a real-world Linux workflow.

---

# 4. Developer Example: Find Most Common HTTP Status Codes

Suppose `access.log`:

```text
GET /api/users 200
POST /api/login 401
GET /api/products 200
GET /api/users 500
POST /api/login 401
GET /api/orders 200
```

Command:

```bash
awk '{print $3}' access.log | sort | uniq -c | sort -nr
```

Output:

```text
3 200
2 401
1 500
```

Let's break it down:

### Step 1

```bash
awk '{print $3}' access.log
```

Output:

```text
200
401
200
500
401
200
```

### Step 2

```bash
sort
```

Output:

```text
200
200
200
401
401
500
```

### Step 3

```bash
uniq -c
```

Output:

```text
3 200
2 401
1 500
```

### Step 4

```bash
sort -nr
```

Sort by count descending.

---

# 5. Pipes Don't Modify Original Files

Important concept:

```bash
sort file.txt | uniq
```

This processes data **in memory/stream**.

Your original `file.txt` remains unchanged.

If you want to save output, you'll learn redirection:

```bash
sort file.txt | uniq > clean.txt
```

---

# 6. A Very Useful Developer Example

Find all `console.log` statements:

```bash
grep -rn "console.log" src/
```

Count them:

```bash
grep -rn "console.log" src/ | wc -l
```

Find unique files containing them:

```bash
grep -rl "console.log" src/
```

Count those files:

```bash
grep -rl "console.log" src/ | wc -l
```

---

# 7. Pipe vs Temporary Files

Without pipes, you might do:

```bash
grep ERROR server.log > errors.txt
sort errors.txt > sorted-errors.txt
uniq -c sorted-errors.txt
```

With pipes:

```bash
grep ERROR server.log | sort | uniq -c
```

Much cleaner.

This is one reason Linux terminals are so powerful.

---

# 8. `tee` Inside a Pipeline

Suppose your pipeline is complicated:

```bash
grep "ERROR" server.log | sort | uniq -c | sort -nr
```

You want to inspect the output after `grep`.

Use `tee`:

```bash
grep "ERROR" server.log | tee errors.txt | sort | uniq -c | sort -nr
```

Now you get:

```text
grep
  ↓
tee ───→ errors.txt
  ↓
sort
  ↓
uniq -c
  ↓
sort -nr
```

`tee` is excellent for debugging pipelines.

---

# 9. Pipe Command Output into `less`

Sometimes command output is huge:

```bash
git log
```

Use:

```bash
git log | less
```

Or:

```bash
ps aux | less
```

Now you can:

- Scroll
    
- Search
    
- Navigate
    

Press:

```text
q
```

to exit.

---

# 10. Pipe into `grep`

Find Node processes:

```bash
ps aux | grep node
```

Find a specific port:

```bash
ss -tulpn | grep 5000
```

Check environment variables:

```bash
env | grep PATH
```

---

# Understanding Linux Philosophy 🧠

Linux follows a powerful idea:

> **Do one thing well, then connect small tools together.**

For example:

```text
grep → search
sort → arrange
uniq → count duplicates
wc   → count
awk  → process fields
```

Individually, each command is simple.

Together:

```bash
grep "ERROR" server.log \
  | awk '{print $NF}' \
  | sort \
  | uniq -c \
  | sort -nr
```

They become extremely powerful.

---

# Important Pipe Pattern to Memorize 🔥

```bash
COMMAND | FILTER | FILTER | RESULT
```

Example:

```bash
cat access.log | grep ERROR | sort | uniq -c
```

But remember: avoid unnecessary `cat`.

Better:

```bash
grep ERROR access.log | sort | uniq -c
```

---

## Your First Terminal Data Pipeline

Try this:

```bash
printf "React\nNode\nReact\nMongoDB\nNode\nReact\n" \
  | sort \
  | uniq -c \
  | sort -nr
```

Expected output:

```text
      3 React
      2 Node
      1 MongoDB
```

Congratulations 🎉 — you're now combining Linux filters into a real pipeline.

---

# Next Topic: Redirection (`>`, `>>`, `<`) 🔥

This is the perfect next step because you'll learn how to control where command input and output go:

```bash
command > output.txt
command >> output.txt
command < input.txt
```

Then after that, I recommend learning:

```text
1. Pipes (Done ✅)
2. Redirection ← Next
3. stdin / stdout / stderr
4. Command chaining (&&, ||, ;)
5. xargs
6. find
7. Regular Expressions
8. Shell scripting basics
```

This sequence will make your Linux terminal skills much stronger, especially for your developer workflow.