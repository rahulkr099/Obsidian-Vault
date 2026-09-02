# Shell Variables & Environment Variables in Linux 🌱

Now we're entering an important area: **how the shell stores and passes data**.

This is especially useful for you as a MERN developer because environment variables are everywhere:

- `PATH`
    
- `HOME`
    
- `NODE_ENV`
    
- `PORT`
    
- `DATABASE_URL`
    
- API keys
    
- `.env` files
    

Let's build the concept from the basics.

---

# 1. What is a Shell Variable?

A variable stores a value.

```bash
name="Rahul"
```

Access it using `$`:

```bash
echo "$name"
```

Output:

```text
Rahul
```

Think:

```text
Variable
   │
   ▼
name ──────→ Rahul
```

---

# 2. Important Rule: No Spaces Around `=`

Correct:

```bash
name="Rahul"
```

Wrong:

```bash
name = "Rahul"
```

Why?

The shell interprets spaces as separators between commands and arguments.

So always:

```bash
VARIABLE=value
```

---

# 3. Accessing Variables

Use `$`.

```bash
name="Rahul"

echo $name
```

Better:

```bash
echo "$name"
```

I recommend getting into the habit of quoting variables.

Why? Suppose:

```bash
name="Rahul Kumar"
```

Then:

```bash
echo "$name"
```

Preserves the value safely.

---

# 4. Different Types of Values

## String

```bash
language="JavaScript"
```

## Number

```bash
age=22
```

## Path

```bash
project="$HOME/projects/my-app"
```

Use:

```bash
echo "$project"
```

---

# 5. Variable Naming Rules

Valid:

```bash
name="Rahul"
user_name="Rahul"
USER_NAME="Rahul"
port123=3000
```

Invalid:

```bash
user-name="Rahul"
123name="Rahul"
user name="Rahul"
```

Good convention:

```bash
lowercase → shell variables
UPPERCASE → environment variables/constants
```

Example:

```bash
project_name="my-api"

PORT=5000
NODE_ENV=development
```

---

# 6. Command Substitution 🔥

You can store command output inside a variable.

Modern syntax:

```bash
current_date=$(date)
```

Then:

```bash
echo "$current_date"
```

Example:

```bash
files=$(ls)
```

Now:

```bash
echo "$files"
```

But for filenames, storing `ls` output in a variable is generally not a robust pattern. We'll discuss safer approaches later.

---

## Useful Example

```bash
current_dir=$(pwd)

echo "You are currently in: $current_dir"
```

Output:

```text
You are currently in: /home/rahul/projects
```

---

# 7. Arithmetic with Variables

Bash supports arithmetic expansion.

```bash
a=10
b=20

result=$((a + b))

echo "$result"
```

Output:

```text
30
```

Other operations:

```bash
$((a + b))
$((a - b))
$((a * b))
$((a / b))
$((a % b))
```

Example:

```bash
port=$((3000 + 1))

echo "$port"
```

Output:

```text
3001
```

---

# 8. Shell Variable Scope 🧠

Create a variable:

```bash
name="Rahul"
```

Check it:

```bash
echo "$name"
```

Works.

But now start a new shell:

```bash
bash
```

Then:

```bash
echo "$name"
```

You may get nothing.

Why?

Because normal shell variables belong only to the **current shell**.

Visual:

```text
Current Shell
│
├── name="Rahul"
│
└── Child Shell
      │
      └── Cannot automatically see normal shell variable
```

This leads us to environment variables.

---

# 9. What is an Environment Variable? 🌍

An environment variable is a variable that is **exported to child processes**.

Example:

```bash
export NAME="Rahul"
```

Now:

```bash
bash
```

Inside the child shell:

```bash
echo "$NAME"
```

Output:

```text
Rahul
```

Visual:

```text
Parent Shell
│
├── export NAME="Rahul"
│
└── Child Process
      │
      └── NAME is available ✅
```

---

# 10. `export`

You can do:

```bash
NAME="Rahul"
export NAME
```

Or shorter:

```bash
export NAME="Rahul"
```

Both work.

---

# 11. Shell Variable vs Environment Variable 🔥

|Feature|Shell Variable|Environment Variable|
|---|---|---|
|Current shell|✅|✅|
|Child processes|❌|✅|
|Uses `export`|❌|✅|
|Example|`name="Rahul"`|`export PORT=3000`|

---

# 12. View Environment Variables

Use:

```bash
printenv
```

or:

```bash
env
```

Example:

```bash
printenv HOME
```

