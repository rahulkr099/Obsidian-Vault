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

Perfect! Day 9 is when Vim finally starts feeling _fun_.  
Today you learn to **move like lightning** inside files — without touching the mouse or arrow keys.  
This is the “superpower day” of your Vim journey.

Let’s break everything into simple, friendly steps.

---

# 🌟 **Day 9 — Vim Movements (Expanded Guide)**

## 🎯 **Goal of the Day**

Move around a file **fast** using:

- hjkl navigation
    
- jumping to top/bottom
    
- searching inside a file
    

By the end of today, your fingers will instinctively move around text.

---

# 🧭 **1. Basic Movement Keys: h j k l**

These are your arrow keys inside Vim.

```
h  → left  
j  → down  
k  → up  
l  → right
```

Tip: Rest your hand on the home row. This is the secret behind Vim’s speed.

---

# 🚀 **2. Jump to Top & Bottom**

### Go to the **top** of the file:

```
gg
```

### Go to the **bottom**:

```
G
```

Try this inside a large file and feel the instant jump.

---

# 🔍 **3. Searching Inside the File**

Type:

```
/word
```

Example:

```
/function
/debug
/hello
```

Then:

- Press **n** → go to next match
    
- Press **N** → go to previous match
    

This is one of your most powerful Vim tools.

---

# 🧪 **Main Task: Move Around a File Without Mouse**

Let’s use everything in one flow.

### Step 1 — Open any file

```bash
nvim app.js
```

(or any code/text file)

---

### Step 2 — Practice hjkl movement

Move:

- 10 lines down (jjjjjjjjjj)
    
- 10 lines up
    
- random left/right navigation
    

Feel the rhythm.

---

### Step 3 — Jump instantly

Try:

```
gg   → top  
G    → bottom  
10G  → go to line 10
```

Pro tip:  
You can also type a number before j/k:

```
20j  → jump 20 lines down  
15k  → jump 15 lines up
```

---

### Step 4 — Search everywhere

Try searching for something common:

```
/const
```

Press:

```
n  (next)
n  
n  
```

Then press N to go backwards.

---

# 🎯 Mini Challenges (Quick & Fun)

### **Challenge 1 — Line Navigation Drill**

Inside any file:

- go to top
    
- go to bottom
    
- jump to line 25
    
- jump back to line 1
    

---

### **Challenge 2 — Search & Inspect**

Search for a keyword like:

```
/import
```

Visit every match using **n**.

---

### **Challenge 3 — Smooth Movement**

Open a long text file (logs, README, codebase) and navigate ONLY using:

- h j k l
    
- gg
    
- G
    
- /search
    

No arrow keys. No mouse.

---

# 💡 Innovation Idea of the Day

### Enable cursor line for easier movement

Add this to your `init.lua` or `.vimrc`:

```lua
vim.opt.cursorline = true
```

This highlights your current line → lovely for beginners.

---

# 🌈 Bonus Tip: Turn on relative line numbers

They help movement become super intuitive.

Add:

```lua
vim.opt.relativenumber = true
```

Then you can do:

```
15j
7k
```

Because you always see distance from the current line.

---

# 🚀 You’re becoming powerful in Vim now.

Day 10 will build on this and introduce editing, deleting, copying, pasting — the real _editing power_ of Vim.

Send **Day 10** whenever you're ready — I’ll expand it fully!

# Day 10-Vim Editing

Great! Day 10 is the day Vim starts feeling like a **real editor**, not just a viewer.  
Today you’ll learn how to delete, copy, paste, undo — all using pure keyboard magic.  
These are the moves you’ll use every single day as a developer.

Let’s keep everything simple and fun.

---

# 🌟 **Day 10 — Vim Editing (Expanded Guide)**

## 🎯 **Goal of the Day**

Edit a file completely using:

- delete
    
- copy
    
- paste
    
- undo
    
- single-character delete
    

By the end of today, you’ll be able to refactor text quickly and cleanly inside Neovim.

---

# ✂️ 1. **dd — Delete a Line**

Deletes the whole line your cursor is on.

```
dd
```

You can also delete multiple lines:

```
3dd   → delete 3 lines
10dd  → delete 10 lines
```

---

# 📋 2. **yy — Copy (Yank) a Line**

Yanks (copies) the current line:

```
yy
```

