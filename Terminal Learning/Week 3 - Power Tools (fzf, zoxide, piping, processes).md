# Day 15-Install fzf

Awesome! Day 15 is a BIG power-up day.  
`fzf` gives you _fuzzy searching_ — the fastest way to jump to any file, command, folder, or history entry in a blink.  
Once you learn this, your terminal workflow becomes insanely fast and smooth.

Let’s make today simple, fun, and super practical.

---

# 🌟 **Day 15 — Install fzf + Fuzzy Search (Expanded Guide)**

## 🎯 **Goal of the Day**

- Install `fzf`
    
- Use it to search files instantly
    
- Combine it with Neovim to open files super fast
    

This becomes your new “teleport anywhere” tool.

---

# 🛠️ **1. Install fzf (Linux Mint)**

Open terminal:

```bash
sudo apt install fzf
```

After installation, restart the terminal.

Test it:

```bash
fzf
```

If it opens an empty interactive box, you're ready!

---

# 🔎 **2. What is Fuzzy Search?**

With `fzf`, you don’t need to type the full file name.  
Type _any part_ of the name → it will match intelligently.

Example:

Typing:

```
hea
```

Matches:

```
Header.jsx
myHeaderComponent.js
theme-header.css
```

Super smart + super fast.

---

# 🚀 **3. Basic Usage**

Simply run:

```bash
fzf
```

You get an interactive list of:

- files
    
- folders
    
- hidden files
    

Use:

- **↑ / ↓** to navigate
    
- **Enter** to select
    

---

# 📂 **4. Fuzzy Search + Open in Neovim (The Real Magic)**

Find a file → then open it with Neovim:

```bash
nvim $(fzf)
```

This is the most common and powerful use case.

Steps:

1. Type `nvim $(fzf)`
    
2. fzf opens
    
3. Type the part of file name
    
4. Hit Enter
    
5. Neovim opens that exact file instantly
    

Feels like teleportation.

---

# 🧪 **Day 15 Task: Use fzf to quickly find and open a file**

Let’s do this step-by-step.

### Step 1 — Go into any project

```bash
cd myproject
```

### Step 2 — Run:

```bash
nvim $(fzf)
```

### Step 3 — Type part of a file name:

```
app
index
style
route
```

Use ↑ ↓ to choose.

### Step 4 — Press **Enter**

Boom — file opens in Neovim.

You’ve now used fuzzy search professionally!

---

# 🎯 Mini Challenges (Fun & Helpful)

### **Challenge 1 — Open multiple files fast**

Run:

```bash
fzf --multi
```

Select several files using **Tab** → press Enter → get list.

---

### **Challenge 2 — Search only directories**

```
fd --type d | fzf
```

Requires `fd` (simple to install later).

---

### **Challenge 3 — Search command history**

```
history | fzf
```

Find old commands instantly.

---

### **Challenge 4 — Switch Git branches using fzf**

Try:

```bash
git branch | fzf
```

Select branch → copy → checkout.

---

# 💡 **Innovation Idea of the Day**

### Create a custom command to open ANY file instantly:

Add to your `~/.zshrc`:

```bash
alias vf='nvim $(fzf)'
```

Reload:

```bash
source ~/.zshrc
```

Now you can do:

```
vf
```

Type any part of the filename → select → boom, Neovim opens it.

This becomes one of your most-used shortcuts as a developer.

---

# 🚀 You’re doing great!

Day 15 gives you **speed** and **freedom** — no more hunting filenames manually.

Send **Day 16** whenever you're ready, and we’ll continue leveling up your terminal workflow!

# Day 16-Install zoxide

Nice! Day 16 is all about **zoxide**, one of the smartest navigation tools you will ever install.  
It upgrades your `cd` command into something _intelligent_.  
You will be able to jump between deeply nested folders with tiny shortcuts.

Today will feel like magic. ✨

---

# 🌟 **Day 16 — Install zoxide (Expanded Guide)**

## 🎯 **Goal of the Day**

- Install zoxide
    
- Replace `cd` with a smarter jump command
    
- Move between folders instantly using fuzzy matching
    

After today, you'll never type long paths again.  
Not even `cd projects/web/backend/src/routes` — just do:

```
z routes
```

and boom → you're there.

---

