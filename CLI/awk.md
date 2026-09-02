# Linux `awk` Command 🔥

`awk` is one of the most powerful text-processing tools in Linux.

You can think of it as a **small programming language designed for processing structured text**.

It is especially useful for:

- Extracting columns
    
- Filtering rows
    
- Calculations
    
- Creating reports
    
- Processing logs
    
- Working with CSV-like data
    

> Simple mental model: **`cut` extracts fields, but `awk` can extract + filter + calculate + format.**

---

# Basic Syntax

```bash
awk 'pattern { action }' file
```

The basic idea:

```text
Input
  ↓
awk reads one line at a time
  ↓
Splits line into fields
  ↓
Checks pattern
  ↓
Performs action
```

---

# 1. Print the Entire Line

Suppose `users.txt`:

```text
Rahul 22 Developer
Aman 25 Designer
Zaid 30 Manager
```

Run:

```bash
awk '{print $0}' users.txt
```

Output:

```text
Rahul 22 Developer
Aman 25 Designer
Zaid 30 Manager
```

Here:

```text
$0 → Entire line
```

---

# 2. Print Specific Columns 🔥

```bash
awk '{print $1}' users.txt
```

Output:

```text
Rahul
Aman
Zaid
```

Fields:

```text
$1 → First column
$2 → Second column
$3 → Third column
```

Example:

```bash
awk '{print $1, $3}' users.txt
```

Output:

```text
Rahul Developer
Aman Designer
Zaid Manager
```

---

# Understanding Fields

Input:

```text
Rahul 22 Developer
```

`awk` sees:

```text
$1      $2       $3
↓       ↓        ↓
Rahul   22       Developer
```

And:

```text
$0 = Rahul 22 Developer
```

---

# 3. Filter Rows Based on Conditions 🔥

Suppose:

```text
Rahul 22 Developer
Aman 25 Designer
Zaid 30 Manager
```

Find people older than 24:

```bash
awk '$2 > 24 {print $0}' users.txt
```

Output:

```text
Aman 25 Designer
Zaid 30 Manager
```

You can also print selected fields:

```bash
awk '$2 > 24 {print $1, $3}' users.txt
```

Output:

```text
Aman Designer
Zaid Manager
```

---

# 4. Filter by Text

Find all Developers:

```bash
awk '$3 == "Developer" {print $1}' users.txt
```

Output:

```text
Rahul
```

---

# 5. Custom Delimiter with `-F`

By default, `awk` uses whitespace as a separator.

For CSV:

```text
Rahul,22,Developer
Aman,25,Designer
Zaid,30,Manager
```

Use:

```bash
awk -F ',' '{print $1, $3}' users.csv
```

Output:

```text
Rahul Developer
Aman Designer
Zaid Manager
```

Here:

```text
-F ',' → Input Field Separator
```

---

# 6. Print Line Numbers

`awk` has a built-in variable called `NR`.

```bash
awk '{print NR, $0}' users.txt
```

Output:

```text
1 Rahul 22 Developer
2 Aman 25 Designer
3 Zaid 30 Manager
```

```text
NR → Current record/line number
```

---

# 7. Count Number of Fields

Use `NF`.

```bash
awk '{print NF}' users.txt
```

For:

```text
Rahul 22 Developer
```

Output:

```text
3
```

```text
NF → Number of fields
```

You can get the last field using:

```bash
awk '{print $NF}' users.txt
```

Output:

```text
Developer
Designer
Manager
```

🔥 `$NF` is extremely useful.

---

# 8. Perform Calculations 🔥

Suppose `products.txt`:

```text
Laptop 50000
Phone 30000
Keyboard 2000
```

Calculate GST-like 18% addition:

```bash
awk '{print $1, $2 * 1.18}' products.txt
```

Output:

```text
Laptop 59000
Phone 35400
Keyboard 2360
```

---

# 9. Calculate Total

Suppose:

```text
Laptop 50000
Phone 30000
Keyboard 2000
```

Run:

```bash
awk '{sum += $2} END {print sum}' products.txt
```

Output:

```text
82000
```

Let's understand:

```text
For every line:
sum = sum + $2

After all lines:
print sum
```

`END` runs after processing the entire file.

---

# 10. Calculate Average

```bash
awk '
{
    sum += $2
    count++
}
END {
    print "Average:", sum / count
}' products.txt
```

Output:

```text
Average: 27333.3
```

This shows why `awk` is like a small programming language.

---

# 11. Use `BEGIN` and `END`

`awk` has special blocks:

```text
BEGIN → Runs before reading input
END   → Runs after reading input
```

Example:

```bash
awk '
BEGIN {
    print "Product Report"
}
{
    print $1, $2
}
END {
    print "Finished"
}' products.txt
```

Output:

```text
Product Report
Laptop 50000
Phone 30000
Keyboard 2000
Finished
```

---

# 12. Formatted Output with `printf`

Instead of `print`:

```bash
awk '{printf "%-15s ₹%d\n", $1, $2}' products.txt
```

Output:

```text
Laptop          ₹50000
Phone           ₹30000
Keyboard        ₹2000
```

Useful for generating reports.

---

