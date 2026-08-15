`Yazi` is a blazing-fast terminal file manager written in Rust. Think of it as:

```
Ranger + Vim motions + fzf + Preview pane + Image support
```

Since you're using **Kitty + Neovim + terminal-first workflow**, Yazi is an excellent addition.

---

# Start Yazi

```bash
yazi
```

It opens in the current directory.

Open a specific directory:

```bash
yazi ~/Projects
```

---

# Basic Navigation

Like Vim:

|Key|Action|
|---|---|
|j|Down|
|k|Up|
|h|Parent directory|
|l|Open directory/file|
|gg|Top|
|G|Bottom|
|q|Quit|
|Esc|Cancel|

---

# Open Files

Move to a file and press:

```
Enter
```

By default:

- Text files → Neovim
- Images → Image viewer
- PDFs → PDF viewer

---

# Create Files

Press:

```
a
```

Then enter:

```
notes.md
```

or

```
src
```

to create a folder.

---

# Rename

Select file and press:

```
r
```

Example:

```
todo.js
↓
todo.service.js
```

---

# Delete

Select file:

```
d
```

Confirm with:

```
y
```

---

# Copy and Paste

### Copy

```
yy
```

### Cut

```
dd
```

### Paste

```
pp
```

---

# Search Files

Press:

```
/
```

Type:

```
auth
```

Yazi filters instantly.

---

# Jump Around

Top:

```
gg
```

Bottom:

```
G
```

---

# Multi-select

Toggle selection:

```
Space
```

Select multiple files and:

```
yy
```

Copy them all.

---

# Show Hidden Files

Press:

```
.
```

You will see:

```
.env
.git
.config
```

---

# Preview Files

Move over:

```
README.md
```

Preview appears automatically.

Great for:

- Markdown
- Code
- JSON
- Images
- PDFs

---

# Open with Neovim

Select file:

```
Enter
```

or:

```bash
yazi
```

Choose:

```
server.js
```

Press Enter.

---

# Go Back

```
h
```

---

# Select Everything

```
v
```

---

# Search by Filename

Press:

```
f
```

Type:

```
todo
```

Jump immediately.

---

# Search Text Inside Files

Press:

```
s
```

Uses ripgrep.

Example:

Search:

```
JWT_SECRET
```

Finds all files containing it.

---

# Sort Files

Press:

```
,
```

Options:

- Name
- Size
- Modified
- Created

---

# Open Shell

Press:

```
:
```

Run commands:

```bash
git status
```

or

```bash
npm run dev
```

Return to Yazi afterward.

---

# Tabs

New tab:

```
t
```

Switch:

```
1
2
3
```

Close:

```
T
```

---

# Favorite Directories

Press:

```
m
```

Create bookmark:

```
p
```

for:

```
~/Projects
```

Jump later:

```
'
```

---

# Useful Operations

### Compress files

Select files:

```
Space
```

Then:

```
:
zip archive.zip *
```

---

### Move files

```
dd
```

Go elsewhere

```
pp
```

---

### Bulk rename

Select files:

```
v
```

Then:

```
:
```

Run:

```bash
vimv
```

---

# Image Preview (Kitty)

Since you're using Kitty, image preview works beautifully.

Move over:

```
wallpaper.jpg
```

Image appears on the right side.

---

# Recommended Keybindings to Remember

## Navigation

```
j k h l
gg
G
```

## Operations

```
yy   copy
dd   cut
pp   paste
r    rename
d    delete
```

## Search

```
/    search
f    find filename
s    grep content
```

## Display

```
.    hidden files
```

## Tabs

```
t
1-9
T
```

---

# Integrating with Your Tools

### Search content

Uses:

```
ripgrep
```

### Preview files

Uses:

```
bat
```

### Fuzzy search

Uses:

```
fzf
```

### Open editor

Uses:

```
Neovim
```

### Images

Uses Kitty protocol.

---

# Example MERN Workflow

### Open project

```bash
yazi ~/Projects/TodoBackend
```

Navigate:

```
src
controllers
auth.controller.js
```

Preview appears.

Press:

```
Enter
```

Neovim opens.

Search:

```
s
```

Type:

```
generateToken
```

Yazi uses ripgrep and shows matching files.

---

# Daily Terminal Stack

```
Yazi     → File manager
eza      → Better ls
fd       → Find files
fzf      → Fuzzy finder
ripgrep  → Search text
bat      → Preview files
zoxide   → Smart cd
lazygit  → Git UI
tmux     → Sessions
Neovim   → Editing
CopyQ    → Clipboard history
```

## Three commands you'll probably use most

```bash
yazi
yazi ~/Projects
yazi .
```

Once you get comfortable with `j k h l`, `yy dd pp`, `/`, and `s`, you'll find yourself using the mouse much less and navigating projects very quickly.

# Zoxide

You're already using the most common command:

```bash
z my_projects
```

