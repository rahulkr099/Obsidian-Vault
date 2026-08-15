Your keymaps are actually good, but they're mixed together. I'd organize them into sections so future-you can find things quickly.

Here's the same keymaps grouped by purpose.

---

## Core Setup

```lua
local keymap = vim.keymap
local opts = { noremap = true, silent = true }
```

---

# Basic Editing

```lua
-- Delete character without copying to register
keymap.set("n", "x", '"_x')

-- Increment / Decrement number under cursor
keymap.set("n", "+", "<C-a>")
keymap.set("n", "-", "<C-x>")

-- Select entire file
keymap.set("n", "<C-a>", "gg<S-v>G")

-- Exit insert mode quickly
keymap.set("i", "jk", "<Esc>")
keymap.set("i", "kj", "<Esc>")
```

---

# Save & Quit

```lua
keymap.set("n", "<Leader>w", ":update<Return>", opts)
keymap.set("n", "<Leader>q", ":quit<Return>", opts)
keymap.set("n", "<Leader>Q", ":qa<Return>", opts)
```

### Cheatsheet

```
<leader>w   Save file
<leader>q   Quit current file
<leader>Q   Quit all
```

---

# File Explorer (NvimTree)

```lua
keymap.set("n", "<Leader>e", ":NvimTreeToggle<Return>", opts)
keymap.set("n", "<Leader>E", ":NvimTreeFindFile<Return>", opts)

keymap.set("n", "<leader>f", ":NvimTreeFindFile<CR>")
```

### Cheatsheet

```
<leader>e   Toggle file tree
<leader>E   Find current file in tree
<leader>f   Focus current file in tree
```

---

# Tabs

```lua
keymap.set("n", "te", ":tabedit ")
keymap.set("n", "<tab>", ":tabnext<Return>", opts)
keymap.set("n", "<s-tab>", ":tabprev<Return>", opts)
keymap.set("n", "tw", ":tabclose<Return>", opts)
```

### Cheatsheet

```
te          New tab
Tab         Next tab
Shift+Tab   Previous tab
tw          Close tab
```

---

# Buffers

```lua
vim.keymap.set("n", "<Tab>", ":bnext<CR>")
vim.keymap.set("n", "<S-Tab>", ":bprevious<CR>")
```

### Note

You currently use:

```lua
<Tab>
<S-Tab>
```

for BOTH tabs and buffers.

The buffer mappings override the tab mappings.

So the earlier tab mappings are effectively unused.

I would keep only buffers.

```
Tab         Next buffer
Shift+Tab   Previous buffer
```

---

# Splits & Windows

```lua
keymap.set("n", "ss", ":split<CR>", opts)
keymap.set("n", "sv", ":vsplit<CR>", opts)

keymap.set("n", "sh", "<C-w>h")
keymap.set("n", "sj", "<C-w>j")
keymap.set("n", "sk", "<C-w>k")
keymap.set("n", "sl", "<C-w>l")
```

### Cheatsheet

```
ss          Horizontal split
sv          Vertical split

sh          Move left
sj          Move down
sk          Move up
sl          Move right
```

---

# Resize Windows

```lua
keymap.set("n", "<C-S-h>", "<C-w><")
keymap.set("n", "<C-S-l>", "<C-w>>")
keymap.set("n", "<C-S-k>", "<C-w>+")
keymap.set("n", "<C-S-j>", "<C-w>-")
```

### Cheatsheet

```
Ctrl+Shift+h   Narrower
Ctrl+Shift+l   Wider
Ctrl+Shift+k   Taller
Ctrl+Shift+j   Shorter
```

---

# Visual Mode Helpers

```lua
keymap.set("v", "J", ":m '>+1<CR>gv=gv", opts)
keymap.set("v", "K", ":m '<-2<CR>gv=gv", opts)
```

### Cheatsheet

```
Visual + J    Move selection down
Visual + K    Move selection up
```

Useful for:

- React JSX
- Tailwind classes
- Reordering code

---

# Search Navigation

```lua
keymap.set("n", "<C-d>", "<C-d>zz")
keymap.set("n", "<C-u>", "<C-u>zz")

keymap.set("n", "n", "nzzzv")
keymap.set("n", "N", "Nzzzv")

keymap.set("n", "<Esc>", ":nohl<CR>", opts)
```

### Cheatsheet

```
Ctrl+d    Half page down (center cursor)
Ctrl+u    Half page up (center cursor)

n         Next search result
N         Previous search result

Esc       Clear search highlight
```

---

# Clipboard

