# Linux stdin, stdout, and stderr 🔥

This is one of the **core concepts of Linux**. Once you understand it, pipes and redirection become much clearer.

Every Linux process normally has **three standard streams**:

```text
0 → stdin   → Standard Input
1 → stdout  → Standard Output
2 → stderr  → Standard Error
```

Think of a command like a machine:

```text
              stdin (0)
                 │
                 ▼
            ┌─────────┐
            │ Command │
            └─────────┘
              │     │
              ▼     ▼
         stdout(1) stderr(2)
```

---

# 1. stdin — Standard Input

`stdin` is where a command receives its input.

By default:

```text
Keyboard → stdin → Command
```

Example:

```bash
cat
```

After running this, type:

```text
Hello Rahul
```

Press Enter, and `cat` prints it back.

Why?

```text
Keyboard
   ↓
stdin
   ↓
cat
   ↓
stdout
   ↓
Terminal
```

Press:

```text
Ctrl + D
```

to signal end of input.

---

# 2. stdout — Standard Output

`stdout` is normal output produced by a command.

Example:

```bash
echo "Hello Rahul"
```

Output:

```text
Hello Rahul
```

Internally:

```text
echo
 ↓
stdout
 ↓
Terminal
```

By default, stdout goes to your terminal.

---

# 3. stderr — Standard Error

`stderr` is used for error messages.

Example:

```bash
ls nonexistent-file
```

Output:

```text
ls: cannot access 'nonexistent-file': No such file or directory
```

This error message goes through:

```text
stderr
```

not stdout.

This separation is very important.

---

# Why Separate stdout and stderr?

Imagine:

```bash
command
```

produces:

```text
Normal result
Normal result
ERROR: Something failed
Normal result
```

Linux separates them internally:

```text
                Command
               /       \
              /         \
         stdout          stderr
            │               │
            ▼               ▼
       Normal output     Errors
```

Even though both appear on your terminal by default.

This allows you to handle them separately.

---

# File Descriptors 🧠

These streams have numbers called **file descriptors**:

|Number|Stream|Meaning|
|---|---|---|
|`0`|stdin|Input|
|`1`|stdout|Normal output|
|`2`|stderr|Error output|

Remember:

```text
0 → Input
1 → Output
2 → Error
```

A simple memory trick:

> **0 comes in, 1 comes out, 2 is for problems.**

---

# 4. Redirect stdout

Normally:

```bash
echo "Hello"
```

Output goes:

```text
stdout → Terminal
```

Redirect it:

```bash
echo "Hello" > output.txt
```

Now:

```text
stdout
   ↓
output.txt
```

Check:

```bash
cat output.txt
```

Output:

```text
Hello
```

---

# Explicit stdout Redirection

These two are equivalent:

```bash
command > output.txt
```

```bash
command 1> output.txt
```

Because:

```text
1 = stdout
```

Usually we omit `1`.

---

# 5. Redirect stderr

Use:

```bash
command 2> errors.txt
```

Example:

```bash
ls existing.txt missing.txt 2> errors.txt
```

Normal output:

```text
existing.txt
```

Still appears in the terminal.

Errors go into:

```text
errors.txt
```

Visual:

```text
                ls
              /    \
             /      \
        stdout      stderr
          │            │
          ▼            ▼
       Terminal    errors.txt
```

---

# 6. Separate stdout and stderr 🔥

You can save them in different files:

```bash
command > output.txt 2> errors.txt
```

Example:

```bash
ls existing.txt missing.txt > output.txt 2> errors.txt
```

Result:

```text
stdout → output.txt
stderr → errors.txt
```

This is extremely useful for debugging.

---

# 7. Pipes Only Connect stdout by Default ⚡

This is a very important concept.

Suppose:

```bash
command | grep something
```

The pipe connects:

```text
stdout → stdin
```

But:

```text
stderr
```

still goes directly to the terminal.

Visual:

```text
              stdout
Command ─────────────────→ Next Command
   │
   │ stderr
   ▼
Terminal
```

---

## Example

```bash
ls existing.txt missing.txt | grep existing
```

You may see:

```text
existing.txt
ls: cannot access 'missing.txt': No such file or directory
```

The error did NOT go through `grep`.

It went directly to stderr → terminal.

---

# 8. Send stderr into stdout: `2>&1` 🔥

This syntax confuses many beginners:

```bash
command 2>&1
```

Let's break it down.

```text
2
↓
stderr

>
↓
Redirect

&1
↓
Wherever stdout currently goes
```

So:

```bash
command > output.txt 2>&1
```

means:

```text
stdout → output.txt
stderr → same destination as stdout
```

Final result:

```text
stdout ──┐
         ├──→ output.txt
stderr ──┘
```

---

# 9. Pipe stdout + stderr Together

Normally:

```bash
command | tee output.log
```

Only stdout goes to `tee`.

To include errors:

```bash
command 2>&1 | tee output.log
```

Flow:

```text
             stdout ──┐
Command               ├──→ tee → Terminal
             stderr ──┘       ↓
                              output.log
```

This is a very useful developer pattern.

Example:

```bash
npm run build 2>&1 | tee build.log
```

Now:

- You see everything in the terminal.
    
- Everything is saved in `build.log`.
    

---

# 10. `/dev/null` — The Linux Black Hole 🕳️

`/dev/null` discards anything sent to it.