That's great! `zoxide` is basically a **smarter `cd`**. It remembers where you go and learns your habits. The more you use it, the better it becomes.

---

# Basic Idea

Instead of:

```bash
cd ~/Projects/TodoBackend
```

you can simply type:

```bash
z todo
```

and zoxide jumps directly there.

---

# See Your Most Visited Directories

```bash
zoxide query -l
```

Example:

```
/home/rahul/Projects
/home/rahul/Projects/TodoBackend
/home/rahul/.config/nvim
/home/rahul/Documents
```

---

# Search Interactively (Highly Recommended)

If fzf integration is enabled, use:

```bash
zi
```

You'll get an interactive menu:

```
Projects/TodoBackend
Projects/StudyNotion
.config/nvim
Downloads
```

Type a few letters:

```
todo
```

Press Enter and you'll jump there.

---

# Jump to Neovim Config

Instead of:

```bash
cd ~/.config/nvim
```

use:

```bash
z nvim
```

---

# Jump to Projects Folder

Instead of:

```bash
cd ~/Projects
```

use:

```bash
z projects
```

---

# Multiple Keywords

Suppose:

```
~/Projects/TodoBackend
~/Projects/TodoFrontend
```

Then:

```bash
z todo back
```

or

```bash
z todo front
```

---

# Open and Edit Quickly

Go to project:

```bash
z todo
```

Open Neovim:

```bash
nvim .
```

or create an alias:

```bash
alias vz='z "$1" && nvim .'
```

Then:

```bash
vz todo
```

---

# List Matches

```bash
zoxide query -l todo
```

Output:

```
~/Projects/TodoBackend
~/Projects/TodoFrontend
```

---

# Remove a Directory

Suppose a project no longer exists:

```bash
zoxide remove ~/Projects/OldProject
```

---

# Add Directory Manually

```bash
zoxide add ~/Projects/MyApp
```

Usually unnecessary because zoxide learns automatically.

---

# Show Scores

```bash
zoxide query -ls
```

Example:

```
95.4  ~/Projects/TodoBackend
80.2  ~/.config/nvim
40.1  ~/Downloads
```

Higher score = more frequently used.

---

# Best Companion: fzf

Use:

```bash
zi
```

This is probably the nicest way to use zoxide.

You can type:

```
nvim
```

or

```
todo
```

and jump instantly.

---

# Useful Aliases

Add these to your `~/.zshrc`:

### Open project with Neovim

```bash
alias nv='zi && nvim .'
```

---

### Lazygit in selected project

```bash
alias lgz='zi && lazygit'
```

---

### Yazi in selected directory

```bash
alias yz='zi && yazi'
```

---

### Terminal in selected project

```bash
alias p='zi'
```

---

# Example Workflow

### Go to TodoBackend

```bash
z todo
```

### Open Yazi

```bash
yazi
```

### Open file in Neovim

```bash
nvim .
```

### Search code

```bash
rg generateToken
```

### Preview files

```bash
fd | fzf --preview 'bat --color=always {}'
```

### Git management

```bash
lazygit
```

---

# Commands Worth Memorizing

|Command|Purpose|
|---|---|
|`z keyword`|Jump to directory|
|`zi`|Interactive jump with fzf|
|`zoxide query -l`|List directories|
|`zoxide query -ls`|Show scores|
|`zoxide remove DIR`|Remove directory|
|`zoxide add DIR`|Add directory manually|

---

## My recommendation for your setup (Kitty + Zsh + Neovim + Yazi)

You will probably use these 90% of the time:

```bash
zi          # choose project
nvim .      # edit
yazi        # browse files
rg text     # search content
fd | fzf    # find files
lazygit     # git
```

This combination creates a very fast terminal-first workflow with almost no need for the mouse.

# CopyQ

Since you already open **CopyQ** with **Alt + W**, you can turn it into a very powerful clipboard manager. Think of it as a history of everything you copy (text, commands, code, links, images).

---

# Basic Workflow

### Copy anything normally

```
Ctrl + C
```

CopyQ automatically saves it.

Examples:

- URLs
- Code snippets
- Commands
- Notes
- Passwords (if not excluded)
- Images

---

# Open CopyQ

Your shortcut:

```
Alt + W
```

(Default is usually Ctrl + Shift + V)

---

# Essential Shortcuts

|Shortcut|Action|
|---|---|
|↑ ↓|Move through clipboard items|
|Enter|Paste selected item|
|Ctrl + F|Search clipboard history|
|Delete|Delete selected item|
|Ctrl + N|Create new item manually|
|F2|Edit item|
|Ctrl + E|Open editor|
|Ctrl + C|Copy selected item again|
|Ctrl + X|Cut selected item|
|Ctrl + Shift + C|Copy item content|
|Tab|Switch tabs|
|Esc|Hide CopyQ|

---

# Search Everything

Open:

```
Alt + W
```

Start typing:

```
express middleware
```

or

```
mongodb atlas
```

It instantly filters results.

Very useful for:

- DSA solutions
- Linux commands
- API URLs
- Git commands

---

# Pin Important Snippets

Right click item →

```
Pin
```

Pinned items stay forever and won't disappear.

Good for:

- MongoDB URI
- Github URLs
- Frequently used commands
- Resume links

---

# Create Tabs

Press:

```
F6
```

or

Menu → Tabs

Create:

### Commands

Contains:

```bash
lsd
btop
lazygit
tmux
```

---

### MERN

Contains:

```jsx
app.use(express.json())
```

```jsx
mongoose.connect()
```

etc.

---

### DSA

Store:

```python
Binary Search
DFS
BFS
Sliding Window
```

---

### Neovim

Store:

```
:w
:q
Lazy sync
Mason
```

---

# Star/Favorite Items

Right click →

```
Tag
```

or

Move to another tab.

Useful for things used every day.

---

# Edit Clipboard

Select item

Press:

```
F2
```

Change content without opening another editor.

---

# Multi-line Notes

Create new item:

```
Ctrl + N
```

Example:

```
Daily Tasks

✓ DSA
✓ Backend
✓ Neovim

Tomorrow:
- JWT
- Treesitter
```

---

# Save Terminal Commands

Create a tab:

```
Linux
```

Store:

```bash
sudo apt update
sudo apt upgrade

git add .
git commit -m ""
git push

npm install
npm run dev
```

Then:

1. Alt + W
2. Search
3. Enter

No need to memorize commands.

---

# Use Tags

Example tags:

```
#mern
#linux
#dsa
#python
#exam
```

Searching becomes easier.

---

# Best Productivity Setup

## Tabs

```
⭐ Favorites
🐧 Linux
⚛ MERN
📚 DSA
📝 Notes
🌐 URLs
🔑 Secrets
```

---

# Ignore Password Managers

Go to:

```
File → Preferences → Items
```

Exclude:

- Bitwarden
- Browser password fields

Avoid storing sensitive passwords.

---

# Useful Commands to Know

## Show CopyQ

Since you use:

```
Alt + W
```

Open → search → Enter

---

## Clear history

```
Ctrl + Delete
```

---

## Move item up/down

```
Ctrl + Shift + Up
Ctrl + Shift + Down
```

---

## Export clipboard

Menu:

```
File → Export
```

Save notes to a file.

---

# Productivity Workflow for a MERN + Linux Developer

### While coding

Copy:

- Error message
- API endpoint
- Mongo query
- StackOverflow solution

CopyQ remembers all.

Later:

```
Alt + W
↓
Enter
```

and paste instantly.

---

# Recommended Tabs for You

```
⭐ Favorite
🐧 Linux Commands
⚛ MERN Snippets
🌿 Git Commands
💻 Neovim
📚 DSA Templates
🌐 Important URLs
📝 Quick Notes
```

### My favorite habit:

Treat CopyQ as your **second brain**. Instead of memorizing commands, snippets, and URLs, save them once and retrieve them with:

```
Alt + W → Type → Enter
```

This is one of the biggest productivity boosts for terminal-first developers.

# fzf

**`fzf` is actually working correctly**.

When you run:

```bash
fd -t d | fzf
```

`fzf` is **only a fuzzy finder**. It prints the selected result to **stdout**. It **does not change your current directory**.

That's why you see:

```
Downloads/
```

or

```
Desktop/DSA Practice/
```

instead of your shell moving there.

---

## Option 1: Change directory after selecting (recommended)

Use command substitution:

```bash
cd "$(fd -t d | fzf)"
```

or

```bash
cd "$(find . -type d | fzf)"
```

Now selecting

```
Desktop/DSA Practice
```

will execute

```bash
cd "Desktop/DSA Practice"
```

---

## Option 2: Create a `cdf` function

Add this to your `~/.zshrc`:

```bash
cdf() {
    local dir
    dir=$(fd --type d --hidden --follow --exclude .git | fzf) || return
    cd "$dir"
}
```

Reload:

```bash
source ~/.zshrc
```

Now simply run

```bash
cdf
```

Choose a directory and you'll immediately be inside it.

---

## Option 3: Use zoxide (best experience)

Since I remember you're using **zoxide**, you can combine it with `fzf`.

```bash
zi
```

or

```bash
zoxide query -i
```

After selecting, it automatically jumps to the directory.

---

## Option 4: Open the selected file in Neovim

For files:

```bash
nvim "$(fd -t f | fzf)"
```

For directories:

```bash
cd "$(fd -t d | fzf)"
```

---

## If you want the same behavior as Yazi

You can define:

```bash
cf() {
    local file
    file=$(fd --type f --hidden --follow --exclude .git | fzf) || return
    nvim "$file"
}

cdf() {
    local dir
    dir=$(fd --type d --hidden --follow --exclude .git | fzf) || return
    cd "$dir"
}
```

