### Goal : Become a terminal first developer
# Day 22-Shell Scripts Basics

Great! Day 22 is where you step into **automation** — shell scripting.  
This is the beginning of doing things _faster_, with fewer mistakes, and in a reusable way.  
Let’s make this day simple, friendly, and powerful.

---

# 🌟 **Day 22 — Shell Script Basics (Expanded Guide)**

## 🎯 **Goal of the Day**

- Create your first shell script
    
- Understand the shebang (`#!/bin/bash`)
    
- Make the script executable
    
- Run it from your terminal
    

This is the foundation of automating tasks like backups, deployments, project setup, etc.

---

# 🧠 **1. Create a simple script**

Inside any folder:

```bash
nvim hello.sh
```

Paste this inside:

```bash
#!/bin/bash
echo "Hello Rahul!"
```

### What this means:

- `#!/bin/bash` → tells Linux which interpreter to use
    
- `echo` → prints text
    

Save:

```
:wq
```

---

# 🔧 **2. Make the script executable**

Right now it's just a file.  
To make it runnable:

```bash
chmod +x hello.sh
```

This adds **execute (x)** permission.

---

# 🚀 **3. Run the script**

Now run it:

```bash
./hello.sh
```

You will see:

```
Hello Rahul!
```

🎉 Congrats — you created a real executable command!

---

# 🧪 **Day 22 Task: Create hello.sh and run it**

You already know the steps:

1. create the file
    
2. add shebang + echo
    
3. save
    
4. chmod +x
    
5. run it
    

Done!

---

# 🎯 Mini Challenges (Fun + Practical)

### **Challenge 1 — Add variables**

Modify your script:

```bash
#!/bin/bash
NAME="Rahul"
echo "Hello $NAME!"
```

Run again.

---

### **Challenge 2 — Accept user input**

Create:

```bash
#!/bin/bash
echo "What is your name?"
read NAME
echo "Hello $NAME!"
```

---

### **Challenge 3 — Show current date**

Add to your script:

```bash
echo "Today is: $(date)"
```

---

### **Challenge 4 — Create a quick project folder**

Make script:

```bash
#!/bin/bash
mkdir -p {src,assets,docs}
echo "Project folders created!"
```

Run it to generate a clean project structure instantly.

---

# 💡 Innovation Idea of the Day

### Put your scripts in ~/bin to run them from anywhere

```bash
mkdir -p ~/bin
mv hello.sh ~/bin/
```

Add to `.zshrc`:

```bash
export PATH="$HOME/bin:$PATH"
```

Reload:

```bash
source ~/.zshrc
```

Now you can run:

```
hello.sh
```

🔥 Just like a real command on your system.

---

# 🚀 You're doing amazing!

Shell scripting unlocks a huge world of automation for you.

Send **Day 23** whenever you’re ready — we keep climbing!

# Day 23-Functions in Shell

Great! Day 23 is where your scripting starts feeling _smart_.  
Shell **functions** let you create your own reusable commands — almost like building mini-programs inside your terminal.

Let’s make this day simple, practical, and fun.

---

# 🌟 **Day 23 — Functions in Shell (Expanded Guide)**

## 🎯 **Goal of the Day**

- Learn how to write a function in your shell
    
- Pass arguments to it
    
- Call it like a real command
    
- Put it inside `.zshrc` so it works everywhere
    

By today, you'll start building your own custom terminal toolkit.

---

# 🧠 **1. Basic Shell Function**

Here’s the example:

```bash
greet() {
  echo "Hi $1"
}
```

This defines a function called **greet**, and `$1` is the first argument.

Call it like:

```bash
greet Rahul
```

Output:

```
Hi Rahul
```

---

# 🔧 **2. Try Inside Your Terminal First**

In your terminal, paste:

```bash
greet() {
  echo "Hi $1"
}
```

Press Enter.

Now run:

```bash
greet Rahul
```

Works immediately!

---

# 🏡 **3. Make It Permanent (Add to .zshrc)**

Open `.zshrc`:

```bash
nvim ~/.zshrc
```

Add the function anywhere:

```bash
greet() {
  echo "Hi $1"
}
```

Save:

```
:wq
```

Reload shell:

```bash
source ~/.zshrc
```

Now you can greet anyone:

```bash
greet Rahul
greet Mom
greet Developer
```

---

# 🧪 **Day 23 Task: Make this function reusable**

You already did it — adding to `.zshrc` makes it work forever.

---

# 🎯 Mini Challenges (Fun & Useful)

### **Challenge 1 — Function with two arguments**

```bash
greet2() {
  echo "Hello $1 $2!"
}
```

Try:

```
greet2 Rahul Kumar
```

---

### **Challenge 2 — Make a function that opens your projects folder**

```bash
proj() {
  cd ~/projects && ls
}
```

Run:

```
proj
```

Instant jump + list.

---

### **Challenge 3 — Create a timestamp function**

```bash
now() {
  echo "Current time: $(date)"
}
```

Try:

```
now
```

---

### **Challenge 4 — File finder function (very powerful)**

```bash
fo() {
  rg -l "$1" | fzf | xargs nvim
}
```

Then run:

```
fo useState
```

Search → select → open.  
One command.

---

# 💡 Innovation Idea of the Day

### Build a tiny “welcome” function that runs each time you open terminal

In `.zshrc`:

```bash
welcome() {
  echo "👋 Welcome Rahul — Terminal ready!"
}

welcome
```

Every new terminal window greets you — feels nice and personal.

---

# 🚀 You're doing amazing!

Shell functions are the first step toward real automation and bigger scripts.

Send **Day 24** whenever you're ready!

# Day 24-Automate Git

Beautiful! Day 24 is where your terminal starts working _for you_.  
Automating Git with a tiny script will save you **hundreds of keystrokes** every month — and it feels amazing to use.

Let’s make today simple, clean, and practical.

---

# 🌟 **Day 24 — Automate Git (Expanded Guide)**

## 🎯 **Goal of the Day**

Create a Git helper script that does:

1️⃣ `git add .`  
2️⃣ `git commit -m "message"`  
3️⃣ `git push`

All in **one single command**.

You’ll be committing faster than ever.

---

# 🧠 Step 1 — Create the Script

Open the file:

```bash
nvim push.sh
```

Add this inside:

```bash
#!/bin/bash
git add .
git commit -m "$1"
git push
```

Save & quit:

```
:wq
```

---

# 🔧 Step 2 — Make It Executable

```bash
chmod +x push.sh
```

Now it becomes a runnable command.

---

# 🚀 Step 3 — Run It

```bash
./push.sh "Day 24: Automated Git script"
```

Output will show:

- files staged
    
- commit success
    
- push to remote
    

This is a huge time saver.

---

# 🧪 **Day 24 Task Completed!**

You now have a personal Git automation tool.

---

# 🎯 Mini Challenges (Fun + Helpful)

### **Challenge 1 — Add date automatically**

Modify your script:

```bash
#!/bin/bash
git add .
git commit -m "$1 — $(date)"
git push
```

Now commit messages include a timestamp.

---

### **Challenge 2 — Make a default commit message if none provided**

```bash
#!/bin/bash
MESSAGE=${1:-"Auto commit"}
git add .
git commit -m "$MESSAGE"
git push
```

Try running without message:

```
./push.sh
```

---

### **Challenge 3 — Add colored output (looks cool)**

```bash
echo -e "\033[32mPushing your changes...🚀\033[0m"
```

---

### **Challenge 4 — Put the script into ~/bin**

So you can run it from ANY folder:

```bash
mkdir -p ~/bin
mv push.sh ~/bin/push
chmod +x ~/bin/push
```

Add to `.zshrc`:

```bash
export PATH="$HOME/bin:$PATH"
```

Reload:

```bash
source ~/.zshrc
```

Now your command becomes:

```
push "message"
```

🔥 Faster. Cleaner. Professional.

---

# 💡 Innovation Idea of the Day

