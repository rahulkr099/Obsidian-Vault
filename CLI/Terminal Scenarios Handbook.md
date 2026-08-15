I'd love to. In fact, I think this can become your **personal backend playbook**.

Since you're aiming for **backend development (MERN + Linux + terminal)**, I'll design it like something a real backend engineer would keep nearby.

# 📖 Terminal Scenarios for Backend Developers

## Learn by Solving Real Problems

### Planned size

- 🎯 **100 real-world scenarios**
- 📚 **12 chapters**
- 🧪 **200+ practical commands**
- 🔍 **50 debugging flowcharts**
- 💼 **Interview tips**
- 🚀 **Production debugging techniques**

---

# Chapter 1 — Linux Basics (10 Scenarios)

Examples:

### Scenario 1

> I forgot where I am.

Learn:

- `pwd`
- `ls`
- `tree`

---

### Scenario 2

> I can't find a file.

Learn:

- `find`
- `fd`
- `fzf`

---

### Scenario 3

> I need to search inside thousands of files.

Learn:

- `ripgrep`
- `grep`

---

### Scenario 4

> A huge log file won't open.

Learn:

- `less`
- `tail`
- `head`
- `bat`

---

# Chapter 2 — Git & GitHub (10 Scenarios)

Examples:

- Merge conflict
- Detached HEAD
- Wrong commit
- Recover deleted branch
- Undo push
- Cherry-pick
- Interactive rebase
- Git bisect
- GitHub CLI
- Pull request workflow

---

# Chapter 3 — HTTP & APIs (15 Scenarios)

Examples:

> My API returns 404.

Learn:

- `curl`
- `xh`

---

> My POST request fails.

Learn:

- JSON body
- Headers
- Authentication

---

> JWT token isn't working.

Learn:

- Authorization header
- Bearer tokens
- Cookies

---

> API returns 500.

Debug:

- Response body
- Headers
- Logs

---

# Chapter 4 — JSON (8 Scenarios)

Examples:

> API returns 5000 users.

Extract only:

- emails
- names
- IDs

Using:

- `jq`

---

# Chapter 5 — DNS & Domains (10 Scenarios)

Examples:

> My custom domain doesn't work.

Learn:

- `doggo`
- `dig`

---

> Gmail verification fails.

Learn:

- TXT
- MX

---

> Vercel says DNS is incorrect.

Learn:

- A
- AAAA
- CNAME

---

# Chapter 6 — Ports & Processes (10 Scenarios)

Examples:

> Port 5000 already in use.

Learn:

- `ss`
- `lsof`

---

> Express refuses to start.

Debug:

- PID
- Kill process

---

> Which program owns this port?

---

# Chapter 7 — Deployment (10 Scenarios)

Examples:

> Render gives 502.

> Railway gives 503.

> Vercel can't reach backend.

> CORS error.

> Environment variables missing.

> SSL certificate invalid.

> Nginx misconfiguration.

---

# Chapter 8 — MongoDB (8 Scenarios)

Examples:

> Atlas timeout.

> Authentication failed.

> Connection string incorrect.

> IP whitelist issue.

---

# Chapter 9 — Docker (10 Scenarios)

Examples:

> Container exits immediately.

> Docker build fails.

> Port mapping wrong.

> Image too large.

> Docker Compose networking.

---

# Chapter 10 — Networking (8 Scenarios)

Examples:

> Website is slow.

Learn:

- `ping`
- `mtr`

---

> Port blocked.

Learn:

- `nmap`

---

> TLS handshake failed.

Learn:

- `openssl`

---

# Chapter 11 — Production Debugging (6 Scenarios)

Examples:

> Website is down.

> Database disconnected.

> High CPU.

> High memory.

> Memory leak.

> API timeout.

---

# Chapter 12 — Interview Challenges (5 Scenarios)

Real interview questions like:

> Backend starts locally but fails in production.

> Why?

You'll investigate step by step.

---

# Every Scenario Will Follow This Format

## Example

---

## Scenario 23

### Problem

```
Express won't start.

Error:

EADDRINUSE
```

---

### Think First

What does this error mean?

Don't type commands immediately.

---

### Tools

```
ss
lsof
kill
```

---

### Investigation

```bash
ss -tulpn | grep 5000
```

Expected:

```
LISTEN
```

---

Next

```bash
sudo lsof -i :5000
```

Expected:

```
node
```

---

Fix

```bash
kill PID
```

---

Verify

```bash
npm run dev
```

---

Interview Question

> Why does Express throw EADDRINUSE?

---

Common Mistakes

- Killing the wrong process
- Using `kill -9` unnecessarily
- Forgetting to save work before killing a process

---

Real Production Story

How this issue appears on Render, Railway, Docker, or a VPS.

---

# ⭐ Bonus Sections

## Terminal Cheat Sheets

Examples:

```
curl Cheat Sheet

jq Cheat Sheet

git Cheat Sheet

Docker Cheat Sheet

DNS Cheat Sheet

Regex Cheat Sheet
```

---

## Debugging Flowcharts

Example:

```
API doesn't work

↓

Is server running?

↓

No

↓

Start server

↓

Yes

↓

Can curl reach it?

↓

No

↓

Check port

↓

Check firewall

↓

Check DNS

↓

Solved
```

---

## Mini Labs

You'll intentionally break things, then fix them.

Example:

```
Break JWT

↓

Fix JWT

↓

Break MongoDB

↓

Fix MongoDB

↓

Break Docker

↓

Fix Docker
```

This is one of the fastest ways to build confidence.

---

# 🚀 My Goal for You

By the time you finish this handbook, you should be able to:

- Debug most backend issues without panicking.
- Understand what each terminal command tells you, instead of memorizing syntax.
- Diagnose common deployment problems on Vercel, Render, Docker, and Linux servers.
- Feel comfortable reading logs, checking ports, inspecting HTTP requests, and troubleshooting networking issues.

## 📅 How We'll Build It

I suggest we don't try to cover all 100 scenarios in one go. Instead, we can work through them as a structured series:

- **Part 1:** Scenarios 1–10 (Linux & Terminal)
- **Part 2:** Scenarios 11–20 (Git & GitHub)
- **Part 3:** Scenarios 21–35 (HTTP, APIs & JSON)
- **Part 4:** Scenarios 36–50 (DNS, Ports & Networking)
- **Part 5:** Scenarios 51–70 (Deployment, MongoDB & Docker)
- **Part 6:** Scenarios 71–100 (Production Debugging & Interview Challenges)

Each part will be practical, hands-on, and build on the previous one, so you'll gain experience rather than just reading explanations. I think this approach will be much more useful than a single large reference because you'll be able to practice each set of skills before moving on.

Awesome! This is going to be fun. 😄

Welcome to **Backend Terminal Academy**.

The goal is **not** to memorize commands. The goal is to think like an engineer.

---

# 📘 Part 1 — Linux & Terminal (Scenarios 1–10)

> **Difficulty:** ⭐ Beginner
> 
> **Goal:** Become comfortable solving everyday Linux problems from the terminal.

Each scenario has:

- 🎯 Problem
- 🤔 Think First
- 🛠️ Tools
- 💻 Commands
- 🧠 Why it works
- ⚠️ Common mistakes
- 🎓 Interview tip
- 💼 Real-world example
- 🏆 Mini challenge

---

