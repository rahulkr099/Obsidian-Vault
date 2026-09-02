# Linux Redirection (`>`, `>>`, `<`) 🔥

Until now, you've been running commands and seeing output in the terminal.

But Linux lets you **redirect input and output** somewhere else.

For example:

```text
Command → Terminal
```

You can change it to:

```text
Command → File
```

This is called **redirection**.

---

# First Understand: stdin, stdout, stderr 🧠

Every Linux command has three standard streams:

```text
0 → stdin   → Standard Input
1 → stdout  → Standard Output
2 → stderr  → Standard Error
```

Visual:

```text
                ┌── stdout (1) → Normal output
Command ────────┤
                ├── stderr (2) → Error messages
                │
                └── stdin  (0) ← Input
```

Normally:

- Keyboard provides input
    
- Terminal displays output
    
- Terminal displays errors
    

Redirection lets us change this.

---

# 1. Output Redirection: `>`

The `>` operator sends output to a file.

```bash
command > file.txt
```

Example:

```bash
echo "Hello Rahul" > hello.txt
```

Now:

```bash
cat hello.txt
```

Output:

```text
Hello Rahul
```

---

## ⚠️ Important: `>` Overwrites

Suppose:

```bash
echo "First line" > notes.txt
```

Then:

```bash
echo "Second line" > notes.txt
```

Now `notes.txt` contains only:

```text
Second line
```

The first content was overwritten.

### Mental model

```text
> = Create / Overwrite
```

---

# 2. Append Output: `>>`

If you don't want to overwrite, use:

```bash
command >> file.txt
```

Example:

```bash
echo "First line" > notes.txt
echo "Second line" >> notes.txt
echo "Third line" >> notes.txt
```

Now:

```bash
cat notes.txt
```

Output:

```text
First line
Second line
Third line
```

### Mental model

```text
>  → overwrite
>> → append
```

---

# 3. Input Redirection: `<`

Normally commands receive input from the keyboard.

You can provide input from a file:

```bash
command < file.txt
```

Example:

```bash
wc -l < users.txt
```

This counts lines from `users.txt`.

Compare:

```bash
wc -l users.txt
```

vs:

```bash
wc -l < users.txt
```

The second version outputs only the count because `wc` doesn't receive the filename argument.

---

# 4. Pipes vs Redirection

These are related but different.

### Pipe

```bash
command1 | command2
```

Connects:

```text
Command → Command
```

### Redirection

```bash
command > file
```

Connects:

```text
Command → File
```

Visual:

```text
PIPE

Command1 → Command2


REDIRECTION

Command → File
```

You can combine them:

```bash
grep ERROR server.log | sort | uniq -c > error-report.txt
```

Flow:

```text
server.log
   ↓
grep ERROR
   ↓
sort
   ↓
uniq -c
   ↓
error-report.txt
```

---

# 5. Redirect stderr: `2>`

Remember:

```text
1 → stdout
2 → stderr
```

Normal output:

```bash
command > output.txt
```

Error output:

```bash
command 2> errors.txt
```

Example:

```bash
ls existing-file missing-file > output.txt 2> errors.txt
```

Now:

### `output.txt`

```text
existing-file
```

### `errors.txt`

Contains the error message about `missing-file`.

This is extremely useful when debugging.

---

# 6. Redirect stdout and stderr Separately

```bash
command > output.txt 2> errors.txt
```

Example:

```bash
npm run build > build-output.log 2> build-errors.log
```

Now you have:

```text
Normal logs → build-output.log
Errors      → build-errors.log
```

---

# 7. Redirect Both stdout and stderr 🔥

A common pattern:

```bash
command > output.log 2>&1
```

Meaning:

```text
stdout → output.log
stderr → stdout → output.log
```

Example:

```bash
npm run build > build.log 2>&1
```

Both normal output and errors go into:

```text
build.log
```

---

## Easier Bash Syntax

In Bash, you can write:

```bash
command &> output.log
```

This redirects both:

```text
stdout + stderr → output.log
```

Example:

```bash
npm run build &> build.log
```

---

