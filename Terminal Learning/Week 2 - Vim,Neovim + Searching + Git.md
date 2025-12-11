# Day 8-Vim/Neovim Basics

Great! Day 8 is **Vim/Neovim day** — the moment your terminal skills really level up.  
Vim feels strange at first, but once you understand the basic "modes" and a few commands, it becomes one of the fastest text editors in the world.

Let’s make today simple, friendly, and confidence-boosting.

---

# 🌟 **Day 8 — Vim / Neovim Basics (Expanded Guide)**

## 🎯 **Goal of the Day**

- Learn how to open a file
    
- Enter insert mode
    
- Write text
    
- Save the file
    
- Quit Vim/Neovim
    

Once you master this flow, everything else becomes easier.

---

# 🛠️ 1. Open a File in Neovim

```bash
nvim file.txt
```

Or create a new file:

```bash
nvim notes.md
```

This will open the file inside the terminal.

---

# 🧠 2. Understand Vim Mode System (VERY IMPORTANT)

Vim has **modes**:

### ✔ Normal Mode (default)

- Move around
    
- Give commands
    
- Press keys like `dd`, `yy`, `u`, etc.
    

### ✔ Insert Mode

- Type text normally (like any editor)
    

### ✔ Command Mode

- Save
    
- Quit
    
- Search
    
- Run commands
    

---

# ✍️ 3. Start Typing (Insert Mode)

Press:

```
i
```

Now type anything you like:

```
This is my Day 8 Neovim practice.
Learning Vim feels good!
```

You're in **Insert Mode**.

---

# ⏹ 4. Exit Insert Mode

Press:

```
Esc
```

Always remember this.  
When something feels stuck, press Escape — it resets Vim's state.

---

# 💾 5. Saving the File

Enter command mode by typing `:` (colon).

### Save only:

```
:w
```

### Quit only:

```
:q
```

### Save + Quit:

```
:wq
```

### If Vim refuses to quit (unsaved changes):

```
:q!
```

---

# 🧪 **Main Task: Create & Save a Text File**

Let’s do it step by step.

### Step 1 — Create a file

```bash
nvim my-notes.txt
```

### Step 2 — Enter insert mode

```
i
```

### Step 3 — Write something

```
Day 8 - Vim Basics
Today I learned:
- Insert mode
- Save
- Quit
```

### Step 4 — Exit insert mode

```
Esc
```

### Step 5 — Save and quit

```
:wq
```

You've officially used Vim. 🎉

---

# 🎯 Mini Challenges (Fun & Quick)

### **Challenge 1 — Create another file**

```bash
nvim todo.txt
```

Write 3 tasks → save → quit.

---

### **Challenge 2 — Edit an existing file**

Open a file → add one more line → save.

---

### **Challenge 3 — Try quitting without saving**

Open a file:

```bash
nvim temp.txt
```

Type anything, then quit without saving:

```
:q!
```

This builds confidence.

---

# 💡 Innovation Idea of the Day

Add a shortcut alias to open the last edited file:

In `~/.zshrc`:

```bash
alias v="nvim ."
```

Or:

```bash
alias e="nvim"
```

Now you can do:

```
e notes.txt
```

Short. Sweet. Fast.

---



# Day 9-Vim Movements



# Day 10-Vim Editing

# Day 11-Powerful Searching with ripgrep

# Day 12-LazyGit

# Day 13-TLDR for Fast Learning

# Day 14-Week 2 Review