Then:

```bash
cf     # opens selected file in nvim
cdf    # changes to selected directory
```

---

### One question:

When you type **only**:

```bash
fzf
```

what behavior do you expect?

- **A.** Jump to the selected directory (`cd`)?
- **B.** Open the selected file in Neovim?
- **C.** Just print the path (default `fzf` behavior)?

Knowing this will help me suggest the cleanest setup for your workflow.

Since you're using Linux Mint, Kitty, Zsh, and terminal-first tools, `fzf` can become one of your most useful productivity tools. Think of it as a **super-fast search and selection tool** for files, commands, processes, directories, Git branches, and much more.

---

# What is fzf?

`fzf` = **Fuzzy Finder**

It lets you search things by typing only a few letters.

For example, typing:

```
init
```

can match:

```
init.lua
my_init_config.lua
```

---

# 1. Search Command History

Press:

```
Ctrl + R
```

Start typing:

```
docker
```

You'll see all commands containing "docker".

Example:

```bash
docker ps
docker compose up
docker logs app
```

Press **Enter** to run the selected command.

This alone saves tons of time.

---

# 2. Search Files

Run:

```bash
fzf
```

It shows all files in the current directory.

Type:

```
todo
```

Select:

```
todo.service.js
```

Press Enter.

---

# 3. Open Files with Neovim

```bash
nvim $(fzf)
```

Choose:

```
server.js
```

Neovim opens it immediately.

---

# Better:

Add this alias:

```bash
alias vf='nvim $(fzf)'
```

Now just type:

```bash
vf
```

Select file → opened in Neovim.

---

# 4. Search Directories

If you have `fd` installed:

```bash
fd -t d | fzf
```

Example:

```
Downloads
Documents
Projects
```

Select one.

---

# Jump Into Directory

Add:

```bash
alias cdf='cd $(fd -t d | fzf)'
```

Then:

```bash
cdf
```

Choose:

```
Projects/StudyNotion
```

You instantly enter that directory.

---

# 5. Search Git Branches

```bash
git branch | fzf
```

Choose:

```
feature/auth
```

Switch:

```bash
git checkout $(git branch | fzf)
```

---

Create alias:

```bash
alias gco='git checkout $(git branch | fzf)'
```

---

# 6. Search Running Processes

```bash
ps aux | fzf
```

Find:

```
node
```

Kill it:

```bash
kill PID
```

---

# 7. Search Installed Packages

```bash
apt list --installed | fzf
```

Search:

```
kitty
neovim
tmux
```

---

# 8. Search Files and Preview Them

Install bat if not already:

```bash
sudo apt install bat
```

Then:

```bash
fzf --preview 'bat --color=always {}'
```

Select:

```
main.js
```

Right side shows file content.

Very useful.

---

# 9. Search with Ripgrep

Find text inside files:

```bash
rg express | fzf
```

Find:

```jsx
app.use(express.json())
```

---

# 10. Search Git Commits

```bash
git log --oneline | fzf
```

Example:

```
Add JWT authentication
Fix MongoDB bug
```

---

# 11. Search Docker Containers

```bash
docker ps | fzf
```

Select container.

---

# 12. Search SSH Hosts

```bash
cat ~/.ssh/config | fzf
```

Quickly connect to servers.

---

# 13. Fuzzy Find Files in Neovim

Inside Neovim:

```
:Telescope find_files
```

or if using Snacks:

```
<leader><space>
```

Similar idea to fzf.

---

# Essential Keyboard Shortcuts

### Ctrl + R

Search command history.

### Ctrl + T

Insert filename into command line.

Example:

Start typing:

```bash
cp
```

Press:

```
Ctrl + T
```

Select:

```
resume.pdf
```

Result:

```bash
cp resume.pdf
```

---

### Alt + C

Jump directories.

Example:

Press:

```
Alt + C
```

Choose:

```
Projects
```

Automatically cd there.

---

# Amazing Aliases

Add to `~/.zshrc`

### Open file in nvim

```bash
alias vf='nvim $(fzf)'
```

---

### Change directory

```bash
alias cdf='cd $(fd -t d | fzf)'
```

---

### Kill process

```bash
alias fkill='kill -9 $(ps -ef | sed 1d | fzf | awk "{print \$2}")'
```

---

### Git branch switch

```bash
alias gco='git checkout $(git branch | sed "s/* //" | fzf)'
```

---

### Open project

```bash
alias proj='cd $(find ~/Projects -type d -maxdepth 1 | fzf)'
```

---

# Combine with zoxide (Highly Recommended)

If you already have zoxide:

```bash
zoxide query -l | fzf
```

or

```bash
zi
```

This gives a fuzzy search of frequently used folders.

---

# My recommended workflow for you

### Open project

