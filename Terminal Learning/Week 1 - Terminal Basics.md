#  (Build Muscle Memory)

# Day 1-Navigation

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

# Day 2-Files & Folders

Awesome! Day 2 is where things start getting real — you’ll actually **create, move, copy, and delete files** like a true terminal user. Let’s expand this in a very practical, hands-on way so you learn fast and confidently.

---

## 🌿 **Day 2 — Files & Folders (Expanded + Practical Guide)**

## 🎯 **Goal of the Day**

Understand how to **create**, **organize**, **rename**, **copy**, and **remove** files/folders.  
These actions become second nature once you practice them a bit.

Let’s break each command into simple language + examples + small tasks.

---

## 📁 **Commands to Learn**

---

## **1. `touch file.txt` — Create a New File**

Creates an empty file.

```bash
touch notes.txt
touch index.html
touch app.js
```

⭐ Tip:  
Touch is great for _quickly creating placeholder files_ in projects.

---

## **2. `mkdir test` — Make a New Folder**

Creates a directory.

```bash
mkdir projects
mkdir images
mkdir backups
```

Useful trick:

```bash
mkdir -p newfolder/inside/deep
```

`-p` automatically creates nested folders.

---

## **3. `rm file.txt` — Remove a File**

Deletes a file permanently.

```bash
rm notes.txt
```

⚠️ This is not like Recycle Bin → **It’s gone forever.**

---

## **4. `rm -r folder` — Remove Folder (recursively)**

Deletes a folder + everything inside.

```bash
rm -r test
```

⚠️ Be careful. Use `ls` first to confirm what you're deleting.

---

## **5. `mv file1 file2` — Move or Rename Files**

### 👉 Rename a file:

```bash
mv oldname.txt newname.txt
```

### 👉 Move file to a folder:

```bash
mv notes.txt documents/
```

---

## **6. `cp file1 file2` — Copy files**

Copy file into a new file:

```bash
cp file.txt backup.txt
```

Copy a file into a folder:

```bash
cp image.png images/
```

Copy entire folders:

```bash
cp -r src/ backup/
```

---

## 🧪 **Main Task: Create a small project & organize it**

Let’s make a real folder structure like developers do.

### Step 1: Make a project folder

```bash
mkdir myproject
cd myproject
```

### Step 2: Create subfolders

```bash
mkdir src assets docs
```

### Step 3: Create some files

```bash
touch src/app.js
touch README.md
touch assets/logo.png
touch docs/notes.txt
```

### Step 4: Rename something

```bash
mv notes.txt docs/project-notes.txt
```

### Step 5: Copy something

```bash
cp README.md docs/README-copy.md
```

### Step 6: Delete something you don’t need

```bash
rm docs/README-copy.md
```

### Step 7: Remove a folder you created by mistake

```bash
rm -r assets
```

Now your terminal brain is warming up.  
You're creating and organizing just like a developer working inside real projects.

---

## 🎯 **Mini Challenges (Fun & Helpful)**

### ✔ Challenge 1

Create a folder named `playground` and inside it:

- create 5 files
    
- rename 2 files
    
- move 1 file into another folder
    
- delete 1 file
    

### ✔ Challenge 2

Create nested folders with one command:

```
mkdir -p school/2024/assignments/math
```

### ✔ Challenge 3

Copy a folder with code:

```
cp -r src src-backup
```

Your hands will start developing muscle memory — that’s the main goal of Day 2.

---

## 💡 **Innovation Idea of the Day**

### **Create a shortcut command for making a new project instantly**

Add this to your `~/.zshrc`:

```bash
mkproject() {
  mkdir -p "$1"/{src,assets,docs}
  touch "$1"/README.md
  echo "Project '$1' created!"
}
```

Now run:

```bash
mkproject blogapp
```

— Boom! A full project structure in one second.

---

If you’re ready, send **Day 3**, and I’ll expand it just like this — step-by-step, simple words, practical exercises, and smart ideas.

# Day 3-View Files

Perfect! Day 3 is all about **viewing files in a developer-friendly way**, and `bat` makes this soooo much nicer than plain `cat`.  
Let’s boost this day with simple explanations, examples, and a few creative ideas to build stronger terminal habits.

---

## 🌟 **Day 3 — Viewing Files (with `bat`)**

## 🎯 **Goal of the Day**

Learn how to **read code files directly in the terminal** with:

- line numbers
    
- syntax highlighting
    
- clean formatting
    

This skill becomes super useful when you debug projects, explore configs, or read logs without opening a full editor.

---

## 🛠️ Step 1: Install `bat`

