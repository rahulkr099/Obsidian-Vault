# Linux `tee` Command 🔀

`tee` is a very useful Linux command that **reads input and sends it to two places at the same time**:

1. **Terminal (stdout)** — so you can see the output.
    
2. **A file** — so you can save the output.
    

Think of a plumbing **T-junction**:

```text
           ┌──→ Terminal
Input ──→ tee
           └──→ File
```

That's where the name `tee` comes from.

---

# Basic Syntax

```bash
tee [OPTIONS] FILE
```

Usually used with a pipe:

```bash
command | tee output.txt
```

---

## 1. Basic Example

```bash
echo "Hello Rahul" | tee hello.txt
```

You will see:

```text
Hello Rahul
```

And `hello.txt` will also contain:

```text
Hello Rahul
```

So unlike this:

```bash
echo "Hello Rahul" > hello.txt
```

which only saves to the file, `tee` does both:

```text
Terminal + File
```

---

# 2. `tee` Overwrites by Default

```bash
echo "First line" | tee notes.txt
```

Then:

```bash
echo "Second line" | tee notes.txt
```

The second command overwrites the file.

Result:

```text
Second line
```

---

# 3. Append with `-a`

Use `-a` to append.

```bash
echo "First line" | tee notes.txt
echo "Second line" | tee -a notes.txt
```

Result:

```text
First line
Second line
```

Think:

```text
tee     → overwrite
tee -a  → append
```

---

# 4. Save Command Output While Seeing It 🔥

Suppose you run:

```bash
npm run build
```

and want to save the output for debugging.

Use:

```bash
npm run build | tee build.log
```

Now:

- Build output appears in your terminal.
    
- Output is saved in `build.log`.
    

This is extremely useful.

---

# 5. Debugging with `tee` in a Pipeline

Suppose you have:

```bash
cat users.txt | grep "Developer" | sort
```

You want to inspect the output after `grep`.

You can insert `tee`:

```bash
grep "Developer" users.txt | tee filtered.txt | sort
```

Pipeline:

```text
users.txt
    │
    ▼
grep Developer
    │
    ▼
tee
 ┌──────┴──────┐
 ▼             ▼
sort       filtered.txt
 │
 ▼
Terminal
```

`tee` is great for **debugging complex pipelines**.

---

# 6. Write to Multiple Files

You can provide multiple files:

```bash
echo "Hello Linux" | tee file1.txt file2.txt
```

Both files will contain:

```text
Hello Linux
```

And you'll still see:

```text
Hello Linux
```

in the terminal.

---

# 7. Append to Multiple Files

```bash
echo "New log entry" | tee -a app.log backup.log
```

This appends the same content to both files.

---

# 8. Using `tee` with `sudo` 🔥

This is one of the most important real-world uses.

Suppose you want to write to a protected file:

```bash
/etc/some-config.conf
```

You might think:

```bash
sudo echo "something" > /etc/some-config.conf
```

⚠️ This usually doesn't work as intended.

Why?

Because `sudo` applies to `echo`, but the `>` redirection is handled by your current shell, which may not have permission.

Instead:

```bash
echo "something" | sudo tee /etc/some-config.conf
```

If you don't want the output printed:

```bash
echo "something" | sudo tee /etc/some-config.conf > /dev/null
```

---

## Append to a Protected File

```bash
echo "new configuration" | sudo tee -a /etc/some-config.conf
```

---

# 9. Save `grep` Results

```bash
grep -rn "TODO" src/ | tee todos.txt
```

You can:

- See all TODOs immediately.
    
- Save them to `todos.txt`.
    

---

# 10. Save Error Output Too

Normally:

```bash
command | tee output.log
```

captures only **stdout**.

To capture stderr too:

```bash
command 2>&1 | tee output.log
```

Example:

```bash
npm run build 2>&1 | tee build.log
```

Explanation:

```text
stdout ──┐
         ├──→ tee → Terminal + build.log
stderr ──┘
```

This is very useful when debugging failed builds.

---

# Real Developer Examples 🚀

### Save backend logs temporarily

```bash
npm run dev 2>&1 | tee server.log
```

### Find and save TODO comments

```bash
grep -rn "TODO" src/ | tee todos.txt
```

### Save Git output

```bash
git status | tee git-status.txt
```

### Debug a complex pipeline

```bash
grep "ERROR" server.log \
  | tee errors.txt \
  | sort \
  | uniq -c \
  | sort -nr
```

Here `tee` lets you preserve the raw error lines before further processing.

---

# `>` vs `>>` vs `tee`

|Command|Terminal Output|File|
|---|---|---|
|`command > file`|❌|Overwrite|
|`command >> file`|❌|Append|
|`command \| tee file`|✅|Overwrite|
|`command \| tee -a file`|✅|Append|

---

## Mental Model 🧠

```text
tee = Split output

          → Terminal
Input → tee
          → File
```

### Most useful commands to remember

```bash
# Save output while viewing it
command | tee output.txt

# Append while viewing
command | tee -a output.txt

# Capture errors too
command 2>&1 | tee output.log

# Write to protected file
echo "text" | sudo tee file
```

---

## Your Linux filter toolkit is becoming powerful 🚀

```text
cat    → Display
less   → Navigate
head   → Beginning
tail   → End / Follow
grep   → Search
sort   → Arrange
uniq   → Remove/count duplicates
wc     → Count
cut    → Extract fields
tr     → Transform characters
tee    → Display + Save
```

### Next command recommendation: `paste`

`paste` is another text-processing command that combines files **side-by-side by columns**, which is a nice contrast to `cat`, which combines files vertically.