```bash
zi
```

↓

Choose project

↓

```bash
nvim .
```

↓

Inside Neovim:

```
<leader><space>
```

Find files

↓

Terminal history:

```
Ctrl+R
```

↓

Clipboard:

```
Alt+W
```

(CopyQ)

---

## Tools working together

```
CopyQ        → clipboard memory
fzf          → search anything
zoxide       → jump directories
bat          → preview files
ripgrep (rg) → search text
lazygit      → git UI
tmux         → session manager
Neovim       → editing
```

This combination is used by many terminal-first developers because it removes a lot of repetitive typing and mouse usage.

# ripgrep

`ripgrep (rg)` is one of the most useful tools for developers. Think of it as **"Ctrl + F for your entire project"**, but extremely fast.

Since you're doing MERN, Neovim, and terminal-first development, you'll probably use `rg` every day.

---

# What is ripgrep?

Instead of manually opening files and searching, you can search all files instantly.

Suppose you want to find:

```jsx
express.json()
```

Just run:

```bash
rg "express.json"
```

Output:

```
server.js
15:app.use(express.json())

app.js
8:app.use(express.json())
```

---

# Basic Syntax

```bash
rg PATTERN
```

Example:

```bash
rg "mongoose"
```

Finds all occurrences of "mongoose" in the current directory.

---

# Search Case Insensitively

```bash
rg -i "jwt"
```

Matches:

```
JWT
jwt
Jwt
```

---

# Search Specific File Type

### Search only JavaScript files

```bash
rg "axios" -g "*.js"
```

### Search only Python files

```bash
rg "binary_search" -g "*.py"
```

### Search React files

```bash
rg "useEffect" -g "*.jsx"
```

---

# Show Line Numbers

```bash
rg -n "middleware"
```

Example:

```
auth.js
34:app.use(authMiddleware)
```

---

# Search Multiple Words

```bash
rg "token|cookie"
```

Finds both:

- token
- cookie

---

# Count Matches

```bash
rg "TODO" -c
```

Output:

```
app.js:4
server.js:2
```

---

# Search a Specific Folder

```bash
rg "express" src/
```

or

```bash
rg "jwt" backend/
```

---

# List Files Containing a Match

```bash
rg -l "mongoose"
```

Output:

```
models/user.js
config/db.js
server.js
```

---

# Show Files WITHOUT Match

```bash
rg -L "TODO"
```

---

# Search Hidden Files

```bash
rg "API_KEY" --hidden
```

Useful for:

- `.env`
- `.gitignore`

---

# Include node_modules

Normally ignored.

```bash
rg "axios" node_modules/
```

or

```bash
rg "axios" --no-ignore
```

---

# Search TODO Comments

```bash
rg "TODO"
```

Output:

```
controllers/user.js
14:// TODO: Add validation

routes/auth.js
8:// TODO: Refresh token
```

---

# Search Function Names

Find:

```jsx
createTodo
```

```bash
rg "createTodo"
```

Output:

```
todo.controller.js
todo.service.js
todo.repository.js
```

Very useful for understanding codebases.

---

# Search Environment Variables

```bash
rg "MONGO_URI"
```

or

```bash
rg "JWT_SECRET"
```

---

# Search Imports

```bash
rg "useState"
```

```bash
rg "express"
```

```bash
rg "axios"
```

---

# Use with fzf (Highly Recommended)

Search:

```bash
rg "middleware"
```

Pipe into fzf:

```bash
rg "middleware" | fzf
```

Choose result interactively.

---

# Open Selected Result in Neovim

```bash
nvim $(rg "middleware" -l | fzf)
```

Search:

```
middleware
```

Choose:

```
authMiddleware.js
```

Opens immediately.

---

# Search Images

```bash
rg ".png"
```

---

# Find Duplicate API Endpoints

```bash
rg "/login"
```

Output:

```
routes/auth.js
controllers/auth.js
frontend/api.js
```

---

# Search React Components

```bash
rg "Navbar"
```

---

# Search CSS Classes

```bash
rg "container"
```

---

# Search Errors

Copy error:

```
MongoServerSelectionError
```

Then:

```bash
rg "MongoServerSelectionError"
```

Find where you handled it.

---

# Useful Flags

|Command|Meaning|
|---|---|
|rg text|Search text|
|rg -i text|Ignore case|
|rg -n text|Show line numbers|
|rg -l text|Show file names only|
|rg -c text|Count matches|
|rg -g "*.js" text|Search only JS files|
|rg --hidden text|Include hidden files|
|rg --no-ignore text|Ignore .gitignore rules|

---

# Useful Aliases

Put in `~/.zshrc`

### Search anything

```bash
alias r='rg'
```

Then:

```bash
r "mongoose"
```

---

### Search and open with nvim

```bash
alias rv='nvim $(rg -l "" | fzf)'
```

---

### Interactive grep

