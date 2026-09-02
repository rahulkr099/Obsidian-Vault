# Linux `uniq` Command 🔁

The `uniq` command is used to **find or remove duplicate adjacent lines**.

The word **adjacent** is very important.

## Basic Syntax

```bash
uniq [OPTIONS] FILE
```

---

# 1. Basic Example

Suppose `names.txt` contains:

```text
Rahul
Rahul
Aman
Aman
Zaid
```

Run:

```bash
uniq names.txt
```

Output:

```text
Rahul
Aman
Zaid
```

It removes consecutive duplicate lines.

---

# ⚠️ Important: `uniq` only handles adjacent duplicates

Suppose:

```text
Rahul
Aman
Rahul
Zaid
Aman
```

Now run:

```bash
uniq names.txt
```

Output:

```text
Rahul
Aman
Rahul
Zaid
Aman
```

Nothing is removed because duplicates are **not next to each other**.

That's why we commonly use:

```bash
sort names.txt | uniq
```

First:

```text
sort
```

makes duplicates adjacent:

```text
Aman
Aman
Rahul
Rahul
Zaid
```

Then:

```text
uniq
```

removes duplicates.

---

# 2. The Most Common Pattern

```bash
sort file.txt | uniq
```

Example:

```text
Input
-----
React
Node
React
MongoDB
Node
```

Command:

```bash
sort technologies.txt | uniq
```

Output:

```text
MongoDB
Node
React
```

---

# 3. Count Duplicate Occurrences 🔥

Use `-c`:

```bash
sort file.txt | uniq -c
```

Example:

```text
React
Node
React
MongoDB
React
Node
```

Command:

```bash
sort technologies.txt | uniq -c
```

Output:

```text
      1 MongoDB
      2 Node
      3 React
```

This is extremely useful for analyzing logs.

---

# 4. Show Only Duplicate Lines

Use `-d`:

```bash
sort file.txt | uniq -d
```

Example input:

```text
React
Node
React
MongoDB
Node
```

Output:

```text
Node
React
```

Only items that appear more than once are shown.

---

# 5. Show Only Unique Lines

Use `-u`:

```bash
sort file.txt | uniq -u
```

Example:

```text
React
Node
React
MongoDB
Node
Express
```

Output:

```text
Express
MongoDB
```

Only lines appearing exactly once are displayed.

---

# 6. Ignore Case

Suppose:

```text
React
react
REACT
Node
```

Normally these are considered different.

Use `-i`:

```bash
sort -f technologies.txt | uniq -i
```

Output:

```text
Node
React
```

`-i` means ignore differences in uppercase/lowercase.

---

# 7. Save Unique Results

```bash
sort file.txt | uniq > unique.txt
```

Or shorter:

```bash
sort -u file.txt > unique.txt
```

Both work.

---

# Real Developer Examples 🔥

## Find repeated errors

```bash
grep "ERROR" server.log | sort | uniq -c
```

You might get:

```text
      15 ERROR: Database timeout
       3 ERROR: Invalid token
       1 ERROR: Server crashed
```

---

## Find the most common errors

```bash
grep "ERROR" server.log | sort | uniq -c | sort -nr
```

Pipeline:

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
```

Result: most frequent errors appear first.

---

## Find unique API endpoints

```bash
grep "/api/" server.log | sort -u
```

---

## Count programming languages in a file

```bash
sort languages.txt | uniq -c | sort -nr
```

---

# `uniq` vs `sort -u`

These two can sometimes produce similar results:

```bash
sort file.txt | uniq
```

and:

```bash
sort -u file.txt
```

For simply getting unique sorted lines, I prefer:

```bash
sort -u file.txt
```

But `uniq` is still important because of its powerful options:

```bash
uniq -c   # Count occurrences
uniq -d   # Show duplicates
uniq -u   # Show only unique lines
```

---

# Quick Cheat Sheet

|Command|Meaning|
|---|---|
|`uniq file.txt`|Remove adjacent duplicates|
|`sort file.txt \| uniq`|Remove all duplicates|
|`uniq -c`|Count occurrences|
|`uniq -d`|Show duplicates only|
|`uniq -u`|Show unique lines only|
|`uniq -i`|Ignore case|

---

## Your Linux filter pipeline is growing 🚀

```text
cat    → Display
less   → Navigate
head   → Beginning
tail   → End / Follow
grep   → Search
sort   → Arrange
uniq   → Handle duplicates
```

### A powerful command to remember

```bash
sort file.txt | uniq -c | sort -nr
```

This pattern appears everywhere in Linux log analysis and data processing.

**Next command I'd recommend: `wc` (word count)** — small command, but surprisingly useful for counting lines, words, characters, and analyzing command output.