Copy multiple lines:

```
5yy  → copy 5 lines
```

---

# 📥 3. **p — Paste Below**

Paste the copied or deleted text **below** the cursor:

```
p
```

To paste _above_ the cursor:

```
P
```

---

# ❌ 4. **x — Delete a Single Character**

Deletes the character under your cursor:

```
x
```

This is perfect for fixing typos quickly.

---

# ↩️ 5. **u — Undo**

Undo the last change:

```
u
```

Redo (opposite of undo):

```
Ctrl + r
```

Undo is your safety net — use it freely.

---

# 🧪 **Main Task: Edit a File Completely Inside Neovim**

Let’s walk through a full editing flow.

### Step 1 — Create or open a file:

```bash
nvim practice.txt
```

---

### Step 2 — Enter Insert Mode & Add Text

Press:

```
i
```

Write something like:

```
Hello! This is my Day 10 Vim practice.
I am learning editing commands.
This line has a mistakeeeeee.
I will try deleting, copying, pasting, undoing.
```

---

### Step 3 — Exit Insert Mode

```
Esc
```

---

### Step 4 — Fix mistakes using today’s commands

#### ✔ Delete the line with mistake:

```
dd
```

#### ✔ Copy the first line:

```
yy
```

#### ✔ Paste it at the bottom:

```
p
```

#### ✔ Delete a few characters using x

Move to a random word and press `x` multiple times.

#### ✔ Undo your changes:

```
u
```

#### ✔ Redo them:

```
Ctrl + r
```

---

### Step 5 — Save & Quit

```
:wq
```

You’ve now _properly edited a file in Vim_ — a real skill.

---

# 🎯 Mini Challenges (Fun & Fast)

### **Challenge 1 — Delete multiple lines**

Open any file and delete 5 lines using:

```
5dd
```

---

### **Challenge 2 — Duplicate a line**

Copy a line with:

```
yy
```

Paste twice:

```
p
p
```

---

### **Challenge 3 — Fix a typo**

Find a wrong character → delete it with `x` → type the correct one.

---

### **Challenge 4 — Undo everything**

Press:

```
u u u u u
```

Then redo:

```
Ctrl + r
```

---

# 💡 Innovation Idea of the Day

### Enable persistent undo in Neovim

This makes undo work even after closing and reopening files.

Add to `init.lua`:

```lua
vim.opt.undofile = true
```

Now Vim remembers your entire editing history — super useful for coding.

---

# 🚀 You're halfway to being comfortable in Vim.

Tomorrow we’ll learn even more powerful editing tricks:  
motions, operators, visual mode, and smarter text manipulation.

Send **Day 11** whenever you're ready — we’ll keep building the momentum!

# Day 11-Powerful Searching with ripgrep

Awesome! Day 11 jumps into **ripgrep (rg)** — one of the FASTEST search tools you’ll ever use.  
This is a real developer superpower, especially in MERN projects where you need to find functions, hooks, components, or bugs inside large folders.

Let’s make searching feel effortless today.

---

# 🌟 **Day 11 — Powerful Searching with ripgrep (Expanded Guide)**

## 🎯 **Goal of the Day**

Learn to search:

- inside folders
    
- inside entire projects
    
- by file type
    
- with line numbers
    
- with speed
    

ripgrep is insanely fast — you’ll feel the difference immediately.

---

# 📚 **Commands to Learn**

---

## 🔎 **1. Basic Search**

```
rg "function"
```

Searches for the word **function** in all files under the current directory.

---

## 🔢 **2. Search with Line Numbers**

```
rg "keyword" -n
```

`-n` shows the exact line number where the match is found.  
Very useful when jumping into files.

---

## 🎯 **3. Search Only in JavaScript Files**

```
rg "text" -t js
```

`-t js` filters strictly to `.js` files  
(You can also use `-t ts`, `-t jsx`, etc.)

---

# 🚀 Bonus Flags (Learn Them Slowly)

Not required today, but useful:

```
-i   → case insensitive  
-w   → match whole word  
-c   → show count  
```

---

# 🧪 **Main Task: Search for all instances of useState inside a project**

Let’s assume you're inside your React project folder.

### Step 1 — Navigate to the project

```bash
cd my-react-app
```

---

### Step 2 — Search for useState everywhere

```bash
rg "useState"
```