```bash
alias rf='rg "" | fzf'
```

---

### Find TODOs

```bash
alias todo='rg "TODO|FIXME"'
```

---

# Workflow for MERN Development

### Find API route

```bash
rg "/login"
```

↓

Find controller

```bash
rg "loginUser"
```

↓

Find service

```bash
rg "generateToken"
```

↓

Open file

```bash
nvim $(rg "generateToken" -l | fzf)
```

---

## Tools That Work Together

```
rg        → search inside files
fzf       → interactive selection
bat       → preview content
zoxide    → jump directories
lazygit   → Git management
CopyQ     → clipboard history
Neovim    → editing
tmux      → sessions
```

This combination forms a powerful terminal-first workflow and can greatly reduce mouse usage and repetitive typing.

`fdfind` (`fd`) is like a modern replacement for the old `find` command. It's much simpler, faster, and works beautifully with `fzf`, `ripgrep`, `bat`, and Neovim.

Since you're a terminal-first developer, `fd` is one of those tools you'll use daily.

---

# Check Installation

On Ubuntu/Debian/Mint, the package is usually installed as:

```bash
fdfind
```

Check:

```bash
fdfind --version
```

Many people create an alias:

```bash
alias fd=fdfind
```

Add it to `~/.zshrc`:

```bash
echo 'alias fd=fdfind' >> ~/.zshrc
source ~/.zshrc
```

Then you can simply use:

```bash
fd
```

---

# Why Use fd Instead of find?

Traditional:

```bash
find . -name "*.js"
```

With fd:

```bash
fd .js
```

Much easier.

---

# Find All Files

```bash
fd
```

Example:

```
server.js
app.js
package.json
todo.service.js
```

---

# Find by Name

Search for files containing "todo":

```bash
fd todo
```

Output:

```
todo.controller.js
todo.service.js
todo.repository.js
```

---

# Find Specific Extension

Find JavaScript files:

```bash
fd -e js
```

Python:

```bash
fd -e py
```

Markdown:

```bash
fd -e md
```

---

# Find Directories Only

```bash
fd -t d
```

Example:

```
src
controllers
models
routes
```

---

# Find Files Only

```bash
fd -t f
```

---

# Search Inside src Folder

```bash
fd auth src/
```

---

# Find Hidden Files

Normally hidden files are ignored.

```bash
fd -H
```

Find `.env`:

```bash
fd -H .env
```

Output:

```
.env
.env.example
```

---

# Include Ignored Files

```bash
fd -I
```

Includes:

- node_modules
- .git

---

# Find Multiple Extensions

```bash
fd -e js -e jsx
```

---

# Execute Commands on Results

Delete all `.log` files:

```bash
fd -e log -x rm {}
```

Here:

```
{}
```

represents each found file.

---

# Open with Neovim

```bash
fd | fzf | xargs nvim
```

Choose a file and open immediately.

---

# Preview Files with bat

```bash
fd | fzf --preview 'bat --color=always {}'
```

Very useful.

---

# Find Directories and cd

```bash
cd $(fd -t d | fzf)
```

Choose:

```
Projects
StudyNotion
TodoBackend
```

Automatically enter it.

---

# Find Images

```bash
fd -e png
```

or

```bash
fd -e jpg
```

---

# Find Config Files

```bash
fd init.lua
```

```bash
fd package.json
```

```bash
fd .env
```

---

# Find Markdown Notes

```bash
fd -e md
```

Output:

```
README.md
notes.md
linux.md
```

---

# Find Large Projects

```bash
fd package.json ~/Projects
```

Shows all Node projects.

---

# Find Git Repositories

```bash
fd .git -t d ~/Projects
```

Output:

```
StudyNotion/.git
TodoBackend/.git
Blogify/.git
```

---

# Find React Components

```bash
fd Navbar
```

or

```bash
fd -e jsx
```

---

# Use with ripgrep

Find JS files:

```bash
fd -e js
```

Search inside them:

```bash
rg express $(fd -e js)
```

---

# Useful Aliases

Add to `~/.zshrc`

### Open files in Neovim

```bash
alias vf='fd | fzf | xargs nvim'
```

Use:

```bash
vf
```

---

### Change directory

```bash
alias cdf='cd $(fd -t d | fzf)'
```

---

### Find package.json

```bash
alias npmproj='fd package.json'
```

---

### Find .env

```bash
alias envf='fd -H .env'
```

---

### Search markdown notes

```bash
alias notes='fd -e md'
```

---

# Workflow Example

### Open a project

```bash
cd ~/Projects
```

### Find service files

```bash
fd service
```

Output:

```
todo.service.js
user.service.js
```

### Search function

```bash
rg createTodo
```

### Open file

```bash
fd service | fzf | xargs nvim
```

---

# My Most Used Commands

