After looking at your Neovim setup, I think the problem is not that you don't have enough shortcuts.

The problem is that your shortcuts are spread across **three navigation systems**:

1. Neovim windows (`sh`, `sj`, `sk`, `sl`)
2. Telescope (`;f`, `;r`, `\\`)
3. NvimTree (`<leader>e`)
4. tmux panes (`Prefix + h/j/k/l`)

As a result, you're constantly asking:

> "Am I navigating files, windows, tabs, buffers, or tmux panes?"

That slows you down.

---

# What I would keep

These are already good.

## File Search

```
;f
```

Find files.

Use this 90% of the time.

---

## Text Search

```
;r
```

Search text in the entire project.

Examples:

```
;r -> useAuth
;r -> axios
;r -> Dashboard
```

This is one of the most powerful shortcuts you have.

---

## Buffers

```
\\
```

Switch between currently open files.

---

## File Tree

```
Space e
```

Open project tree.

---

# What I would add

Add these to your `keymaps.lua`.

## Recently Opened Files

```lua
vim.keymap.set("n", ";o", function()
  require("telescope.builtin").oldfiles()
end, { desc = "Recent files" })
```

Now:

```
;o
```

Shows recently opened files.

This becomes your "go back where I was" key.

---

## Search Current Buffer

```lua
vim.keymap.set("n", ";b", function()
  require("telescope.builtin").current_buffer_fuzzy_find()
end)
```

Now:

```
;b
```

Search inside current file only.

Very useful in React components.

---

## Project Symbols

```lua
vim.keymap.set("n", ";p", function()
  require("telescope.builtin").lsp_document_symbols()
end)
```

Now:

```
;p
```

Jump to:

```
functions
components
interfaces
hooks
types
```

inside current file.

---

# React Navigation Workflow

When working on MERN projects:

### Open file

```
;f
```

Type:

```
Navbar
Dashboard
Login
```

---

### Search code

```
;r
```

Type:

```
handleSubmit
axios
useAuth
```

---

### Search current component

```
;b
```

Type:

```
handleSubmit
useEffect
```

---

### Jump to function

```
;p
```

---

### Return to recent file

```
;o
```

---

# Remove Tabs From Your Workflow

Currently you have:

```
te
Tab
Shift+Tab
tw
```

Honestly, as a React developer, I would barely use tabs.

Use:

```
Buffers
+
Telescope
```

instead.

Most modern Neovim users spend their day in:

```
;f
;r
\\
```

and rarely touch tabs.

---

# Make NvimTree More Useful

Add:

```lua
vim.keymap.set("n", "<leader>f", ":NvimTreeFindFile<CR>")
```

Now:

```
Space f
```

reveals the current file in the tree.

Very helpful when exploring unfamiliar projects.

---

# Your Daily Navigation Cheat Sheet

If I were learning with your setup, I would memorize only these:

```
;f      Find file
;r      Search project text
\\       Open buffers
;o      Recent files
;b      Search current file
;p      Symbols in file

Space e Open file tree
Space f Reveal current file

sh sj sk sl   Move windows

Prefix+h/j/k/l  Move tmux panes
```

The biggest improvement for you will not come from adding 50 more shortcuts. It will come from building the habit:

```
Need file?      -> ;f
Need code?      -> ;r
Need open file? -> \\
Need recent?    -> ;o
Need tree?      -> Space e
```

Once those 5–6 keys become muscle memory, navigating even a large React codebase becomes much faster.

This is actually where many new Neovim users struggle.

You have **three ways** to create files and folders:

## Method 1: NvimTree (Recommended)

Open the file tree:

```
Space e
```

Navigate to the folder.

### Create File

Press:

```
a
```

Then type:

```
components/Navbar.jsx
```

or

```
src/pages/Login.jsx
```

Press Enter.

NvimTree will automatically create the file.

---

### Create Folder

Press:

```
a
```

Then type:

```
components
```

and end with a slash:

```
components/
```

Press Enter.

Folder created.

---

### Rename

Select file:

```
r
```

---

### Delete

Select file:

```
d
```

---

### Copy