### Add success notification at the end

In the script:

```bash
echo "✅ Git push complete!"
```

It feels satisfying every time.

---

# 🚀 Amazing job, Rahul!

Your terminal workflow is getting ultra-efficient.  
These small automations build into big productivity.

Send **Day 25** whenever you're ready — we’re close to finishing your 30-day journey!

# Day 25-Automate Project Setup

Amazing! Day 25 is where your terminal skills turn into **real-life automation**.  
Today you’ll create a script that sets up a brand-new project in seconds — folders, packages, and even opening it in your editor.

This is the kind of tool that makes you feel _unstoppable_ as a developer.  
Let’s build it step by step in simple language.

---

# 🌟 **Day 25 — Automate Project Setup (Expanded Guide)**

## 🎯 **Goal of the Day**

Write a script that does the following automatically:

1️⃣ Creates a project folder  
2️⃣ Creates subfolders (src, assets, etc.)  
3️⃣ Installs dependencies (Node packages)  
4️⃣ Opens the project in VS Code or Neovim

One command → fresh project ready.

---

# 🧠 Step 1 — Create the Script File

```bash
nvim setup.sh
```

Add this inside:

```bash
#!/bin/bash

# 1. Create project folder
mkdir "$1"
cd "$1"

# 2. Create subfolders
mkdir src assets components

# 3. Initialize node project & install packages
npm init -y
npm install express dotenv

# 4. Create starter files
echo "console.log('Project $1 started');" > src/index.js

# 5. Open project in VS Code
code .
```

Save:

```
:wq
```

---

# 🔧 Step 2 — Make It Executable

```bash
chmod +x setup.sh
```

---

# 🚀 Step 3 — Run It!

```bash
./setup.sh myapp
```

It will:

- make `myapp/`
    
- create `src`, `assets`, `components`
    
- install express + dotenv
    
- generate `index.js`
    
- open VS Code
    

🔥 Clean + fast + professional.

---

# 🧪 **Day 25 Task Completed!**

You built your own project generator — huge productivity win.

---

# 🎯 Mini Challenges (Fun + Very Useful)

### **Challenge 1 — Add Git initialization**

Inside script:

```bash
git init
git add .
git commit -m "Initial commit"
```

---

### **Challenge 2 — Allow user to choose packages**

Ask user:

```bash
echo "Enter packages to install:"
read PKGS
npm install $PKGS
```

---

### **Challenge 3 — Add a README automatically**

```bash
echo "# Project: $1" > README.md
```

---

### **Challenge 4 — Make multiple project types**

Use flags:

```
./setup.sh myapp react
./setup.sh myapi node
```

Inside script:

```bash
if [ "$2" = "react" ]; then
  npm create vite@latest .
fi
```

---

# 💡 Innovation Idea of the Day

### Put the script into `~/bin` and run it like a real command

```bash
mv setup.sh ~/bin/project
chmod +x ~/bin/project
```

Now simply do:

```
project myapp
```

It’s like creating your own CLI tool.  
That’s next-level developer life. 🚀

---

# You're doing amazing, Rahul!

Day 25 shows that you’re not just learning terminal — you’re **building automation that saves real time**.

Send **Day 26** whenever you're ready!

# Day 26-Dotfiles

Love it — Day 26 is one of the most _powerful_ days: dotfiles turn your laptop setup into a repeatable, versioned, shareable system. Do this well and you can set up any new machine in minutes.

I’ll give you two common, reliable ways to manage dotfiles, step-by-step commands, a safe backup strategy, an example bootstrap script you can copy, and a few smart improvements you can add later.

# Day 26 — Dotfiles (Expanded Guide)

## 🎯 Goal

Store your terminal config (like `~/.zshrc`, `~/.config/nvim`, aliases, `~/bin` scripts) in a Git repo on GitHub and install them on any machine with one command.

---

# Option A — Simple & clear: dotfiles repo + symlinks (recommended for most users)

This is easy to understand and flexible.

### 1) Create a repo on GitHub