```bash
fd                      # all files
fd todo                 # files containing "todo"
fd -e js                # javascript files
fd -t d                 # directories only
fd -H .env              # hidden files
fd | fzf                # interactive file picker
fd | fzf --preview 'bat --color=always {}'
fd | fzf | xargs nvim   # open in neovim
```

---

## Terminal Productivity Stack

```
fd        → find files/directories
rg        → search text inside files
fzf       → interactive selection
bat       → preview files
zoxide    → jump directories
lazygit   → Git UI
CopyQ     → clipboard history
Neovim    → editing
tmux      → sessions
```

These tools complement each other very well and create a fast terminal workflow with very little mouse usage.

# eza

`eza` (formerly `exa`) is a modern replacement for `ls`. It adds colors, icons, Git status, tree view, and better file information. Since you're using Linux Mint + Kitty + Nerd Fonts + terminal-first tools, `eza` is a great productivity tool.

---

# 1. Basic Usage

Instead of:

```bash
ls
```

Use:

```bash
eza
```

Example output:

```
README.md
package.json
src
public
node_modules
```

---

# 2. Long Listing

Like `ls -l`:

```bash
eza -l
```

Shows:

- Permissions
- Owner
- Size
- Date

Example:

```
drwxr-xr-x  src
-rw-r--r--  package.json
```

---

# 3. Show Hidden Files

```bash
eza -la
```

Equivalent to:

```bash
ls -la
```

You'll see:

```
.git
.env
.zshrc
.config
```

---

# 4. Show Icons

Since you use Nerd Fonts:

```bash
eza --icons
```

Example:

```
📄 README.md
📦 package.json
📁 src
📁 public
```

---

# 5. Tree View ⭐

Very useful for projects:

```bash
eza --tree
```

Output:

```
.
├── src
│   ├── controllers
│   ├── routes
│   └── models
├── package.json
└── README.md
```

Limit depth:

```bash
eza --tree --level=2
```

---

# 6. Show Git Status

Inside a Git repository:

```bash
eza -l --git
```

Example:

```
M app.js
A auth.js
```

Where:

- `M` = modified
- `A` = added
- `?` = untracked

---

# 7. Sort by Newest

```bash
eza -l --sort=modified
```

Useful for seeing recently changed files.

---

# 8. Sort by Size

```bash
eza -l --sort=size
```

Largest files first.

---

# 9. Reverse Order

```bash
eza -lr
```

---

# 10. Show Directories Only

```bash
eza -D
```

Example:

```
src
controllers
routes
models
```

---

# 11. Recursive Listing

```bash
eza -R
```

Lists everything recursively.

---

# 12. Tree With Git Status

```bash
eza --tree --git-ignore
```

Ignores:

- node_modules
- .git

Very useful in large projects.

---

# 13. Show File Sizes Nicely

```bash
eza -lh
```

Example:

```
2.3K package.json
4.8M video.mp4
```

---

# Useful Aliases

Add these to `~/.zshrc`:

### Replace ls

```bash
alias ls='eza --icons'
```

---

### Long listing

```bash
alias ll='eza -lah --icons'
```

---

### Tree view

```bash
alias lt='eza --tree --level=2 --icons'
```

---

### Directories only

```bash
alias ld='eza -D'
```

---

### Git status

```bash
alias lg='eza -lah --git --icons'
```

---

### Recent files

```bash
alias recent='eza -lah --sort=modified'
```

---

# Combine With Other Tools

## Find file and open with Neovim

```bash
fd | fzf | xargs nvim
```

## Search text

```bash
rg "express"
```

## Show project tree

```bash
eza --tree --level=2 --icons
```

## Jump directory

```bash
zoxide query -l | fzf
```

---

# Example MERN Workflow

### See project structure

```bash
lt
```

Output:

```
src
├── controllers
├── middleware
├── routes
├── services
└── models
```

### Search for JWT

```bash
rg JWT_SECRET
```

### Find a file

```bash
fd auth
```

### Open file

```bash
fd auth | fzf | xargs nvim
```

### Check Git changes

```bash
lg
```

---

# My Most Used Aliases

Put these in `~/.zshrc`:

```bash
alias ls='eza --icons'
alias ll='eza -lah --icons'
alias lt='eza --tree --level=2 --icons'
alias lg='eza -lah --git --icons'
alias recent='eza -lah --sort=modified'
```

---

# Terminal Productivity Stack

|Tool|Purpose|
|---|---|
|`eza`|Better `ls`|
|`fd`|Find files|
|`rg`|Search inside files|
|`fzf`|Interactive selection|
|`bat`|Better cat with syntax highlighting|
|`zoxide`|Smart cd|
|`lazygit`|Git UI|
|`tmux`|Session manager|
|`CopyQ`|Clipboard history|
|`Neovim`|Editing|

This combination gives you a very fast terminal-first workflow and eliminates much of the need for the mouse.

# bat

`bat` is one of those tools that quickly becomes hard to live without. Think of it as **`cat` with superpowers**:

- Syntax highlighting
- Line numbers
- Git modifications
- Paging like `less`
- Works beautifully with `fzf`, `fd`, and `ripgrep`

---

# Check Installation

```bash
bat --version
```

On Ubuntu/Mint, the command may be:

```bash
batcat --version
```

If so, create an alias:

```bash
echo "alias bat='batcat'" >> ~/.zshrc
source ~/.zshrc
```

---

# Basic Usage

Instead of:

```bash
cat app.js
```

Use:

```bash
bat app.js
```

You'll see:

- Syntax highlighting
- Line numbers
- Header with filename

---

# View Multiple Files

```bash
bat package.json app.js
```

---

# Show File with Line Numbers

```bash
bat server.js
```

Example:

```jsx
1 const express = require('express')
2 const app = express()
3 app.use(express.json())
```

---

# View Markdown Nicely

```bash
bat README.md
```

Markdown is rendered beautifully.

---

# Show Without Header

Default:

```bash
bat app.js
```

Without header:

```bash
bat --style=plain app.js
```

---

# Show Specific Lines

```bash
bat app.js --line-range 20:40
```

Displays only lines 20-40.

---

# Use as a Pager

Instead of:

```bash
man git
```

Try:

```bash
MANPAGER="bat" man git
```

Much prettier.

---

# Search + Preview with fzf ⭐

```bash
fd | fzf --preview 'bat --color=always {}'
```

Left side:

```
app.js
server.js
package.json
```

Right side:

Shows file contents instantly.

This is one of the most useful combinations.

---

# Open Selected File in Neovim

```bash
fd | fzf --preview 'bat --color=always {}' | xargs nvim
```

---

# Preview Ripgrep Results

Search:

```bash
rg express
```

Open matching files:

```bash
rg express -l | fzf --preview 'bat --color=always {}'
```

---

# Show Hidden Files

```bash
bat .env
```

Great for:

- `.env`
- `.gitignore`
- `.zshrc`

---

# Show JSON Beautifully

```bash
bat package.json
```

Instead of ugly:

```json
{"name":"app","version":"1.0.0"}
```

You'll get colored formatting.

---

# View Logs

```bash
bat server.log
```

---

# Follow Logs (tail equivalent)

```bash
tail -f server.log
```

or combine:

```bash
tail -f server.log | bat
```

---

# Compare Files

Use with diff:

```bash
git diff | bat
```

Very useful.

---

# Git Integration

Show modified code:

```bash
git show | bat
```

---

# Useful Aliases

Put these in `~/.zshrc`

### Replace cat

```bash
alias cat='bat'
```

---

### Pretty JSON

```bash
alias json='bat package.json'
```

---

### Preview files interactively

```bash
alias preview='fzf --preview "bat --color=always {}"'
```

---

### Open file in Neovim

```bash
alias vf='fd | fzf --preview "bat --color=always {}" | xargs nvim'
```

---

### Browse projects

```bash
alias files='fd | fzf --preview "bat --color=always {}"'
```

---

# Combine with Other Tools

## fd + bat

Find JS files:

```bash
fd -e js
```

Preview one:

```bash
fd -e js | fzf --preview 'bat --color=always {}'
```

---

## rg + bat

Search:

```bash
rg JWT_SECRET
```

Preview:

```bash
rg JWT_SECRET -l | fzf --preview 'bat --color=always {}'
```

---

## eza + bat

See files:

```bash
eza --icons
```

Read one:

```bash
bat server.js
```

---

## CopyQ + bat

Copy code from CopyQ, then inspect file with:

```bash
bat app.js
```

---

# Daily Workflow Example

### See project tree

```bash
eza --tree --level=2
```

### Find file

```bash
fd auth
```

### Search code

```bash
rg generateToken
```

### Preview result

```bash
rg generateToken -l | fzf --preview 'bat --color=always {}'
```

### Open selected file

```bash
fd | fzf --preview 'bat --color=always {}' | xargs nvim
```

---

# My Most Used Commands

```bash
bat app.js
bat README.md
bat .env
fd | fzf --preview 'bat --color=always {}'
rg express -l | fzf --preview 'bat --color=always {}'
git diff | bat
```

---

# Terminal Productivity Stack

```
eza     → better ls
fd      → find files
rg      → search text
fzf     → fuzzy search
bat     → preview files
zoxide  → smart cd
lazygit → Git UI
tmux    → sessions
CopyQ   → clipboard history
Neovim  → editing
```

## The three combinations you'll probably use the most

### 1. Find + Preview + Open

```bash
fd | fzf --preview 'bat --color=always {}' | xargs nvim
```

### 2. Search text + Preview

```bash
rg express -l | fzf --preview 'bat --color=always {}'
```

### 3. Search command history

```
Ctrl + R
```

Together, these tools can make your terminal feel like a fast IDE.