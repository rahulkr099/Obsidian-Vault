# Linux `sort` Command 🔢🔤

The `sort` command is used to **arrange lines of text in a specific order**.

By default, it sorts lines **alphabetically**.

## Basic Syntax

```bash
sort [OPTIONS] FILE
```

---

## 1. Basic Alphabetical Sorting

Suppose `names.txt` contains:

```text
Rahul
Aman
Zaid
Bharat
```

Run:

```bash
sort names.txt
```

Output:

```text
Aman
Bharat
Rahul
Zaid
```

⚠️ `sort` does **not modify the original file**. It only prints the sorted result.

---

# 2. Sort in Reverse Order

Use `-r`:

```bash
sort -r names.txt
```

Output:

```text
Zaid
Rahul
Bharat
Aman
```

---

# 3. Numeric Sorting 🔥

Consider `numbers.txt`:

```text
100
2
50
10
```

If you run:

```bash
sort numbers.txt
```

Output:

```text
10
100
2
50
```

Why? Because normal `sort` treats everything as **text**.

Use `-n` for numbers:

```bash
sort -n numbers.txt
```

Output:

```text
2
10
50
100
```

---

# 4. Reverse Numeric Sorting

```bash
sort -nr numbers.txt
```

Output:

```text
100
50
10
2
```

You can combine options:

```text
-n → numeric
-r → reverse
```

So:

```bash
sort -nr
```

means:

> Sort numbers in descending order.

---

# 5. Remove Duplicates with `-u`

Suppose:

```text
React
Node.js
React
MongoDB
Node.js
```

Run:

```bash
sort -u technologies.txt
```

Output:

```text
MongoDB
Node.js
React
```

`-u` means **unique**.

This is equivalent to:

```bash
sort technologies.txt | uniq
```

But:

```bash
sort -u technologies.txt
```

is shorter and cleaner.

---

# 6. Sort by a Specific Column

This is extremely useful.

Suppose `users.txt`:

```text
Rahul 25
Aman 30
Zaid 20
```

Sort by age:

```bash
sort -k2 -n users.txt
```

Output:

```text
Zaid 20
Rahul 25
Aman 30
```

Explanation:

```text
-k2 → Sort using column 2
-n  → Treat it as a number
```

---

# 7. Reverse Column Sorting

```bash
sort -k2 -nr users.txt
```

Output:

```text
Aman 30
Rahul 25
Zaid 20
```

---

# 8. Sort CSV Files

Suppose:

```text
name,age,role
Rahul,25,developer
Aman,30,designer
Zaid,20,manager
```

Sort by age:

```bash
sort -t',' -k2 -n users.csv
```

Explanation:

```text
-t',' → delimiter is comma
-k2   → second column
-n    → numeric sorting
```

---

# 9. Ignore Case

Normally uppercase and lowercase can affect sorting.

Use:

```bash
sort -f names.txt
```

`-f` means **ignore case**.

Example:

```text
apple
Banana
cherry
Apple
```

```bash
sort -f fruits.txt
```

---

# 10. Check Whether a File Is Already Sorted

Use `-c`:

```bash
sort -c names.txt
```

If the file is sorted correctly, there may be no output.

If not:

```text
sort: names.txt:3: disorder: Aman
```

Useful in shell scripts and validation.

---

# 11. Save Sorted Output

Remember: `sort` doesn't modify the original file.

To save the result:

```bash
sort names.txt > sorted_names.txt
```

Now:

```text
names.txt
```

remains unchanged, while:

```text
sorted_names.txt
```

contains sorted data.

---

# Using `sort` with Pipes 🔥

This is where Linux becomes powerful.

Suppose you have a log file:

```text
ERROR
INFO
ERROR
WARNING
INFO
ERROR
```

Find unique log types:

```bash
cat server.log | sort | uniq
```

Better:

```bash
sort server.log | uniq
```

Even better:

```bash
sort -u server.log
```

---

## Count Frequency of Items

This is a classic Linux pattern:

```bash
sort file.txt | uniq -c
```

Example input:

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

---

# Sort by Frequency 🔥

You can find the most common item:

```bash
sort file.txt | uniq -c | sort -nr
```

Example:

```text
      3 React
      2 Node
      1 MongoDB
```

Let's understand the pipeline:

```text
file
 ↓
sort
 ↓
uniq -c
 ↓
sort -nr
 ↓
Most frequent first
```

This pipeline concept is one of the most important things in Linux.

---

# Real Developer Examples

### Find duplicate lines in a file

```bash
sort file.txt | uniq -d
```

### Get unique API endpoints from logs

```bash
grep "/api" server.log | sort -u
```

### Find most common IP addresses in logs

```bash
awk '{print $1}' access.log | sort | uniq -c | sort -nr | head
```

### Sort files by size

```bash
du -h * | sort -h
```

Here `-h` means **human-readable numeric sorting**.

Example values:

```text
500K
2M
10M
1G
```

Normal numeric sorting won't understand these units correctly, but `sort -h` does.

---

# Useful `sort` Options Cheat Sheet

|Option|Meaning|
|---|---|
|`-r`|Reverse order|
|`-n`|Numeric sort|
|`-u`|Remove duplicates|
|`-f`|Ignore case|
|`-k2`|Sort by column 2|
|`-t','`|Specify delimiter|
|`-h`|Human-readable numbers|
|`-c`|Check if already sorted|

---

## Mental Model 🧠

```text
sort
│
├── Alphabetical → sort file.txt
├── Reverse → sort -r file.txt
├── Numbers → sort -n file.txt
├── Unique → sort -u file.txt
└── Column → sort -k2 -n file.txt
```

### Your Linux filter toolkit so far

```text
cat    → Display file
less   → Read large files
head   → First lines
tail   → Last lines / live logs
grep   → Search
sort   → Arrange lines
```

## Next recommended command: `uniq`

`uniq` works beautifully with `sort` and teaches an important detail: **why sorting is often needed before removing duplicates**.