```lua
keymap.set({ "n", "v" }, "<Leader>y", '"+y', opts)
keymap.set("n", "<Leader>Y", '"+Y', opts)
```

### Cheatsheet

```
<leader>y   Copy selection
<leader>Y   Copy whole line
```

Copies to system clipboard.

---

# Telescope

```lua
vim.keymap.set("n", ";o", function()
  require("telescope.builtin").oldfiles()
end)

vim.keymap.set("n", ";b", function()
  require("telescope.builtin").current_buffer_fuzzy_find()
end)

vim.keymap.set("n", ";p", function()
  require("telescope.builtin").lsp_document_symbols()
end)
```

### Cheatsheet

```
;o      Recent files
;b      Search current file
;p      Symbols in current file
```

---

# LSP

```lua
keymap.set("n", "<C-j>", function()
  vim.diagnostic.goto_next()
end, opts)

keymap.set("n", "<C-S-i>", function()
  vim.lsp.buf.format({ async = true })
end)
```

### Cheatsheet

```
Ctrl+j         Next diagnostic
Ctrl+Shift+i   Format file
```

---

# Lazygit

```lua
keymap.set(
  "n",
  "<Leader>g",
  "<cmd>lua _LAZYGIT_TOGGLE()<CR>",
  { desc = "Lazygit", noremap = true, silent = true }
)
```

### Cheatsheet

```
<leader>g   Open Lazygit
```

---

# Trouble

```lua
<leader>xx
<leader>xw
<leader>xr
<leader>xd
```

### Cheatsheet

```
<leader>xx   All diagnostics
<leader>xw   Buffer diagnostics
<leader>xr   References
<leader>xd   Definitions
```

---

# Harpoon

```lua
<leader>a
<C-e>

<leader>1
<leader>2
<leader>3
<leader>4
<leader>5
```

### Cheatsheet

```
<leader>a   Add file

Ctrl+e      Harpoon menu

<leader>1   File 1
<leader>2   File 2
<leader>3   File 3
<leader>4   File 4
<leader>5   File 5
```

---

# Debugger (DAP)

```lua
F5
F10
F11
F12

<leader>db
<leader>dc
<leader>dr
<leader>du
```

### Cheatsheet

```
F5          Continue
F10         Step Over
F11         Step Into
F12         Step Out

<leader>db  Breakpoint
<leader>dc  Continue
<leader>dr  REPL
<leader>du  Debug UI
```

---

# Kulala (HTTP Client)

```lua
<leader>hr
<leader>hn
<leader>hp
```

### Cheatsheet

```
<leader>hr   Run request
<leader>hn   Next request
<leader>hp   Previous request
```

For `.http` files:

```
GET <http://localhost:5000/api/users>
```

then:

```
<leader>hr
```

to send the request.

---

# The 15 Keys You'll Use Most

```
<leader>w     Save

<leader>e     Explorer

Tab           Next buffer
Shift+Tab     Previous buffer

ss            Split
sv            VSplit

sh sj sk sl   Move windows

;o            Recent files

<leader>g     Lazygit

<leader>a     Harpoon add
Ctrl+e        Harpoon menu

<leader>1-5   Harpoon jump

<leader>hr    Run API request
```

These are the ones you'll likely use every day while building MERN projects.

Absolutely. The shortcut names alone don't make much sense until you see a real workflow.

---

# 1. GitSigns

Imagine you committed this file:

```jsx
function login() {
  console.log("login");
}
```

Later you change it:

```jsx
function login() {
  console.log("user login");
}
```

GitSigns shows a marker in the gutter.

---

## `]h` → Next Git change

Suppose:

```jsx
10 function login() {
11   console.log("user login");
12 }
13
14 function logout() {
15   console.log("logout");
16 }
```

and lines 11 and 15 are modified.

Cursor is on line 1.

Press:

```
]h
```

Cursor jumps to line 11.

Press again:

```
]h
```

Cursor jumps to line 15.

---

## `[h` → Previous Git change

If you're on line 15:

```
[h
```

Cursor jumps back to line 11.

---

## `<leader>hp` → Preview Hunk

Suppose line 11 changed.

Cursor on line 11.

Press:

```
<leader>hp
```

Remember:

```
leader = Space
```

So:

```
Space h p
```

Popup:

```diff
- console.log("login");
+ console.log("user login");
```

Very useful before committing.

---

## `<leader>hs` → Stage Hunk

Imagine:

```jsx
console.log("login");
```

became:

```jsx
console.log("user login");
```

Cursor on that change.

Press:

```
Space h s
```

Git stages ONLY that change.

Equivalent to:

```bash
git add -p
```

but easier.

---

# 2. AutoPairs

You don't press any keybinding.

It works automatically.

---

You type:

```jsx
(
```

Neovim creates:

```jsx
(|)
```

Cursor stays in middle.

---

You type:

```jsx
{
```

Result:

```jsx
{|}
```

---

You type:

```jsx
"
```

Result:

```jsx
"|"
```

---

Without AutoPairs:

```jsx
()
{}
""
''
[]
```

You type everything manually.

---

# 3. Surround

This plugin is magic for React and HTML.

---

Suppose cursor is inside:

```html
hello
```

---

## `ysiw"`

Meaning:

```
y = add
s = surround
iw = inner word
" = with quotes
```

Press:

```
ysiw"
```

Result:

```html
"hello"
```

---

## `ysiw(`

Before:

```html
hello
```

Press:

```
ysiw(
```

Result:

```html
(hello)
```

---

## `ysiw]`

Before:

```html
hello
```

Result:

```html
[hello]
```

---

# React Example

Before:

```jsx
Login
```

Cursor on Login.

Press:

```
ysiwtbutton
```

Result:

```jsx
<button>Login</button>
```

---

## Add a div

Before:

```jsx
Login
```

Press:

```
ysiwtdiv
```

Result:

```jsx
<div>Login</div>
```

---

# Change Surround

Suppose:

```jsx
<div>Hello</div>
```

Cursor inside.

Press:

```
cstsection
```

Result:

```jsx
<section>Hello</section>
```

Meaning:

```
c = change
s = surround
t = tag
section = new tag
```

---

# Delete Surround

Before:

```jsx
<div>Hello</div>
```

Cursor inside.

Press:

```
dst
```

Result:

```jsx
Hello
```

Meaning:

```
d = delete
s = surround
t = tag
```

---

# 4. Comment.nvim

---

## `gcc`

Before:

```jsx
const user = "Rahul";
```

Cursor on line.

Press:

```
gcc
```

Result:

```jsx
// const user = "Rahul";
```

Press again:

```
gcc
```

Result:

```jsx
const user = "Rahul";
```

---

## Comment multiple lines

Go to Visual Mode:

```
V
```

Select:

```jsx
const user = "Rahul";
const age = 21;
const city = "Delhi";
```

Press:

```
gc
```

Result:

```jsx
// const user = "Rahul";
// const age = 21;
// const city = "Delhi";
```

---

# Most Useful Ones For MERN

If you only learn 5 today, learn these:

|Shortcut|What it does|
|---|---|
|`gcc`|Comment line|
|`ysiwtdiv`|Wrap word in `<div>`|
|`dst`|Remove HTML tag|
|`]h`|Next Git change|
|`<Space>hp`|Preview Git change|

For React development, `nvim-surround` is probably the plugin that will save you the most time because you're constantly wrapping text with:

```jsx
<div>
<section>
<Button>
<Link>
<span>
```

and changing tags while building components.

## `flash.nvim` — Jump anywhere in 3 keystrokes

The concept is simple: instead of scrolling or using `/search`, you type `s` + any 2 characters you can **see on screen**, and flash shows you a label to teleport there instantly.

---

## Basic Usage

**`s` → type 2 chars → press the label letter**

Example — you want to jump to the word `useState`:

```
s → u → s → (flash highlights all "us" matches and shows labels like "a", "b", "c") → press the label
```

You're there. 3 keystrokes.

---

## The moves to learn first

|Key|What it does|
|---|---|
|`s{2chars}`|Jump forward anywhere on screen|
|`S{2chars}`|Jump using treesitter (selects whole code blocks)|
|`f{char}`|Enhanced find on current line (like vim's `f` but better)|
|`r{char}`|Remote flash — yank/delete from a distant location without moving cursor|

---

## Real MERN workflow examples

**Scenario 1** — You're in a React component and want to jump to `useEffect`:

```
s → u → e → press label
```

**Scenario 2** — You want to delete a whole function block without moving there:

```
d → r → first 2 chars of function name → press label
```

Deletes it, cursor stays where you are.

**Scenario 3** — Select an entire `if` block with treesitter:

```
S → if → press label (selects the whole block)
```

---

## How to practice

For the first week, **force yourself to use `s` every time you catch yourself pressing `hjkl` more than 3 times** to reach something. That's the habit trigger.

A good drill — open any JS file and try:

```
s → co → (jump to console.log)
s → re → (jump to return statement)
s → im → (jump to imports at top)
```

Within a week it becomes faster than your mouse. Within a month you won't remember how you coded without it.