Example:

```bash
echo "Hello" > /dev/null
```

Output disappears.

Visual:

```text
Output
  ↓
/dev/null
  ↓
Gone 🕳️
```

---

## Hide Errors

```bash
find / -name "*.log" 2> /dev/null
```

This means:

```text
Normal results → Terminal
Errors         → Discard
```

Useful because searching system directories often produces many permission errors.

---

# 11. Hide Normal Output

```bash
command > /dev/null
```

Example:

```bash
npm install > /dev/null
```

Normal output disappears.

But errors still appear.

---

# 12. Hide Everything

```bash
command > /dev/null 2>&1
```

Meaning:

```text
stdout → /dev/null
stderr → stdout → /dev/null
```

Nothing appears.

---

# 13. Order Matters ⚠️🔥

Compare these:

### Version 1

```bash
command > output.txt 2>&1
```

Step-by-step:

```text
Step 1:
stdout → output.txt

Step 2:
stderr → wherever stdout goes

Result:
stdout → output.txt
stderr → output.txt
```

---

### Version 2

```bash
command 2>&1 > output.txt
```

Step-by-step:

```text
Step 1:
stderr → current stdout (Terminal)

Step 2:
stdout → output.txt

Result:

stdout → output.txt
stderr → Terminal
```

So these are **not the same**.

This is one of the most important redirection concepts.

---

# 14. `&>` Shortcut

In Bash:

```bash
command &> output.txt
```

Means:

```bash
command > output.txt 2>&1
```

Both stdout and stderr go to the same file.

Example:

```bash
npm run build &> build.log
```

---

# 15. stdin Redirection

Normally:

```text
Keyboard → stdin
```

But you can redirect input from a file.

Suppose:

```text
names.txt
```

contains:

```text
Rahul
Aman
Zaid
```

Run:

```bash
sort < names.txt
```

Now:

```text
names.txt
    ↓
stdin
    ↓
sort
    ↓
stdout
    ↓
Terminal
```

---

# 16. Pipe vs Input Redirection

These both provide input.

### Using `<`

```bash
sort < names.txt
```

Input comes from:

```text
File
```

### Using pipe

```bash
cat names.txt | sort
```

Input comes from:

```text
Another command
```

But the first is better here:

```bash
sort < names.txt
```

Or even simpler:

```bash
sort names.txt
```

Avoid unnecessary:

```bash
cat file | command
```

when the command can directly read the file.

---

# 17. Practical Developer Example 🚀

Suppose you're running your Node backend:

```bash
npm run dev
```

You want to save everything:

```bash
npm run dev > server.log 2>&1
```

But now you won't see logs in the terminal.

Better:

```bash
npm run dev 2>&1 | tee server.log
```

Result:

```text
Node Server
     │
     ├── stdout ──┐
     │            │
     └── stderr ──┘
                  ↓
                 tee
                /   \
               ↓     ↓
          Terminal  server.log
```

🔥 Very useful for debugging.

---

# 18. A Complete Example

Let's create a situation.

Run:

```bash
ls package.json nonexistent.txt > output.txt 2> errors.txt
```

You get:

### `output.txt`

```text
package.json
```

### `errors.txt`

```text
ls: cannot access 'nonexistent.txt': No such file or directory
```

Now combine both:

```bash
ls package.json nonexistent.txt > combined.txt 2>&1
```

### `combined.txt`

```text
package.json
ls: cannot access 'nonexistent.txt': No such file or directory
```

---

# Quick Cheat Sheet 🧠

```text
0 → stdin
1 → stdout
2 → stderr
```

|Command|Meaning|
|---|---|
|`command > file`|stdout → file|
|`command 1> file`|stdout → file|
|`command >> file`|append stdout|
|`command 2> file`|stderr → file|
|`command 2>> file`|append stderr|
|`command > out 2> err`|Separate output/errors|
|`command > file 2>&1`|Both → file|
|`command &> file`|Both → file (Bash)|
|`command 2>&1 \| tee log`|See + save everything|
|`command 2> /dev/null`|Hide errors|
|`command > /dev/null`|Hide output|
|`command > /dev/null 2>&1`|Hide everything|

---

# The Ultimate Mental Model 🧠

Whenever you run:

```bash
command
```

Imagine:

```text
                    ┌────────────┐
stdin (0) ─────────▶│            │──────▶ stdout (1)
                    │  COMMAND   │
                    │            │──────▶ stderr (2)
                    └────────────┘
```

Then Linux gives you the power to redirect any arrow.

```text
stdout → File
stderr → Another File
stdin  ← File
stdout → Another Command
```

That is the foundation behind:

- Pipes
    
- Redirection
    
- Shell scripting
    
- Process communication
    
- Logging
    
- Automation
    

---

## Your Linux Foundation Is Getting Strong 🚀

You've completed:

```text
Text Processing
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
└── awk

Shell Power
├── Pipes
├── Redirection
├── Command Chaining
├── xargs
├── find
├── Regex
└── stdin / stdout / stderr 🔥
```

# Next Recommended Topic: Shell Variables & Environment Variables 🌱

This is the next natural step before shell scripting.

You'll learn:

```bash
name="Rahul"
echo "$name"
```

and:

```bash
export DATABASE_URL="..."
echo "$PATH"
```

This will help you understand `.env` files, environment configuration, Node.js processes, and shell scripts much better.