This will show:

- file paths
    
- matching lines
    
- highlighted text
    

---

### Step 3 — Add line numbers (recommended)

```bash
rg "useState" -n
```

Now you’ll see something like:

```
src/App.jsx:10: const [count, setCount] = useState(0);
src/components/Header.jsx:4: const [open, setOpen] = useState(false);
```

Easy to jump into files using Neovim:

```bash
nvim src/App.jsx +10
```

---

### Step 4 — Search only inside JS/JSX files

```bash
rg "useState" -t js -t jsx
```

This avoids searching in JSON, CSS, or build folders.

---

# 🎯 Mini Challenges (Fun + Practical)

### **Challenge 1 — Find all imports**

```
rg "import"
```

---

### **Challenge 2 — Find all console logs**

```
rg "console.log"
```

Clean them before deployment 😄

---

### **Challenge 3 — Find every route**

```
rg "Route" -t jsx
```

---

### **Challenge 4 — Case-insensitive search**

```
rg "usestAte" -i
```

---

# 💡 Innovation Idea of the Day

### Create an alias to search faster

Add this to `~/.zshrc`:

```bash
alias rgi='rg -n -i'
```

Now you can do:

```
rgi "useState"
```

Quick, clean, and powerful.

---

# 🚀 Ready for Day 12?

You handled ripgrep like a pro — searching codebases will feel 10× easier now.

Send **Day 12** whenever you’re ready!

# Day 12-LazyGit

Nice! Day 12 is super exciting because **LazyGit** makes Git feel smooth, visual, and fast — without leaving the terminal.  
Today you’ll learn to stage, commit, push, and switch branches with easy keyboard shortcuts.

Let’s make this day simple and confidence-boosting.

---

# 🌟 **Day 12 — LazyGit (Expanded Guide)**

## 🎯 **Goal of the Day**

Use LazyGit to:

- stage changes
    
- write a commit
    
- push to GitHub
    
- switch branches
    

Everything inside the terminal — no VS Code, no Git CLI needed today.

---

# 🛠️ 1. Open LazyGit

Inside a Git project folder:

```bash
lazygit
```

You’ll see panels for:

- files changed
    
- commits
    
- branches
    
- stash
    
- logs
    

It looks clean and animated. Perfect for everyday work.

---

# 🎮 **2. Basic LazyGit Controls (Must Know)**

LazyGit uses simple hotkeys.  
These will quickly become muscle memory.

---

## 🟦 **A → Stage / Unstage Files**

Press:

```
a
```

This stages all changes (same as `git add .`).

To stage single file:

- Move with ↑/↓ keys
    
- Press `a`
    

---

## 🟩 **c → Commit**

After staging:

```
c
```

Type your commit message → press **Enter** to confirm.

---

## 🟨 **p → Push**

Push your commit to GitHub:

```
p
```

LazyGit will show push progress at the bottom.

---

## 🟫 **Branch Switching**

Press:

```
b
```

Or:

```
← →  arrows
```

You’ll see:

- list of branches
    
- option to checkout
    
- option to create new branch
    

Press **Enter** to switch to the highlighted branch.

---

# 🧪 **Main Task: Make a Commit Using LazyGit Only**

Here’s your complete flow:

---

### ✔ Step 1 — Make some changes in your project

Edit any file:

```bash
nvim src/app.js
```

Add one small line like:

```js
console.log("Day 12 LazyGit practice");
```

Save & quit.

---

### ✔ Step 2 — Open LazyGit

```bash
lazygit
```

---

### ✔ Step 3 — Stage changes

Highlight the file → press:

```
a
```

Or press **A** (capital A) to stage everything.

---

### ✔ Step 4 — Commit

Press:

```
c
```

A box opens — type your message:

```
Day 12: Practicing LazyGit commit
```

Press **Enter** to confirm.

---

### ✔ Step 5 — Push the commit

Press:

```
p
```

LazyGit will push to your current branch.

---

✨ **You just made a full commit using LazyGit only!**  
This is the workflow many developers use daily.

---

# 🎯 Mini-Challenges (Fast + Fun)

### **Challenge 1 — Create a new branch**

Inside LazyGit:

```
b → n
```

Name it:

```
feature/day12-test
```

---

### **Challenge 2 — Checkout a branch**

