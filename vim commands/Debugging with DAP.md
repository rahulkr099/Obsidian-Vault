This is one of those skills that can save you **hours** every week.

Most beginners debug like this:

```jsx
console.log("1")
console.log("2")
console.log("3")
console.log("4")
console.log(user)
console.log(response)
console.log(token)
```

A debugger lets you **pause time** and inspect everything.

---

# Mental Model

Imagine your program is a movie.

Normally:

```
Start
↓
Line 1
↓
Line 2
↓
Line 3
↓
End
```

Too fast.

With DAP:

```
Start
↓
Line 1
↓
PAUSE
↓
Inspect everything
↓
Continue
```

---

# The 5 Things You Must Master

## 1. Breakpoint

Stop execution here.

Example:

```jsx
async function login() {
  const response = await axios.post(...)
  const user = response.data
  setUser(user)
}
```

Breakpoint:

```jsx
const user = response.data
```

Execution pauses.

You inspect:

```
response
user
token
```

---

## 2. Continue

After inspection:

```
Continue
```

Program runs normally.

---

## 3. Step Over

Run next line.

Example:

```jsx
const user = response.data
setUser(user)
navigate("/")
```

Step Over:

```
Line 1
↓
Line 2
↓
Line 3
```

without entering functions.

---

## 4. Step Into

Example:

```jsx
loginUser(data)
```

Instead of executing immediately:

```
Jump inside loginUser()
```

Now you can inspect its logic.

---

## 5. Watch Variables

Monitor:

```
user
token
response
```

live.

Every step updates values.

---

# Scenario 1: React Login Not Working

Code:

```jsx
const handleSubmit = async () => {
  const response = await loginUser(formData)
  setUser(response.user)
}
```

Problem:

```
User stays null
```

---

Debug:

Breakpoint:

```jsx
setUser(response.user)
```

Inspect:

```
response
response.user
```

Maybe:

```jsx
response.user === undefined
```

Bug found.

---

# Scenario 2: API Returning Wrong Data

Backend:

```jsx
router.post("/login", async (req, res) => {
  ...
})
```

Breakpoint:

```jsx
const user = await User.findOne(...)
```

Inspect:

```
req.body
email
password
user
```

---

Maybe:

```
email = undefined
```

Now you know frontend isn't sending it.

---

# Scenario 3: JWT Authentication Broken

Code:

```jsx
const token = req.headers.authorization
```

Breakpoint here.

Inspect:

```
req.headers
token
```

Maybe:

```
authorization = undefined
```

Instantly reveals issue.

---

# Scenario 4: useEffect Running Too Many Times

Code:

```jsx
useEffect(() => {
  fetchUser()
}, [user])
```

App keeps calling API.

Breakpoint:

```jsx
fetchUser()
```

Every pause shows:

```
user value
```

You realize:

```
user changes
↓
effect runs
↓
user changes
↓
effect runs
```

Infinite loop.

---

# Scenario 5: State Isn't Updating

Code:

```jsx
setUser(newUser)
```

Breakpoint before.

Inspect:

```
current user
newUser
```

Then step over.

Check state change.

---

# Scenario 6: Backend Crashes

Instead of:

```jsx
console.log()
console.log()
console.log()
```

Pause before:

```jsx
await User.create(...)
```

Inspect:

```
req.body
email
password
```

Often you'll immediately see:

```
password = undefined
```

---

# Scenario 7: Why Is This Function Called?

Breakpoint:

```jsx
createPost()
```

When execution stops:

Look at:

```
Call Stack
```

Example:

```
App.jsx
↓
Dashboard.jsx
↓
PostForm.jsx
↓
createPost()
```

Now you know who called it.

---

# React Debugging Workflow

When debugging React:

```
Breakpoint
↓
Inspect props
↓
Inspect state
↓
Inspect context
↓
Step Over
↓
Observe changes
```

---

# Express Debugging Workflow

When debugging backend:

```
Breakpoint
↓
Inspect req.body
↓
Inspect req.params
↓
Inspect req.query
↓
Inspect database result
↓
Inspect response
```

---

# TypeScript Debugging Workflow

Breakpoint:

```tsx
const user = response.data
```

Inspect:

```
typeof user
user
response
```

Catch:

```
undefined
null
wrong type
missing field
```

instantly.

---

# Common MERN Bugs

## Authentication

Check:

```
token
user
cookies
headers
```

---

## API

Check:

```
req.body
req.params
req.query
response
```

---

## React

Check:

```
props
state
context
useEffect
```

---

## MongoDB

Check:

```
query
result
document
```

---

# Daily DAP Cheat Sheet

