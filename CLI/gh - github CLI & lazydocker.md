Since you're using **Linux Mint** and already have a terminal-first workflow (Kitty + Zsh + Neovim + LazyGit), **GitHub CLI (`gh`)** will fit perfectly.

---

# What is GitHub CLI (`gh`)?

`gh` is the **official command-line tool from GitHub**.

Instead of opening GitHub in your browser, you can:

- Create repositories
- Clone repositories
- Create Pull Requests
- Review Pull Requests
- Create Issues
- View GitHub Actions
- Manage Releases
- Manage Gists
- Browse repositories

Think of it as:

```
Git  → manages your local repository
GitHub → hosts your repository online

gh = GitHub from your terminal
```

---

# Install on Linux Mint

## Method 1 (Recommended)

```bash
(type -p wget >/dev/null || (sudo apt update && sudo apt install wget -y)) \
&& sudo mkdir -p -m 755 /etc/apt/keyrings \
&& wget -qO- <https://cli.github.com/packages/githubcli-archive-keyring.gpg> \
| sudo tee /etc/apt/keyrings/githubcli-archive-keyring.gpg >/dev/null \
&& sudo chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg \
&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] <https://cli.github.com/packages> stable main" \
| sudo tee /etc/apt/sources.list.d/github-cli.list >/dev/null \
&& sudo apt update \
&& sudo apt install gh -y
```

---

## Verify installation

```bash
gh --version
```

Example:

```
gh version 2.xx.x
<https://github.com/cli/cli/releases/latest>
```

---

# Login to GitHub

Run:

```bash
gh auth login
```

You'll be asked a few questions.

### 1.

```
What account do you want to log into?
```

Choose

```
GitHub.com
```

---

### 2.

```
Preferred protocol?
```

Choose

```
SSH
```

Since you're a developer, SSH is the better long-term option.

---

### 3.

```
Authenticate Git with your credentials?
```

Choose

```
Yes
```

---

### 4.

```
How would you like to authenticate?
```

Choose

```
Login with a web browser
```

It will display something like:

```
First copy your one-time code:

ABCD-1234

Press Enter to open github.com...
```

Open the browser.

Enter the code.

Authorize.

Done.

---

Verify:

```bash
gh auth status
```

Example:

```
✓ Logged in to github.com

✓ Git operations configured

✓ Token is valid
```

---

# Essential Commands

---

## 1. Check login

```bash
gh auth status
```

---

## 2. Logout

```bash
gh auth logout
```

---

## 3. Clone repository

Instead of

```bash
git clone <https://github.com/facebook/react.git>
```

use

```bash
gh repo clone facebook/react
```

---

## 4. Create repository

Inside your project:

```bash
gh repo create
```

It asks:

```
Repository name?

Public or Private?

Push existing code?
```

After answering, it creates the repository and pushes your code if you choose.

---

## 5. Open repository in browser

```bash
gh repo view --web
```

No need to manually navigate.

---

## 6. View repository information

```bash
gh repo view
```

Example:

```
Stars

Forks

Description

README
```

---

## 7. List your repositories

```bash
gh repo list
```

Example:

```
Todo-App

StudyNotion

Portfolio

URL-Shortener
```

---

# Pull Requests

This is where `gh` really shines.

---

## List PRs

```bash
gh pr list
```

---

## Create PR

```bash
gh pr create
```

You'll be asked for:

```
Title

Description

Base branch

Target branch
```

Done.

---

## View PR

```bash
gh pr view
```

---

## Checkout someone else's PR

```bash
gh pr checkout 15
```

Great for code reviews.

---

## Merge PR

```bash
gh pr merge
```

---

# Issues

Create issue

```bash
gh issue create
```

List issues

```bash
gh issue list
```

View issue

```bash
gh issue view 12
```

Close issue

```bash
gh issue close 12
```

---

# GitHub Actions (CI/CD)

List workflows

```bash
gh workflow list
```

Run workflow

```bash
gh workflow run CI
```

Watch workflow

```bash
gh run watch
```

List runs

```bash
gh run list
```

View failed logs

```bash
gh run view
```

---

# Releases

List releases

```bash
gh release list
```

Create release

```bash
gh release create v1.0
```

Download release

```bash
gh release download
```

---

# Gists

Create gist