# 🛠️ **1. Install zoxide**

Run:

```bash
sudo apt install zoxide
```

Now add it to your shell by editing `.zshrc`:

```bash
echo 'eval "$(zoxide init zsh)"' >> ~/.zshrc
source ~/.zshrc
```

Great — zoxide is now active.

---

# 🔮 **2. Basic Usage: Smart CD**

Instead of:

```
cd long/path/to/your/folder
```

Just type:

```
z folderName
```

Because zoxide remembers every folder you visit.

---

# 🧠 How zoxide works (simple explanation)

- Every time you `cd` into a folder, zoxide _learns it_.
    
- Next time you want that folder, use a small keyword:
    
    ```
    z doc
    → jumps to ~/Documents  
    ```
    
- Even fuzzy matches work:
    
    ```
    z pro
    → jumps to ~/projects
    ```
    

---

# 🚀 **3. Useful Commands**

### Jump to a folder (most used):

```
z folder
```

### Jump using partial name:

```
z src
z comp
z down
```

### Show history of visited directories:

```
zoxide query -l
```

### Jump to most frequently used directory:

```
z
```

---

# 🧪 **Day 16 Task: Jump Between Folders Instantly**

Let’s do this hands-on.

### Step 1 — Visit 3–5 folders normally:

```bash
cd ~
cd ~/Documents
cd ~/Downloads
cd ~/projects
cd ~/projects/myapp
```

This teaches zoxide your folders.

---

### Step 2 — Now TELEPORT using `z`

Try:

```
z down
```

You should jump to `~/Downloads`.

Try:

```
z pro
```

You should jump to `~/projects`.

Try:

```
z myapp
```

You should jump right into your app folder.

This is why zoxide feels magical — it understands what you mean.

---

# 🎯 Mini Challenges (Fun + Useful)

### **Challenge 1 — Fast project switching**

Move to a completely different directory:

```
z documents
```

Then instantly jump back:

```
z myapp
```

Feels like teleporting.

---

### **Challenge 2 — Deep folder jump**

Create a nested folder:

```bash
mkdir -p ~/practice/week16/subfolder/demo
cd ~/practice/week16/subfolder/demo
```

Now move away:

```bash
cd ~
```

Jump back instantly:

```
z demo
```

---

### **Challenge 3 — List your zoxide memory**

```
zoxide query -l
```

See all folders zoxide learned so far.

---

# 💡 Innovation Idea of the Day

### Make `cd` behave like `z` (super convenient)

Add this to your `.zshrc`:

```bash
alias cd="z"
```

Now typing:

```
cd proj
```

instantly jumps to your projects folder.  
Feels natural and incredibly fast.

---

# 🚀 You're flying through your terminal learning journey!

Zoxide is one of the biggest quality-of-life boosts — you’ll feel it instantly.

Send **Day 17** whenever you’re ready!

# Day 17-Pipes & Redirection

Great! Day 17 is where your terminal skills start becoming **creative**.  
Pipes (`|`) and redirection (`>` `>>`) let you _combine commands_ like Lego blocks and build your own mini tools.  
This is how advanced developers automate workflows.

Let’s make it simple, clear, and powerful.

---

# 🌟 **Day 17 — Pipes & Redirection (Expanded Guide)**

## 🎯 **Goal of the Day**

Learn how to:

- pipe output from one command into another
    
- redirect output into a file
    
- append new content to existing files
    
- build a custom pipeline that boosts your productivity
    

---

# 🔧 **1. Pipes (`|`) — Connect commands together**

The pipe sends the _output_ of one command into the _input_ of another.

Example:

```
ls | bat
```

Meaning:

- `ls` lists files
    
- `bat` displays them with syntax highlighting
    

Try a few yourself:

### View running processes nicely:

```
ps aux | bat
```

### Search inside history:

```
history | fzf
```

### Search with line numbers and highlight:

```
rg "function" | bat
```

---

# 📝 **2. Redirection (`>`) — Save output to a file**

### Write output into a new file:

```
rg "useEffect" > results.txt
```

Warning:  
`>` **overwrites** the file completely.

---

# 📌 **3. Appending (`>>`) — Add to an existing file**

Append instead of replace:

```
echo "New line added" >> notes.txt
```

Append search results:

```
rg "TODO" >> todo-logs.txt
```

This keeps adding content below old content.

---

# 🧪 **Examples to Try (Quick Practice)**

### Save all `.js` files list:

```
find . -name "*.js" > js-files.txt
```

### Count imports and save:

```
rg "import" -n > imports.txt
```

### Pretty list of directories:

```
ls -l | bat
```

### Live log viewer:

```
tail -f app.log | bat
```

---

# 🚀 **Day 17 Task: Build a Workflow-Improving Pipeline**

Let’s create a pipeline that actually helps your daily work.

Here are **3 example workflows** you can choose from — or create your own.  
(Do at least one.)

---

# 🛠️ **Workflow Idea 1 — Find files → filter → open**

```bash
rg -l "useState" | fzf | xargs nvim
```

Meaning:

- search for files containing useState
    
- pick one with fzf
    
- open it in Neovim instantly
    

🔥 This is a REAL developer power move.

---

# 🛠️ **Workflow Idea 2 — Search code → preview with bat**

```bash
rg "console.log" -n | bat
```

Makes debugging much nicer and readable.

---

# 🛠️ **Workflow Idea 3 — Export search results to a file**

```bash
rg "TODO" -n > todos.txt
```

Then view the file:

```
bat todos.txt
```

---

# 🎯 Mini Challenges (Fun + Useful)

### **Challenge 1 — Append instead of overwrite**

```
echo "Day 17 practice" >> review.txt
```

---

### **Challenge 2 — Combine 3 commands**

Example:

```
ls | grep "src" | bat
```

---

### **Challenge 3 — Make a log viewer pipeline**

```
tail -f log.txt | rg "error"
```

(This will highlight errors live!)

---

# 💡 Innovation Idea of the Day

### Create your own pipeline function for daily use

Add to your `.zshrc`:

```bash
function searchopen() {
  rg -l "$1" | fzf | xargs nvim
}
```

Reload:

```bash
source ~/.zshrc
```

Now simply run:

```
searchopen useEffect
```

This searches → selects → opens in Neovim automatically.  
Feels like magic.

---

# 🚀 Amazing job reaching Day 17!

You now understand how terminal tools _work together_, which is the secret behind real productivity.

Send **Day 18** whenever you’re ready!

# Day 18-File Permissions

Great! Day 18 takes you into **file permissions** — an important part of being comfortable in Linux.  
Today is simple but powerful: you’ll learn how to make a script executable so you can run it like a real command.

Let’s make everything super clear.

---

# 🌟 **Day 18 — File Permissions (Expanded Guide)**

## 🎯 **Goal of the Day**

Understand:

- how permissions work
    
- how to use `chmod`
    
- what `chown` does
    
- how to make any script executable
    

Once you know this, running your own tools becomes effortless.

---

# 🧠 **1. Understanding Permissions (Quick & Easy)**

Run:

```bash
ls -l
```

You will see something like:

```
-rw-r--r--
```

This represents:

- read (r)
    
- write (w)
    
- execute (x)
    

If a script doesn’t have **x**, you cannot run it.

---

# 🔧 **2. chmod — Change File Permissions**

### Make a script executable:

```
chmod +x script.sh
```

Now you can run it with:

```
./script.sh
```

That’s the main command for today.

---

### Give full permissions (not recommended everywhere):

```
chmod 777 file
```

### Remove execute permission:

```
chmod -x script.sh
```

---

# 👑 **3. chown — Change File Owner**

You won’t use this daily, but it’s important to know.

```
sudo chown rahul:rahul file.txt
```

or change owner only:

```
sudo chown rahul file.txt
```

Useful when:

- files are owned by root
    
- you downloaded or copied something into system folders
    

---

# 🧪 **Day 18 Task: Make a script executable**

Let’s do it step-by-step.

### Step 1 — Create a script

```bash
echo 'echo "Hello from Day 18!"' > hello.sh
```

### Step 2 — Check its permissions

```bash
ls -l hello.sh
```

You’ll probably see:

```
-rw-r--r--
```

No execute permission yet.

---

### Step 3 — Add execute permission

```bash
chmod +x hello.sh
```

---

### Step 4 — Run the script

```bash
./hello.sh
```

You should see:

```
Hello from Day 18!
```

