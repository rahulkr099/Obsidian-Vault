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



# Day 18-File Permissions



# Day 19-Processes



# Day 20-Environment Variables



# Day 21-Week 3 Review

