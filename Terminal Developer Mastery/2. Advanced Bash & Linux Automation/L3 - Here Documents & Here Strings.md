> **This lesson teaches you how professional Bash scripts generate files, automate interactive commands, send emails, create configuration files, and handle multi-line text cleanly.**

If you've ever wondered how installation scripts create configuration files automatically or how deployment scripts generate `.env` files, this lesson is the answer.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Use Here Documents (`<<`)
- Use Here Strings (`<<<`)
- Control variable expansion
- Create configuration files
- Generate source code automatically
- Feed input into commands
- Build cleaner automation scripts

**Estimated Time:** 5–7 hours

**Difficulty:** ⭐⭐⭐☆☆

---

# What is a Here Document?

A **Here Document** (often called a _heredoc_) lets you pass multiple lines of text to a command without creating a separate file.

Basic syntax:

```bash
command <<DELIMITER
multiple
lines
of
text
DELIMITER
```

Everything between the delimiters is treated as the command's input.

---

# Your First Here Document

```bash
cat <<EOF
Hello Rahul
Welcome to Bash
EOF
```

Output:

```
Hello Rahul
Welcome to Bash
```

Think of `EOF` as a marker. It can be almost any word, as long as the opening and closing markers match exactly.

Examples:

```bash
<<EOF
<<END
<<CONFIG
<<SQL
<<JSON
```

---

# Creating Files

One of the most common uses.

```bash
cat > hello.txt <<EOF
Hello World
This is Bash.
EOF
```

Now:

```bash
cat hello.txt
```

Output:

```
Hello World
This is Bash.
```

---

# Backend Example — Generate `.env`

```bash
cat > .env <<EOF
PORT=3000
NODE_ENV=development
DATABASE_URL=mongodb://localhost:27017/blog
JWT_SECRET=change-me
EOF
```

No text editor required.

---

# Variable Expansion

Variables expand automatically.

```bash
name="Rahul"

cat <<EOF
Hello $name
Today is $(date)
EOF
```

Output:

```
Hello Rahul
Today is Fri Jul 25 ...
```

Both variables and command substitutions are evaluated.

---

# Prevent Variable Expansion

Sometimes you want the text literally.

Use **quoted delimiters**.

```bash
cat <<'EOF'
Hello $USER
Today is $(date)
EOF
```

Output:

```
Hello $USER
Today is $(date)
```

Nothing is expanded.

This is extremely useful when generating scripts or templates.

---

# Indenting Heredocs

Use `<<-` (notice the hyphen).

```bash
cat <<-EOF
	This line starts with a tab.
	This one too.
EOF
```

Leading **tabs** (not spaces) are stripped from the output.

This keeps your Bash code neatly indented.

---

# Appending to Files

Overwrite:

```bash
cat > notes.txt <<EOF
First line
EOF
```

Append:

```bash
cat >> notes.txt <<EOF
Second line
EOF
```

Result:

```
First line
Second line
```

---

# Generate JSON

Backend example:

```bash
cat > config.json <<EOF
{
  "name": "blog-api",
  "port": 3000,
  "debug": true
}
EOF
```

Useful when scaffolding projects.

---

# Generate YAML

```bash
cat > docker-compose.yml <<EOF
services:
  app:
    image: node:20
    ports:
      - "3000:3000"
EOF
```

Common in Docker automation.

---

# Generate SQL

```bash
cat <<SQL
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);
SQL
```

Great for generating migration scripts.

---

# Generate Shell Scripts

```bash
cat > start.sh <<'EOF'
#!/usr/bin/env bash

echo "Application Started"
EOF

chmod +x start.sh
```

Notice the quoted `EOF` so `$` characters inside remain untouched.

---

# Real Backend Example — README Generator

```bash
project="Blog API"

cat > README.md <<EOF
# $project

## Installation

npm install

## Run

npm start
EOF
```

Instant documentation.

---

# What is a Here String?

A **Here String** sends **one string** as input to a command.

Syntax:

```bash
command <<< "text"
```

---

# Example

```bash
wc -w <<< "Hello Linux World"
```

Output:

```
3
```

Without creating a temporary file.

---

# Example — Search Text

```bash
grep "Linux" <<< "Hello Linux World"
```

Output:

```
Hello Linux World
```

---

# Example — Read Into Variables

```bash
read name <<< "Rahul"

echo "$name"
```

Output:

```
Rahul
```

---

# Split Multiple Values

```bash
read first last <<< "Rahul Kumar"

echo "$first"
echo "$last"
```

Output:

```
Rahul
Kumar
```

Very handy when parsing simple structured data.

---

# Backend Example — Parse Version

```bash
version="v22.10.0"

read major minor patch <<< "${version//./ }"

echo "$major"
```

You'll refine parsing techniques further in Lesson 4.

---

# Combining Heredoc and Command Substitution

```bash
today=$(date +%F)

cat <<EOF
Backup Report

Date: $today
User: $(whoami)
EOF
```