Congrats — you just made your first executable script! 🎉

---

# 🎯 Mini Challenges (Quick + Useful)

### **Challenge 1 — Make a small script to list files**

```bash
echo 'ls -la' > list.sh
chmod +x list.sh
./list.sh
```

---

### **Challenge 2 — Make a backup script**

```bash
echo 'cp -r ~/projects ~/projects-backup' > backup.sh
chmod +x backup.sh
```

---

### **Challenge 3 — Remove execute permission**

```bash
chmod -x hello.sh
```

Try running it again — it won't run.

---

# 💡 Innovation Idea of the Day

### Add a folder for all your personal scripts

```
mkdir ~/bin
```

Add to `.zshrc`:

```bash
export PATH="$HOME/bin:$PATH"
```

Now any script you put into `~/bin` becomes runnable from **anywhere**, like a real Linux command.

Example:

```
cp myscript.sh ~/bin/myscript
chmod +x ~/bin/myscript
myscript
```

You're literally creating your own commands. 🚀

---

# 🎉 You're doing amazing — Day 18 completed!

Permissions are a key part of Linux mastery, and you've nailed the basics.

Send **Day 19** whenever you're ready!

# Day 19-Processes

Great! Day 19 is all about **processes** — understanding what’s running on your system and controlling it.  
This is a core Linux skill, and today’s task (killing a process by PID) will make you feel much more confident handling your system.

Let’s make this super simple and practical.

---

# 🌟 **Day 19 — Processes (Expanded Guide)**

## 🎯 **Goal of the Day**

Learn how to:

- list running processes
    
- find the PID of a process
    
- kill a process using that PID
    
- use top/htop/btop to monitor in real-time
    

By the end of today, you’ll know how to handle stuck apps, runaway scripts, or heavy background processes like a pro.

---

# 🔧 **1. ps — Show Processes**

The simplest version:

```bash
ps
```

Shows only your current shell processes.

More useful version:

```bash
ps aux
```

Meaning:

- **a**: all users
    
- **u**: show user
    
- **x**: include processes not attached to terminals
    

If you want to find a specific process:

```
ps aux | grep node
ps aux | grep firefox
ps aux | grep python
```

---

# 🧟 **2. kill — Stop a Process**

First, find the PID:

```
ps aux | grep node
```

You’ll see something like:

```
12345  node app.js
```

Here **12345** is the PID.

Now kill it:

```bash
kill 12345
```

If it still doesn’t stop, use force kill:

```bash
kill -9 12345
```

🛑 Use `-9` only when normal kill doesn’t work — it force-terminates instantly.

---

# 📊 **3. top — Live Process Viewer**

Run:

```bash
top
```

You’ll see:

- CPU usage
    
- Memory usage
    
- Process PIDs
    

Quit using:

```
q
```

top is good but a bit old-fashioned.

---

# ⚡ **4. htop / btop — Better Monitoring**

Since you already installed **btop**, use it:

```bash
btop
```

Inside btop:

- highlight a process
    
- press **k** to kill it
    
- confirm
    

Much easier than manual PID typing!

---

# 🧪 **Day 19 Task: Kill a Running Process by PID**

Let’s do this step-by-step.

---

### ✔ Step 1 — Create a fake running process (so you don’t affect real apps)

Open a new terminal tab and run:

```bash
sleep 500
```

This command does nothing for 500 seconds — perfect test process.

---

### ✔ Step 2 — Find its PID

In another terminal:

```bash
ps aux | grep sleep
```

You’ll see something like:

```
rahul   42918  0.0  0.0  ...   sleep 500
```

Here **42918** is the PID.

---

### ✔ Step 3 — Kill it

```bash
kill 42918
```

Check again:

```bash
ps aux | grep sleep
```

If it’s gone → task complete!  
If it’s still running, do:

```bash
kill -9 42918
```

---

# 🎯 Mini Challenges (Fun + Helpful)

### **Challenge 1 — Kill your Node server**

Start a server:

```bash
npm run dev
```

Find PID:

```
ps aux | grep node
```

Kill it:

```
kill PID
```

---

### **Challenge 2 — Find a heavy program**

Use:

```
btop
```

Sort by CPU or memory → kill an unimportant process.

---

### **Challenge 3 — Kill a zombie process**

