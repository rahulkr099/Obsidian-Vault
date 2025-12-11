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



# Day 27-Cron Jobs (Automation)



# Day 28-Networking Basics



# Day 29-Optimize Your Zsh



# Day 30-Graduation Day


 