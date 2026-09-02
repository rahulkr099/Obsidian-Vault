# Linux `paste` Command 📋

The `paste` command is used to **merge lines from multiple files side by side**.

Think of it like combining columns in a spreadsheet.

> `cat` combines files vertically.  
> `paste` combines files horizontally.

---

## Basic Syntax

```bash
paste [OPTIONS] FILE1 FILE2
```

---

# 1. Basic Example

Suppose `names.txt` contains:

```text
Rahul
Aman
Zaid
```

And `roles.txt` contains:

```text
Developer
Designer
Manager
```

Run:

```bash
paste names.txt roles.txt
```

Output:

```text
Rahul   Developer
Aman    Designer
Zaid    Manager
```

By default, `paste` uses a **TAB** between columns.

Visual idea:

```text
names.txt        roles.txt

Rahul            Developer
Aman      +      Designer
Zaid             Manager

        ↓ paste

Rahul    Developer
Aman     Designer
Zaid     Manager
```

---

# 2. Use a Custom Delimiter

By default, the delimiter is a tab.

Use `-d` to specify another delimiter.

### Use a comma

```bash
paste -d ',' names.txt roles.txt
```

Output:

```text
Rahul,Developer
Aman,Designer
Zaid,Manager
```

### Use `:`

```bash
paste -d ':' names.txt roles.txt
```

Output:

```text
Rahul:Developer
Aman:Designer
Zaid:Manager
```

---

# 3. Merge More Than Two Files

Suppose:

### `names.txt`

```text
Rahul
Aman
Zaid
```

### `ages.txt`

```text
22
25
30
```

### `roles.txt`

```text
Developer
Designer
Manager
```

Run:

```bash
paste names.txt ages.txt roles.txt
```

Output:

```text
Rahul   22   Developer
Aman    25   Designer
Zaid    30   Manager
```

With a comma delimiter:

```bash
paste -d ',' names.txt ages.txt roles.txt
```

Output:

```text
Rahul,22,Developer
Aman,25,Designer
Zaid,30,Manager
```

This is a simple way to generate CSV-style data.

---

# 4. Serial Mode with `-s` 🔥

Normally, `paste` works vertically:

```text
Rahul
Aman
Zaid
```

With `-s`, it combines lines horizontally.

```bash
paste -s names.txt
```

Output:

```text
Rahul    Aman    Zaid
```

By default, separated by tabs.

Use a comma:

```bash
paste -s -d ',' names.txt
```

Output:

```text
Rahul,Aman,Zaid
```

This is very useful when you want to convert:

```text
React
Node
Express
MongoDB
```

into:

```text
React,Node,Express,MongoDB
```

---

# 5. Different Delimiters

You can provide multiple delimiters:

```bash
paste -d ',:' file1 file2 file3
```

For example:

```text
Rahul,22:Developer
Aman,25:Designer
```

It cycles through the delimiters.

---

# 6. Files with Different Number of Lines

Suppose:

### `names.txt`

```text
Rahul
Aman
Zaid
Ali
```

### `roles.txt`

```text
Developer
Designer
```

Run:

```bash
paste -d ',' names.txt roles.txt
```

Output:

```text
Rahul,Developer
Aman,Designer
Zaid,
Ali,
```

When one file ends, `paste` leaves that column empty.

---

# Real Developer Examples 🚀

## Create CSV from separate files

```bash
paste -d ',' names.txt emails.txt roles.txt > users.csv
```

---

## Combine IDs with usernames

Suppose:

```text
ids.txt
-------
101
102
103
```

```text
users.txt
---------
rahul
aman
zaid
```

Run:

```bash
paste -d ':' ids.txt users.txt
```

Output:

```text
101:rahul
102:aman
103:zaid
```

---

## Convert lines into comma-separated values

```bash
paste -sd ',' technologies.txt
```

Suppose:

```text
React
Node.js
Express
MongoDB
```

Output:

```text
React,Node.js,Express,MongoDB
```

This is a command worth remembering:

```bash
paste -sd ',' file.txt
```

### Breakdown

```text
-s → serial mode
-d → delimiter
',' → comma
```

---

# `cat` vs `paste`

|Command|Combines files how?|
|---|---|
|`cat file1 file2`|Vertically|
|`paste file1 file2`|Horizontally|

Example:

### `cat`

```text
Rahul
Aman
Developer
Designer
```

### `paste`

```text
Rahul    Developer
Aman     Designer
```

---

# Combine `paste` with Other Commands

## Create a comma-separated list

```bash
grep "TODO" file.txt | paste -sd ','
```

---

## Combine usernames and shells

```bash
cut -d ':' -f 1 /etc/passwd > users.txt
cut -d ':' -f 7 /etc/passwd > shells.txt

paste -d ',' users.txt shells.txt
```

Output:

```text
root,/bin/bash
rahul,/bin/bash
```

---

## Useful Options Cheat Sheet

|Option|Meaning|
|---|---|
|`paste file1 file2`|Merge side by side|
|`-d ','`|Use custom delimiter|
|`-s`|Merge serially|
|`paste -sd ',' file`|Convert lines → CSV-style list|

---

## Mental Model 🧠

```text
paste = Join horizontally

File 1        File 2
------        ------
Rahul         Developer
Aman          Designer

       ↓

Rahul    Developer
Aman     Designer
```

### Your Linux text-processing toolkit now 🚀

```text
cat    → Display/combine vertically
less   → Navigate large files
head   → First lines
tail   → Last lines/follow logs
grep   → Search
sort   → Arrange
uniq   → Handle duplicates
wc     → Count
cut    → Extract columns
tr     → Transform characters
tee    → Display + save
paste  → Combine horizontally
```

## Next command I recommend: `sed` 🔥

This is where Linux text processing becomes much more powerful. `sed` lets you **search, replace, delete, and modify text streams directly from the terminal**.