Select file:

```
c
```

---

### Cut / Move

Select file:

```
x
```

Then navigate elsewhere and:

```
p
```

---

## Method 2: Telescope + Oil (if installed)

I didn't see Oil.nvim in your config.

So ignore this for now.

---

## Method 3: Terminal (Most Powerful)

Since you're learning Linux and terminal-first development, I strongly recommend learning these.

### Create Folder

```bash
mkdir components
```

### Create Nested Folders

```bash
mkdir -p src/components/ui
```

### Create File

```bash
touch Navbar.jsx
```

### Create Multiple Files

```bash
touch Login.jsx Signup.jsx Dashboard.jsx
```

### Create React Structure

```bash
mkdir -p src/components
mkdir -p src/pages
mkdir -p src/hooks
mkdir -p src/context

touch src/pages/Home.jsx
touch src/pages/Login.jsx
touch src/components/Navbar.jsx
```

---

# What Senior Developers Usually Do

For a React project:

### Open terminal

```
Ctrl+`
```

or tmux pane.

### Create structure

```bash
mkdir -p src/components
mkdir -p src/pages
mkdir -p src/hooks
```

### Open file

```
;f
```

Type:

```
Navbar
```

Press Enter.

Start coding.

---

# My Recommendation

For you:

### Files/Folders

Use terminal:

```bash
mkdir
touch
mv
rm
```

because you're already learning Linux.

### Navigation

Use:

```
;f
```

for finding files.

### Project Exploration

Use:

```
Space e
```

for NvimTree.

A typical workflow would look like:

```bash
mkdir -p src/components
touch src/components/Navbar.jsx
```

Then in Neovim:

```
;f
Navbar
```

Enter.

This is usually faster than manually clicking through folders in a tree.

The most important thing to understand is:

```
File ≠ Buffer ≠ Window ≠ Tab ≠ tmux Pane
```

Many beginners mix these up.

---

# 1. Close Current File (Buffer)

Try:

```
:bd
```

(Buffer Delete)

This closes the current file but keeps Neovim running.

---

If your config mapping exists:

```
Space q
```

it may close the current window.

---

# 2. Switch Between Open Files

You currently have multiple files open:

```
App.jsx
index.html
package.json
App.css
```

### Next file

```
:bn
```

(Buffer Next)

### Previous file

```
:bp
```

(Buffer Previous)

---

A better setup would be:

```lua
vim.keymap.set("n", "<Tab>", ":bnext<CR>")
vim.keymap.set("n", "<S-Tab>", ":bprevious<CR>")
```

Then:

```
Tab
Shift+Tab
```

switch files instantly.

---

# 3. See All Open Files

You already have:

```
\\
```

This opens Telescope Buffers.

Super useful.

---

# 4. Open Another File

Use:

```
;f
```

Search:

```
Navbar
Home
Login
```

Press Enter.

This is how most Neovim users navigate projects.

---

# 5. Close ALL Files

```
:bufdo bd
```

or

```
:qa
```

Quit all.

---

# 6. Split Screen

### Vertical split

```
:vsplit
```

or your mapping:

```
sv
```

---

### Horizontal split

```
:split
```

or

```
ss
```

---

# 7. Move Between Splits

You already have:

```
sh
sj
sk
sl
```

Think:

```
h ←
j ↓
k ↑
l →
```

---

# 8. Resize Splits

Native:

```
Ctrl+w >
Ctrl+w <
Ctrl+w +
Ctrl+w -
```

---

# 9. NvimTree Navigation

When cursor is in the tree:

```
Enter      Open
a          Create
r          Rename
d          Delete
x          Cut
c          Copy
p          Paste
R          Refresh
```

---

# 10. Reveal Current File In Tree

Add this:

```lua
vim.keymap.set("n", "<leader>f", ":NvimTreeFindFile<CR>")
```

Then:

```
Space f
```

shows where current file lives.

Very useful.

---

# 11. React Developer Daily Workflow

What I would do:

### Open project

```
Space e
```

---

### Find file

```
;f
```

---

### Search code

```
;r
```

---

### Switch open files

```
\\
```

---

### Close file

```
:bd
```

---

### Move between splits

```
sh sj sk sl
```

---

# The 10 Commands I'd Memorize First

```
Space e   Toggle tree

