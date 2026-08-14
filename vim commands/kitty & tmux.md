For your MERN workflow, I'd suggest:

### Window 1 (Development)

```
Ctrl+a c
```

Open a new tmux window.

Inside:

```
┌───────────────────────────────┬─────────────┐
│                               │ npm run dev │
│                               ├─────────────┤
│            nvim               │ mongosh     │
│                               └─────────────┘
└───────────────────────────────┘
```

Commands:

```
nvim
npm run dev
mongosh
```

---

### Window 2 (Git)

```
Ctrl+a c
```

Run:

```
lazygit
```

---

### Window 3 (API Testing)

```
nvim requests/auth.http
```

Run Kulala requests there.

---

### Most important tmux commands

```
Ctrl+a c   New window
Ctrl+a n   Next window
Ctrl+a p   Previous window
Ctrl+a ,   Rename window

Ctrl+a v   Vertical split
Ctrl+a s   Horizontal split

Ctrl+a h   Move left
Ctrl+a j   Move down
Ctrl+a k   Move up
Ctrl+a l   Move right

Ctrl+a x   Kill pane
Ctrl+a d   Detach tmux
```

---

One thing I'd like you to try right now:

1. Start tmux
2. Press `Ctrl+a c`
3. Do you see a second window appear in the bottom status bar?

If yes, your tmux setup is

You're thinking about it the wrong way.

With tmux, **tmux becomes your workspace**, not Neovim.

You do **not** do this:

```
Terminal 1
└── nvim

Terminal 2
└── tmux
    ├── npm run dev
    ├── mongosh
    └── lazygit
```

Instead, you do this:

```
Terminal
└── tmux
    ├── nvim
    ├── npm run dev
    ├── mongosh
    └── lazygit
```

Only **one terminal window** is needed.

---

### What it looks like

Open terminal:

```bash
tmux
```

Create 4 panes.

Then:

```
┌─────────────────────┬─────────────────────┐
│                     │                     │
│       nvim          │    npm run dev      │
│                     │                     │
├─────────────────────┼─────────────────────┤
│                     │                     │
│      mongosh        │      lazygit        │
│                     │                     │
└─────────────────────┴─────────────────────┘
```

Neovim is only running in the **top-left pane**.

The other panes are normal terminals.

---

### What most Neovim users do

Most terminal-first developers keep Neovim in one large pane and the rest smaller:

```
┌───────────────────────────────┬───────────┐
│                               │           │
│                               │ npm dev   │
│                               ├───────────┤
│            nvim               │ mongosh   │
│                               ├───────────┤
│                               │ lazygit   │
│                               │           │
└───────────────────────────────┴───────────┘
```

This is much more practical.

---

### Can I have 4 panes INSIDE Neovim?

Yes, but that's a different thing.

Inside Neovim:

```
:vsplit
:split
```

creates windows:

```
┌──────────┬──────────┐
│ file1    │ file2    │
├──────────┼──────────┤
│ file3    │ terminal │
└──────────┴──────────┘
```

These are **Neovim windows**, not tmux panes.

You can even open terminals inside Neovim:

```
:terminal
```

or

```lua
vim.cmd("terminal")
```

---

### What I recommend for you

Since you're still getting comfortable with Neovim:

**Use tmux for terminals.**

```
tmux
├── nvim
├── npm run dev
├── mongosh
└── lazygit
```

**Use Neovim splits for files.**

```
nvim
├── routes/user.js
├── controller/user.js
├── requests/auth.http
└── schema/user.js
```

This separation is exactly how many backend and MERN developers work:

- tmux manages programs
- Neovim manages files

Once you're comfortable, we can make a single command like:

```bash
mern
```

that automatically opens your project, launches tmux, starts the server, opens mongosh, and loads Neovim in the correct directory. That's where tmux starts feeling really powerful.

Absolutely. Once you get comfortable with tmux, you'll wonder how you worked without it.

For a MERN project, I would start with a **simple 4-pane layout**.

