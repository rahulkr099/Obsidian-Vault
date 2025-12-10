Great! You’ve learned `h,j,k,l` for movement… now the magic begins 😄
In Vim, there are mainly **two worlds**:
---
# 🟦 1. **Normal Mode** (moving, copying, editing commands)
This is where you move your cursor, delete lines, yank, paste, etc.
You are already in this when Vim opens.
---
# 🟩 2. **Insert Mode** (actually typing code)
To start typing, just press ANY of these:
|Key|What it does|
|---|---|
|`i`|Insert BEFORE cursor|
|`a`|Insert AFTER cursor|
|`o`|New line BELOW and insert|
|`O`|New line ABOVE and insert|
👉 Example workflow:
```
Normal Mode → press i → type code → press Esc to return
```
---
# 🔄 Switching Between Modes
### To write code
```
i  → start writing where cursor is
a  → start writing after cursor
o  → open new line below and type
```
### To stop writing & return to movement mode
```
Esc
```
Just like that.
---
# ⭐ Super Useful Insert Shortcuts
### You want to edit a line quickly?
|Action|Command|
|---|---|
|Go to end of line and start typing|`A`|
|Go to beginning and start typing|`I`|
|Delete line and start typing|`cc`|
|Replace character|`r`|
|Replace word|`cw`|
Example:
Cursor is in the middle:
```
print("Hello")
       ↑ here
```
Press:
```
A
```
You land at:
```
print("Hello")|
```
and you start typing.
---
# 🚀 Small Workflow Example For Coding
Imagine your line is:
```
console.log("Rahul")
```
You want to change `Rahul` to `World`.
### Step-by-step:
1.  Use `w` to go to the word:`console.log("Rahul")
              ^
`
1.  Press `ci"`(Change Inside Quotes)
Now insert mode opens automatically, cursor inside quotes:
```
"|"
```
3.  TypeWorld
3.  Press `Esc` — done!
---
# 🍬 Little Innovative Tricks To Improve Coding Faster
### 1. Use Visual Mode for quick selections
```
v       → select characters
V       → select line
Ctrl+v  → select block (columns)
```
Example:
Want to comment multiple lines?
```
V jj
```
(Select 3 lines)
Then:
```
I// Esc
```
👉 All lines get commented instantly.
---
### 2. Use macros to repeat actions
Press:
```
qa     → start recording macro into register a
(do some actions)
q      → stop
@a     → replay actions
```
Perfect for repeating similar lines.
---
### 3. Use `.` to repeat your last command
Example:
```
x deletes a character
```
Next time?
Just press `.`
Repeats again!
---
# 🌱 Keep practicing!
Soon you won't think:
> "How to switch modes?"
Instead your fingers will automatically:
*   `Esc` → move
*   `i/o/a` → code
*   `.` → repeat
*   `ci` → change inside
*   `di` → delete inside
---
You’re already stepping into real developer-level editing 😎
With time, this mode-switching becomes **addictive**, fast, and fun.