;f        Find file
;r        Search text

\\         Open buffers

:bd       Close current file

sv        Vertical split
ss        Horizontal split

sh        Left split
sj        Down split
sk        Up split
sl        Right split
```

If you're coming from VS Code, the biggest mindset change is:

```
Don't browse folders.
Search files.
```

In a React project with 100+ files, experienced Neovim users usually open files with `;f` much more often than they navigate the tree. The tree is mainly for creating, moving, and understanding project structure.

Absolutely. And I think you're at the perfect stage for this.

Your biggest limitation is **not React, TypeScript, or MERN**.

It's:

```
Finding things
Moving around
Managing files
Managing terminals
Understanding codebases
```

Senior developers don't type faster. They **navigate faster**.

---

# Week 1 Goal

By the end of this week you should be able to:

```
Open any file in < 2 seconds
Jump to any function in < 2 seconds
Search any text in project in < 3 seconds
Switch files without Explorer
Use terminal without leaving Neovim
```

No mouse.

---

# Day 1-2: Telescope Mastery

Forget every Telescope feature.

Learn only these.

## Find Files

Open:

```
;f
```

(or whatever key you mapped)

Practice:

```
Find App.jsx
Find AuthContext.jsx
Find package.json
Find vite.config.js
```

Don't use file explorer.

Challenge:

```
Open 20 files using Telescope only
```

---

## Live Grep

Search text across project.

```
;g
```

(or your mapping)

Search:

```
useState
useEffect
axios
login
register
```

This is how senior developers find code.

Not by clicking folders.

---

## Find Current Buffer

```
;/
```

Search inside current file.

Practice:

```
Find all functions
Find specific variable
Find imports
```

---

# Day 3: LSP Navigation

This is where the magic happens.

Create a React project.

Whenever you see:

```jsx
<LoginForm />
```

Use:

```
gd
```

Go Definition.

Instantly opens:

```jsx
LoginForm.jsx
```

---

When you see:

```jsx
loginUser()
```

Use:

```
gd
```

Jump to implementation.

---

When you don't know what something does:

```
K
```

Shows documentation.

---

Find everywhere something is used:

```
gr
```

Example:

```jsx
createUser
```

Shows:

```
auth.js
userController.js
signup.jsx
```

This is one of the most powerful features in Neovim.

---

# Day 4: Buffers

Most beginners keep opening and closing files.

Pros don't.

---

Open:

```
App.jsx
Navbar.jsx
Login.jsx
Register.jsx
AuthContext.jsx
```

Now you have 5 buffers.

Switch:

```
Shift+l
Shift+h
```

(or your mappings)

Practice until it feels natural.

---

Rule:

```
Never close file after reading it.
Keep it in buffer.
Jump between buffers.
```

---

# Day 5: Splits

Learn exactly 4 commands.

Create horizontal split:

```
ss
```

Create vertical split:

```
sv
```

Move:

```
sh
sj
sk
sl
```

Practice:

```
Left: Login.jsx
Right: AuthContext.jsx
```

Read both simultaneously.

This is huge for MERN projects.

---

# Day 6: Toggleterm Workflow

Stop opening external terminals.

---

Terminal 1:

```bash
npm run dev
```

---

Terminal 2:

```bash
npm run server
```

---

Terminal 3:

```bash
git status
```

---

Typical day:

```
Code
Run app
Check git
Commit
Push
```

Never leave Neovim.

---

# Day 7: LazyGit

This will replace:

```bash
git add .
git commit
git push
```

for many tasks.

Open:

```
:LazyGit
```

Practice:

### Stage file

```
Space
```

### Commit

```
c
```

### Push

```
P
```

### Pull

```
p
```

### View history

```
Enter
```

---

# Daily Exercise (15 minutes)

Open your Blogify project.

Without mouse:

### Task 1

Find:

```
Login page
```

using Telescope.

---

### Task 2

Jump to:

```
AuthContext
```

using `gd`.

---

### Task 3

Search:

```
axios
```

using Live Grep.

---

### Task 4

Open:

```
Login.jsx
AuthContext.jsx
```

in vertical splits.

---

### Task 5

Run:

```bash
npm run dev
```

inside Toggleterm.

---

### Task 6

Open LazyGit.

View recent commits.

---

# Final Goal

After 2-3 weeks, your workflow should look like:

```
Open project
↓
Telescope file search
↓
gd to jump through code
↓
gr to find usages
↓
Split windows to compare files
↓
Toggleterm to run app
↓
LazyGit to commit
↓
Never touch mouse
```

That's the workflow used by many experienced Neovim developers, and it's much more valuable than installing another 20 plugins.

Perfect. Let's add **Trouble.nvim** properly.

## Step 1: Create a new plugin file

Create:

```
~/.config/nvim/lua/plugins/trouble.lua
```

Paste:

```lua
return {
  {
    "folke/trouble.nvim",
    dependencies = {
      "nvim-tree/nvim-web-devicons",
    },
    opts = {},
  },
}
```

---

## Step 2: Add useful keymaps

Open:

```
~/.config/nvim/lua/config/keymaps.lua
```

Add:

```lua
vim.keymap.set(
  "n",
  "<leader>xx",
  "<cmd>Trouble diagnostics toggle<CR>",
  { desc = "Diagnostics (Trouble)" }
)