## Breakpoint

```
Toggle Breakpoint
```

Use when:

```
I want execution to stop here.
```

---

## Continue

```
Continue
```

Use when:

```
I finished inspecting.
```

---

## Step Over

```
Next line
```

Use when:

```
I don't care about function internals.
```

---

## Step Into

```
Enter function
```

Use when:

```
I suspect bug inside function.
```

---

## Step Out

```
Leave function
```

Use when:

```
I already checked inside.
```

---

## Watch

```
user
token
response
```

Use when:

```
I want live updates.
```

---

# What Senior Developers Actually Do

A lot of debugging follows this pattern:

```
Bug occurs
↓
Set breakpoint near bug
↓
Inspect variables
↓
Follow call stack
↓
Find wrong value
↓
Fix source
```

Not:

```
Add 50 console.logs
```

If you eventually set up `nvim-dap`, I recommend memorizing only these first:

```
Breakpoint
Continue
Step Over
Step Into
Step Out
Watch
Call Stack
```

Those seven concepts solve the vast majority of React, Node.js, Express, and TypeScript debugging tasks.

Excellent catch.

I explained the **debugging concepts**, but not the actual **Neovim keybindings**.

The reason is that **nvim-dap ships with almost no default keybindings**. You create your own.

For MERN development, this is the setup I'd recommend.

---

# DAP Keymap Setup

Put this in:

```
lua/config/keymaps.lua
```

```lua
local dap = require("dap")
local dapui = require("dapui")

vim.keymap.set("n", "<F5>", dap.continue, { desc = "Debug Continue" })

vim.keymap.set("n", "<F10>", dap.step_over, { desc = "Step Over" })

vim.keymap.set("n", "<F11>", dap.step_into, { desc = "Step Into" })

vim.keymap.set("n", "<F12>", dap.step_out, { desc = "Step Out" })

vim.keymap.set("n", "<leader>db", dap.toggle_breakpoint,
  { desc = "Toggle Breakpoint" })

vim.keymap.set("n", "<leader>dc", dap.continue,
  { desc = "Continue" })

vim.keymap.set("n", "<leader>dr", dap.repl.open,
  { desc = "Open REPL" })

vim.keymap.set("n", "<leader>du", dapui.toggle,
  { desc = "Toggle DAP UI" })
```

---

# The Cheat Sheet

## Start Debugging

```
F5
```

Meaning:

```
Run
Continue
Resume
```

This is the most-used key.

---

## Toggle Breakpoint

Move cursor:

```jsx
const user = await loginUser()
```

Press:

```
<leader>db
```

Result:

```
● breakpoint added
```

Press again:

```
breakpoint removed
```

---

## Step Over

```
F10
```

Example:

```jsx
const user = await loginUser()
setUser(user)
navigate("/")
```

Cursor execution:

```
Line 1
↓
Line 2
↓
Line 3
```

without entering functions.

---

## Step Into

```
F11
```

Example:

```jsx
loginUser(data)
```

becomes:

```jsx
function loginUser(data) {
```

Debugger enters the function.

---

## Step Out

```
F12
```

Example:

```jsx
function loginUser() {
   ...
}
```

You're inside.

Press:

```
F12
```

and return to caller.

---

## Continue

```
F5
```

again.

Continue until:

```
next breakpoint
```

or

```
program ends
```

---

# My React Workflow

Imagine:

```jsx
const handleSubmit = async () => {
  const response = await loginUser(data)
  setUser(response.user)
}
```

### Step 1

Cursor:

```jsx
setUser(response.user)
```

Press:

```
<leader>db
```

---

### Step 2

Start debugger:

```
F5
```

---

### Step 3

Program pauses.

Open UI:

```
<leader>du
```

See:

```
response
response.user
data
```

---

### Step 4

Next line:

```
F10
```

---

### Step 5

Continue:

```
F5
```

---

# What You'll Use 95% of the Time

Honestly:

```
<leader>db   Toggle Breakpoint
F5           Continue
F10          Step Over
F11          Step Into
<leader>du   Toggle UI
```

That's almost everything.

---

# My Opinion for Your Setup

Since you already have a lot of `<leader>` mappings:

```
;a    Telescope
Harpoon
Trouble
LazyGit
```

I'd keep debugging on **function keys**:

```
F5
F10
F11
F12
```

because:

- Every debugger uses them
- VS Code uses them
- JetBrains uses them
- Tutorials use them
- Easy to remember

After a week, your brain will automatically associate:

```
F5  = Run
F10 = Next line
F11 = Enter function
F12 = Exit function
```

and debugging will feel natural no matter which editor you use.