# Linux Command Chaining (`&&`, `||`, `;`) ⛓️

Command chaining means running **multiple commands in one line** and controlling **when the next command runs**.

The three main operators are:

```bash
&&
||
;
```

They look similar, but their behavior is very different.

---

# First: Understand Exit Status 🧠

Every Linux command returns an **exit status**.

```text
0       → Success ✅
non-zero → Failure ❌
```

You can check the previous command's exit status with:

```bash
echo $?
```

Example:

```bash
mkdir test
echo $?
```

If successful:

```text
0
```

If something fails:

```text
non-zero value
```

This is the foundation of `&&` and `||`.

---

# 1. `&&` — Run Next Command Only If Previous Succeeds ✅

Syntax:

```bash
command1 && command2
```

Meaning:

> Run `command2` only if `command1` succeeds.

---

## Example

```bash
mkdir myproject && cd myproject
```

Flow:

```text
mkdir myproject
       │
       ├── Success → cd myproject
       │
       └── Failure → Stop
```

This is safer than:

```bash
mkdir myproject ; cd myproject
```

because if `mkdir` fails, `cd` could still run.

---

## Developer Example

```bash
npm install && npm run dev
```

Meaning:

```text
npm install
     │
     ├── Success → npm run dev
     │
     └── Failure → Don't start server
```

---

## Multiple Commands

```bash
command1 && command2 && command3
```

Example:

```bash
mkdir project && cd project && npm init -y
```

Flow:

```text
mkdir
  ↓ success
cd
  ↓ success
npm init
```

If any command fails, the chain stops.

---

# 2. `||` — Run Next Command Only If Previous Fails ❌

Syntax:

```bash
command1 || command2
```

Meaning:

> If `command1` fails, run `command2`.

---

## Example

```bash
mkdir project || echo "Project already exists"
```

If `mkdir project` succeeds:

```text
(no echo)
```

If it fails:

```text
Project already exists
```

---

## Developer Example

```bash
npm run build || echo "Build failed!"
```

If build succeeds:

```text
Build completes normally
```

If build fails:

```text
Build failed!
```

---

# 3. `;` — Run Commands Regardless of Success or Failure

Syntax:

```bash
command1 ; command2
```

Meaning:

> Run both commands no matter what happens.

Example:

```bash
mkdir project ; cd project
```

Flow:

```text
mkdir project
     │
     ├── Success ──┐
     │             ▼
     └── Failure → cd project
```

The second command always runs.

---

## Example

```bash
echo "Starting"; npm run build; echo "Finished"
```

Even if `npm run build` fails:

```text
Starting
Finished
```

will still execute.

---

# Comparison Table 🔥

|Operator|Meaning|
|---|---|
|`&&`|Run next only if previous succeeds|
|`||
|`;`|Always run next|

---

# Visual Mental Model 🧠

```text
command1 && command2

Success? ──YES──→ command2
    │
    NO
    ↓
   STOP
```

```text
command1 || command2

Success? ──YES──→ STOP
    │
    NO
    ↓
command2
```

```text
command1 ; command2

command1
    ↓
Always
    ↓
command2
```

---

# 4. Combining `&&` and `||` 🔥

This is a very common pattern:

```bash
command && echo "Success" || echo "Failed"
```

Example:

```bash
npm run build && echo "Build successful!" || echo "Build failed!"
```

Looks like an `if-else`:

```text
npm run build

Success → Build successful!
Failure → Build failed!
```

---

## ⚠️ Important Caveat

Be careful with long chains like:

```bash
command1 && command2 || command3
```

This does **not always behave like a traditional `if/else`**.

It behaves approximately as:

```text
(command1 && command2) || command3
```

Example:

```bash
true && false || echo "Failed"
```

Output:

```text
Failed
```

Because `command2` failed.

For complex logic, shell `if` statements are clearer.

---

# 5. Practical Project Setup Example 🚀

Suppose you want to create a Node project:

```bash
mkdir my-api && \
cd my-api && \
npm init -y && \
npm install express
```

The `\` is just a line continuation, making it readable.

Flow:

```text
Create folder
      ↓