vim.keymap.set(
  "n",
  "<leader>xw",
  "<cmd>Trouble diagnostics toggle filter.buf=0<CR>",
  { desc = "Buffer Diagnostics" }
)

vim.keymap.set(
  "n",
  "<leader>xr",
  "<cmd>Trouble lsp_references toggle<CR>",
  { desc = "LSP References" }
)

vim.keymap.set(
  "n",
  "<leader>xd",
  "<cmd>Trouble lsp_definitions toggle<CR>",
  { desc = "Definitions" }
)
```

---

## Step 3: Install

Inside Neovim:

```
:Lazy sync
```

Wait until installation completes.

---

## Step 4: Test

Open a React or TypeScript project.

Intentionally create an error:

```tsx
const name: string = 123
```

Now press:

```
<leader>xx
```

You should get a VS Code-like Problems panel showing:

```
Type 'number' is not assignable to type 'string'
```

---

## My recommended shortcuts

You'll use these daily:

|Shortcut|Purpose|
|---|---|
|`<leader>xx`|All project errors|
|`<leader>xw`|Current file errors|
|`<leader>xr`|Find references|
|`gd`|Go definition|
|`gr`|Find references (quick)|
|`K`|Hover docs|

---

## Next plugin after Trouble

After you confirm Trouble works, the next thing I would add is:

```
ThePrimeagen/harpoon
```

because you've repeatedly mentioned that you're struggling with file navigation.

Harpoon + Telescope is usually the point where Neovim starts feeling dramatically faster than VS Code for large React projects.

Nothing bad happens. Harpoon and Telescope solve **different problems** and work extremely well together.

Think of it like this:

### Telescope = Search Engine

When you don't know where a file is:

```
AuthContext.jsx
UserProfile.jsx
Dashboard.jsx
```

you use Telescope:

```
;f
```

Search:

```
auth
```

and open the file.

This is like Google.

---

### Harpoon = Favorites Bar

When you already know which files you use constantly:

```
App.jsx
AuthContext.jsx
Login.jsx
Register.jsx
Navbar.jsx
```

you add them to Harpoon once.

Then jump instantly:

```
1 -> App.jsx
2 -> AuthContext.jsx
3 -> Login.jsx
4 -> Register.jsx
5 -> Navbar.jsx
```

No searching.

This is like browser bookmarks.

---

## Real MERN Example

Let's say you're building authentication.

You constantly switch between:

```
frontend/src/pages/Login.jsx
frontend/src/context/AuthContext.jsx
frontend/src/services/auth.js
backend/controllers/authController.js
backend/routes/authRoutes.js
```

### Without Harpoon

Every time:

```
;f
auth
Enter
```

Search again.

Search again.

Search again.

---

### With Harpoon

Once:

```
Add Login.jsx
Add AuthContext.jsx
Add auth.js
Add authController.js
Add authRoutes.js
```

Then:

```
1
2
3
4
5
```

Instant jumps.

---

## What I use Telescope for

Things I don't visit often:

```
vite.config.js
package.json
README.md
Dockerfile
.env.example
```

Search them when needed.

---

## What I use Harpoon for

Files I'm actively editing today:

```
Current feature files
Current bug files
Current API files
```

---

## If I were you

I'd learn in this order:

```
1. Telescope
2. Buffers
3. Splits
4. LazyGit
5. ToggleTerm
6. Harpoon
```

Because right now you're still building your navigation habits.

Once you're comfortable with Telescope, Harpoon becomes amazing.

If you install Harpoon today, you'll probably use it like:

```
1 -> App.jsx
2 -> AuthContext.jsx
3 -> Login.jsx
4 -> Register.jsx
```

and keep Telescope for everything else.

That's actually how many React and Next.js developers use Neovim. Telescope finds files; Harpoon jumps between the handful of files you're actively working on.

Since you're using **LazyVim**, let's install the **new Harpoon 2** version.

---

# Step 1: Create plugin file

Create:

```
~/.config/nvim/lua/plugins/harpoon.lua
```

Paste:

```lua
return {
  {
    "ThePrimeagen/harpoon",
    branch = "harpoon2",
    dependencies = {
      "nvim-lua/plenary.nvim",
    },
    config = function()
      local harpoon = require("harpoon")

      harpoon:setup()
    end,
  },
}
```

---

# Step 2: Add keymaps

Open:

```
~/.config/nvim/lua/config/keymaps.lua
```

Add:

```lua
local harpoon = require("harpoon")