# 13. Search for Patterns

Suppose `server.log`:

```text
INFO Server started
ERROR Database failed
INFO User logged in
ERROR Token invalid
```

Find ERROR lines:

```bash
awk '/ERROR/ {print}' server.log
```

Similar to:

```bash
grep "ERROR" server.log
```

But `awk` lets you do more:

```bash
awk '/ERROR/ {print NR, $0}' server.log
```

Output:

```text
2 ERROR Database failed
4 ERROR Token invalid
```

---

# 14. Developer Example: Process Logs 🔥

Suppose access log:

```text
GET /api/users 200
POST /api/login 401
GET /api/products 200
GET /api/users 500
```

Print only failed requests:

```bash
awk '$3 >= 400 {print}' access.log
```

Output:

```text
POST /api/login 401
GET /api/users 500
```

Get only endpoints with errors:

```bash
awk '$3 >= 400 {print $2}' access.log
```

Output:

```text
/api/login
/api/users
```

---

# 15. Count HTTP Status Codes 🔥

Suppose:

```text
GET /api/users 200
POST /api/login 401
GET /api/products 200
GET /api/users 500
POST /api/login 401
```

Run:

```bash
awk '{print $3}' access.log | sort | uniq -c
```

Output:

```text
2 200
2 401
1 500
```

Or do it purely with `awk`:

```bash
awk '{count[$3]++} END {for (status in count) print status, count[status]}' access.log
```

Output order may vary:

```text
200 2
401 2
500 1
```

This introduces **associative arrays** in `awk`.

---

# 16. Use Conditions

You can use normal programming conditions.

### Greater than

```bash
awk '$2 > 20 {print}' file.txt
```

### Equal

```bash
awk '$3 == "Developer" {print}' file.txt
```

### Not equal

```bash
awk '$2 != 200 {print}' file.txt
```

### AND

```bash
awk '$2 > 20 && $3 == "Developer" {print}' file.txt
```

### OR

```bash
awk '$3 == "Developer" || $3 == "Manager" {print}' file.txt
```

---

# 17. Practical `/etc/passwd` Example

The `/etc/passwd` file uses `:`.

Print usernames and shells:

```bash
awk -F ':' '{print $1, $7}' /etc/passwd
```

Example:

```text
root /bin/bash
rahul /bin/bash
```

Print users with UID >= 1000:

```bash
awk -F ':' '$3 >= 1000 {print $1}' /etc/passwd
```

---

# `awk` vs `cut`

Suppose:

```text
Rahul 22 Developer
```

### `cut`

```bash
cut -d ' ' -f 1
```

Good for simple extraction.

### `awk`

```bash
awk '$2 > 20 {print $1}'
```

Can:

- Extract
    
- Filter
    
- Calculate
    

So:

|Tool|Best For|
|---|---|
|`cut`|Simple fixed fields|
|`grep`|Search lines|
|`sed`|Edit text|
|`awk`|Process structured data|

---

# Most Important Built-in Variables 🧠

|Variable|Meaning|
|---|---|
|`$0`|Entire line|
|`$1`|First field|
|`$2`|Second field|
|`$NF`|Last field|
|`NR`|Current line number|
|`NF`|Number of fields|

These are worth memorizing.

---

# Real Developer Commands 🚀

### Print first column

```bash
awk '{print $1}' file.txt
```

### Print last column

```bash
awk '{print $NF}' file.txt
```

### Filter HTTP errors

```bash
awk '$3 >= 400 {print}' access.log
```

### Calculate total

```bash
awk '{sum += $2} END {print sum}' file.txt
```

### CSV processing

```bash
awk -F ',' '{print $1, $3}' users.csv
```

### Count status codes

```bash
awk '{count[$3]++} END {for (x in count) print x, count[x]}' access.log
```

### Find largest value

```bash
awk 'NR == 1 || $2 > max {max = $2} END {print max}' file.txt
```

---

# Mental Model 🧠

```text
awk = Text Processing + Programming

Input line
    ↓
Split into fields
    ↓
Pattern/Condition
    ↓
Action
    ↓
Result
```

The core pattern to remember is:

```bash
awk 'condition { action }' file
```

Example:

```bash
awk '$3 >= 400 {print $2}' access.log
```

Read it like English:

> If column 3 is greater than or equal to 400, print column 2.

---

## Your Linux Filter Toolkit 🎯

```text
cat    → Display files
less   → Navigate files
head   → Beginning of files
tail   → End/follow logs
grep   → Search text
sort   → Sort lines
uniq   → Handle duplicates
wc     → Count
cut    → Extract fields
tr     → Transform characters
tee    → Display + save
paste  → Merge columns
sed    → Stream editing
awk    → Advanced text processing 🔥
```

### My recommendation for the next topic

You've now covered the major **classic Linux filters**. A great next step is to learn **pipes (`|`), redirection (`>`, `>>`, `<`), and command chaining** properly.

That's where all these commands become much more powerful because you'll start combining them like LEGO blocks:

```bash
grep "ERROR" server.log | awk '{print $NF}' | sort | uniq -c | sort -nr
```

This is the point where Linux command-line skills start feeling like a real superpower. 🚀