### **On Linux Mint / Ubuntu**

```bash
sudo apt install bat
```

But the command will be installed as `batcat`.  
So create an alias to use it as `bat`:

```bash
echo 'alias bat="batcat"' >> ~/.zshrc
source ~/.zshrc
```

Now you can simply type:

```bash
bat file.txt
```

---

## 📚 **Day 3 Commands (Explained Simply)**

---

## **1. `bat file` — View a file beautifully**

```bash
bat app.js
bat README.md
bat config.json
```

You will see:

- **line numbers**
    
- **colors**
    
- **syntax highlighting**
    
- a small separator bar
    

It feels like VS Code inside your terminal.

---

## **2. `bat --style=plain file` — Plain mode**

This removes decorations and keeps it simple.

```bash
bat --style=plain app.js
```

Useful when:

- You want clean output
    
- You’re copying code into chat or documentation
    
- You dislike extra styling for specific files
    

---

## 🧪 **Main Task: Explore a Code File**

Pick any real file from your system:

- `.js`
    
- `.js`
    
- `.css`
    
- `.py`
    
- `.json`
    
- `.md`
    

Run:

```bash
bat fileNameHere
```

### While viewing, notice:

✔ Line numbers  
✔ Color highlighting  
✔ Where functions start  
✔ Where variables are declared  
✔ Formatting structure

### Then try plain mode:

```bash
bat --style=plain fileNameHere
```

This will help your eyes understand the difference between styled and plain output.

---

## 🎯 **Mini Challenges**

### **Challenge 1 — Compare Views**

Run:

```bash
bat app.js
bat --style=plain app.js
```

Notice how your brain reads both differently.

---

### **Challenge 2 — View a big log file**

If you have any log file:

```bash
bat /var/log/syslog
```

Even logs look better with syntax highlighting.

---

### **Challenge 3 — Try paging**

Pipe output through `less`:

```bash
bat app.js | less
```

Use:

- `j` / `k` to scroll
    
- `q` to quit
    

This becomes useful for long files.

---

## 💡 **Innovation Idea of the Day**

### **Create a super alias to always show line numbers and plain style switch**

Add to your `~/.zshrc`:

```bash
alias b='bat --paging=always'
alias bp='bat --style=plain --paging=always'
```

Now you can quickly test both modes:

```
b main.py
bp main.py
```

Short, fast, developer-friendly.

---


# Day 4-Yazi File Explorer

Nice! Day 4 is where your terminal starts feeling **alive**.  
Yazi is fast, modern, and insanely useful once you know a few keys.  
Let’s expand this day properly so you get full control of your file system _without touching the mouse_.

---

## 🌟 **Day 4 — Yazi File Explorer (Expanded Guide)**

## 🎯 **Goal of the Day**

Use **Yazi** as your full file explorer for the entire day.  
You’ll learn:

- moving around files
    
- entering/exiting folders
    
- deleting, copying, pasting
    
- previewing files instantly
    

By the end of today, your file management speed will jump to the next level.

---

## 🧭 **1. Opening Yazi**

```bash
yazi
```

You’ll see:

- Left: Directory tree
    
- Middle: File list
    
- Right: Preview (text, images, PDF thumbnails, etc.)
    

It’s like a turbocharged terminal version of Finder/Nautilus.

---

## 🎮 **2. Navigation Keys (Very Simple)**

### ✔ Move Up/Down

```
j  → down  
k  → up
```

### ✔ Enter folders

```
l  → go inside
```

### ✔ Go back

```
h  → go out (parent folder)
```

This `hjkl` navigation is the same logic as Vim & Neovim.  
You’re building muscle memory already. 🧠💪

---

## 🗑️ **3. Delete Files (dd)**

```
dd → delete selected file/folder
```

Yazi will confirm deletion if settings allow it.  
Be careful but confident — this is very fast.

---

## 📎 **4. Copy + Paste (yy / p)**

### ✔ Copy

```
yy
```

### ✔ Paste

```
p
```

Examples:

- Copy `image.png` → go to `assets` → press **p**
    
- Copy whole folders → paste anywhere
    

Yazi supports batch selections too.

---

## ⭐ **Extra Useful Hotkeys (Learn These Today If Possible)**

### **Space** → select multiple files

`Space` to select/deselect files (multi-select mode)

### **`i`** → show file info (size, type, permissions)

### **`Tab`** → switch between panels

(e.g., jump to preview → jump back)

### **`q`** → quit Yazi

These aren’t required, but trust me—they make you 3× faster.

---

## 🧪 **Main Task of the Day**