# 8. Redirect Errors to `/dev/null`

Sometimes you want to ignore errors.

```bash
command 2> /dev/null
```

Example:

```bash
find / -name "something" 2> /dev/null
```

Why?

Some directories may produce:

```text
Permission denied
```

Sending stderr to `/dev/null` hides those errors.

---

# What is `/dev/null`? 🕳️

Think of it as a **black hole for data**.

```text
Output → /dev/null → Gone forever
```

Example:

```bash
echo "Hello" > /dev/null
```

You won't see anything.

---

# 9. Discard Normal Output

```bash
command > /dev/null
```

Example:

```bash
npm install > /dev/null
```

⚠️ Usually not recommended while debugging because you lose useful information.

---

# 10. Discard Everything

```bash
command > /dev/null 2>&1
```

This means:

```text
stdout → /dev/null
stderr → stdout → /dev/null
```

Nothing appears.

Example:

```bash
some-command > /dev/null 2>&1
```

---

# 11. Redirection with `tee`

You already learned `tee`.

Compare:

### Only save output

```bash
npm run build > build.log
```

You won't see output in the terminal.

### Save + see output

```bash
npm run build | tee build.log
```

You get:

```text
npm run build
     │
     ▼
    tee
   ↙   ↘
Terminal  build.log
```

To capture errors too:

```bash
npm run build 2>&1 | tee build.log
```

🔥 Very useful developer command.

---

# 12. Order Matters! ⚠️

These two commands look similar but behave differently.

### Correct

```bash
command > output.log 2>&1
```

First:

```text
stdout → output.log
```

Then:

```text
stderr → same place as stdout
```

Both go to `output.log`.

---

### Different behavior

```bash
command 2>&1 > output.log
```

First:

```text
stderr → current stdout (terminal)
```

Then:

```text
stdout → output.log
```

Result:

```text
stdout → output.log
stderr → terminal
```

So **redirection order matters**.

This is an important Linux concept.

---

# 13. Useful Real Developer Examples 🚀

### Save all npm build logs

```bash
npm run build > build.log 2>&1
```

### Save and watch logs

```bash
npm run dev 2>&1 | tee server.log
```

### Find errors and save report

```bash
grep "ERROR" server.log > errors.txt
```

### Create a unique list

```bash
sort users.txt | uniq > unique-users.txt
```

### Append a timestamp to logs

```bash
date >> application.log
```

### Ignore permission errors

```bash
find / -name "*.log" 2> /dev/null
```

---

# Quick Cheat Sheet 🧠

|Symbol|Meaning|
|---|---|
|`>`|Redirect output (overwrite)|
|`>>`|Redirect output (append)|
|`<`|Redirect input|
|`2>`|Redirect errors|
|`2>>`|Append errors|
|`2>&1`|Send stderr to stdout|
|`&>`|Redirect stdout + stderr|
|`/dev/null`|Discard output|

---

# A Practical Exercise 🔥

Create a file:

```bash
printf "React\nNode\nReact\nMongoDB\nNode\nReact\n" > tech.txt
```

Now create a frequency report:

```bash
sort tech.txt | uniq -c | sort -nr > report.txt
```

Check it:

```bash
cat report.txt
```

Output:

```text
3 React
2 Node
1 MongoDB
```

You've now combined:

```text
Input
  ↓
sort
  ↓
uniq -c
  ↓
sort -nr
  ↓
> Save into file
```

That's a real Linux data-processing pipeline. 🚀

---

# Your Linux Learning Path So Far

```text
Linux Text Processing
│
├── cat
├── less
├── head
├── tail
├── grep
├── sort
├── uniq
├── wc
├── cut
├── tr
├── tee
├── paste
├── sed
├── awk
├── pipes |
└── redirection > >> < 🔥
```

## Next Topic: Command Chaining (`&&`, `||`, `;`) ⚡

This teaches you how to control command execution:

```bash
npm install && npm run dev
```

```bash
mkdir project || echo "Directory already exists"
```

```bash
command1 ; command2
```

This is especially useful for automation, shell scripts, and your developer workflow.