```bash
gh gist create notes.md
```

List gists

```bash
gh gist list
```

---

# Search GitHub

Repositories

```bash
gh search repos express
```

Issues

```bash
gh search issues bug
```

Pull Requests

```bash
gh search prs authentication
```

---

# Real MERN Workflow

Imagine you've finished a new authentication feature.

### 1. Check your changes

```bash
lazygit
```

Stage, commit, and push.

---

### 2. Create a Pull Request

```bash
gh pr create
```

---

### 3. Watch your CI

```bash
gh run watch
```

If your tests fail, fix the issue, commit, and push again.

---

### 4. Merge

```bash
gh pr merge
```

Everything without leaving the terminal.

---

# Useful Aliases

Add these to your `~/.zshrc`:

```bash
alias ghrepo='gh repo view --web'
alias ghprs='gh pr list'
alias ghpr='gh pr create'
alias ghruns='gh run list'
alias ghwatch='gh run watch'
alias ghissues='gh issue list'
alias ghclone='gh repo clone'
```

Reload:

```bash
source ~/.zshrc
```

---

# Beginner Learning Order

I recommend learning `gh` in this order:

1. ✅ `gh auth login`
2. ✅ `gh repo create`
3. ✅ `gh repo clone`
4. ✅ `gh repo view`
5. ✅ `gh pr create`
6. ✅ `gh pr list`
7. ✅ `gh pr merge`
8. ✅ `gh issue create`
9. ✅ `gh run watch`
10. ✅ `gh release create`

---

# My Recommendation for You

Considering you're building MERN projects, contributing to open source, and using Linux as your primary development environment, this combination is excellent:

- 📝 **Neovim** → Write code
- 🌿 **LazyGit** → Manage local Git commits, branches, staging, and merges
- 🐙 **GitHub CLI (`gh`)** → Interact with GitHub (repositories, pull requests, issues, actions)
- 🐳 **LazyDocker** → Manage Docker containers
- 🔍 **ripgrep + fd + fzf** → Navigate and search code quickly

These tools complement each other rather than replace one another, and they're widely used by developers who prefer working from the terminal.

This is one of the most common questions, and many developers think they overlap. They actually solve **different problems** and work great together.

Here's the simplest way to think about them:

> **LazyGit = Manage your local Git repository**
> 
> **GitHub CLI (`gh`) = Manage your GitHub account and repositories**

---

# Quick Comparison

|Feature|LazyGit|GitHub CLI (`gh`)|
|---|---|---|
|Local Git operations|✅ Excellent|✅ Basic|
|Push/Pull|✅|✅|
|Commit|✅|✅|
|Interactive staging|⭐⭐⭐⭐⭐|❌|
|Resolve merge conflicts|⭐⭐⭐⭐⭐|❌|
|Browse Git history|⭐⭐⭐⭐⭐|❌|
|Create Pull Request|❌|⭐⭐⭐⭐⭐|
|Review Pull Requests|❌|⭐⭐⭐⭐⭐|
|Create Issues|❌|⭐⭐⭐⭐⭐|
|GitHub Actions|❌|⭐⭐⭐⭐⭐|
|Releases|❌|⭐⭐⭐⭐⭐|
|Clone GitHub repos|❌|⭐⭐⭐⭐⭐|

---

# What LazyGit is for

Think of LazyGit as a beautiful interface for commands like:

```bash
git add
git commit
git checkout
git branch
git stash
git rebase
git merge
git diff
git log
```

Instead of remembering dozens of Git commands, you press keys.

For example:

```
Status

Modified:
 app.js
 server.js
 auth.js
```

Press:

```
Space
```

Stage file.

Press

```
c
```

Commit.

Press

```
P
```

Push.

Done.

---

## Things I use LazyGit for every day

### View changed files

```
git status
```

becomes

```
lazygit
```

---

### Stage selected lines

You can stage only part of a file.

Very useful.

---

### View beautiful diff

```
Old line
New line
```

without typing

```
git diff
```

---

### Switch branches

Instead of

```bash
git checkout feature/login
```

Press

```
b
```

Choose branch.

Done.

---

### Resolve merge conflicts

One of LazyGit's strongest features.

---

# What GitHub CLI (`gh`) is for

Now imagine your code is already on GitHub.

You want to:

- Create Pull Request
- Review Pull Request
- Create Issue
- Download Release
- Clone repository
- Manage GitHub Actions
- Open repository in browser

This is what `gh` does.

---

## Example 1

Clone repository

Instead of

```bash
git clone <https://github.com/facebook/react.git>
```

You can do

```bash
gh repo clone facebook/react
```

---

## Example 2

Create repository

Instead of

1. Open browser
2. Login
3. Click New Repository
4. Fill form

Just

```bash
gh repo create
```

---

## Example 3

Create Pull Request

Instead of opening GitHub website

```bash
gh pr create
```

You'll be prompted for:

```
Title
Description
Base branch
Target branch
```

PR created.

---

## Example 4

See your Pull Requests

```bash
gh pr list
```

Example output

```
#41 Fix login

#42 Add analytics

#43 Update README
```

---

## Example 5

Check CI/CD

```bash
gh run list
```

See

```
✓ Tests Passed

✓ Build Passed

✗ Deploy Failed
```

---

## Example 6

Create Issue

```bash
gh issue create
```

---

## Example 7

Review PR

```bash
gh pr checkout 17
```

Now you're reviewing someone else's code.

---

## Example 8

Watch Actions logs

```bash
gh run watch
```

No browser.

---

# Real MERN Workflow

Imagine you're working on your Todo App.

### During coding

```
nvim
```

↓

```
npm run dev
```

↓

```
lazygit
```

↓

Commit

↓

Push

---

Now the code is on GitHub.

You need to:

```
Create PR
```

↓

```
gh pr create
```

Reviewer comments

↓

```
gh pr view
```

Fix code

↓

```
lazygit
```

Commit

↓

```
gh pr checks
```

CI Passed

↓

Merge.

---

# They work together

Most professional developers use both.

```
Code
     │
     ▼
 Neovim
     │
     ▼
 LazyGit
     │
 Commit
 Push
     │
     ▼
 GitHub
     │
     ▼
    gh
(PRs, Issues, Actions, Releases)
```

---

# For your learning path

Since you're aiming for backend development with the MERN stack, here's what I'd prioritize:

### Install immediately ⭐⭐⭐⭐⭐

- ✅ `gh` (GitHub CLI)
- ✅ `lazygit` (already installed)
- ✅ `git-delta` (already installed)

This combination covers almost everything you'll do with Git and GitHub.

### Learn after Docker ⭐⭐⭐⭐☆

- `lazydocker` — similar experience to LazyGit, but for managing Docker containers, images, volumes, and networks from the terminal.

Once you start containerizing your Node.js applications, you'll likely find `lazydocker` just as useful as `lazygit` is for Git.

If **LazyGit** is the best terminal UI for Git, then **LazyDocker** is the equivalent for Docker.

> **Docker CLI** → Powerful but lots of commands to remember.
> 
> **LazyDocker** → A fast, keyboard-driven interface for managing Docker visually in your terminal.

Since you're planning to become a backend developer, Docker will eventually become part of your daily workflow.

---

# What is LazyDocker?

LazyDocker is a terminal UI that lets you manage:

- 🐳 Containers
- 📦 Images
- 💾 Volumes
- 🌐 Networks
- 📜 Logs
- 📊 Resource usage
- ⚙️ Docker Compose projects

without remembering dozens of Docker commands.

---

# Installation

### Option 1 (Recommended)

```bash
curl <https://raw.githubusercontent.com/jesseduffield/lazydocker/master/scripts/install_update_linux.sh> | bash
```

Move it to your PATH:

```bash
sudo mv ~/.local/bin/lazydocker /usr/local/bin/
```

Verify:

```bash
lazydocker --version
```

---

### Option 2 (Go)

```bash
go install github.com/jesseduffield/lazydocker@latest
```

---

# Start it

Simply run:

```bash
lazydocker
```

You'll see something similar to:

```
Containers
─────────────────────────────

✔ mongo
✔ backend
✔ redis

Images
Volumes
Networks
Logs
```

Everything is keyboard-driven.

---

# Interface Overview

```
+----------------------------------------------------+
| Containers | Images | Volumes | Networks | Events |
+----------------------------------------------------+

backend
mongo
redis

------------------------------------------

Container Logs

Server started...

Mongo Connected...

Listening on port 5000...
```