## 🔥 **“Manage files using Yazi only” challenge**

### Do these inside Yazi:

#### ✔ 1. Navigate deep into your folders

Use only **j/k/h/l**.

---

#### ✔ 2. Create a practice folder (from terminal)

Before entering Yazi:

```bash
mkdir ~/yazi-playground
touch ~/yazi-playground/a.txt
touch ~/yazi-playground/b.txt
mkdir ~/yazi-playground/sub
```

Open it:

```bash
yazi ~/yazi-playground
```

---

#### ✔ 3. Inside Yazi:

- Open `yazi-playground`
    
- Move into `sub`
    
- Go back to parent
    
- Delete `b.txt` using **dd**
    
- Copy `a.txt` using **yy**
    
- Paste it into `sub` using **p**
    
- Select multiple files (Space)
    
- View preview using right panel
    
- Quit using **q**
    

---

## 🎯 **Mini Challenges (Fun & Useful)**

### **Challenge 1: Speed drill**

Move down 10 files quickly using **j**.  
Move up using **k**.  
Enter 3 folders deep without touching your mouse.

---

### **Challenge 2: Organize chaos**

Pick a random directory (Downloads is perfect 😄)  
Use Yazi to:

- delete junk
    
- move files into new folders
    
- tidy the mess
    

This one gives an immediate real-life win.

---

### **Challenge 3: View a code file**

Highlight a `.js` / `.py` / `.json` file  
Look at the preview pane with syntax highlighting.

---

## 💡 Innovation Idea of the Day

### **Set a shortcut to open Yazi instantly**

Add to your `~/.zshrc`:

```bash
alias y="yazi"
```

Now simply type:

```bash
y
```

Lightning-fast access → helps you use Yazi daily without thinking.

---


# Day 5-VS Code Terminal + Zsh

Great! Day 5 brings everything together — **your coding environment + your terminal workflow**.  
Once VS Code uses Zsh, every command, alias, and customization becomes part of your daily dev routine.  
Let’s make this day smooth, practical, and fun.

---

## 🌟 **Day 5 — VS Code Terminal + Zsh (Expanded Guide)**

## 🎯 **Goal of the Day**

- Make **Zsh** the default terminal inside VS Code.
    
- Learn a few basic but powerful Zsh commands.
    
- Create **3 useful aliases** to speed up your workflow.
    

By the end of today, your editor + terminal combo will feel super professional.

---

## 🛠️ **1. Set VS Code Default Terminal to Zsh**

Open VS Code → press:

```
Ctrl + Shift + P
```

Search for:

```
Terminal: Select Default Profile
```

Choose:

```
zsh
```

Now open a new terminal inside VS Code:

```
Ctrl + `
```

If you see Zsh, congrats — it’s working! 🎉

---

## 📚 **2. Commands to Practice**

Let’s break them down in simple words.

---

## **1. `clear` → Clear your screen**

```bash
clear
```

or just press:

```
Ctrl + L
```

This gives you a fresh terminal without closing anything.

---

## **2. `history` → See all commands you ran**

```bash
history
```

You’ll notice:

- command numbers
    
- everything you typed recently
    
- great for learning from your mistakes 😄
    

Try searching inside history:

```
history | grep git
```

---

## **3. `alias` → Create shortcuts**

This makes long commands super short.

Example:

```bash
alias gs="git status"
alias ll="ls -la"
alias c="clear"
```

Add aliases permanently by editing:

```
~/.zshrc
```

---

## 🧪 **Main Task: Add 3 New Aliases**

Here are 3 good, practical, developer-friendly alias ideas for you.  
Feel free to copy them, or create your own.

---

## 🎯 **Alias 1 — Quick navigation to Downloads**

```bash
echo 'alias dl="cd ~/Downloads"' >> ~/.zshrc
```

Now you can type:

```
dl
```

Boom — you’re in Downloads.

---

## 🎯 **Alias 2 — Pretty file listing**

(Assuming you use **lsd**)

```bash
echo 'alias ls="lsd -la"' >> ~/.zshrc
```

This gives:

- icons
    
- colors
    
- hidden files
    
- proper directory structure
    

Much cleaner than default `ls`.

---

## 🎯 **Alias 3 — Start your dev environment fast**

```bash
echo 'alias dev="cd ~/projects && ls"' >> ~/.zshrc
```

Changes into your projects folder instantly.

---

After adding aliases, reload your shell:

```bash
source ~/.zshrc
```

Now test each alias and enjoy your speed boost.

---

## 🎯 Mini Challenges (Fun & Quick)

### **Challenge 1**

Create an alias that opens VS Code:

```bash
alias v="code ."
```

---

### **Challenge 2**

Create an alias to update your system:

```bash
alias update="sudo apt update && sudo apt upgrade -y"
```

---

### **Challenge 3**

Make an alias for clearing + listing files in one shot:

```bash
alias cl="clear && ls"
```

---

## 💡 Innovation Idea of the Day

### Create an alias that shows your top 10 most-used commands:

Add this:

```bash
alias topcmd='history | awk "{print \$2}" | sort | uniq -c | sort -nr | head'
```

Now run:

```
topcmd
```

You’ll instantly see:

- what you type often
    
- where you can create new aliases
    
- how your habits are forming
    

Magic for productivity!

---



# Day 6-btop + System Monitoring

Awesome, Day 6!  
Today is super fun because **btop** makes system monitoring feel beautiful and interactive — almost like you're watching your computer’s heartbeat in real time.  
Let’s expand everything so you truly understand what you’re looking at.

---

## 🌟 **Day 6 — btop + System Monitoring (Expanded Guide)**

## 🎯 **Goal of the Day**

Understand how to monitor:

- **CPU usage**
    
- **RAM usage**
    
- **Processes**
    
- **Tasks consuming resources**
    

By the end of today, you’ll be able to spot heavy apps, lag issues, and system performance patterns instantly.

---

## 🛠️ 1. Run btop

Just type:

```bash
btop
```

You’ll see a colorful dashboard with panels for CPU, RAM, Disk, Network, and Processes.

It feels like a hacker movie — but real and useful. 😄

---

## 🧠 2. What to Explore Inside btop

Let’s break down the important sections so you understand everything clearly.

---

## 🔥 **1. CPU Panel**

Look for:

- **Usage %** — how much load your system is under
    
- **Temperature** (if shown)
    
- **Per-core usage**
    

🎯 If one core is 100%, the system may feel slow even if others are free.

---

## 💾 **2. RAM Panel**

Shows:

- **Used**
    
- **Free**
    
- **Cached**
    
- **Swap** (if your RAM fills up)
    

Why RAM matters:

- If RAM is always near 90–95%, your system will slow down.
    
- Cached memory is good — it speeds up the system.
    

---

## ⚙️ **3. Process List**

This is the heart of btop.

You’ll see:

- process names
    
- CPU usage
    
- memory usage
    
- PIDs
    

Try sorting by pressing:

```
P → sort by CPU
M → sort by memory
T → sort by time
```

High CPU = usually heavy apps  
High memory = browsers, VS Code, Node apps

---

## 🔎 **4. Kill Processes from btop**

If something freezes or misbehaves:

- Highlight the process
    
- Press **`k`**
    
- Confirm kill
    

This is way faster than using `kill` in terminal manually.

---

## 🧪 **Main Task of the Day**

Today you’ll explore your whole system using only btop.

### ✔ Step 1 — Check CPU usage

Notice:

- which apps spike
    
- how many cores you have
    
- live graph movement
    

Try opening Chrome or VS Code and watch CPU spikes.

---

### ✔ Step 2 — Check RAM usage

Open heavy apps and see how RAM changes.

Close them and observe the decrease.

---

### ✔ Step 3 — Sort Processes

Inside the process panel, try:

```
Shift + P → sort by CPU  
Shift + M → sort by memory  
Shift + T → sort by time alive
```

---

### ✔ Step 4 — Try killing a small process

Don’t kill anything important 😄  
Maybe open a random program and kill it from btop to understand the workflow.

---

# 🎯 Mini-Challenges

### **Challenge 1 — Stress Test (Safe & Fun)**

Open:

- VS Code
    
- Chrome (4–5 tabs)
    
- Terminal
    
- A video
    

Now watch CPU/RAM spike in btop.

---

### **Challenge 2 — Find the Top Memory Hog**

Sort by Memory and note what your biggest consumer is.

---

### **Challenge 3 — Find the Lightest Process**

Sort reverse (press again) and see tiny background tasks.

---

# 💡 Innovation Idea of the Day

### Set an alias to open btop faster:

Add this to `~/.zshrc`:

```bash
alias bt="btop"
```

Reload:

```bash
source ~/.zshrc
```

Now you can open monitoring instantly:

```
bt
```

Perfect when your laptop feels slow and you want to check what's happening.

---

# 🚀 Ready for Day 7?

Send me Day 7 whenever you want, and I’ll expand it with simple steps, practical exercises, and productivity boosters.

You’re learning fast — keep going!

# Day 7-Week 1 Review