Highlight a branch → press **Enter**.

---

### **Challenge 3 — Stage only ONE file**

Modify 2 files, but stage only one using `a` on the selected file.

---

### **Challenge 4 — Open file diff quickly**

Press:

```
Enter
```

on any changed file to see its diff.

This is extremely helpful when reviewing changes.

---

# 💡 Innovation Idea of the Day

### Add a hotkey in Zsh to open LazyGit instantly from anywhere:

In your `~/.zshrc`:

```bash
alias lg="lazygit"
```

Reload:

```bash
source ~/.zshrc
```

Now just type:

```
lg
```

It becomes part of your natural workflow.

---

# 🚀 Great progress!

LazyGit is one of the biggest productivity boosts in your terminal journey.

Send **Day 13** whenever you're ready — we’ll keep building this momentum!

# Day 13-TLDR for Fast Learning

Nice! Day 13 is all about **learning faster** using TLDR — one of the most underrated tools in the terminal world.  
Instead of reading long, confusing man pages, TLDR gives you **simple examples**, exactly what you need as a developer.

Let’s make today super productive and fun.

---

# 🌟 **Day 13 — TLDR for Fast Learning (Expanded Guide)**

## 🎯 **Goal of the Day**

Use TLDR to:

- learn new commands quickly
    
- understand real examples
    
- discover everyday useful utilities
    

Today you'll practice with **tar**, **grep**, and **find** — three commands you’ll use for the rest of your programming life.

---

# 🧠 **1. Using TLDR**

Just run:

```bash
tldr tar
tldr grep
tldr find
```

TLDR will show:

- simple descriptions
    
- a list of common use cases
    
- examples you can copy immediately
    

You’ll understand more from TLDR in 10 seconds than man pages in 10 minutes.

---

# 📚 **Command 1 — tar (Archiving & Compressing)**

Use TLDR:

```bash
tldr tar
```

Most useful examples:

### Create a tar archive:

```bash
tar -cvf files.tar folder/
```

### Extract a tar archive:

```bash
tar -xvf files.tar
```

### Extract a .tar.gz:

```bash
tar -xvzf archive.tar.gz
```

You’ll use this whenever downloading open-source tools, Node binaries, or libraries.

---

# 🔍 **Command 2 — grep (Search inside text)**

Use TLDR:

```bash
tldr grep
```

Everyday examples:

### Search for a word in a file:

```bash
grep "error" logs.txt
```

### Search recursively in folders:

```bash
grep -R "import" src/
```

### Case-insensitive search:

```bash
grep -i "react"
```

ripgrep is faster, but grep is universal and always installed.

---

# 🔎 **Command 3 — find (Search for files/folders)**

Use TLDR:

```bash
tldr find
```

Important examples:

### Find all .js files:

```bash
find . -name "*.js"
```

### Find a specific file:

```bash
find . -name "config.json"
```

### Find only folders:

```bash
find . -type d -name "src"
```

### Find & delete:

```bash
find . -name "*.log" -delete
```

find + delete = _superpower_, use carefully.

---

# 🧪 **Main Task: Learn 3 New Everyday Commands Using TLDR**

Choose **any 3 commands you’ve never used before**, for example:

- `chmod`
    
- `curl`
    
- `wget`
    
- `du`
    
- `df`
    
- `head`
    
- `tail`
    
- `sed`
    
- `awk`
    
- `ps`
    

Then run:

```
tldr commandName
```

For example:

```
tldr chmod
tldr curl
tldr ps
```

Read 3–5 examples from each.

Try at least **one example** yourself.

---

# 🎯 Suggested Everyday Commands to Learn (Beginner-Friendly)

Here are 3 great options:

---

## 🔧 **Command A — chmod**

Change permissions of a file:

```
chmod +x script.sh
```

---

## 🌐 **Command B — curl**

Quickly hit APIs from terminal:

```
curl https://api.github.com
```

---

## 🧩 **Command C — head / tail**

Show the first / last 10 lines of a file:

```
head app.log
tail app.log
tail -f app.log   # live follow (super useful)
```

---

# 🎯 Mini Challenges (Fun & Fast)

### **Challenge 1 — Create and extract a tar file**

```
tar -cvf test.tar src/
tar -xvf test.tar
```

---

### **Challenge 2 — Search for TODO comments**