```
┌─────────────────────┬─────────────────────┐
│                     │                     │
│      Neovim         │    npm run dev      │
│                     │                     │
├─────────────────────┼─────────────────────┤
│                     │                     │
│      mongosh        │      lazygit        │
│                     │                     │
└─────────────────────┴─────────────────────┘
```

---

# Step 1: Start tmux

Open terminal:

```bash
tmux
```

---

# Step 2: Create Right Split

Press:

```
Ctrl+a |
```

(Your `.tmux.conf` likely uses `Ctrl+a` as prefix.)

You now have:

```
┌────────────┬────────────┐
│            │            │
│            │            │
└────────────┴────────────┘
```

---

# Step 3: Create Bottom Split on Left

Move to left pane:

```
Ctrl+a ←
```

Then:

```
Ctrl+a -
```

Now:

```
┌────────────┬────────────┐
│            │            │
├────────────┤            │
│            │            │
└────────────┴────────────┘
```

---

# Step 4: Create Bottom Split on Right

Move right:

```
Ctrl+a →
```

Then:

```
Ctrl+a -
```

Result:

```
┌────────────┬────────────┐
│            │            │
├────────────┼────────────┤
│            │            │
└────────────┴────────────┘
```

Perfect.

---

# Step 5: Run Commands

### Pane 1

```bash
nvim
```

### Pane 2

```bash
npm run dev
```

### Pane 3

```bash
mongosh
```

### Pane 4

```bash
lazygit
```

---

# Pane Navigation

Move around:

```
Ctrl+a h
Ctrl+a j
Ctrl+a k
Ctrl+a l
```

or

```
Ctrl+a ←
Ctrl+a ↓
Ctrl+a ↑
Ctrl+a →
```

depending on your config.

Check your `.tmux.conf` if you're unsure.

---

# Resize Panes

Usually:

```
Ctrl+a H
Ctrl+a J
Ctrl+a K
Ctrl+a L
```

or

```
Ctrl+a Ctrl+Arrow
```

depending on mappings.

---

# Create New Window

Think of a window as another workspace.

```
Ctrl+a c
```

Example:

```
Window 1 → MERN Project
Window 2 → DSA Practice
Window 3 → Notes
```

---

# Switch Windows

Next:

```
Ctrl+a n
```

Previous:

```
Ctrl+a p
```

Direct:

```
Ctrl+a 1
Ctrl+a 2
Ctrl+a 3
```

---

# Save Your Session

Install the tmux plugins:

- [tmux-resurrect](https://github.com/tmux-plugins/tmux-resurrect?utm_source=chatgpt.com)
- [tmux-continuum](https://github.com/tmux-plugins/tmux-continuum?utm_source=chatgpt.com)

Then tmux can restore:

- windows
- pane layout
- running commands
- working directories

After a reboot:

```bash
tmux attach
```

and everything comes back.

---

# My Recommended MERN Workflow

### Window 1 — Development

```
nvim        | npm run dev
------------+------------
mongosh     | lazygit
```

### Window 2 — Documentation

```
browser-like terminal tools
curl
notes
```

### Window 3 — Testing

```
nvim requests/*.http
```

Run Kulala requests from here.

---

# Bonus: Open Everything Automatically

Create a script:

```bash
mkdir -p ~/.local/bin
nvim ~/.local/bin/mern
```

```bash
#!/bin/bash

cd ~/Projects/my-app || exit

tmux new-session -d -s mern

tmux send-keys -t mern "nvim" C-m

tmux split-window -h
tmux send-keys "npm run dev" C-m

tmux select-pane -L
tmux split-window -v
tmux send-keys "mongosh" C-m

tmux select-pane -R
tmux split-window -v
tmux send-keys "lazygit" C-m

tmux attach -t mern
```

Make executable:

```bash
chmod +x ~/.local/bin/mern
```

Now every time you start a project:

```bash
mern
```

and your entire MERN workspace appears instantly with Neovim, server logs, MongoDB shell, and Git UI already running. This is a huge productivity boost for a terminal-first developer.

Based on the Kitty config you're using, here's the cheat sheet I'd keep nearby for a few days.

# Kitty Cheat Sheet

## Tabs

|Action|Keybinding|
|---|---|
|New Tab|`Ctrl + Shift + T`|
|Close Tab|`Ctrl + Shift + W`|
|Previous Tab|`Alt + ,`|
|Next Tab|`Alt + .`|
|Go to Tab 1|`Alt + 1`|
|Go to Tab 2|`Alt + 2`|
|Go to Tab 3|`Alt + 3`|
|Go to Tab 4|`Alt + 4`|
|Go to Tab 5|`Alt + 5`|

### MERN Workflow

```
Alt+1 → Neovim
Alt+2 → npm run dev
Alt+3 → mongosh
Alt+4 → lazygit
```

---

# Splits

## Create Splits

|Action|Keybinding|
|---|---|
|Vertical Split|`Alt + V`|
|Horizontal Split|`Alt + S`|

### Example

```
Current
┌──────────┐
│ Terminal │
└──────────┘
```

`Alt + V`

```
┌──────┬──────┐
│      │      │
└──────┴──────┘
```

`Alt + S`

```
┌──────────┐
│          │
├──────────┤
│          │
└──────────┘
```

---

# Split Navigation

Same as Vim and Neovim.

|Move|Keybinding|
|---|---|
|Left|`Alt + H`|
|Down|`Alt + J`|
|Up|`Alt + K`|
|Right|`Alt + L`|

### Memory Trick

```
h ←
j ↓
k ↑
l →
```

---

# Resize Splits

|Action|Keybinding|
|---|---|
|Narrower|`Alt + Shift + H`|
|Wider|`Alt + Shift + L`|
|Shorter|`Alt + Shift + J`|
|Taller|`Alt + Shift + K`|

---

# Clipboard

|Action|Keybinding|
|---|---|
|Copy|`Ctrl + Shift + C`|
|Paste|`Ctrl + Shift + V`|

---

# Utilities

|Action|Keybinding|
|---|---|
|Open URL Hint Mode|`F7`|

When you press `F7`, Kitty highlights all URLs on screen and lets you open one.

---

# Quick Launches

|Action|Keybinding|
|---|---|
|Open Neovim|`F2`|
|Open Lazygit|`F3`|
|Open Mongosh|`F4`|

---

# Font Size

|Action|Keybinding|
|---|---|
|Increase Font|`Ctrl + =`|
|Decrease Font|`Ctrl + -`|
|Reset Font|`Ctrl + 0`|

---

# Recommended MERN Layout

```
Tab 1 → Neovim
Tab 2 → npm run dev
Tab 3 → mongosh
Tab 4 → lazygit
```

Daily navigation:

```
Alt+1
Alt+2
Alt+3
Alt+4
```

You rarely need to touch the mouse.

---

# The 10 Shortcuts You'll Use 90% of the Time

```
Ctrl+Shift+T   New Tab
Ctrl+Shift+W   Close Tab

Alt+1          Neovim
Alt+2          Server
Alt+3          MongoDB
Alt+4          Lazygit

Alt+,          Previous Tab
Alt+.          Next Tab

Alt+V          Vertical Split
Alt+S          Horizontal Split

Alt+H/J/K/L    Move Between Splits
```

If you memorize just those 10 shortcuts, you'll be productive in Kitty very quickly.

This is one of the most important things to understand as a terminal-first developer.

People often think **Kitty and tmux compete**, but they actually solve different problems.

### Rename Current Tab

```
kitty @ set-tab-title"Neovim"
```

Example:

```
kitty @ set-tab-title"Server"
kitty @ set-tab-title"MongoDB"
kitty @ set-tab-title"Lazygit"
```

---

### Rename a Specific Tab

First list tabs:

```
kitty @ls
```

You'll see JSON output containing tab IDs.

Then:

```
kitty @ set-tab-title--match id:3"MongoDB"
```

---

### Temporary Shortcut

If you're on your Server tab:

```
kitty @ set-tab-title"Server"
```

and the tab title changes immediately.

---

### Automatic Naming (My Favorite)

Instead of manually renaming tabs every time, add aliases to your `.zshrc`:

```
aliasnv='kitty @ set-tab-title "Neovim" && nvim'
aliaslg='kitty @ set-tab-title "Lazygit" && lazygit'
aliasmongo='kitty @ set-tab-title "MongoDB" && mongosh'
aliasserver='kitty @ set-tab-title "Server"'
```

Usage:

```
nv
```

opens Neovim and names the tab:

```
Neovim
```

or:

```
mongo
```

starts mongosh and names the tab:

```
MongoDB
```

---

# Simple Explanation

## Kitty = Terminal Emulator

Kitty is the application you launch from your desktop.

```
Linux Desktop
    ↓
Kitty
```

Its job:

- Display terminal windows
- Render text
- Show colors
- Handle fonts
- Create tabs
- Create splits

Examples of terminal emulators:

- Kitty
- Alacritty
- Ghostty
- WezTerm
- GNOME Terminal

---

## tmux = Terminal Multiplexer

tmux runs **inside** Kitty.

```
Linux Desktop
    ↓
Kitty
    ↓
tmux
    ↓
zsh
    ↓
nvim
```

Its job:

- Manage terminal sessions
- Create panes
- Create windows
- Keep processes running
- Restore sessions

---

# Visual Example

## Kitty Only

```
Kitty
├── Tab 1: nvim
├── Tab 2: npm run dev
├── Tab 3: mongosh
└── Tab 4: lazygit
```

Close Kitty:

```
Everything dies.
```

---

## Kitty + tmux

```
Kitty
└── tmux
    ├── Window 1: nvim
    ├── Window 2: npm run dev
    ├── Window 3: mongosh
    └── Window 4: lazygit
```

Close Kitty:

```
tmux keeps running.
```

Reopen Kitty:

```bash
tmux attach
```

Everything comes back.

---

# Biggest Difference

## Kitty

If you accidentally close the window:

```
nvim      ❌
server    ❌
mongosh   ❌
lazygit   ❌
```

Everything is gone.

---

## tmux

If you accidentally close the window:

```
nvim      ✅
server    ✅
mongosh   ✅
lazygit   ✅
```

Everything is still running.

---

# Why Backend Developers Love tmux

Imagine:

```bash
npm run dev
```

Server has been running for:

```
2 hours
```

You accidentally close Kitty.

### Without tmux

```
Server stopped.
```

### With tmux

```
Server still running.
```

Reconnect:

```bash
tmux attach
```

and continue.

---

# What Kitty Does Better

Kitty has:

### Better Fonts

```
✓ Nerd Fonts
✓ Ligatures
✓ Transparency
✓ Blur
✓ Themes
```

### Better Graphics

```
✓ Images
✓ Unicode
✓ Performance
```

### Better Mouse Support

```
✓ Drag
✓ Scroll
✓ Click
```

tmux is not designed for these.

---

# What tmux Does Better

### Persistent Sessions

```
tmux attach
```

### Session Restore

```
tmux-resurrect
tmux-continuum
```

### SSH Workflows

```
Laptop
    ↓ SSH
Remote Server
    ↓
tmux
```

Disconnect internet?

```
Process continues running.
```

Reconnect later.

---

# For Your Current Situation

You're learning:

- Neovim
- MERN
- Git
- MongoDB
- Linux

At this stage, I'd use:

```
Kitty Tabs
├── Neovim
├── npm run dev
├── mongosh
└── lazygit
```

because it's simpler.

---

# When to Start Using tmux

Use tmux when you start thinking:

```
I want sessions to survive terminal closes.

I want to reconnect later.

I want automatic workspace restoration.

I want SSH workflows.
```

---

# My Recommendation for You

### Today

```
Kitty
├── Tab 1 → Neovim
├── Tab 2 → npm run dev
├── Tab 3 → mongosh
└── Tab 4 → lazygit
```

### 2–3 Months Later

```
Kitty
└── tmux
    ├── Neovim
    ├── npm run dev
    ├── mongosh
    └── lazygit
```

Learn Neovim first. Then tmux will make much more sense and feel genuinely useful rather than just another tool to configure.