Sometimes after closing apps, tiny leftover processes remain.  
Find and kill them manually.

---

# 💡 Innovation Idea of the Day

### Make a helper function to kill processes faster

Add to `~/.zshrc`:

```bash
function kgrep() {
  ps aux | grep "$1"
}
```

Reload:

```bash
source ~/.zshrc
```

Now type:

```
kgrep node
```

Shows all Node processes instantly.

Even better, a one-line kill:

```bash
function killp() {
  kill $(ps aux | grep "$1" | awk '{print $2}')
}
```

Then:

```
killp node
```

Kills ALL node processes.  
Very powerful — use carefully.

---

# 🚀 You crushed Day 19!

You now understand processes — a huge part of terminal mastery.

Send **Day 20** whenever you're ready!

# Day 20-Environment Variables

Awesome! Day 20 is a really important one — **environment variables** are the backbone of how your terminal, programs, shells, and even frameworks communicate.  
Today will feel simple, but the skill is extremely powerful.

Let’s make it super clear and practical.

---

# 🌟 **Day 20 — Environment Variables (Expanded Guide)**

## 🎯 **Goal of the Day**

- Understand what environment variables are
    
- Check your PATH
    
- Create your own variables
    
- Add them permanently to `.zshrc`
    

By the end of today, you’ll know how to set configs, API keys, tokens, usernames, ports, and custom shortcuts in your environment.

---

# 🧠 **1. echo $PATH — What is PATH?**

Run:

```bash
echo $PATH
```

PATH is a list of directories where your system looks for commands.

Example output:

```
/usr/local/bin:/usr/bin:/home/rahul/bin
```

If a directory is in PATH, you can run programs inside it _from anywhere_.

---

# 🔧 **2. export NAME="Rahul"**

Temporary environment variable:

```bash
export NAME="Rahul"
```

Check it:

```bash
echo $NAME
```

Output:

```
Rahul
```

But this disappears when you close your terminal.

That’s why we need `.zshrc`.

---

# 🏡 **3. Make Variables Permanent (Add to .zshrc)**

To add custom environment variables that live forever:

### Open `.zshrc`:

```bash
nvim ~/.zshrc
```

Add a line like:

```bash
export PROJECT_OWNER="Rahul"
```

Save & quit:

```
:wq
```

Reload:

```bash
source ~/.zshrc
```

Check it:

```bash
echo $PROJECT_OWNER
```

Nice — it now works in every terminal session.

---

# 🧪 **Day 20 Task: Add a Custom Variable into .zshrc**

Let’s do a full hands-on example.

### Step 1 — Open `.zshrc`

```bash
nvim ~/.zshrc
```

### Step 2 — Add your custom variable

Pick any variable name — here are great ideas:

```
export DEV_NAME="Rahul"
export WORKSPACE="$HOME/projects"
export DEFAULT_EDITOR="nvim"
export API_ENV="development"
```

Let’s add this one:

```
export DEV_NAME="Rahul"
```

### Step 3 — Save & reload the shell

```bash
source ~/.zshrc
```

### Step 4 — Test

```bash
echo $DEV_NAME
```

Output:

```
Rahul
```

🎉 Perfect — your custom variable is now active globally.

---

# 🎯 Mini Challenges (Fun + Helpful)

### **Challenge 1 — Set your default project directory**

Inside `.zshrc`:

```
export PROJECTS="$HOME/projects"
```

Jump with:

```
cd $PROJECTS
```

---

### **Challenge 2 — Store a port number**

```
export PORT=3000
echo $PORT
```

Useful for Node apps.

---

### **Challenge 3 — Make a dynamic greeting**

Add:

```
export GREETING="Hello, Rahul! Welcome back to the terminal."
```

Check:

```
echo $GREETING
```

Feels personal. 😊

---

# 💡 Innovation Idea of the Day

### Create an alias that uses your environment variable

Add to `.zshrc`:

```bash
alias hi='echo $GREETING'
```

Now type:

```
hi
```

Your terminal greets you!  
A small joy every day.

---

# 🚀 Amazing job reaching Day 20!

Environment variables are key in real-world development — this knowledge will help you with Node, Python, Docker, Git, and deployment.

Send **Day 21** whenever you're ready!

# Day 21-Week 3 Review