```
grep -R "TODO" .
```

---

### **Challenge 3 — Find all PNG images**

```
find . -name "*.png"
```

---

### **Challenge 4 — Discover 3 commands with TLDR**

Try:

```
tldr awk
tldr du
tldr sed
```

Pick your 3 favorite new commands.

---

# 💡 Innovation Idea of the Day

### Make a shortcut to open TLDR instantly:

Add to your `.zshrc`:

```bash
alias t="tldr"
```

Now you can learn new commands super fast:

```
t chmod
t awk
t curl
```

---

# 🚀 You’re doing great — TLDR will boost your learning speed massively.

Send **Day 14** whenever you're ready!

# Day 14-Week 2 Review

Nice! Day 14 is your **Week 2 Review**, and this one feels REALLY good — because today you prove to yourself that you can handle a full development workflow using **only the terminal**.

Let’s make it smooth, simple, and confidence-boosting.  
By the end of today, you'll be able to work like a real backend engineer: fast, focused, and keyboard-only.

---

# 🌟 **Day 14 — Week 2 Review (Expanded Guide)**

## 🎯 **Goal of the Day**

Do a **complete developer workflow** without touching your mouse:

1️⃣ Search for a file in your project  
2️⃣ Open it in Neovim  
3️⃣ Edit it  
4️⃣ Save it  
5️⃣ Commit changes using LazyGit

This is your first _real_ terminal-only coding cycle.  
You’re leveling up fast!

---

# 🪄 **Step 1 — Search the File (with ripgrep or find)**

Let’s say you want to find where `useEffect` is used.

Use ripgrep:

```bash
rg "useEffect"
```

Or find a specific file:

```bash
find . -name "Header.jsx"
```

Pick one result → copy its path.

Example:

```
src/components/Header.jsx
```

---

# ✍️ **Step 2 — Open the File in Neovim**

```bash
nvim src/components/Header.jsx
```

Or open directly at a specific line:

```bash
nvim src/components/Header.jsx +12
```

This takes you straight to the matched line — very handy!

---

# 🔧 **Step 3 — Edit the File in Vim**

Inside Neovim:

### Enter Insert Mode:

```
i
```

Make your edits:

- update a variable
    
- fix indentation
    
- add a console.log
    
- change a hook
    
- update a comment
    

Example edit:

```js
console.log("Updated from Day 14 terminal practice!");
```

### Exit Insert Mode:

```
Esc
```

### Save and Quit:

```
:wq
```

You’ve now edited code fully inside the terminal!

---

# 🔄 **Step 4 — Open LazyGit for Commit**

Inside your project folder:

```bash
lazygit
```

Use the keys:

### Stage all changed files:

```
a
```

### Commit:

```
c
```

Type a message:

```
Day 14: Completed full-term editing workflow
```

Press **Enter**.

### Push:

```
p
```

LazyGit handles everything beautifully.

---

# 🎉 **You just completed a FULL developer workflow in pure terminal!**

This is how advanced engineers work daily.  
You're moving into that zone now. Proud of you!

---

# 🎯 Mini Challenges (Fun & Practical)

### **Challenge 1 — Open files faster**

Search for "useState" and open directly at first result:

```
nvim $(rg -l "useState" | head -1)
```

---

### **Challenge 2 — Edit two files**

- search
    
- open
    
- edit
    
- save
    
- commit  
    All inside terminal.
    

---

### **Challenge 3 — Rename a variable across project**

Search everywhere:

```
rg "isOpen"
```

Open each file and edit using Vim.

---

### **Challenge 4 — Do everything WITHOUT stopping**

Try this flow:

```
rg → nvim → :wq → lazygit → commit → push
```

Feels very smooth!

---

# 💡 Innovation Idea of the Day

### Create a super helpful shortcut to search → open → edit quickly:

Add in `.zshrc`:

```bash
function vsearch() {
  nvim $(rg -l "$1" | head -1)
}
```

Reload:

```bash
source ~/.zshrc
```

Now run:

```
vsearch useState
```

Boom — opens the first file containing `useState` instantly.

---

# 🚀 You're doing incredible!

Week 2 was amazing — searching, editing, LazyGit, ripgrep, Neovim…  
Your workflow is becoming sharp.

Send **Day 15** whenever you’re ready — we’ll step into more advanced terminal habits!