Enter folder
      ↓
Initialize npm
      ↓
Install Express
```

Each step runs only if the previous one succeeds.

---

# 6. Real MERN Developer Examples 🔥

### Install dependencies then start server

```bash
npm install && npm run dev
```

---

### Build frontend and deploy

```bash
npm run build && npm run deploy
```

Deployment won't happen if the build fails.

This is exactly the kind of logic you want.

---

### Run tests before pushing

```bash
npm test && git add . && git commit -m "Update" && git push
```

Flow:

```text
Tests
  ↓
Pass?
  ↓ YES
git add
  ↓
commit
  ↓
push
```

If tests fail, nothing gets pushed.

---

# 7. `||` for Fallback Commands

Suppose a directory might already exist:

```bash
mkdir logs || true
```

This tells the shell:

> Try to create `logs`. If it fails, consider it okay.

But a clearer modern alternative is often:

```bash
mkdir -p logs
```

`mkdir -p` is usually better when you intentionally want the directory to exist.

---

# 8. Useful Pattern: Try Something, Otherwise Fallback

```bash
command1 || command2
```

Example:

```bash
grep "ERROR" server.log || echo "No errors found"
```

⚠️ Small caveat: `grep` returns failure status when no match is found, so this pattern works nicely for simple checks.

---

# 9. Background Commands with `&`

Don't confuse `&&` with `&`.

### `&&`

```bash
command1 && command2
```

Conditional chaining.

### `&`

```bash
command &
```

Run command in the background.

Example:

```bash
npm run dev &
```

The shell immediately gives control back.

We'll cover background jobs separately.

---

# 10. Parentheses and Grouping

You can group commands:

```bash
(command1 && command2) || command3
```

Example:

```bash
(npm test && npm run build) || echo "Pipeline failed"
```

Meaning:

```text
Run tests
   ↓
If successful → Build
   ↓
If anything fails
   ↓
Pipeline failed
```

This is cleaner for automation.

---

# 11. A Realistic Backend Workflow

Imagine you're working on your MERN backend:

```bash
npm test && npm run lint && npm run build && npm start
```

Meaning:

```text
Tests
  ↓
Lint
  ↓
Build
  ↓
Start Server
```

Each stage acts as a safety checkpoint.

---

# Quick Cheat Sheet 📌

```bash
# Run next only on success
command1 && command2

# Run next only on failure
command1 || command2

# Always run next
command1 ; command2

# Success/failure message
command && echo "Success" || echo "Failed"

# Safe project workflow
npm test && npm run build && npm start
```

---

# Practice Challenge 💪

Try understanding these before running them:

### Challenge 1

```bash
true && echo "Hello"
```

Output?

```text
Hello
```

---

### Challenge 2

```bash
false && echo "Hello"
```

Output?

```text
Nothing
```

---

### Challenge 3

```bash
false || echo "Fallback"
```

Output:

```text
Fallback
```

---

### Challenge 4

```bash
false ; echo "Always runs"
```

Output:

```text
Always runs
```

---

# Mental Model to Remember 🧠

```text
&& → Success → Continue

|| → Failure → Fallback

;  → Don't care → Continue
```

---

## Your Linux Command-Line Foundation So Far 🚀

```text
Text Processing
├── cat
├── less
├── head / tail
├── grep
├── sort / uniq
├── wc
├── cut / tr
├── tee / paste
├── sed
└── awk

Shell Control
├── Pipes |
├── Redirection > >> <
└── Command Chaining && || ;
```

## Next Topic: `xargs` 🔥

This is the perfect next command because `xargs` lets you take output from one command and turn it into **arguments for another command**.

Example:

```bash
find . -name "*.log" | xargs rm
```

Understanding `xargs` will unlock much more powerful Linux automation and command pipelines.