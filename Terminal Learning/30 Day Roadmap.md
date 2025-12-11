# Week 1 - Terminal Basics (Build Muscle Memory)

### Day 1-Navigation

Great start! Let's turn your **Day 1 — Navigation** into a full, practical, and fun learning session. I’ll add explanations, examples, mini-tasks, tips, and one small “innovation idea” to make your terminal journey even stronger.

---

## 🌱 **Day 1 — Navigation (Expanded & Beginner-Friendly)**

### ✅ **Goal of the Day**

Learn how to **move confidently inside your file system** using just the terminal.  
This is the base of everything you’ll learn later — scripting, automation, Git, Neovim, servers… all start with navigation.

---

## 🧭 **Commands to Learn (with clear meaning + examples)**

### **1. `pwd` — Where am I right now?**

Shows your **current directory path**.

```bash
pwd
```

Example output:

```
/home/rahul/Documents
```

✨ Tip: If you ever feel lost inside complex folders, `pwd` is your best friend.

---

### **2. `ls` — What is inside this folder?**

Lists files and directories.

```bash
ls
```

Useful flags (learn them slowly):

- `ls -l` → long list
    
- `ls -a` → show hidden files
    
- `ls -la` → detailed + hidden (very common)
    

---

### **3. `cd` — Move into a folder**

Moves you to another directory.

```bash
cd Documents
cd Downloads
```

✨ Remember: folder names are **case-sensitive**.

---

### **4. `cd ..` — Move one step back**

Goes up to the parent directory.

```
cd ..
```

---

### **5. `cd ~` — Go to HOME instantly**

Your fastest way home.

```
cd ~
```

Shortcut:

```
cd
```

(Just typing `cd` with nothing also takes you home.)

---

## 🧪 **Practical Task (Expanded)**

### 🔹 **Task 1: Explore your home folder**

Run:

```bash
pwd
ls
```

Check:

- Can you see Documents, Downloads, Pictures, etc.?
    

---

### 🔹 **Task 2: Move around**

Try these step by step:

```bash
cd Documents
pwd
ls

cd ..
ls

cd Downloads
pwd
ls
```

---

### 🔹 **Task 3: Jump Home**

From anywhere, try:

```bash
cd ~
pwd
```

---

## 🎯 **Mini Challenges for Confidence**

Try these small challenges (they build habits).

### **Challenge A: Where am I?**

Navigate randomly into 2–3 folders, then find your way back home _without using the mouse_.

### **Challenge B: Explore hidden files**

```bash
cd ~
ls -la
```

Check what hidden files exist (like `.bashrc`, `.config`, `.zshrc`).

### **Challenge C: Go deep**

```bash
cd ~/Documents
cd ..
cd ~/Downloads
cd ..
cd ~/.config
cd ..
```

Be comfortable with back-and-forth movement.

---

## 🚀 Innovation Idea of the Day:

**Create a "Path Tracker" alias that shows your current folder beautifully.**

Add this inside your `~/.zshrc`:

```bash
alias whereami='echo "You are in: $(pwd)"'
```

Now try:

```
whereami
```

This builds awareness of your file movements and looks cooler than plain `pwd`.

---

## 🌟 Tomorrow (Day 2) Preview

You’ll learn about:

- `mkdir`
    
- `touch`
    
- `cp`
    
- `mv`
    
- `rm`
    
- directory structure practice
    

You're building a strong foundation already — and one day at a time, you’ll become extremely fluent in terminal workflows.

---

If you'd like, send **Day 2**, and I’ll expand it just like this!

### Day 2-Files & Folders

### Day 3-View Files

### Day 4-Yazi File Explorer

### Day 5-VS Code Terminal + Zsh

### Day 6-btop + System Monitoring

### Day 7-Week 1 Review

# Week 2 - Vim/Neovim + Searching + Git

### Day 8-Vim/Neovim Basics

### Day 9-Vim Movements

### Day 10-Vim Editing

### Day 11-Powerful Searching with ripgrep

### Day 12-LazyGit

### Day 13-TLDR for Fast Learning

### Day 14-Week 2 Review

# Week 3 - Power Tools (fzf, zoxide, piping, processes)

### Day 15-Install fzf

### Day 16-Install zoxide

Day 17-Pipes & Redirection

Day 18-File Permissions

Day 19-Processes

Day 20-Environment Variables

Day 21-Week 3 Review

# Week 4 - Scripting, Automation & Real Ter

Day 22-Shell Scripts Basics

Day 23-Functions in Shell

Day 24-Automate Git

Day 25-Automate Project Setup

Day 26-Dotfiles

Day 27-Cron Jobs (Automation)

Day 28-Networking Basics

Day 29-Optimize Your Zsh

 Day 30-Graduation Day