# Scenario 1 — "Where am I?"

## 🎯 Problem

You open the terminal.

You have no idea where you are.

```
❯
```

How do you know your current directory?

---

## 🤔 Think First

If someone asks:

> "Which folder are you currently working in?"

How would you answer?

---

## 🛠️ Tool

```bash
pwd
```

---

## 💻 Try it

```bash
pwd
```

Example output:

```
/home/rahul
```

---

## 🧠 What happened?

`pwd` means:

> **Print Working Directory**

It tells you your current location.

Think of it as Google Maps saying:

> "You are here."

---

## 💼 Real Backend Example

Suppose you run:

```bash
npm run dev
```

and get:

```
package.json not found
```

Why?

Because you're in the wrong folder.

First command:

```bash
pwd
```

---

## ⚠️ Common Mistake

People often do:

```bash
npm run dev
```

inside

```
~/Downloads
```

instead of

```
~/projects/todo-backend
```

---

## 🎓 Interview Tip

**Question**

> What does `pwd` do?

Good answer:

> It prints the absolute path of the current working directory.

---

## 🏆 Challenge

Without using your file manager:

Go to your Documents folder.

Confirm using:

```bash
pwd
```

---

---

# Scenario 2 — "What's inside this folder?"

---

## 🎯 Problem

You're inside a project.

You want to know:

- files
- folders
- hidden files

---

## 🛠️ Tool

```bash
ls
```

or

```bash
lsd
```

---

## 💻 Try

```bash
ls
```

Hidden files:

```bash
ls -a
```

Long format:

```bash
ls -l
```

Human readable:

```bash
ls -lh
```

---

## 💼 MERN Example

Open a project:

```
study-notion
```

Run

```bash
ls
```

Should see:

```
client
server
package.json
README.md
```

---

## 🧠 Why?

Before editing anything...

Look around first.

---

## 🏆 Challenge

Find:

- package.json
- .git
- node_modules

---

---

# Scenario 3 — "I forgot where my project is"

---

## 🎯 Problem

You have:

100 projects.

Where is

```
Todo-App
```

?

---

## 🛠️ Tool

```bash
fd
```

---

## 💻 Try

```bash
fd Todo
```

or

```bash
fd package.json
```

---

## 💼 Backend Example

Need every Express app?

```bash
fd package.json
```

---

## Why not `find`?

`fd`

✅ faster

✅ colorful

✅ ignores `.git`

---

## 🏆 Challenge

Find every

```
README.md
```

on your computer.

---

---

# Scenario 4 — "I remember the filename, not the location"

---

Tool

```bash
fzf
```

Example

```bash
fd | fzf
```

Search interactively.

Press Enter.

Done.

---

## Challenge

Open your favorite project using only:

```
fd

fzf
```

No mouse.

---

---

# Scenario 5 — "I need one line from 10,000 files"

---

Tool

```bash
rg
```

Example

```bash
rg express
```

---

Need route?

```bash
rg router
```

Need JWT?

```bash
rg jwt
```

---

Backend developers use this every day.

---

Challenge

Find every

```
mongoose.connect
```

inside one of your projects.

---

---

# Scenario 6 — "This file is huge"

---

Don't use

```bash
cat logfile.log
```

❌

Instead

```bash
less logfile.log
```

Navigate:

Space → next page

b → previous

q → quit

---

Challenge

Open:

```bash
/var/log/syslog
```

(or another large log file on your system)

---

---

# Scenario 7 — "Show me the last errors"

Tool

```bash
tail
```

Example

```bash
tail app.log
```

Live logs

```bash
tail -f app.log
```

This is exactly how you'll watch logs on servers.

---

Challenge

Create

```bash
echo hello > app.log
```

Then

```bash
tail -f app.log
```

Open another terminal:

```bash
echo "New log entry" >> app.log
```

Watch it appear live.

---

---

# Scenario 8 — "This JSON is unreadable"

Instead of

```bash
cat package.json
```

Use

```bash
bat package.json
```

Syntax highlighting makes it much easier to read.

---

Challenge

Open

```bash
package.json
README.md
```

using `bat`.

---

---

# Scenario 9 — "I keep typing long paths"

Instead of

```bash
cd ~/Documents/Projects/MERN/StudyNotion/server/controllers
```

Use

```bash
z server
```

or

```bash
z study
```

---

Challenge

Navigate between three projects using only `zoxide`.

---

---

# Scenario 10 — "Something is using all my RAM"

Tool

```bash
btop
```

Look for:

- CPU usage
- Memory usage
- Running processes
- Network activity

---

Challenge

Run:

```bash
btop
```

Find the process using the most CPU.

---

# 🎓 End of Part 1 Challenge

Without using your mouse, complete this workflow:

```
Open terminal
        │
        ▼
Find your MERN project
        │
        ▼
Go into it
        │
        ▼
List its files
        │
        ▼
Search for "express"
        │
        ▼
Open package.json
        │
        ▼
Find README.md
        │
        ▼
Monitor system resources
```

Use only these tools:

```
pwd
lsd
fd
fzf
rg
bat
zoxide
btop
```

---

# 🏅 Bonus Exercise (Recommended)

Time yourself and try to complete these tasks in under **3 minutes**:

1. Open your terminal.
2. Jump to your main MERN project using `zoxide`.
3. List the project contents with `lsd`.
4. Find every `package.json` using `fd`.
5. Search for `express` using `rg`.
6. Open `package.json` with `bat`.
7. Start `btop` and identify the top CPU process.
8. Exit `btop` and return to the terminal.

Repeat this challenge every few days. You'll be surprised how quickly these commands become second nature.

---

📖 **Next Part:** **Git & GitHub for Backend Developers (Scenarios 11–20)**, where we'll practice recovering from mistakes, resolving merge conflicts, navigating history, and using `lazygit` and `gh` effectively. That section is built around real problems you'll encounter while working on MERN projects.

Excellent! This is my favorite chapter because **Git mistakes happen to everyone**. The difference between a beginner and an experienced developer is that experienced developers know how to recover.

---

# 📘 Part 2 — Git & GitHub for Backend Developers (Scenarios 11–20)

> **Difficulty:** ⭐⭐ Beginner → Intermediate
> 
> **Goal:** Learn how to recover from mistakes without panicking.

---

# 🎯 Scenario 11 — "What changed?"

## Problem

You worked for 3 hours.

You forgot what you changed.

---

## Think First

Before committing, always ask:

> What exactly am I about to commit?

---

## Tools

```bash
git status
git diff
lazygit
```

---

## Commands

Check status:

```bash
git status
```

Example:

```
modified: server.js

modified: package.json

new file: auth.js
```

See actual changes:

```bash
git diff
```

Or use:

```bash
lazygit
```

Press:

```
Files Panel

↓

Select file

↓

Enter
```

---

## Real MERN Example

Suppose you edited:

```
controllers/

middleware/

routes/

models/
```

Before committing:

```bash
git diff
```

You'll often catch accidental debug statements like:

```jsx
console.log(req.body);
```

before they reach GitHub.

---

## Interview Tip

**Question**

How do you see unstaged changes?

Answer:

```bash
git diff
```

---

## Challenge

Modify one file.

Then answer:

- Which file changed?
- Which line changed?

---

---

# 🎯 Scenario 12 — "Oops... I edited the wrong file"

Problem

You accidentally changed:

```
.env.example
```

Instead of

```
.env
```

---

## Tools

```bash
git restore
```

---

## Command

```bash
git restore filename
```

Example

```bash
git restore package.json
```

All changes disappear.

---

## Be Careful

This **cannot** be undone easily.

Always check:

```bash
git diff
```

first.

---

## Challenge

Change [README.md](http://README.md).

Restore it.

Verify:

```bash
git status
```

---

---

# 🎯 Scenario 13 — "I forgot to add one file"

Problem

Commit already created.

Forgot

```
middleware/auth.js
```

---

## Tools

```bash
git add
git commit --amend
```

---

## Commands

```bash
git add middleware/auth.js

git commit --amend
```

Git adds it to the previous commit.

No new commit needed.

---

## Interview Tip

When should you use:

```bash
git commit --amend
```

Answer:

To modify the most recent commit before pushing.

---

---

# 🎯 Scenario 14 — "My commit message is terrible"

Current message

```
fix
```

😅

---

Better:

```
Fix JWT authentication middleware
```

---

Command

```bash
git commit --amend
```

Editor opens.

Write better message.

---

Challenge

Rename your last commit.

---

---

# 🎯 Scenario 15 — "I committed too early"

History

```
Commit A

↓

Commit B

↓

Commit C
```

Need to remove

```
Commit C
```

---

## Tool

```bash
git reset
```

---

Soft reset

```bash
git reset --soft HEAD~1
```

Commit removed.

Files stay.

---

Hard reset

```bash
git reset --hard HEAD~1
```

Commit gone.

Files gone.

⚠️ Dangerous.

---

Interview Question

Difference between

```
soft

mixed

hard
```

Know this well.

---

---

# 🎯 Scenario 16 — "I pushed a bug"

Never do

```bash
git reset --hard
git push --force
```

on shared branches.

Instead

```bash
git revert
```

---

Command

```bash
git revert COMMIT_ID
```

Creates a new commit that undoes the old one.

---

Real Company Workflow

Bug in production.

↓

Revert.

↓

Deploy.

↓

Fix later.

---

---

# 🎯 Scenario 17 — "Where did my code go?"

You deleted a branch.

Panic.

---

Tool

```bash
git reflog
```

Example

```bash
git reflog
```

Output

```
HEAD@{0}

HEAD@{1}

HEAD@{2}
```

Recover:

```bash
git checkout HASH
```

---

Think of `git reflog` as Git's safety net.

---

---

# 🎯 Scenario 18 — "I forgot which branch I'm on"

Command

```bash
git branch
```

Current branch:

```
*
```

Example

```
main

* feature/auth
```

Switch

```bash
git switch main
```

Create

```bash
git switch -c feature/payment
```

---

Challenge

Create

```
feature/profile
```

Switch back.

Delete it.

---

---

# 🎯 Scenario 19 — "Merge conflict!"

Everyone gets them.

Never panic.

---

Example

You

```
login.js
```

Friend

```
login.js
```

Both edit same line.

Git

```
CONFLICT
```

---

Resolve

```bash
git status
```

Open file.

See

```
<<<<<<< HEAD

=======

>>>>>>>
```

Edit.

Save.

Then

```bash
git add .
```

```bash
git commit
```

---

Lazygit makes this much easier.

---

---

# 🎯 Scenario 20 — "Someone asked me to review a Pull Request"

Instead of browser

Use

```bash
gh
```

List PRs

```bash
gh pr list
```

View

```bash
gh pr view 12
```

Checkout

```bash
gh pr checkout 12
```

Merge

```bash
gh pr merge
```

---

# 🏅 Mini Boss Fight

You cloned a MERN project.

Your tasks:

```
Clone repository

↓

Create feature branch

↓

Edit README

↓

Commit

↓

Push

↓

Open Pull Request

↓

Review PR

↓

Merge PR
```

Tools

```
git

gh

lazygit
```

---

# 🚨 Production Incident

It's Friday evening.

You pushed:

```
Authentication update
```

Now users can't log in.

What do you do?

Think before reading the answer.

---

### Step 1

```bash
git log --oneline
```

Find the bad commit.

---

### Step 2

If it's already in production:

```bash
git revert BAD_COMMIT_HASH
```

Don't rewrite history.

---

### Step 3

Push the revert.

---

### Step 4

Verify the fix.

---

### Step 5

Create a new branch to properly fix the original issue.

---

# 💡 Git Commands Every Backend Developer Should Know

|Command|When to Use|
|---|---|
|`git status`|Check what's changed|
|`git diff`|See line-by-line changes|
|`git add -p`|Stage only selected changes|
|`git restore <file>`|Discard changes to a file|
|`git commit`|Save your work|
|`git commit --amend`|Fix the last commit|
|`git log --oneline --graph --all`|Visualize history|
|`git switch <branch>`|Change branches|
|`git switch -c <branch>`|Create and switch to a branch|
|`git stash`|Temporarily save unfinished work|
|`git stash pop`|Restore stashed work|
|`git fetch`|Download remote updates|
|`git pull --rebase`|Update your branch cleanly|
|`git revert`|Safely undo a pushed commit|
|`git reflog`|Recover from many mistakes|

---

# 🎮 Level-Up Challenge (Recommended)

Create a practice repository called `git-playground` and complete these tasks without using GitHub Desktop or VS Code's Git interface:

1. Initialize a Git repository.
2. Create a `README.md` and make your first commit.
3. Create a `feature/login` branch.
4. Make three separate commits.
5. Amend the last commit message.
6. Stash an unfinished change.
7. Switch back to `main`.
8. Restore the stashed work.
9. Create a merge conflict on purpose and resolve it.
10. Delete the feature branch and recover it using `git reflog`.

If you can complete this lab comfortably, you'll have a level of Git confidence that many junior developers don't yet have.

---

# 📖 Next Part: **HTTP, REST APIs & JSON (Scenarios 21–35)**

This is where everything comes together for backend development. We'll use:

- `curl`
- `xh`
- `jq`
- HTTP methods (GET, POST, PUT, PATCH, DELETE)
- Headers
- Cookies
- JWT authentication
- File uploads
- API debugging
- Real Express server scenarios

In my experience, this is the chapter where backend development starts to feel "real" because you're interacting with APIs the same way frontend apps, mobile apps, and other services do.

Awesome! 🎉

Welcome to what I think is **the most important chapter** for a backend developer.

If you master this chapter, you'll understand **how frontend and backend actually communicate**.

---

# 📘 Part 3 — HTTP, REST APIs & JSON (Scenarios 21–35)

> **Difficulty:** ⭐⭐ Beginner → Intermediate
> 
> **Goal:** Think like Postman, but from the terminal.

We'll use:

- ✅ `curl`
- ✅ `xh`
- ✅ `jq`

---

# Before We Start

Imagine this architecture.

```
React
   │
   ▼
HTTP Request
   │
   ▼
Express Server
   │
   ▼
Controller
   │
   ▼
Service
   │
   ▼
MongoDB
```

Every request goes through **HTTP**.

Your job is to understand every part.

---

# 🎯 Scenario 21 — "Is my API alive?"

## Problem

Your Express server is running.

But...

Is it really?

---

## Think

Don't open Chrome.

Backend developers usually test the API first.

---

## Tool

```bash
curl
```

---

## Command

```bash
curl <http://localhost:5000>
```

Example

```json
{
  "message": "Server is running"
}
```

---

## Better

Use

```bash
xh GET localhost:5000
```

Cleaner output.

---

## Why?

Before debugging React...

Always verify the backend.

---

## Real Example

React says

```
Network Error
```

First command

```bash
curl <http://localhost:5000>
```

If this fails...

React isn't the problem.

---

## Challenge

Create

```jsx
app.get("/", (req,res)=>{
    res.json({
        status:"Running"
    })
})
```

Test it.

---

---

# 🎯 Scenario 22 — "Can I create a user?"

---

POST request

Instead of browser

Use

```bash
xh
```

Example

```bash
xh POST localhost:5000/users \
name=Rahul \
age:=21
```

Notice

```
=
```

means string

while

```
:=
```

means number

---

Response

```json
{
    "id":1,
    "name":"Rahul",
    "age":21
}
```

---

Challenge

Create

```
POST /users
```

---

---

# 🎯 Scenario 23 — "My API returns ugly JSON"

---

Tool

```bash
jq
```

Instead

```bash
curl API
```

Do

```bash
curl API | jq
```

Beautiful.

---

Extract names

```bash
curl API | jq '.users[].firstName'
```

---

Challenge

Print only emails.

---

---

# 🎯 Scenario 24 — "What headers did the server send?"

Headers are extremely important.

See them.

```bash
curl -I localhost:5000
```

or

```bash
xh -h GET localhost:5000
```

---

Find

```
Content-Type

Server

Date

Cache-Control
```

---

Interview

Difference between

Body

Headers

Status Code

---

---

# 🎯 Scenario 25 — "Why am I getting 404?"

Response

```
404 Not Found
```

What does it mean?

Usually

Wrong URL

Wrong Route

Wrong HTTP Method

---

Debug

```bash
curl localhost:5000/users
```

Then

```bash
curl localhost:5000/user
```

Notice difference.

---

Challenge

Intentionally type wrong endpoint.

---

---

# 🎯 Scenario 26 — "Why am I getting 500?"

500 means

Server crashed.

Check response.

```bash
curl localhost:5000/users
```

Then

Check terminal logs.

---

Real Life

Forgot

```jsx
await
```

Server crashes.

---

Challenge

Throw an error.

See

---

---

# 🎯 Scenario 27 — "Authentication"

Protected route.

Need

JWT.

---

Without token

```bash
curl localhost:5000/profile
```

Result

```
401 Unauthorized
```

---

With token

```bash
curl \
-H "Authorization: Bearer TOKEN" \
localhost:5000/profile
```

or

```bash
xh GET localhost:5000/profile \
Authorization:"Bearer TOKEN"
```

---

Challenge

Protect

```
/profile
```

---

---

# 🎯 Scenario 28 — "Cookies"

See cookies.

```bash
curl -I localhost:5000
```

Look

```
Set-Cookie
```

---

Send cookie

```bash
curl \
--cookie \
"token=abc123"
```

---

Challenge

Login.

Receive cookie.

Reuse cookie.

---

---

# 🎯 Scenario 29 — "Upload a file"

Use

```bash
curl
```

Example

```bash
curl \
-F "image=@cat.png" \
localhost:5000/upload
```

---

Challenge

Upload

```
resume.pdf
```

---

---

# 🎯 Scenario 30 — "Measure API Speed"

```bash
time curl localhost:5000
```

Output

```
real

user

sys
```

---

Question

Why is API slow?

---

---

# 🎯 Scenario 31 — "Status Codes"

Know these.

```
200 OK

201 Created

204 No Content

301 Moved Permanently

302 Found

304 Not Modified

400 Bad Request

401 Unauthorized

403 Forbidden

404 Not Found

409 Conflict

422 Unprocessable Entity

429 Too Many Requests

500 Internal Server Error

502 Bad Gateway

503 Service Unavailable
```

Interview favorite.

---

---

# 🎯 Scenario 32 — "PUT vs PATCH"

PUT

Replace everything.

PATCH

Update part.

---

Example

PUT

```json
{
"name":"Rahul",
"age":22
}
```

PATCH

```json
{
"age":22
}
```

---

---

# 🎯 Scenario 33 — "OPTIONS"

Browser sends

```
OPTIONS
```

before

POST

This is

CORS.

---

If OPTIONS fails

Frontend fails.

---

Challenge

Look at Network tab.

Observe OPTIONS.

---

---

# 🎯 Scenario 34 — "Delete User"

```bash
xh DELETE localhost:5000/users/1
```

or

```bash
curl \
-X DELETE \
localhost:5000/users/1
```

---

Challenge

Delete one user.

---

---

# 🎯 Scenario 35 — "Debug Like a Backend Engineer"

Suppose

```
Frontend

↓

Login

↓

Network Error
```

What should you do?

---

Step 1

```bash
curl localhost:5000/login
```

---

Step 2

```bash
xh POST localhost:5000/login
```

---

Step 3

Check

```
Status Code
```

---

Step 4

Check

Headers.

---

Step 5

Check

JSON.

---

Step 6

Check Express logs.

---

Step 7

Check MongoDB.

---

# 🎮 Mini Boss Fight

Build this API:

```
GET /users

POST /users

GET /users/:id

PATCH /users/:id

DELETE /users/:id
```

Test **everything** without Postman.

Only use:

```
curl
xh
jq
```

---

# 🏆 Production Incident

It's **9:00 PM**.

Your React app shows:

```
AxiosError: Network Error
```

What would you do?

### Step 1: Is the backend running?

```bash
curl <http://localhost:5000>
```

### Step 2: Is the port open?

```bash
ss -tulpn | grep 5000
```

### Step 3: Can you reach the endpoint?

```bash
xh GET localhost:5000/users
```

### Step 4: Did the server return valid JSON?

```bash
xh GET localhost:5000/users | jq
```

### Step 5: Check the backend logs.

If all five checks pass, the problem is likely in the frontend configuration (such as the API base URL, CORS, or request code).

---

# 🚀 Master Challenge — Build an API Tester

Create a small Express app with these routes:

```
GET    /health
GET    /users
GET    /users/:id
POST   /users
PATCH  /users/:id
DELETE /users/:id
POST   /login
GET    /profile
```

Now create a file called **`api-test.sh`** that automatically tests every endpoint.

Example:

```bash
#!/usr/bin/env bash

echo "Health Check"
xh GET localhost:5000/health

echo "Create User"
xh POST localhost:5000/users \
  name="Rahul" \
  email="rahul@example.com"

echo "List Users"
xh GET localhost:5000/users

echo "Login"
xh POST localhost:5000/login \
  email="rahul@example.com" \
  password="password123"
```

Running one script to verify your API after every change is a habit used by many backend developers. It helps you catch issues quickly without repeatedly opening a browser or Postman.

---

## ⭐ Your Next Adventure (Part 4)

Part 4 is where backend developers usually have their biggest "aha!" moment.

We'll cover:

- 🌐 DNS (`doggo`, `dig`)
- 🔌 Ports (`ss`, `lsof`)
- 🌍 Networking (`ping`, `mtr`, `traceroute`)
- 🔒 HTTPS & SSL (`openssl`)
- 🏠 Custom domains
- ☁️ Vercel + Render deployments
- 🛠️ Debugging "site not opening", "API not reachable", "CORS", and "SSL certificate" issues

By the end of that chapter, you'll know how to diagnose many deployment and networking problems using only the terminal.

This is one of my favorite chapters because this is where developers stop saying:

> "It doesn't work."

and start saying:

> "The DNS is fine, but the backend isn't listening on port 5000."

That's a huge difference.

---

# 📘 Part 4 — Networking, DNS & Deployment (Scenarios 36–50)

> **Difficulty:** ⭐⭐⭐ Intermediate
> 
> **Goal:** Learn to debug network and deployment issues like a backend engineer.

You'll master:

- 🌐 DNS
- 📡 Ports
- 🔒 HTTPS
- ☁️ Deployments
- 🌍 Domains
- 🚀 Render, Vercel, VPS

---

# Before We Begin

Understand this picture.

```
Browser
     │
     ▼
DNS
     │
     ▼
IP Address
     │
     ▼
Server
     │
     ▼
Port
     │
     ▼
Express
     │
     ▼
MongoDB
```

If something breaks...

Your job is to find **which box is broken**.

---

# 🎯 Scenario 36 — "My website doesn't open"

Suppose:

```
<https://myapp.com>
```

Browser:

```
This site can't be reached
```

---

## Think

Is it

❌ React?

❌ Express?

❌ MongoDB?

Maybe none of them.

---

## First Question

Can DNS find your website?

---

## Tool

```bash
doggo myapp.com
```

or

```bash
dig myapp.com
```

---

Good output

```
A

104.21.xx.xx
```

No output?

DNS problem.

---

## Real Example

You buy

```
rahulportfolio.com
```

After deployment

Run

```bash
doggo rahulportfolio.com
```

No A record?

Fix DNS first.

---

## Challenge

Check

```
google.com

github.com

vercel.com

render.com
```

Which IP addresses do they resolve to?

---

---

# 🎯 Scenario 37 — "What are Nameservers?"

Domain

↓

DNS Provider

↓

Website

---

Tool

```bash
doggo google.com NS
```

or

```bash
dig NS google.com
```

Output

```
ns1.google.com

ns2.google.com
```

---

Question

Who controls DNS?

Nameservers.

---

Real Life

Hostinger

Cloudflare

GoDaddy

Route53

All change nameservers.

---

Challenge

Find the nameservers for your own domain (or any public domain you're curious about).

---

---

# 🎯 Scenario 38 — "Email isn't working"

Someone says

```
I never received verification email.
```

---

Check

```bash
doggo gmail.com MX
```

or

```bash
dig MX gmail.com
```

MX

=

Mail Exchange

---

Challenge

Find MX records for

```
gmail.com

outlook.com

proton.me
```

---

---

# 🎯 Scenario 39 — "Google verification failed"

Need TXT record.

Check

```bash
doggo example.com TXT
```

Example

```
google-site-verification

SPF

DKIM

DMARC
```

---

Backend developers do this often.

Especially when using

- Resend
- Zoho
- Gmail Workspace
- SendGrid

---

Challenge

Inspect the TXT records for a domain you own or a public domain.

---

---

# 🎯 Scenario 40 — "Which process is using port 5000?"

Express won't start.

Error

```
EADDRINUSE
```

---

Tool

```bash
ss
```

Run

```bash
ss -tulpn | grep 5000
```

---

See

```
LISTEN
```

Good.

---

Find owner

```bash
sudo lsof -i :5000
```

---

Kill

```bash
kill PID
```

---

Challenge

Start an Express server.

Find its PID.

Kill it.

Restart it.

---

---

# 🎯 Scenario 41 — "Is my backend actually listening?"

Express says

```
Server started
```

Really?

---

Run

```bash
ss -tulpn
```

Should show

```
5000
```

If not

Your app never opened the port.

---

Challenge

Compare:

- Express server running
- Express server stopped

How does `ss` change?

---

---

# 🎯 Scenario 42 — "Can my computer reach the server?"

Tool

```bash
ping
```

Example

```bash
ping google.com
```

---

Output

```
64 bytes

time=17ms
```

Question

Latency?

Packet loss?

---

Challenge

Compare:

```
google.com

github.com

cloudflare.com
```

---

---

# 🎯 Scenario 43 — "Where is the network slow?"

Tool

```bash
mtr
```

or

```bash
traceroute
```

Run

```bash
mtr google.com
```

Shows

Every router.

Packet loss.

Latency.

---

Real Production

Website slow.

Is it

Server?

ISP?

Internet?

---

---

# 🎯 Scenario 44 — "What ports are open?"

Tool

```bash
nmap
```

Example

```bash
nmap localhost
```

See

```
22

80

443

3000

5000
```

---

Challenge

Scan your own machine.

---

⚠️ Only scan systems you own or have permission to test.

---

---

# 🎯 Scenario 45 — "HTTPS certificate problem"

Browser

```
Not Secure
```

---

Tool

```bash
openssl
```

Example

```bash
openssl s_client -connect google.com:443
```

Find

Issuer

Expiry

TLS Version

Cipher

---

Challenge

Inspect GitHub's certificate.

---

---

# 🎯 Scenario 46 — "Is my API reachable?"

Instead of browser

Use

```bash
curl
```

```bash
curl <https://api.example.com/users>
```

or

```bash
xh GET api.example.com/users
```

---

Question

200?

404?

500?

---

Challenge

Test your deployed backend.

---

---

# 🎯 Scenario 47 — "Frontend says Network Error"

React

↓

Axios

↓

```
Network Error
```

---

Investigation

```
Is backend running?

↓

Can curl reach it?

↓

Port open?

↓

DNS OK?

↓

HTTPS OK?

↓

CORS?
```

Notice:

React is almost the last thing you check.

---

---

# 🎯 Scenario 48 — "Deployment Debugging"

Your stack

```
React

↓

Vercel

↓

Render

↓

MongoDB Atlas
```

Users report:

```
Login failed.
```

---

Checklist

✅ DNS

✅ HTTPS

✅ Backend

✅ Environment Variables

✅ Database

✅ JWT

---

Challenge

Write your own debugging checklist.

---

---

# 🎯 Scenario 49 — "My website is slow"

Question

Backend?

Frontend?

Database?

DNS?

---

Tools

```bash
time
curl
ping
mtr
```

Example

```bash
time curl <https://example.com>
```

---

Challenge

Compare response times for a few public websites.

---

---

# 🎯 Scenario 50 — "Production Incident"

Imagine it's 3 AM.

Pager rings.

```
Website Down
```

Don't panic.

---

Investigation Order

```
DNS

↓

Ping

↓

HTTPS

↓

HTTP

↓

Port

↓

Process

↓

Logs

↓

Database
```

---

Commands

```bash
doggo myapp.com

ping myapp.com

curl <https://myapp.com>

ss -tulpn

sudo lsof -i :5000

journalctl -u your-service

tail -f logs/app.log
```

---

# 🎮 Mini Boss Fight

Your React frontend on Vercel can't reach your Express backend on Render.

Users only see:

```
AxiosError: Network Error
```

Without opening VS Code, investigate using the terminal.

Suggested order:

1. Verify the backend URL with `curl` or `xh`.
2. Check DNS with `doggo` or `dig`.
3. Confirm HTTPS with `openssl s_client`.
4. If testing locally, verify the listening port with `ss`.
5. Check the backend logs.
6. Verify environment variables (API URL, JWT secret, database URL).
7. Test the API endpoint directly.
8. Confirm CORS configuration if the API works from the terminal but not the browser.

---

# 🧠 Interview Round

**Q1:** What's the difference between DNS and an IP address?

**Expected answer:** DNS translates human-readable domain names (like `example.com`) into IP addresses that computers use to communicate.

---

**Q2:** What does port 443 mean?

**Expected answer:** It's the default port for HTTPS.

---

**Q3:** Why would you use `ss` instead of `ping`?

**Expected answer:** `ping` checks network reachability to a host. `ss` shows which ports and sockets are open on the local system.

---

**Q4:** What does an MX record do?

**Expected answer:** It tells other mail servers where to deliver email for a domain.

---

**Q5:** If `curl <https://api.example.com/health`> returns `200 OK`, but your React app still shows "Network Error", what are some likely causes?

Good answers include:

- CORS misconfiguration
- Wrong frontend API URL
- Mixed HTTP/HTTPS content
- Browser-specific authentication or cookie issues

---

# 📚 Practice Lab

Deploy a small Express application with a `/health` endpoint.

Then verify it using only terminal tools:

```bash
doggo your-domain.com
curl <https://your-domain.com/health>
xh GET <https://your-domain.com/health>
openssl s_client -connect your-domain.com:443
```

Finally, stop the server and observe how the results change.

---

# 🚀 Next Part (Part 5)

This is where you'll move from networking into **containers and deployment**:

- 🐳 Docker
- 📦 Docker Compose
- 🗄️ MongoDB containers
- 🌐 Nginx reverse proxy
- 🔄 Environment variables
- 📋 Logs
- 🛠️ Health checks
- 🚀 Deploying production-ready MERN applications

This chapter ties together everything you've learned so far and is one of the most valuable skills for backend engineering.

I'm really enjoying this series. 😊

This chapter is where many developers go from **"I can build a backend"** to **"I can deploy and run a backend."**

---

# 📘 Part 5 — Docker, Docker Compose & Production Deployment (Scenarios 51–70)

> **Difficulty:** ⭐⭐⭐⭐ Intermediate
> 
> **Goal:** Package, run, debug, and deploy applications the way companies do.

By the end of this chapter, you'll understand why Docker is everywhere in backend development.

---

# Before We Start

Without Docker:

```
My Laptop
│
├── Node 20
├── MongoDB
├── Redis
├── npm
├── Environment Variables
└── Works only on my machine 😅
```

With Docker:

```
Docker Image
│
├── Node
├── Dependencies
├── Source Code
├── Environment Variables
└── Runs the same everywhere ✅
```

---

# 🎯 Scenario 51 — "It works on my laptop"

## Problem

You send your backend to your friend.

They run:

```bash
npm install
npm run dev
```

It crashes.

Why?

Different:

- Node version
- npm version
- OS
- Environment

---

## Solution

Docker.

---

## Check Docker

```bash
docker --version
```

---

## Interview

**Why Docker?**

Good answer:

> Docker packages the application and its dependencies into a portable container that behaves the same across environments.

---

---

# 🎯 Scenario 52 — "Run my first container"

Pull nginx.

```bash
docker run nginx
```

Oops.

Terminal hangs.

Why?

Because nginx runs in foreground.

---

Run detached.

```bash
docker run -d nginx
```

See running containers.

```bash
docker ps
```

Stop.

```bash
docker stop CONTAINER_ID
```

---

Challenge

Run nginx.

Stop it.

Run again.

---

---

# 🎯 Scenario 53 — "Which containers exist?"

Running:

```bash
docker ps
```

All:

```bash
docker ps -a
```

Remove:

```bash
docker rm CONTAINER
```

---

Real life

Your laptop has:

```
15 stopped containers.
```

Clean them.

---

---

# 🎯 Scenario 54 — "Container logs"

Express crashes.

Container exits.

Don't guess.

Read logs.

```bash
docker logs CONTAINER
```

Follow logs.

```bash
docker logs -f CONTAINER
```

---

Real life

90% of Docker debugging starts here.

---

---

# 🎯 Scenario 55 — "Enter the container"

Need shell.

```bash
docker exec -it CONTAINER bash
```

Some images:

```bash
docker exec -it CONTAINER sh
```

Now you're inside.

Check:

```bash
pwd

ls

env
```

---

Challenge

Enter nginx.

Explore.

Exit.

---

---

# 🎯 Scenario 56 — "Build my Express app"

Dockerfile

```docker
FROM node:22-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 5000

CMD ["npm","start"]
```

Build.

```bash
docker build -t todo-backend .
```

Run.

```bash
docker run -p 5000:5000 todo-backend
```

---

Interview

Difference

Image

vs

Container

---

---

# 🎯 Scenario 57 — "Why can't I access localhost?"

Container running.

Browser:

```
localhost:5000
```

Fails.

Forgot

```bash
-p 5000:5000
```

---

Think.

Container port ≠ Host port.

---

Challenge

Map

```
8080

↓

5000
```

---

---

# 🎯 Scenario 58 — "Environment Variables"

Never hardcode.

Bad

```jsx
const secret="123456";
```

Good

```jsx
process.env.JWT_SECRET
```

Run

```bash
docker run \
-e JWT_SECRET=abc123 \
todo-backend
```

---

Challenge

Print one environment variable.

---

---

# 🎯 Scenario 59 — "Docker Compose"

Instead of

```
Mongo

↓

Node

↓

Redis
```

starting individually...

Compose.

```yaml
services:
  backend:
  mongodb:
```

Run

```bash
docker compose up
```

Stop

```bash
docker compose down
```

---

Challenge

Start two containers.

---

---

# 🎯 Scenario 60 — "MongoDB in Docker"

```yaml
mongodb:
  image: mongo
```

Connect

```
mongodb://mongodb:27017
```

NOT

```
localhost
```

Because containers talk through service names.

---

Huge interview question.

---

---

# 🎯 Scenario 61 — "Restart Policy"

Server restarts.

Container dies.

Automatically restart.

```yaml
restart: unless-stopped
```

---

---

# 🎯 Scenario 62 — "Volumes"

Without volume

Delete container.

Lose data.

With volume

Data survives.

```yaml
volumes:
  mongo-data:
```

---

Challenge

Delete Mongo container.

See data remains.

---

---

# 🎯 Scenario 63 — "Health Checks"

Container running.

Application dead.

Need

Health endpoint.

```
GET /health
```

Docker checks.

Healthy.

or

Unhealthy.

---

Interview favorite.

---

---

# 🎯 Scenario 64 — "Nginx Reverse Proxy"

Instead of

```
localhost:5000
```

Users see

```
example.com
```

Nginx

↓

Express

---

Benefits

- HTTPS
- Load balancing
- Compression
- Static files

---

---

# 🎯 Scenario 65 — "Production Logs"

Container

↓

Logs

```bash
docker logs
```

App

↓

Logs

```bash
tail -f app.log
```

System

↓

Logs

```bash
journalctl
```

Know where to look.

---

---

# 🎯 Scenario 66 — "Image Size"

Node image

1GB.

Alpine

200MB.

Smaller image.

Faster deployment.

---

Challenge

Compare image sizes.

---

---

# 🎯 Scenario 67 — "Multi-stage Build"

Don't ship

```
node_modules

tests

docs
```

Use

Builder

↓

Production

Smaller image.

---

---

# 🎯 Scenario 68 — "Docker Network"

Container A

↓

Container B

Can they talk?

Create

```bash
docker network create backend-network
```

Attach containers.

---

---

# 🎯 Scenario 69 — "Production Deployment"

Pipeline

```
GitHub

↓

Docker Build

↓

Push Image

↓

Server Pull

↓

Run Container

↓

Nginx

↓

HTTPS

↓

Users
```

Understand every arrow.

---

---

# 🎯 Scenario 70 — "Production Outage"

Users say:

```
Website Down
```

Your checklist:

```
Is container running?

↓

docker ps

↓

Logs?

↓

docker logs

↓

Health endpoint?

↓

curl /health

↓

Port mapped?

↓

docker ps

↓

Database?

↓

Environment Variables?

↓

Nginx?

↓

Solved.
```

---

# 🎮 Mini Boss Fight

Create a complete MERN backend deployment.

Requirements:

```
Express
        │
        ▼
Docker
        │
        ▼
MongoDB Container
        │
        ▼
Docker Compose
        │
        ▼
Health Endpoint
        │
        ▼
Nginx
```

Verify using:

```bash
curl <http://localhost/health>
```

---

# 🧠 Interview Questions

### Q1

Image vs Container?

**Answer**

An image is a read-only blueprint. A container is a running instance of that image.

---

### Q2

Why Docker Compose?

Because applications usually consist of multiple services (backend, database, cache, etc.) that need to start together.

---

### Q3

Why use volumes?

To persist data outside the container's lifecycle.

---

### Q4

Why not connect to MongoDB using `localhost` inside a container?

Because `localhost` refers to the current container itself. In Docker Compose, containers communicate using the **service name** on the shared network.

---

### Q5

Why create a `/health` endpoint?

To allow Docker, load balancers, and monitoring systems to verify that the application is actually responding—not just that the process is running.

---

# 🏗️ Real Company Architecture

A typical production setup looks like this:

```
GitHub
   │
   ▼
GitHub Actions (CI)
   │
   ▼
Docker Image
   │
   ▼
Container Registry
   │
   ▼
Production Server
   │
   ▼
Nginx Reverse Proxy
   │
   ▼
Express API
   │
   ▼
MongoDB
```

As a junior backend developer, understanding this flow is often more valuable than memorizing dozens of Docker commands.

---

# 🎯 Weekly Project

Build a **Production-Ready Todo API** with:

- Express
- MongoDB
- Dockerfile
- `docker-compose.yml`
- Health endpoint (`/health`)
- Environment variables
- Persistent MongoDB volume
- Nginx reverse proxy
- README with setup instructions

This single project demonstrates many of the deployment skills employers look for.

---

# 🚀 Part 6 Preview — Production Debugging & Monitoring (Scenarios 71–100)

This is the final chapter and my favorite.

You'll learn how experienced backend engineers investigate incidents:

- 📋 Reading logs effectively
- ⚡ CPU and memory debugging
- 🧠 Memory leaks
- 🔍 Profiling Node.js applications
- 📈 Monitoring and metrics
- 🔄 Process managers (PM2)
- 🛠️ Systemd services
- 🧪 Load testing
- 🚨 Incident response
- 🎯 Real interview debugging exercises

By the end of Part 6, you'll have a complete journey from writing backend code to operating it in production. That's the skill set that turns a MERN developer into a backend engineer.

Perfect. You've now reached the chapter that separates **developers who write code** from **engineers who operate systems**.

This chapter isn't about learning more commands. It's about **thinking during production incidents**.

---

# 📘 Part 6 — Production Debugging & Monitoring (Scenarios 71–100)

> **Difficulty:** ⭐⭐⭐⭐ Advanced
> 
> **Goal:** Diagnose production issues calmly and systematically.

By the end of this chapter, you'll know how to answer:

> **"The website is down. Now what?"**

---

# The Production Mindset

Never start with assumptions.

Never say:

```
MongoDB is probably down.
```

Instead:

```
Observe

↓

Collect Evidence

↓

Form Hypothesis

↓

Verify

↓

Fix

↓

Verify Again
```

This is exactly how senior engineers work.

---

# 🎯 Scenario 71 — "Users say the API is slow"

## Symptoms

Users complain:

```
Login takes 10 seconds.
```

---

## Don't Guess

Could be:

```
Network

↓

Server

↓

Database

↓

External API

↓

CPU

↓

Memory
```

---

## First Checks

Measure response time:

```bash
time curl <http://localhost:5000/health>
```

Then:

```bash
curl -w "\nTotal: %{time_total}s\n" <http://localhost:5000/health>
```

---

## Challenge

Compare:

- `/health`
- `/users`
- `/login`

Which is slower?

---

---

# 🎯 Scenario 72 — "CPU is 100%"

Tool

```bash
btop
```

Look for

```
CPU

Process

Load Average
```

---

Alternative

```bash
top
```

---

Need only Node?

```bash
ps aux | grep node
```

---

Challenge

Run

```bash
yes > /dev/null
```

Watch CPU spike.

Stop it.

```bash
Ctrl+C
```

Observe how `btop` changes.

---

---

# 🎯 Scenario 73 — "Memory keeps increasing"

Symptoms

```
400MB

↓

600MB

↓

900MB

↓

Killed
```

Memory leak.

---

Check

```bash
free -h
```

Process

```bash
ps aux --sort=-%mem
```

---

Node

```bash
node --inspect app.js
```

Use Chrome DevTools to inspect heap snapshots.

---

Challenge

Monitor memory before and after running your app.

---

---

# 🎯 Scenario 74 — "Server crashed"

Users:

```
Connection refused
```

---

Check

```bash
ps aux | grep node
```

No process?

Application exited.

---

Next

```bash
journalctl -u your-service
```

or

```bash
docker logs CONTAINER
```

---

Challenge

Throw an uncaught exception.

Find it in logs.

---

---

# 🎯 Scenario 75 — "Why did Node crash?"

Common reasons

```
Unhandled Promise Rejection

↓

Out Of Memory

↓

Syntax Error

↓

Port Already Used

↓

Environment Variable Missing
```

---

Logs tell the story.

Always read them completely.

---

Challenge

Delete

```
JWT_SECRET
```

Observe startup failure.

---

---

# 🎯 Scenario 76 — "Application logs"

Bad logging

```jsx
console.log("Error");
```

Better

```jsx
console.error({
  route: req.originalUrl,
  user: req.user?.id,
  message: err.message,
});
```

---

Challenge

Improve one route's logging.

---

---

# 🎯 Scenario 77 — "PM2"

Run app

```bash
pm2 start app.js
```

List

```bash
pm2 list
```

Logs

```bash
pm2 logs
```

Restart

```bash
pm2 restart app
```

---

Interview

Why PM2?

Automatic restarts, log management, process monitoring, and clustering.

---

---

# 🎯 Scenario 78 — "Systemd"

Production server

```bash
systemctl status myapp
```

Restart

```bash
sudo systemctl restart myapp
```

Enable on boot

```bash
sudo systemctl enable myapp
```

---

Challenge

Read an existing service file:

```bash
systemctl cat ssh
```

(or another installed service)

---

---

# 🎯 Scenario 79 — "Disk is full"

Check

```bash
df -h
```

Biggest folders

```bash
du -sh *
```

Need deeper?

```bash
du -sh ./* | sort -h
```

---

Challenge

Find the largest directory in your home folder.

---

---

# 🎯 Scenario 80 — "Logs filled the disk"

Find

```bash
du -sh /var/log/*
```

Clear only when appropriate.

Compress old logs.

Use log rotation.

---

Interview

Why rotate logs?

To prevent disk exhaustion.

---

---

# 🎯 Scenario 81 — "Environment variables missing"

Check

```bash
printenv
```

Need one

```bash
echo "$JWT_SECRET"
```

---

Challenge

Create

```bash
export MY_NAME=Rahul
```

Read it.

Open a new terminal.

What changed?

---

---

# 🎯 Scenario 82 — "Database isn't responding"

First

```bash
mongosh
```

Can you connect?

If Docker

```bash
docker exec -it mongodb mongosh
```

Then

```jsx
show dbs
```

---

Challenge

Stop MongoDB.

Observe backend behavior.

Restart it.

---

---

# 🎯 Scenario 83 — "API works locally but not in production"

Checklist

```
Environment Variables

↓

Database URL

↓

CORS

↓

HTTPS

↓

Reverse Proxy

↓

Firewall

↓

DNS
```

Never skip steps.

---

---

# 🎯 Scenario 84 — "Too many requests"

Users get:

```
429 Too Many Requests
```

Likely cause

Rate limiting.

Check middleware.

Verify expected behavior.

---

Challenge

Configure a small rate limit and trigger it with repeated requests.

---

---

# 🎯 Scenario 85 — "Who is connected?"

Sockets

```bash
ss -tun
```

Listening services

```bash
ss -tulpn
```

---

Challenge

Start your Express server and identify its listening socket.

---

---

# 🎯 Scenario 86 — "High load"

Investigate

```
CPU

↓

Memory

↓

Disk

↓

Database

↓

External APIs
```

Don't assume.

Measure.

---

---

# 🎯 Scenario 87 — "Node profiling"

Start

```bash
node --inspect app.js
```

Use Chrome DevTools.

Find

- Hot functions
- Memory leaks
- Heavy allocations

---

---

# 🎯 Scenario 88 — "Load testing"

Simple benchmark

```bash
ab -n 1000 -c 50 <http://localhost:5000/health>
```

Modern alternative

```bash
npx autocannon <http://localhost:5000/health>
```

Observe:

- Requests/sec
- Latency
- Errors

---

Challenge

Compare `/health` and `/users`.

---

---

# 🎯 Scenario 89 — "Monitoring"

What should you monitor?

```
CPU

Memory

Disk

Response Time

Error Rate

Database Connections

Request Count
```

If you don't measure it, you can't improve it.

---

---

# 🎯 Scenario 90 — "Alerts"

Good alert

```
API error rate > 5%
```

Bad alert

```
One request failed
```

Alerts should be actionable.

---

---

# 🎯 Scenario 91 — "Deployment failed"

Checklist

```
Build successful?

↓

Environment variables?

↓

Docker image?

↓

Logs?

↓

Health endpoint?
```

---

---

# 🎯 Scenario 92 — "Rollback"

New deployment broken.

Rollback.

```
Version 1.2.0

↓

Version 1.1.9
```

Always have a recovery plan.

---

---

# 🎯 Scenario 93 — "Database migration"

Sequence

```
Backup

↓

Run migration

↓

Verify

↓

Deploy
```

Never migrate blindly.

---

---

# 🎯 Scenario 94 — "Security incident"

Checklist

```
Rotate secrets

↓

Invalidate tokens

↓

Review logs

↓

Patch vulnerability

↓

Verify
```

---

---

# 🎯 Scenario 95 — "Unexpected 500 errors"

Investigate

```
Logs

↓

Stack Trace

↓

Request Payload

↓

Database

↓

External APIs
```

Reproduce before fixing.

---

---

# 🎯 Scenario 96 — "High latency after deployment"

Compare

Before deployment

↓

After deployment

What changed?

Configuration?

Database indexes?

External services?

---

---

# 🎯 Scenario 97 — "Users report random failures"

Questions

- Same route?
- Same browser?
- Same country?
- Same time?
- Same user?

Patterns matter.

---

---

# 🎯 Scenario 98 — "Incident Commander"

During a production outage:

1. Acknowledge the incident.
2. Assign roles if working in a team.
3. Gather facts.
4. Mitigate impact.
5. Communicate updates.
6. Fix the root cause.
7. Write a postmortem.

---

---

# 🎯 Scenario 99 — "Postmortem"

A good postmortem answers:

- What happened?
- Why did it happen?
- How was it detected?
- How was it fixed?
- What will prevent it next time?

Focus on improving the system, not blaming people.

---

---

# 🎯 Scenario 100 — "The Complete Production Investigation"

Imagine it's **2:17 AM**.

The alert says:

```
🚨 API unavailable
```

Your investigation flow:

```
1. Can DNS resolve?

↓

2. Can I reach the server?

↓

3. Is HTTPS working?

↓

4. Is the service running?

↓

5. Is the port listening?

↓

6. Check application logs.

↓

7. Check Docker or PM2.

↓

8. Check database connectivity.

↓

9. Verify environment variables.

↓

10. Test /health.

↓

11. Test real endpoints.

↓

12. Confirm users are recovered.
```

---

# 🎮 Final Boss Fight

You are on call.

At **1:43 AM**, you receive three alerts:

```
❌ Login failing
❌ CPU at 98%
❌ Error rate increased to 27%
```

Without opening your editor, investigate using only terminal tools.

Suggested workflow:

```bash
btop
ps aux | grep node
ss -tulpn
curl <http://localhost:5000/health>
docker ps
docker logs <container>
free -h
df -h
journalctl -u your-service
```

Record:

- What you observed
- Your hypothesis
- The evidence supporting it
- The fix
- How you verified recovery

---

# 🎓 Congratulations!

You've completed **100 real-world backend scenarios**, covering:

- ✅ Linux & terminal fundamentals
- ✅ Git & GitHub workflows
- ✅ HTTP, REST APIs & JSON
- ✅ Networking & deployment
- ✅ Docker & containers
- ✅ Production debugging & operations

## My Recommendation for You

Given your MERN focus and interest in backend engineering, here are three capstone projects that combine everything you've learned:

1. **Production-Ready Todo API**
    - JWT authentication
    - Docker Compose
    - MongoDB
    - Health endpoint
    - Nginx reverse proxy
    - PM2 or Docker deployment
    - Request logging
    - Rate limiting
2. **URL Shortener (v2)**
    - Custom aliases
    - Analytics dashboard
    - Redis caching
    - Dockerized deployment
    - Automated API test script
    - Monitoring endpoint
3. **Mini Incident Lab**
    - Intentionally introduce failures (wrong environment variable, stopped database, occupied port, expired JWT, etc.)
    - Practice diagnosing each issue using only terminal tools.

---

## One Final Piece of Advice

Many developers spend most of their time learning new frameworks.

The developers who become strong backend engineers spend a significant amount of time learning to answer questions like:

- **Why did this fail?**
- **How do I prove my hypothesis?**
- **How do I fix it safely?**
- **How do I make sure it never happens again?**

That mindset will serve you well regardless of whether you're working with Express today or a different backend stack in the future.