You might see:

```text
/home/rahul
```

Check:

```bash
echo "$HOME"
```

---

# 13. Important Environment Variables 🔥

## `$HOME`

Your home directory:

```bash
echo "$HOME"
```

Example:

```text
/home/rahul
```

Go home:

```bash
cd "$HOME"
```

---

## `$USER`

Current username:

```bash
echo "$USER"
```

---

## `$SHELL`

Your current login shell:

```bash
echo "$SHELL"
```

Example:

```text
/bin/bash
```

---

## `$PWD`

Current directory:

```bash
echo "$PWD"
```

Equivalent conceptually to:

```bash
pwd
```

---

## `$PATH` 🔥🔥

One of the most important.

```bash
echo "$PATH"
```

You may see:

```text
/usr/local/bin:/usr/bin:/bin:/home/rahul/.local/bin
```

When you run:

```bash
node
```

Linux searches directories listed in `$PATH`.

Conceptually:

```text
node
 │
 ▼
Search PATH directories
 │
 ├── /usr/local/bin
 ├── /usr/bin
 ├── /bin
 └── ~/.local/bin
```

When it finds the executable:

```text
/usr/bin/node
```

it runs it.

You can verify:

```bash
which node
```

or better:

```bash
command -v node
```

---

# 14. Temporarily Modify PATH

Suppose you have scripts here:

```text
~/my-scripts
```

You can add it:

```bash
export PATH="$PATH:$HOME/my-scripts"
```

Now commands inside that directory can potentially be run directly by name.

Check:

```bash
echo "$PATH"
```

---

## Prepend vs Append

### Append

```bash
export PATH="$PATH:$HOME/my-scripts"
```

Your directory is searched later.

### Prepend

```bash
export PATH="$HOME/my-scripts:$PATH"
```

Your directory is searched first.

Be careful with prepending because you can accidentally override system commands.

---

# 15. Temporary Environment Variables

You can set a variable for just one command:

```bash
PORT=5000 node server.js
```

Meaning:

```text
PORT=5000
   │
   └── Available only to node server.js
```

After the command:

```bash
echo "$PORT"
```

It won't necessarily exist in your current shell.

This pattern is extremely useful.

---

# 16. Node.js Example 🚀

Run:

```bash
PORT=5000 NODE_ENV=development node server.js
```

Inside Node.js:

```javascript
console.log(process.env.PORT);
console.log(process.env.NODE_ENV);
```

Output:

```text
5000
development
```

This is how environment variables get passed from Linux → Node.js.

---

# 17. Permanent Environment Variables

Suppose you always want:

```bash
export EDITOR=nvim
```

You can put it in your shell configuration.

For Bash:

```text
~/.bashrc
```

For Zsh:

```text
~/.zshrc
```

For Fish:

```text
~/.config/fish/config.fish
```

Since you're using Linux Mint, first check your active shell:

```bash
echo "$SHELL"
```

If it says:

```text
/bin/bash
```

then your interactive Bash configuration is usually:

```bash
~/.bashrc
```

---

## Example

Open:

```bash
nvim ~/.bashrc
```

Add:

```bash
export EDITOR=nvim
export NODE_ENV=development
```

Reload:

```bash
source ~/.bashrc
```

Now:

```bash
echo "$EDITOR"
```

Output:

```text
nvim
```

---

# 18. `source` Command

Normally, a script runs in a separate shell process.

Example:

```bash
./script.sh
```

But:

```bash
source script.sh
```

runs commands in the **current shell**.

Example `variables.sh`:

```bash
PROJECT="MERN"
export PORT=5000
```

Run:

```bash
source variables.sh
```

Now:

```bash
echo "$PROJECT"
echo "$PORT"
```

Both are available in your current shell.

Shortcut:

```bash
. variables.sh
```

The dot `.` means the same as `source`.

---

# 19. `.env` Files vs Shell Environment Variables 🔥

As a MERN developer, this distinction is important.

A `.env` file might contain:

```env
PORT=5000
DATABASE_URL=mongodb://localhost:27017/mydb
JWT_SECRET=my-secret
```

But Linux does **not automatically load `.env` files**.

You need something to load them.

For Node.js, you may use a library such as `dotenv`, or Node's built-in environment-file support in modern Node versions.

Example conceptually:

```text
.env file
   ↓
Environment loader
   ↓
process.env
   ↓
Node.js application
```

So:

```text
.env ≠ automatically exported Linux environment
```

This is an important distinction.

---

