# Linux `tail` Command

The `tail` command displays the **last part of a file**. By default, it shows the **last 10 lines**.

This is extremely useful for developers when checking **logs, errors, and server output**.

## Basic Syntax

```bash
tail [OPTIONS] FILE
```

---

## 1. Display the last 10 lines

```bash
tail file.txt
```

Example:

```bash
tail server.log
```

Output:

```text
Server started on port 5000
Connected to MongoDB
GET /api/users 200
POST /api/auth/login 401
Error: Invalid token
```

---

## 2. Display a specific number of lines

Use `-n`.

### Last 5 lines

```bash
tail -n 5 server.log
```

Shortcut:

```bash
tail -5 server.log
```

But I recommend using `-n 5` because it's clearer.

---

## 3. The Developer Superpower: `tail -f` 🔥

```bash
tail -f server.log
```

The `-f` means **follow**.

`tail` will keep running and automatically display new lines added to the file.

Imagine your backend writes logs like:

```text
Server started
GET /api/users
POST /api/login
Database query executed
```

As new requests arrive, you'll see them live in your terminal.

### Exit `tail -f`

Press:

```text
Ctrl + C
```

---

# Real Backend Example

Suppose your Node.js application writes logs to:

```text
logs/app.log
```

Run:

```bash
tail -f logs/app.log
```

Then make an API request.

You might immediately see:

```text
GET /api/products 200
POST /api/auth/login 200
GET /api/users 500
```

This makes debugging much easier.

---

## 4. Follow the last N lines

Sometimes a log file is huge.

You don't want to see the default last 10 lines.

```bash
tail -n 50 -f server.log
```

Meaning:

1. Show the last 50 existing lines.
    
2. Keep watching for new lines.
    

This is a command you'll use a lot:

```bash
tail -n 100 -f logs/app.log
```

---

## 5. Watch multiple files

```bash
tail -f app.log error.log
```

Output will indicate which file the lines come from.

Useful when monitoring:

```text
app.log
error.log
database.log
```

Example:

```bash
tail -f logs/app.log logs/error.log
```

---

## 6. Start from a specific point

### Everything after line 10

```bash
tail -n +10 file.txt
```

This means:

> Start displaying from line 10.

Example:

```bash
tail -n +20 file.txt
```

Shows everything from line 20 onward.

⚠️ Notice the difference:

```bash
tail -n 20 file.txt
```

= Last 20 lines.

```bash
tail -n +20 file.txt
```

= Start from line 20.

---

# `tail` vs `head`

|Command|What it shows|
|---|---|
|`head file.txt`|First 10 lines|
|`tail file.txt`|Last 10 lines|
|`head -n 20 file.txt`|First 20 lines|
|`tail -n 20 file.txt`|Last 20 lines|

---

# Combining `tail` with Pipes

### Get the last 20 lines and search for errors

```bash
tail -n 20 server.log | grep ERROR
```

### Last 100 lines containing MongoDB

```bash
tail -n 100 server.log | grep MongoDB
```

### Monitor logs and filter errors live

```bash
tail -f server.log | grep ERROR
```

This is a very useful debugging workflow.

---

## Practical commands worth remembering

```bash
# Last 50 lines
tail -n 50 server.log

# Watch logs live
tail -f server.log

# Last 100 lines + live updates
tail -n 100 -f server.log

# Watch logs and show only errors
tail -f server.log | grep ERROR
```

### Terminal-first developer tip 💡

When your backend is running in production, one of the first debugging patterns you'll encounter is:

```bash
tail -n 100 -f application.log
```

Then reproduce the bug and watch what happens in real time.

**Next natural command: `head`** — it's the opposite of `tail` and has some surprisingly useful developer use cases.