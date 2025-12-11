Absolutely Rahul — here is your **complete, clean, developer-friendly cheat sheet** of all commands from your 30-Day Terminal Mastery Journey.  
Simple words. Easy scanning. Everything in one place.  
This becomes your **terminal bible**. 🔥

---

# 🌟 **30-Day Terminal Mastery — Full Command Cheat Sheet**

_(Organized by topic for fast recall)_

---

# **📁 Day 1–3: Navigation + Files**

### **Navigation**

```
pwd
ls
ls -la
cd folder
cd ..
cd ~
```

### **Files & Folders**

```
touch file.txt
mkdir folder
rm file.txt
rm -r folder
mv file1 file2
cp file1 file2
```

### **Viewing Files**

```
bat file
bat --style=plain file
```

---

# **📂 Day 4–7: File Managers + Review**

### **Yazi File Explorer**

```
yazi
j/k = up/down
h/l = back/enter
dd = delete
yy = copy
p = paste
```

### **General Review**

Create/move/delete files, open file editors, search.

---

# **📝 Day 8–10: Vim / Neovim**

### **Basics**

```
nvim file
i      (insert mode)
Esc
:w     (save)
:q     (quit)
:wq    (save & quit)
```

### **Navigation**

```
h j k l
gg        (top)
G         (bottom)
/word     (search)
n / N     (next/previous)
```

### **Editing**

```
dd   (delete line)
yy   (copy line)
p    (paste)
x    (delete char)
u    (undo)
```

---

# **🔎 Day 11: Searching (ripgrep)**

```
rg "text"
rg "keyword" -n
rg "text" -t js
rg -l "text"      (list files only)
```

---

# **🌀 Day 12: LazyGit**

```
lazygit
a    (stage)
c    (commit)
p    (push)
b    (branches)
d    (diff)
```

---

# **📘 Day 13: TLDR**

```
tldr tar
tldr grep
tldr find
```

---

# **🧠 Day 14: Week Review**

Search → open → edit → commit → push.

---

# **⚡ Day 15: fzf (Fuzzy Finder)**

```
fzf
nvim $(fzf)
```

---

# **🚀 Day 16: zoxide (Smart cd)**

```
z folder
z foldername
z ..
z ~
zoxide query -l
```

---

# **🔗 Day 17: Pipes & Redirection**

### **Pipes**

```
|
ls | bat
rg "error" | bat
```

### **Redirection**

```
>   (overwrite)
>>  (append)

rg "TODO" > result.txt
echo "line" >> notes.txt
```

---

# **🔐 Day 18: Permissions**

```
chmod +x script.sh
chmod -x script.sh
chmod 777 file
chown user:user file
```

---

# **⚙️ Day 19: Processes**

### Process Info

```
ps
ps aux
ps aux | grep node
```

### Kill Process

```
kill PID
kill -9 PID
```

### Monitoring

```
top
htop
btop
```

---

# **🌍 Day 20: Environment Variables**

```
echo $PATH
export NAME="Rahul"
echo $NAME
```

Add permanent variables in `~/.zshrc`:

```
export VAR="value"
```

---

# **🔁 Day 21: Week Review**

Search → Edit → Commit → Push (terminal only).

---

# **📜 Day 22: Shell Scripts**

Create:

```
#!/bin/bash
echo "Hello!"
```

Run:

```
chmod +x file.sh
./file.sh
```

---

# **🔧 Day 23: Functions in Shell**

```
greet() {
  echo "Hi $1"
}

greet Rahul
```

---

# **📦 Day 24: Git Automation Script**

push.sh:

```
git add .
git commit -m "$1"
git push
```

Run:

```
./push.sh "message"
```

---

# **🏗️ Day 25: Project Setup Script**

Creates folders + installs packages + opens editor.

Commands used:

```
mkdir
npm init -y
npm install
code .
```

---

# **📁 Day 26: Dotfiles**

```
ln -s source target
git add .
git commit -m
git push
```

---

# **⏰ Day 27: Cron Jobs**

Open cron:

```
crontab -e
```

Examples:

```
0 2 * * * cp -r ~/projects ~/backup
0 * * * * echo "log" >> logs.txt
```

---

# **🌐 Day 28: Networking Basics**

```
curl url
curl -I url
wget url
ping google.com
ping -c 4 google.com
ip a
ifconfig
```

---

# **🎨 Day 29: Zsh Optimization**

Plugins:

```
plugins=(git z fzf sudo history web-search)
```

Aliases:

```
alias gs="git status"
alias v="nvim"
alias ..="cd .."
alias cl="clear && ls"
```

---

# **🎓 Day 30: Full Terminal Workflow**

- `z project`
    
- `fzf`
    
- `nvim file`
    
- `rg "text"`
    
- `lazygit`
    
- `npm run dev`
    
- `btop`
    

You're officially a terminal-first developer. 🚀🔥

---

# 🎁 Want this cheat sheet as a **PDF**, **image poster**, or **GitHub README**?

Tell me the format — I’ll generate a clean version for you!