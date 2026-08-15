`<leader>` is a special key in Neovim that acts like a **custom shortcut prefix**.

It can be:

```lua
vim.g.mapleader = " "
```

which means:

```
<leader> = Space
```

or

```lua
vim.g.mapleader = ";"
```

which means:

```
<leader> = ;
```

or any other key you choose.

---

### How to check yours

Look in your Neovim config for:

```lua
vim.g.mapleader = " "
```

or

```lua
vim.g.mapleader = ";"
```

Usually it's in:

```
lua/config/options.lua
```

or

```
lua/config/keymaps.lua
```

or

```
init.lua
```

Search for:

```bash
grep -R "mapleader" ~/.config/nvim
```

---

### If you have:

```lua
vim.g.mapleader = " "
```

then:

```
<leader>w
```

means:

```
Space w
```

and:

```
<leader>e
```

means:

```
Space e
```

and:

```
<leader>1
```

means:

```
Space 1
```

---

### Why most people use Space

Because it's very easy to reach:

```
Space e   → Explorer
Space w   → Save
Space g   → Lazygit
Space a   → Harpoon Add
Space 1   → Harpoon File 1
```

Your thumb is already on the space bar.

---

### Looking at your keymaps

You have mappings like:

```lua
<leader>w
<leader>e
<leader>g
<leader>a
<leader>1
```

and also mappings like:

```lua
;o
;b
;p
```

Notice:

```
;o
;b
;p
```

are **not leader mappings**.

They literally mean:

```
Press ;
Then o
```

```
Press ;
Then b
```

```
Press ;
Then p
```

So:

|Mapping|Keys Pressed|
|---|---|
|`<leader>w`|Space + w (if leader is space)|
|`<leader>g`|Space + g|
|`;o`|; then o|
|`;b`|; then b|
|`;p`|; then p|

---

Run this inside Neovim:

```
:echo mapleader
```

If it prints nothing, your leader is probably a space (`" "`).

Or show me the output of:

```bash
grep -R "mapleader" ~/.config/nvim
```

and I'll tell you exactly what your leader key is.

My leader is:

![image.png](attachment:1a49f056-96a8-450c-8811-2c499876f1a0:image.png)

Perfect. Your leader key is definitely **Space**.

You have:

```lua
vim.g.mapleader = " "
```

So whenever you see:

```lua
<leader>w
```

read it as:

```
Space w
```

---

## Your Most Important Keybindings

### File Operations

```
Space w    Save file
Space q    Quit current file
Space Q    Quit all files
```

---

### File Explorer

```
Space e    Toggle NvimTree
Space E    Find current file in tree
Space f    Focus current file in tree
```

---

### Harpoon

```
Space a    Add current file

Ctrl+e     Open Harpoon menu

Space 1    Jump to file 1
Space 2    Jump to file 2
Space 3    Jump to file 3
Space 4    Jump to file 4
Space 5    Jump to file 5
```

---

### Lazygit

```
Space g
```

Opens Lazygit.

---

### Trouble

```
Space x x    Diagnostics
Space x w    Buffer diagnostics
Space x r    References
Space x d    Definitions
```

Think:

```
x = problems/errors
```

---

### Kulala (API Testing)

```
Space h r    Run HTTP request
Space h n    Next request
Space h p    Previous request
```

Think:

```
h = HTTP
```

---

### Debugger

```
Space d b    Breakpoint
Space d c    Continue
Space d r    REPL
Space d u    Debug UI
```

Think:

```
d = Debug
```

---

## Non-Leader Keybindings

These are NOT leader mappings:

```
;o
;b
;p
```

Meaning:

```
Press ;
Then o
```

```
Press ;
Then b
```

```
Press ;
Then p
```

### Telescope

```
;o    Recent files
;b    Search current buffer
;p    Document symbols
```

---

## How I Remember Them

Your config already follows a nice pattern:

```
Space + e = Explorer
Space + f = Find file
Space + g = Git
Space + a = Add to Harpoon

Space + x = Trouble
Space + d = Debugger
Space + h = HTTP (Kulala)
```

So when you add future mappings, try to keep the same idea:

```
Space + g = Git stuff
Space + d = Debug stuff
Space + h = HTTP stuff
Space + t = Test stuff
Space + s = Search stuff
```

This makes your Neovim feel organized instead of becoming a random collection of shortcuts.