---

# Scenario 1 — MERN Stack

Imagine your project uses:

```
React
Node
MongoDB
Redis
```

Normally you'd run:

```bash
docker ps
docker logs backend
docker exec -it mongo bash
docker stop redis
docker restart backend
docker stats
```

That's a lot of commands.

With LazyDocker:

```
lazydocker
```

Arrow keys.

Done.

---

# Scenario 2 — View Logs

Instead of:

```bash
docker logs -f backend
```

Open:

```
backend
```

Press

```
l
```

Instant logs.

```
Connected to Mongo

Listening on port 5000

GET /users

POST /login
```

---

# Scenario 3 — Restart Container

Normally

```bash
docker restart backend
```

LazyDocker

```
Select backend

Press r
```

Done.

---

# Scenario 4 — Stop Container

Normally

```bash
docker stop mongo
```

LazyDocker

```
Select mongo

Press s
```

Done.

---

# Scenario 5 — Open Shell

Normally

```bash
docker exec -it backend bash
```

LazyDocker

Select container

Press

```
e
```

You're inside the container.

---

# Scenario 6 — Delete Image

Instead of

```bash
docker image rm imageID
```

Press

```
x
```

Confirm.

Done.

---

# Scenario 7 — Watch CPU & RAM

Normally

```bash
docker stats
```

LazyDocker shows live usage:

```
backend

CPU 4%

RAM 212MB

Network

2MB/s
```

---

# Scenario 8 — Docker Compose

Run

```bash
docker compose up
```

Then open

```bash
lazydocker
```

You immediately see:

```
backend

mongo

redis

nginx
```

If one crashes:

```
Exited (1)
```

You notice it instantly.

---

# Scenario 9 — Debugging

Your Express app keeps restarting.

Instead of:

```bash
docker ps
docker logs
docker inspect
docker stats
```

LazyDocker shows:

```
Logs

CPU

Restart Count

Exit Code

Status
```

in one place.

---

# Scenario 10 — Clean Up

You'll eventually accumulate lots of unused resources:

- Images
- Volumes
- Networks
- Containers

LazyDocker lets you browse and remove them interactively instead of memorizing cleanup commands.

---

# Most Useful Keyboard Shortcuts

|Key|Action|
|---|---|
|↑ ↓|Move|
|Enter|Open details|
|Tab|Switch panels|
|`l`|View logs|
|`e`|Open shell inside container|
|`r`|Restart container|
|`s`|Stop container|
|`x`|Remove selected item|
|`d`|Show detailed information|
|`?`|Help|
|`q`|Quit|

---

# Example: Todo App with Docker

Suppose you have:

```
todo-app/
├── backend/
├── frontend/
├── docker-compose.yml
└── mongo/
```

Start everything:

```bash
docker compose up -d
```

Open LazyDocker:

```bash
lazydocker
```

You might see:

```
✓ backend

✓ frontend

✓ mongodb
```

Need backend logs?

```
backend

↓

l
```

Need a MongoDB shell?

```
mongodb

↓

e
```

Need to restart only the backend?

```
backend

↓

r
```

No terminal commands required.

---

# LazyDocker vs Docker CLI

|Task|Docker CLI|LazyDocker|
|---|---|---|
|List containers|`docker ps`|Built in|
|View logs|`docker logs -f`|`l`|
|Restart|`docker restart`|`r`|
|Stop|`docker stop`|`s`|
|Open shell|`docker exec -it`|`e`|
|Stats|`docker stats`|Live panel|
|Remove image|`docker image rm`|`x`|
|Browse volumes|Multiple commands|Built in|

---

# When should you learn it?

For your current stage, I'd suggest this order:

1. ✅ Linux terminal basics
2. ✅ Git + LazyGit
3. ✅ Neovim
4. ✅ Docker fundamentals (images, containers, volumes, networks, Docker Compose)
5. ⭐ Learn **LazyDocker**
6. Kubernetes (later)

The key is to understand **Docker concepts first**. Once you know what containers, images, volumes, and networks are, LazyDocker becomes a productivity tool rather than something that hides how Docker works.

Given your goal of becoming a strong MERN backend developer, Docker and Docker Compose are among the highest-value skills to add next. After you're comfortable with those, LazyDocker will make day-to-day development much smoother.