Create a new repo named `dotfiles` (public or private) on GitHub.

### 2) Locally: prepare a folder for your dotfiles

```bash
mkdir -p ~/dotfiles
cd ~/dotfiles
git init
git remote add origin git@github.com:YOUR_USERNAME/dotfiles.git
```

### 3) Organize files inside `~/dotfiles`

A recommended structure:

```
~/dotfiles
├─ zsh/.zshrc
├─ nvim/init.lua           # or init.vim
├─ nvim/lua/               # plugin + config files
├─ bin/                   # your scripts (executable)
├─ aliases/.aliases       # optional separate file included from .zshrc
├─ README.md
├─ install/bootstrap.sh
```

Put your actual configs (not copies) in these paths. Example: move `~/.zshrc` to `~/dotfiles/zsh/.zshrc`.

### 4) Backup existing dotfiles (always do this)

```bash
mkdir -p ~/.dotfiles_backup
mv ~/.zshrc ~/.dotfiles_backup/ 2>/dev/null || true
mv ~/.config/nvim ~/.dotfiles_backup/ 2>/dev/null || true
mv ~/bin ~/dotfiles_backup/ 2>/dev/null || true
```

### 5) Create symlinks (link real location → repo file)

From your home folder:

```bash
# Zsh
ln -s ~/dotfiles/zsh/.zshrc ~/.zshrc

# Neovim
mkdir -p ~/.config
ln -s ~/dotfiles/nvim ~/.config/nvim

# Scripts
mkdir -p ~/bin
ln -s ~/dotfiles/bin/* ~/bin/   # symlink each script into ~/bin
chmod +x ~/bin/*                 # make executable
```

> If you prefer, symlink each file individually to avoid surprises.

### 6) Commit & push to GitHub

```bash
cd ~/dotfiles
git add .
git commit -m "initial dotfiles"
git push -u origin main
```

### 7) Bootstrap script (one-command install)

Create `~/dotfiles/install/bootstrap.sh`:

```bash
#!/usr/bin/env bash
set -e

DOTFILES="$HOME/dotfiles"
BACKUP="$HOME/.dotfiles_backup"

echo "Backing up current dotfiles to $BACKUP"
mkdir -p "$BACKUP"
mv ~/.zshrc "$BACKUP/" 2>/dev/null || true
mv ~/.config/nvim "$BACKUP/" 2>/dev/null || true
mv ~/bin "$BACKUP/" 2>/dev/null || true

echo "Cloning dotfiles..."
git clone git@github.com:YOUR_USERNAME/dotfiles.git "$DOTFILES"

echo "Creating symlinks..."
ln -sf "$DOTFILES/zsh/.zshrc" ~/.zshrc
mkdir -p ~/.config
ln -sfn "$DOTFILES/nvim" ~/.config/nvim
mkdir -p ~/bin
for f in "$DOTFILES"/bin/*; do
  ln -sf "$f" ~/bin/$(basename "$f")
done
chmod +x ~/bin/*

echo "Reloading shell..."
source ~/.zshrc || true

echo "Done. Dotfiles installed."
```

Make it executable:

```bash
chmod +x ~/dotfiles/install/bootstrap.sh
```

On a new machine you can run:

```bash
git clone git@github.com:YOUR_USERNAME/dotfiles.git ~/dotfiles
~/dotfiles/install/bootstrap.sh
```

Or (if you host public repo) a one-liner:

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/YOUR_USERNAME/dotfiles/main/install/bootstrap.sh)"
```

> **Security note:** only run curl|bash on your own trusted repo.

---

# Option B — Advanced: Bare Git repo (single-folder magic, no symlinks)

This is the “dotfiles as a bare repo” method (used by power users). It avoids symlinks by making `~` itself the working tree.

Quick commands (read before running):

```bash
git clone --bare git@github.com:YOUR_USERNAME/dotfiles.git $HOME/.cfg

# define helper
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'

