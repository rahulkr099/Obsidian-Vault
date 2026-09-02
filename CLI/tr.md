# Linux `tr` Command 🔄

`tr` stands for **translate**. It is used to **transform characters** from standard input.

You can use it to:

- Replace characters
    
- Convert lowercase ↔ uppercase
    
- Delete characters
    
- Squeeze repeated characters
    

Unlike many commands, `tr` generally works with **stdin**, so you'll often use it with pipes.

## Basic Syntax

```bash
tr [OPTIONS] SET1 [SET2]
```

Think:

```text
SET1 → characters to find
SET2 → characters to replace them with
```

---

# 1. Replace Characters

```bash
echo "hello world" | tr 'a-z' 'A-Z'
```

Output:

```text
HELLO WORLD
```

Here:

```text
a-z → lowercase letters
A-Z → uppercase letters
```

---

# 2. Convert Uppercase to Lowercase

```bash
echo "HELLO RAHUL" | tr 'A-Z' 'a-z'
```

Output:

```text
hello rahul
```

---

# 3. Replace Spaces with Another Character

Suppose:

```text
Hello Rahul Kumar
```

Replace spaces with `_`:

```bash
echo "Hello Rahul Kumar" | tr ' ' '_'
```

Output:

```text
Hello_Rahul_Kumar
```

Useful when generating simple filenames.

---

# 4. Replace Delimiters

Suppose CSV-like data:

```text
Rahul,Aman,Zaid
```

Convert commas into new lines:

```bash
echo "Rahul,Aman,Zaid" | tr ',' '\n'
```

Output:

```text
Rahul
Aman
Zaid
```

Very useful for processing environment variables like `$PATH`.

```bash
echo "$PATH" | tr ':' '\n'
```

Example output:

```text
/usr/local/bin
/usr/bin
/bin
/home/rahul/.local/bin
```

---

# 5. Delete Characters with `-d` 🔥

Use `-d`.

Remove all digits:

```bash
echo "Rahul123Developer456" | tr -d '0-9'
```

Output:

```text
RahulDeveloper
```

Remove spaces:

```bash
echo "Hello Rahul Kumar" | tr -d ' '
```

Output:

```text
HelloRahulKumar
```

Remove newlines:

```bash
cat file.txt | tr -d '\n'
```

This joins everything into one line.

Better without unnecessary `cat`:

```bash
tr -d '\n' < file.txt
```

---

# 6. Squeeze Repeated Characters with `-s`

This is a very useful feature.

Suppose:

```text
Hello     Rahul
```

There are multiple spaces.

Run:

```bash
echo "Hello     Rahul" | tr -s ' '
```

Output:

```text
Hello Rahul
```

`-s` means **squeeze repeated characters**.

---

## Remove Multiple Blank Lines

```bash
tr -s '\n' < file.txt
```

This converts repeated newlines into a single newline.

---

# 7. Delete + Squeeze Together

You can combine options.

Suppose:

```text
Hello,,,World,,,,Linux
```

Run:

```bash
echo "Hello,,,World,,,,Linux" | tr -s ','
```

Output:

```text
Hello,World,Linux
```

---

# 8. Use Character Classes

Instead of writing:

```text
A-Z
```

You can use POSIX character classes.

### Lowercase

```bash
tr '[:lower:]' '[:upper:]'
```

Example:

```bash
echo "hello linux" | tr '[:lower:]' '[:upper:]'
```

Output:

```text
HELLO LINUX
```

### Other useful classes

|Class|Meaning|
|---|---|
|`[:lower:]`|Lowercase letters|
|`[:upper:]`|Uppercase letters|
|`[:digit:]`|Numbers|
|`[:alpha:]`|Letters|
|`[:alnum:]`|Letters + numbers|
|`[:space:]`|Whitespace|

---

# 9. Real Developer Examples 🔥

## Convert text to lowercase

```bash
echo "NODEJS EXPRESS MONGODB" | tr 'A-Z' 'a-z'
```

Useful in shell scripts.

---

## Generate simple slug-like text

```bash
echo "My MERN Stack Project" | tr 'A-Z ' 'a-z-'
```

Output:

```text
my-mern-stack-project
```

For production-grade URL slugs, you'd need more processing, but this shows the idea.

---

## Clean repeated spaces

```bash
echo "Hello     Linux     Developer" | tr -s ' '
```

Output:

```text
Hello Linux Developer
```

---

## Extract unique PATH directories

```bash
echo "$PATH" | tr ':' '\n' | sort -u
```

Pipeline:

```text
$PATH
  ↓
tr ':' '\n'
  ↓
Separate directories into lines
  ↓
sort -u
  ↓
Remove duplicates
```

---

# `tr` vs `sed`

This distinction is useful:

|Command|Best For|
|---|---|
|`tr`|Character-by-character transformation|
|`sed`|Text substitution and line editing|
|`awk`|Field/column processing|

Example:

```bash
tr 'a-z' 'A-Z'
```

Perfect for `tr`.

But replacing a word:

```text
Hello World → Hello Linux
```

Better with `sed`:

```bash
sed 's/World/Linux/'
```

Because `tr` translates **individual characters**, not whole words.

---

# Important Limitation

This will **not work as expected**:

```bash
echo "Hello World" | tr "Hello" "Linux"
```

Why?

Because `tr` maps characters position by position:

```text
H → L
e → i
l → n
l → u
o → x
```

It does **not understand words**.

For word replacement, use `sed`.

---

# Most Useful `tr` Options

|Command|Meaning|
|---|---|
|`tr 'a-z' 'A-Z'`|Lowercase → Uppercase|
|`tr 'A-Z' 'a-z'`|Uppercase → Lowercase|
|`tr ',' '\n'`|Replace comma with newline|
|`tr -d '0-9'`|Delete digits|
|`tr -d ' '`|Delete spaces|
|`tr -s ' '`|Remove repeated spaces|

---

## Mental Model 🧠

```text
tr = Character Transformer

Replace → tr SET1 SET2
Delete  → tr -d SET
Squeeze → tr -s SET
```

### Your Linux filter toolkit so far 🚀

```text
cat    → Display files
less   → Navigate large files
head   → Beginning of files
tail   → End / follow logs
grep   → Search patterns
sort   → Sort lines
uniq   → Handle duplicates
wc     → Count
cut    → Extract fields
tr     → Transform characters
```

## Next recommended command: `tee` 🔀

`tee` is a very practical command because it lets you **see command output on the terminal while also saving it to a file**. This is especially useful for logs, builds, and debugging pipelines.