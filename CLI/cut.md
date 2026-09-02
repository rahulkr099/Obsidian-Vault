# Linux `cut` Command ✂️

The `cut` command is used to **extract specific parts of each line** from a file or command output.

You can extract based on:

- Characters
    
- Bytes
    
- Fields/columns
    

For developers, the most useful feature is usually **extracting fields using a delimiter**.

---

# Basic Syntax

```bash
cut [OPTIONS] FILE
```

---

## 1. Extract Specific Characters

Suppose `file.txt` contains:

```text
Rahul Kumar
Aman Singh
Zaid Khan
```

Get characters 1 to 5:

```bash
cut -c 1-5 file.txt
```

Output:

```text
Rahul
Aman 
Zaid 
```

Here:

```text
-c → character positions
```

---

## 2. Extract a Single Character Position

```bash
cut -c 1 file.txt
```

Output:

```text
R
A
Z
```

You can also select multiple positions:

```bash
cut -c 1,3,5 file.txt
```

---

# 3. Extract Fields Using a Delimiter 🔥

This is the most useful usage.

Suppose `users.csv` contains:

```text
Rahul,22,Developer
Aman,25,Designer
Zaid,30,Manager
```

Extract the first column:

```bash
cut -d ',' -f 1 users.csv
```

Output:

```text
Rahul
Aman
Zaid
```

Explanation:

```text
-d ',' → delimiter is comma
-f 1    → select field 1
```

---

## Extract Multiple Fields

Get name and role:

```bash
cut -d ',' -f 1,3 users.csv
```

Output:

```text
Rahul,Developer
Aman,Designer
Zaid,Manager
```

---

## Extract a Range of Fields

```bash
cut -d ',' -f 1-2 users.csv
```

Output:

```text
Rahul,22
Aman,25
Zaid,30
```

---

# 4. Real Linux Example: `/etc/passwd` 🔥

The `/etc/passwd` file uses `:` as a delimiter.

Example:

```text
root:x:0:0:root:/root:/bin/bash
rahul:x:1000:1000:Rahul:/home/rahul:/bin/bash
```

Get usernames:

```bash
cut -d ':' -f 1 /etc/passwd
```

Output:

```text
root
rahul
```

Get usernames and shells:

```bash
cut -d ':' -f 1,7 /etc/passwd
```

Output:

```text
root:/bin/bash
rahul:/bin/bash
```

---

# 5. Extract Everything Except Certain Fields

Use `--complement`.

Suppose:

```text
Rahul,22,Developer
```

Remove the age field:

```bash
cut -d ',' -f 2 --complement users.csv
```

Output:

```text
Rahul,Developer
```

---

# 6. Using `cut` with Pipes 🔥

Suppose:

```bash
ls -l
```

produces:

```text
-rw-r--r-- 1 rahul users 1234 Aug 20 file.txt
```

You might extract a field:

```bash
ls -l | cut -d ' ' -f 9
```

⚠️ But this is fragile because `ls -l` uses variable spacing. For structured data, `awk` is often better.

---

## Extract usernames from `/etc/passwd`

```bash
cat /etc/passwd | cut -d ':' -f 1
```

Better:

```bash
cut -d ':' -f 1 /etc/passwd
```

No unnecessary `cat` 😄

---

# 7. Extract Environment Variable Paths

Check your `PATH`:

```bash
echo $PATH
```

Example:

```text
/usr/local/bin:/usr/bin:/bin:/home/rahul/.local/bin
```

Split it into separate lines:

```bash
echo $PATH | tr ':' '\n'
```

You could also extract specific parts with `cut`:

```bash
echo $PATH | cut -d ':' -f 1
```

---

# `cut` + Other Linux Commands

## Get unique usernames

```bash
cut -d ':' -f 1 /etc/passwd | sort -u
```

---

## Extract API endpoint column from CSV

```bash
cut -d ',' -f 3 api_logs.csv
```

---

## Count unique roles

```bash
cut -d ',' -f 3 users.csv | sort | uniq -c
```

Example output:

```text
      5 Developer
      2 Designer
      3 Manager
```

---

# Important Limitation of `cut`

`cut` works best when data has a **consistent delimiter**.

For example:

```text
Rahul,22,Developer
```

Perfect for:

```bash
cut -d ',' -f 2
```

But if spacing is inconsistent:

```text
Rahul     22    Developer
Aman  25       Designer
```

Then `cut -d ' '` can behave unexpectedly.

For irregular whitespace, use `awk` later.

---

# Most Important Options

|Option|Meaning|
|---|---|
|`-c 1-5`|Extract characters 1–5|
|`-d ','`|Set delimiter|
|`-f 1`|Select field 1|
|`-f 1,3`|Select fields 1 and 3|
|`-f 1-3`|Select range|
|`--complement`|Exclude selected fields|

---

## Mental Model 🧠

```text
cut = Extract parts

Characters → -c
Delimiter  → -d
Fields     → -f
```

### Example to remember

```bash
cut -d ':' -f 1 /etc/passwd
```

Think:

> Split each line using `:` → Give me column 1.

---

## Your Linux filter toolkit 🚀

```text
cat    → Display
less   → Navigate
head   → First lines
tail   → Last lines / follow logs
grep   → Search
sort   → Arrange
uniq   → Remove/count duplicates
wc     → Count
cut    → Extract columns
```

### Next command I recommend: `tr`

`tr` means **translate**. It can replace characters, change lowercase → uppercase, delete characters, and transform text streams. It combines very nicely with `cut`, `grep`, and pipes.