Output is generated dynamically.

---

# Real Project Example — Nginx Config Generator

```bash
domain="example.com"

cat > nginx.conf <<EOF
server {
    listen 80;

    server_name $domain;

    location / {
        proxy_pass <http://localhost:3000>;
    }
}
EOF
```

This is a common pattern in deployment automation.

---

# Hands-on Lab

Create:

```
generate-env.sh
```

Requirements:

Ask the user for:

- Project name
- Port
- Database URL
- JWT Secret

Generate:

```
.env
```

using a Here Document.

---

# Mini Project

Create:

```
project-scaffold.sh
```

It should create:

```
README.md
package.json
.env.example
docker-compose.yml
.gitignore
```

Generate all file contents using Here Documents.

No manual editing.

---

# Common Mistakes

## Delimiter Doesn't Match

Wrong:

```bash
cat <<EOF
Hello
END
```

The opening and closing delimiters **must** match.

---

## Extra Spaces

Wrong:

```bash
cat <<EOF
Hello
 EOF
```

The closing delimiter must start at the beginning of the line (unless you're intentionally using `<<-` with tabs).

---

## Forgetting Quotes

Wrong if you want literal text:

```bash
cat <<EOF
$HOME
EOF
```

Correct:

```bash
cat <<'EOF'
$HOME
EOF
```

---

## Using Here Documents for Small Strings

Instead of:

```bash
grep "hello" <<EOF
hello world
EOF
```

Use:

```bash
grep "hello" <<< "hello world"
```

Here Strings are cleaner for single-line input.

---

# Interview Questions

1. What is a Here Document?
2. What is a Here String?
3. What's the difference between `<<` and `<<<`?
4. How do you prevent variable expansion in a heredoc?
5. When would you use `<<-`?
6. How are heredocs used in deployment scripts?

---

# Cheat Sheet

```bash
# Here Document
cat <<EOF
Hello
EOF

# Create file
cat > file.txt <<EOF
Hello
EOF

# Append
cat >> file.txt <<EOF
More
EOF

# No expansion
cat <<'EOF'
$HOME
EOF

# Here String
grep hello <<< "hello world"

# Read variable
read name <<< "Rahul"

# Read two variables
read first last <<< "Rahul Kumar"
```

---

# Weekly Challenge 🚀

Build a tool named:

```
mern-init.sh
```

Run:

```bash
./mern-init.sh blog-api
```

It should:

1. Create the project folder.
2. Generate:

```
README.md
.env
.gitignore
docker-compose.yml
package.json
```

1. Every file must be created using **Here Documents**.
2. Ask the user for:

- Project description
- Port
- MongoDB URL

1. Fill those values into the generated files.

---

# ⭐ Pro Challenge (Backend Engineer)

Create a tool called:

```
express-generator-lite.sh
```

Example:

```bash
./express-generator-lite.sh my-api
```

Automatically create:

```
my-api/
├── src/
│   ├── controllers/
│   ├── routes/
│   ├── middleware/
│   ├── models/
│   ├── services/
│   ├── config/
│   └── app.js
├── package.json
├── .env
├── README.md
└── docker-compose.yml
```

Use:

- Here Documents
- Command Substitution
- Parameter Expansion
- Functions
- Error Handling

This is very close to how real project generators (like `create-react-app` or `npm init`) work.

---

# ⭐ Module 2 Progress

```
✅ Lesson 1 — Advanced Parameter Expansion
✅ Lesson 2 — Command Substitution & Process Substitution
✅ Lesson 3 — Here Documents & Here Strings

⬜ Lesson 4 — Advanced Text Processing (grep, sed, awk, cut, sort, uniq, tr, xargs)
⬜ Lesson 5 — Regular Expressions
⬜ Lesson 6 — Signals, Traps & Process Control
⬜ Lesson 7 — Background Jobs & Parallel Processing
⬜ Lesson 8 — Scheduling (cron, at, systemd timers)
⬜ Lesson 9 — Writing Reusable Bash Libraries
⬜ Lesson 10 — API Automation with curl & JSON
⬜ Lesson 11 — Production Automation Projects
⬜ Lesson 12 — Final DevOps Toolkit Capstone
```

---

# 💡 Backend Engineer Insight

If you've ever used tools like:

- `npm init`
- `create-vite`
- `create-next-app`
- `docker init`
- `npx express-generator`

they're all generating files from templates. While many are written in JavaScript or Go, the same concept is easy to implement in Bash using **Here Documents**.

Mastering heredocs is the foundation for automating project scaffolding, deployment configuration, Docker Compose generation, Nginx configuration, CI/CD files, and many other backend workflows.

In **Lesson 4**, we'll cover one of the most valuable skill sets for Linux engineers: **advanced text processing** with `grep`, `sed`, `awk`, `cut`, `sort`, `uniq`, `tr`, and `xargs`. These tools are indispensable for parsing logs, transforming data, and building powerful command-line pipelines.