-- Add current file
vim.keymap.set("n", "<leader>a", function()
  harpoon:list():add()
end, { desc = "Harpoon Add File" })

-- Toggle menu
vim.keymap.set("n", "<C-e>", function()
  harpoon.ui:toggle_quick_menu(harpoon:list())
end, { desc = "Harpoon Menu" })

-- Jump to files
vim.keymap.set("n", "<leader>1", function()
  harpoon:list():select(1)
end)

vim.keymap.set("n", "<leader>2", function()
  harpoon:list():select(2)
end)

vim.keymap.set("n", "<leader>3", function()
  harpoon:list():select(3)
end)

vim.keymap.set("n", "<leader>4", function()
  harpoon:list():select(4)
end)

vim.keymap.set("n", "<leader>5", function()
  harpoon:list():select(5)
end)
```

---

# Step 3: Install

Inside Neovim:

```
:Lazy sync
```

Restart Neovim.

---

# Step 4: Test

Open:

```
App.jsx
Login.jsx
Register.jsx
AuthContext.jsx
```

For each file:

```
<leader>a
```

to add it.

---

Open the Harpoon menu:

```
Ctrl + e
```

You'll see:

```
1 App.jsx
2 Login.jsx
3 Register.jsx
4 AuthContext.jsx
```

---

Jump instantly:

```
<leader>1
<leader>2
<leader>3
<leader>4
```

---

# My recommended MERN workflow

During authentication feature development:

```
1 -> Login.jsx
2 -> Register.jsx
3 -> AuthContext.jsx
4 -> authService.js
5 -> authController.js
```

Then:

```
<leader>1
<leader>5
<leader>2
<leader>4
```

No Telescope search needed.

---

# Even Better (My Favorite)

Add these keymaps too:

```lua
vim.keymap.set("n", "<C-S-P>", function()
  harpoon:list():prev()
end)