# 20. Default Values with `${VAR:-default}` 🔥

Very useful in scripts.

```bash
echo "${PORT:-3000}"
```

Meaning:

> Use `$PORT`; if it's unset or empty, use `3000`.

Example:

```bash
PORT=5000

echo "${PORT:-3000}"
```

Output:

```text
5000
```

Without `PORT`:

```text
3000
```

---

# 21. Require a Variable

You can enforce that a variable exists:

```bash
echo "${DATABASE_URL:?DATABASE_URL is required}"
```

If the variable isn't set, Bash shows an error.

Very useful in deployment scripts.

Example:

```bash
: "${DATABASE_URL:?DATABASE_URL must be set}"
```

The `:` is a shell builtin that does nothing, but variable expansion still happens.

This is common in production scripts.

---

# 22. Useful Variable Expansion 🔥

Suppose:

```bash
file="server.js"
```

### Remove `.js`

```bash
echo "${file%.js}"
```

Output:

```text
server
```

---

Suppose:

```bash
file="src/server.js"
```

Get filename:

```bash
echo "${file##*/}"
```

Output:

```text
server.js
```

Get directory:

```bash
echo "${file%/*}"
```

Output:

```text
src
```

These are powerful Bash features and often faster than spawning external commands.

---

# 23. Quoting Variables ⚠️

Suppose:

```bash
folder="My Project"
```

This is dangerous:

```bash
cd $folder
```

The shell may interpret it as two arguments:

```text
My
Project
```

Better:

```bash
cd "$folder"
```

Rule of thumb:

> **Almost always quote variable expansions.**

```bash
"$variable"
"${variable}"
```

---

# 24. Curly Braces `${}`

Compare:

```bash
name="Rahul"

echo "$nameDeveloper"
```

Bash looks for a variable called:

```text
nameDeveloper
```

Instead:

```bash
echo "${name}Developer"
```

Output:

```text
RahulDeveloper
```

Curly braces clearly define the variable boundary.

---

# Practical Developer Examples 🚀

## Start Express server

```bash
PORT=5000 NODE_ENV=development npm run dev
```

---

## Use default port

```bash
PORT="${PORT:-5000}"

echo "Server running on port $PORT"
```

---

## Check required secrets

```bash
: "${DATABASE_URL:?DATABASE_URL is required}"
: "${JWT_SECRET:?JWT_SECRET is required}"
```

---

## Add custom scripts to PATH

```bash
export PATH="$HOME/scripts:$PATH"
```

---

# Cheat Sheet 🧠

```bash
# Create variable
name="Rahul"

# Read variable
echo "$name"

# Environment variable
export PORT=5000

# View environment
printenv

# Command substitution
date=$(date)

# Arithmetic
result=$((10 + 20))

# Temporary variable for one command
PORT=5000 node server.js

# Default value
echo "${PORT:-3000}"

# Required variable
: "${DATABASE_URL:?Required}"

# Reload shell config
source ~/.bashrc

# Add directory to PATH
export PATH="$HOME/bin:$PATH"
```

---

# The Big Picture 🧠

```text
Shell Variable
     │
     │ Current shell only
     ▼
name="Rahul"


Environment Variable
     │
     │ Exported to child processes
     ▼
export PORT=5000


Node.js
     │
     ▼
process.env.PORT
```

This connection is important:

```text
Linux Shell
    ↓
Environment Variables
    ↓
Node.js Process
    ↓
process.env
    ↓
Express Application
```

Understanding this will help you a lot later with Docker, CI/CD, deployment, and production configuration.

---

# Your Linux Roadmap So Far 🚀

```text
Linux CLI Foundation
│
├── Text Processing
│   ├── grep
│   ├── sed
│   ├── awk
│   └── regex
│
├── Shell Operations
│   ├── pipes
│   ├── redirection
│   ├── chaining
│   ├── xargs
│   └── find
│
├── Process Streams
│   ├── stdin
│   ├── stdout
│   └── stderr
│
└── Shell Environment
    ├── Variables
    ├── Environment variables
    ├── PATH
    ├── export
    └── source
```

## Next Topic: Shell Expansion 🔥

This is a very powerful Linux topic and explains things like:

```bash
echo *.js
```

```bash
mkdir project-{frontend,backend,database}
```

```bash
echo {1..10}
```

```bash
echo ~
```

You'll learn **how Bash transforms your command before executing it**—including brace expansion, globbing, tilde expansion, command substitution, and more. This is a major step toward becoming a terminal-first developer.