# checkout
config checkout
# if files conflict, backup and retry:
mkdir -p .config-backup && config checkout 2>&1 | egrep "\s+\." | awk {'print $1'} | xargs -I{} mv {} .config-backup/{}

# hide untracked
config config --local status.showUntrackedFiles no
```

This method is powerful but a bit trickier to understand; use it if you like fewer symlinks and cleaner git status.

---

# Helpful examples (small config snippets)

**Example `zsh/.zshrc` (minimal):**

```bash
export PATH="$HOME/bin:$PATH"
export DOTFILES="$HOME/dotfiles"

# source aliases
[ -f "$DOTFILES/aliases/.aliases" ] && source "$DOTFILES/aliases/.aliases"

# fzf + zoxide init (example)
[ -f /usr/bin/fzf ] && source /usr/share/fzf/key-bindings.zsh 2>/dev/null
eval "$(zoxide init zsh)" 2>/dev/null

# prompt and common aliases
alias gs="git status"
alias lg="lazygit"
```

**Example `bin/push` (move your push.sh here):**

```bash
#!/usr/bin/env bash
MESSAGE=${1:-"Auto commit"}
git add .
git commit -m "$MESSAGE"
git push
```

---

# Mini tasks (do these today)

1. Create `~/dotfiles` and move at least these files into it:
    
    - `zsh/.zshrc` (your current `.zshrc`)
        
    - `nvim/init.lua` or `nvim/init.vim`
        
    - `bin/push` (your Git helper)
        
    - `aliases/.aliases` (optional)
        
2. Add symlinks for each file into its real location.
    
3. Commit & push to GitHub.
    
4. On a different machine (or a new terminal user profile), clone and run your `bootstrap.sh` to verify it works.
    

---

# Mini challenges (improve your setup)

- Add `make` support: a `Makefile` with `make install` that runs the bootstrap.
    
- Use **GNU Stow** to manage groups of dotfiles instead of manual symlinks:
    
    ```bash
    sudo apt install stow
    cd ~/dotfiles
    stow zsh
    stow nvim
    ```
    
- Encrypt secrets: **never** commit API keys to Git. Use environment variables or a secret manager. Use `git-crypt` or `openssl` if you must store something encrypted.
    
- Add `dotbot` or a GitHub Actions workflow to auto-apply dotfiles on push (CI-assisted bootstrap).
    

---

# Innovation idea (next-level)

Add a tiny GitHub Action that runs when you push to `dotfiles` which:

- Lints your `.zshrc` and `init.lua`
    
- Runs a quick `stow --check` or `bash -n` for scripts
    
- Optionally creates a GitHub Release with a snapshot of dotfiles
    

This gives you safe rollbacks and CI checks for your configs.

---

# Quick checklist before finishing

-  Backed up old configs to `~/.dotfiles_backup`
    
-  Repo created on GitHub
    
-  Files moved into `~/dotfiles` and symlinked
    
-  `~/bin` scripts executable and `PATH` updated
    
-  Bootstrap script tested on another machine or a VM
    

---

If you want, I can:

- generate a ready-to-use `bootstrap.sh` tailored to your current dotfiles (paste your `.zshrc` or tell me which files you want included)
    
- or show the exact `git` commands for the bare-repo method step-by-step.
    

Which would you like next?

# Day 27-Cron Jobs (Automation)

Great! Day 27 is all about **Cron Jobs** — your first step into _true automation_.  
Cron lets your computer run tasks **automatically** at fixed times: every minute, every hour, daily, weekly, or on custom schedules.

Once you understand this, your computer starts working _for you_, not the other way around.

Let’s keep this simple, practical, and fun.

---

# 🌟 **Day 27 — Cron Jobs (Automation) — Expanded Guide**

## 🎯 **Goal of the Day**

Learn how to:

- create scheduled jobs
    
- automate backups
    
- automate cleanup
    
- send logs or reminders
    

Everything happens in the background — no need to touch your terminal.

---

# 🧠 **1. Open Crontab (Cron Table)**

Run:

```bash
crontab -e
```

If it asks for an editor, choose **nano** (easy) or **nvim** (if you're comfortable).

This file controls all your scheduled tasks.

---

# ⏱️ **2. Cron Job Format**

Cron jobs follow this pattern:

```
* * * * *  command
| | | | |
| | | | └── day of week (0–6)
| | | └──── month (1–12)
| | └────── day of month (1–31)
| └──────── hour (0–23)
└────────── minute (0–59)
```

Example:

```
0 9 * * * echo "Good morning!" >> ~/logs.txt
```

Runs every day at 9:00 AM.

---

# 🔧 **3. Examples**

### ✔ **Auto Backup (daily)**

Back up a folder every day at 2 AM:

```
0 2 * * * cp -r ~/projects ~/projects-backup
```

---

### ✔ **Auto Cleanup (every week)**

Clean your Downloads folder every Sunday at 7 PM:

```
0 19 * * 0 rm -rf ~/Downloads/*
```

(You can make this safer using a delete script instead.)

---

### ✔ **Send Logs (every hour)**

Append system logs to a file:

```
0 * * * * echo "Log check at $(date)" >> ~/cron-logs.txt
```

---

# 🧪 **Day 27 Task: Create One Automation Job**

Let’s automate something today.

### 👉 Example: Auto-backup your dotfiles every night

1. Open crontab:
    

```bash
crontab -e
```

2. Add this line:
    

```
0 1 * * * cp -r ~/dotfiles ~/dotfiles-backup
```

This creates a backup at **1 AM every day**.

---

# 🎯 Mini Challenges (Fun + Powerful)

### **Challenge 1 — Take a screenshot every hour**

(If you install shutter or flameshot)

```
0 * * * * flameshot full -p ~/screenshots/
```

---

### **Challenge 2 — Make a daily journal entry**

Automatically create a markdown file:

```
0 21 * * * echo "Day summary for $(date)" >> ~/journal/$(date +\%F).md
```

---

### **Challenge 3 — Auto-update your system (weekly)**

```
0 3 * * 1 sudo apt update && sudo apt upgrade -y
```

(Use with caution — updates need trust.)

---

### **Challenge 4 — Clear logs monthly**

```
0 0 1 * * > ~/cron-logs.txt
```

---

# 💡 Innovation Idea of the Day

### Make a script that runs on a schedule

Instead of putting big commands into crontab, create a script:

`~/bin/cleanup.sh`:

```bash
#!/bin/bash
rm -rf ~/Downloads/*
echo "Cleanup done at $(date)" >> ~/.cleanup-log
```

Make it executable:

```bash
chmod +x ~/bin/cleanup.sh
```

Then add this to crontab:

```
0 18 * * * ~/bin/cleanup.sh
```

🔥 Clean system every day at 6 PM, automatically.

---

# 🚀 You're doing amazing, Rahul!

Cron jobs unlock automation at the **system level** — this is real power.

Send **Day 28** whenever you're ready!

# Day 28-Networking Basics

Nice! Day 28 is all about **Networking Basics** — super useful for backend developers, API testing, server debugging, and general system awareness.  
Today you’ll learn simple, everyday commands in a friendly way without going too deep into heavy networking theory.

Let’s keep it clean, simple, and practical — with a few cool ideas as always. 🚀

---

# 🌟 **Day 28 — Networking Basics (Expanded Guide)**

## 🎯 **Goal of the Day**

Learn how to:

- test APIs
    
- download files
    
- check connectivity
    
- view IP info
    
- inspect network interfaces
    

These commands will help you debug servers, deploy apps, check network issues, and test endpoints.

---

# 🔧 **1. curl — The API Tester**

Use `curl` to make HTTP requests right from your terminal.

### ✔ GET request:

```bash
curl https://api.github.com
```

### ✔ GET JSON + pretty print:

```bash
curl https://api.github.com | jq
```

(If `jq` installed)

### ✔ GET with headers:

```bash
curl -I https://google.com
```

### ✔ POST request:

```bash
curl -X POST -d "name=Rahul" https://httpbin.org/post
```

🔥 **curl will become your best friend for backend APIs.**

---

# 📥 **2. wget — Download anything**

### ✔ Download a file:

```bash
wget https://example.com/file.zip
```

### ✔ Download with filename:

```bash
wget -O myfile.zip https://example.com/file.zip
```

### ✔ Resume incomplete downloads:

```bash
wget -c https://example.com/bigfile.iso
```

---

# 🌐 **3. ping — Test connectivity**

Check if a server is reachable.

### ✔ Ping Google:

```bash
ping google.com
```

Stop with:

```
Ctrl + C
```

### ✔ Ping a specific number of times:

```bash
ping -c 4 google.com
```

Useful for checking network issues.

---

# 🧠 **4. ip — View current IP details**

Modern replacement for ifconfig.

### ✔ Show your IP addresses:

```bash
ip a
```

### ✔ Show routing table:

```bash
ip route
```

### ✔ Show active network links:

```bash
ip link
```

---

# 📡 **5. ifconfig — Old but still common**

```bash
ifconfig
```

Shows:

- IP addresses
    
- network interfaces
    
- active connections
    

Still used in many tutorials and scripts.

---

# 🧪 **Practical Task for Day 28**

Try these one by one:

### ✔ Step 1 — Check your internet

```bash
ping -c 3 google.com
```

---

### ✔ Step 2 — Test a public API

```bash
curl https://jsonplaceholder.typicode.com/posts/1
```

---

### ✔ Step 3 — Download a sample file

```bash
wget https://example.com
```

---

### ✔ Step 4 — See your IP details

```bash
ip a
```

---

### ✔ Step 5 — Compare with ifconfig

```bash
ifconfig
```

Done! You’ve learned the essential networking commands.

---

# 🎯 Mini Challenges (Fun + Useful)

### **Challenge 1 — Test your own backend API**

```bash
curl http://localhost:3000/api/status
```

---

### **Challenge 2 — Measure latency**

```bash
ping -c 5 github.com
```

---

### **Challenge 3 — Save API response to a file**

```bash
curl https://api.github.com > github.json
```

Then open with:

```
bat github.json
```

---

### **Challenge 4 — Check default gateway**

```bash
ip route
```

You’ll see which router your machine uses.

---

# 💡 Innovation Idea of the Day

### Create a script that checks your internet health

Make a script:

`~/bin/netcheck.sh`:

```bash
#!/bin/bash
echo "Checking network..."
ping -c 2 google.com >/dev/null && echo "Internet OK!" || echo "No Internet!"
echo "IP info:"
ip a | grep inet
```

Make it executable:

```bash
chmod +x ~/bin/netcheck.sh
```

Run anytime:

```
netcheck.sh
```

Super helpful during debugging.

---

# 🚀 You’re almost at the finish line!

Networking basics are crucial for backend + DevOps + deployment — you just unlocked a big skill.

Send **Day 29** whenever you're ready!

# Day 29-Optimize Your Zsh

Day 29 is FUN because you get to **upgrade your Zsh experience**—make it faster, cleaner, smarter, and more beautiful.  
This is the day your terminal feels truly _yours_.

Let’s keep everything simple, practical, and full of fresh ideas.

---

# 🌟 **Day 29 — Optimize Your Zsh (Expanded Guide)**

## 🎯 **Goal of the Day**

Improve your Zsh setup with:

- useful plugins
    
- theme tweaks
    
- shortcut improvements
    
- organized alias groups
    

By the end of today, your Zsh will look professional and work lightning-fast.

---

# 🔌 **1. Add Useful Oh-My-Zsh Plugins**

Open your `.zshrc`:

```bash
nvim ~/.zshrc
```

Find the line:

```
plugins=(git)
```

Replace it with something richer:

```
plugins=(
  git
  z
  fzf
  sudo
  vscode
  history
  colored-man-pages
  web-search
)
```

### What these do:

- **git** → shortcuts for Git
    
- **z** → smart directory jumping (works with zoxide too)
    
- **fzf** → fuzzy search shortcuts
    
- **sudo** → quickly re-run last command with sudo
    
- **vscode** → open VS Code from terminal
    
- **history** → enhanced history commands
    
- **colored-man-pages** → pretty man pages
    
- **web-search** → search Google directly from terminal
    

Reload:

```bash
source ~/.zshrc
```

---

# 🎨 **2. Theme Tweaks**

If you use Oh-My-Zsh, edit your theme:

```
ZSH_THEME="agnoster"
```

Or try a modern one:

```
ZSH_THEME="robbyrussell"
ZSH_THEME="agnoster"
ZSH_THEME="bira"
ZSH_THEME="avit"
```

### Tip for a clean look:

Disable the right-side prompt:

```
prompt_context=""
```

Or use **powerlevel10k** for professional look:

```bash
git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
```

Then set:

```
ZSH_THEME="powerlevel10k/powerlevel10k"
```

Restart terminal → follow the guided wizard.

---

# ⌨️ **3. Add Smart Shortcuts (Quality-of-Life Improvements)**

Add these inside `.zshrc`:

### ✔ Clear + list

```bash
alias cl="clear && ls"
```

### ✔ Open Neovim fast

```bash
alias v="nvim"
alias vv="nvim ."
```

### ✔ Go home

```bash
alias ..="cd .."
alias ...="cd ../.."
```

### ✔ Fast navigation with zoxide

```bash
alias cd="z"
```

---

# 🗂️ **4. Organize Aliases Into Groups**

Keep your `.zshrc` clean by grouping aliases.

### Example structure:

```bash
# ----------------------
# Navigation Aliases
# ----------------------
alias ..="cd .."
alias ...="cd ../.."
alias dl="cd ~/Downloads"

# ----------------------
# Git Aliases
# ----------------------
alias gs="git status"
alias ga="git add ."
alias gc="git commit -m"
alias gp="git push"

# ----------------------
# Tools
# ----------------------
alias lg="lazygit"
alias bt="btop"
alias y="yazi"
```

Makes your configuration easier to understand.

---

# ⚡ **5. Add Instant Fuzzy File Finder Function**

Inside `.zshrc`:

```bash
f() {
  nvim $(fzf)
}
```

Now type:

```
f
```

→ fuzzy find file  
→ open instantly in Neovim.

---

# 🧪 **Day 29 Task: Optimize your Zsh**

Do these:

1. Add at least **3 new plugins**
    
2. Add or change your **theme**
    
3. Add **5 helpful aliases**
    
4. Organize them under headings
    
5. Add **1 new shortcut or function**
    

Reload:

```bash
source ~/.zshrc
```

Now enjoy:

```
fast navigation
better autocomplete
beautiful prompt
organized workflow
```

---

# 🎯 Mini Challenges (Fun + Useful)

### **Challenge 1 — Add autosuggestions**

Install:

```bash
sudo apt install zsh-autosuggestions
```

Add plugin:

```
plugins+=(zsh-autosuggestions)
```

---

### **Challenge 2 — Highlight your commands**

```bash
sudo apt install zsh-syntax-highlighting
```

Add plugin:

```
plugins+=(zsh-syntax-highlighting)
```

---

### **Challenge 3 — Add a welcome message**

Inside `.zshrc`:

```bash
echo "👋 Welcome Rahul! Ready to build something awesome?"
```

---

### **Challenge 4 — Add a custom path**

```bash
export PATH="$HOME/bin:$PATH"
```

---

# 💡 Innovation Idea of the Day

### Build a “productivity mode” toggle

Inside `.zshrc`:

```bash
focus() {
  clear
  echo "✨ Focus Mode Enabled"
  tmux new-session -A -s focus
}
```

Run:

```
focus
```

→ Opens a clean tmux session for deep work.

---

# 🚀 You’re nearly at the finish line!

Your Zsh is now optimized and feels _professional_.  
One more day and your 30-day terminal journey is complete.

Send **Day 30** whenever you're ready!

# Day 30-Graduation Day


 