vim.keymap.set("n", "<C-S-N>", function()
  harpoon:list():next()
end)
```

Now you can cycle through your working files like browser tabs.

---

After installing, send me your current `keymaps.lua`, and I'll help organize all your shortcuts (Telescope, Harpoon, Trouble, ToggleTerm, Splits, Buffers) into a clean system that's easy to remember.

This is exactly the right question.

Most people learn Neovim like this:

```
Install plugin
Install plugin
Install plugin
Install plugin
```

But experienced developers learn:

```
Navigation
Navigation
Navigation
Navigation
```

Let's turn these into skills you can practice every day.

---

# Stage 1: Telescope Mastery (The Search Brain)

Goal:

```
Never open a file tree.
```

---

## Skill 1: Find Files

Practice for 5 minutes.

Open your MERN project.

Then find:

```
App.jsx
package.json
AuthContext.jsx
Login.jsx
vite.config.js
```

using Telescope only.

Challenge:

```
Do not touch Explorer.
Do not use mouse.
```

After 2-3 days you'll know file names better than folder structures.

---

## Skill 2: Live Grep

Search project-wide.

Examples:

```
axios
useEffect
login
register
JWT
```

Imagine:

```
User reports login bug
```

Don't open folders.

Use:

```
Live Grep → "login"
```

and jump directly.

This is how senior developers debug.

---

## Skill 3: Search Current Buffer

Inside a 500-line file:

Search:

```
handleSubmit
fetchData
useEffect
```

instead of scrolling.

---

# Stage 2: Buffer Mastery

Most beginners:

```
Open file
Read
Close file
Open another file
```

Slow.

---

Think of buffers as:

```
Open tabs in browser
```

Keep them alive.

---

Example:

Open:

```
Login.jsx
Register.jsx
Navbar.jsx
AuthContext.jsx
```

Now cycle:

```
Next Buffer
Previous Buffer
```

without reopening anything.

---

Exercise:

Keep 10 files open.

Navigate only through buffers.

Do not use Telescope.

---

# Stage 3: Split Mastery

This is where productivity jumps.

---

Example:

Left:

```
AuthContext.jsx
```

Right:

```
Login.jsx
```

---

You can read:

```
login()
```

and

```
AuthContext
```

simultaneously.

---

Practice:

## Vertical Split

```
Login.jsx
|
AuthContext.jsx
```

---

## Horizontal Split

```
Controller
------------
Route
```

---

Exercise:

Build authentication with:

```
Frontend left
Backend right
```

---

Navigate:

```
sh
sj
sk
sl
```

until your fingers stop thinking.

---

# Stage 4: Harpoon Mastery

This is NOT a file finder.

Telescope finds.

Harpoon remembers.

---

Imagine today you're working on:

```
Login.jsx
Register.jsx
AuthContext.jsx
authService.js
authController.js
```

Add all 5 to Harpoon.

---

Now stop using Telescope.

Use:

```
Next
Previous
Menu
```

only.

---

Exercise:

Add 5 files.

For 30 minutes:

```
No Telescope.
Only Harpoon.
```

You'll understand the difference immediately.

---

# Stage 5: Combine Everything

This is the real workflow.

---

Need a new file?

```
Telescope
```

---

Need to revisit a working file?

```
Harpoon
```

---

Need to compare files?

```
Split
```

---

Need to move among open files?

```
Buffers
```

---

# Real MERN Example

Suppose you're building login.

### Find file

```
Telescope → Login.jsx
```

---

### Add to Harpoon

```
Login.jsx
AuthContext.jsx
authService.js
authController.js
```

---

### Open split

```
Login.jsx | AuthContext.jsx
```

---

### Cycle

```
Harpoon Next
Harpoon Previous
```

---

### Keep buffers alive

```
10-15 files open
```

No closing.

---

# 7-Day Challenge

### Day 1

Only Telescope.

No file tree.

---

### Day 2

Only Telescope + Buffers.

---

### Day 3

Only Splits.

---

### Day 4

Harpoon.

---

### Day 5

Telescope + Harpoon.

---

### Day 6

Telescope + Harpoon + Splits.

---

### Day 7

Build a small feature:

```
Login
Signup
Forgot Password
```

using:

- Telescope
- Buffers
- Splits
- Harpoon

without touching the mouse.

---

After one week, you'll stop thinking:

```
Where is this file?
```

and start thinking:

```
What do I want to change?
```

That's when Neovim starts feeling fast instead of complicated.