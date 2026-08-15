For a MERN developer, you do **not** need to memorize all of LazyGit.

You need the **20% of shortcuts that give 80% of the value**.

The most important thing to remember:

```
Git knowledge first
LazyGit shortcuts second
```

LazyGit is just a faster interface for Git. ([LinkedIn](https://www.linkedin.com/posts/jonzaro_lazygit-has-been-an-unlock-for-my-git-workflow-activity-7458196268637671424-txK4?utm_source=chatgpt.com))

---

# Open LazyGit

Inside your project:

```bash
lazygit
```

or in Neovim:

```
:LazyGit
```

---

# The 5 Panels You Need

```
1 = Status
2 = Files
3 = Branches
4 = Commits
5 = Stash
```

Jump directly using the number keys. ([lazygit](https://lazygit.dev/keybindings/?utm_source=chatgpt.com))

For your daily work you'll spend:

```
90% Files
8% Branches
2% Commits
```

---

# Daily Workflow Cheat Sheet

## 1. Stage File

Move to file:

```
j / k
```

Stage:

```
Space
```

Unstage:

```
Space
```

again. ([lazygit](https://lazygit.dev/keybindings/?utm_source=chatgpt.com))

Equivalent Git:

```bash
git add file.js
```

---

## 2. Stage All Files

```
a
```

Equivalent:

```bash
git add .
```

([lazygit](https://lazygit.dev/keybindings/?utm_source=chatgpt.com))

---

## 3. Commit

```
c
```

Type message:

```
feat: add authentication
```

Press Enter.

Equivalent:

```bash
git commit -m "feat: add authentication"
```

([lazygit](https://lazygit.dev/keybindings/?utm_source=chatgpt.com))

---

## 4. Push

```
Shift + P
```

Equivalent:

```bash
git push
```

A very commonly used shortcut. ([Medium](https://medium.com/%40rasmusfangel/level-up-git-with-lazygit-b5e6c923c5d7?utm_source=chatgpt.com))

---

## 5. Pull

```
p
```

Equivalent:

```bash
git pull
```

([Medium](https://medium.com/%40rasmusfangel/level-up-git-with-lazygit-b5e6c923c5d7?utm_source=chatgpt.com))

---

# File Inspection

## Open Diff

Move to file and:

```
Enter
```

See exactly what changed. ([lazygit](https://lazygit.dev/keybindings/?utm_source=chatgpt.com))

This is extremely useful before committing.

---

## Open File in Neovim

```
e
```

([GitHub](https://github.com/jesseduffield/lazygit/blob/master/docs/keybindings/Keybindings_en.md?utm_source=chatgpt.com))

---

## Discard Changes

```
d
```

Equivalent:

```bash
git restore file
```

Be careful.

([lazygit](https://lazygit.dev/keybindings/?utm_source=chatgpt.com))

---

# Branch Workflow

Go to:

```
3
```

(Branches panel)

---

## Create Branch

```
n
```

Example:

```
feature/authentication
```

([Oliver Guenther](https://oliverguenther.de/2021/04/lazygit-an-introduction-series/?utm_source=chatgpt.com))

Equivalent:

```bash
git checkout -b feature/authentication
```

---

## Checkout Branch

Select branch:

```
Space
```

([Oliver Guenther](https://oliverguenther.de/2021/04/lazygit-an-introduction-series/?utm_source=chatgpt.com))

---

## Delete Branch

```
d
```

(Only when safe)

([Ulf Schneider](https://ulfschneider.io/2024-07-09-lazygit/?utm_source=chatgpt.com))

---

# Search

Inside any panel:

```
/
```

Search files, commits, branches, etc. ([lazygit](https://lazygit.dev/keybindings/?utm_source=chatgpt.com))

---

# Help

Most important shortcut:

```
?
```

Shows all shortcuts for the current panel. ([lazygit](https://lazygit.dev/keybindings/?utm_source=chatgpt.com))

You don't need to memorize everything.

When stuck:

```
?
```

---

# My Recommended MERN Workflow

Imagine you're working on login functionality.

### Step 1

Code normally in Neovim.

### Step 2

Open:

```
:LazyGit
```

### Step 3

Review changes:

```
Files Panel
```

### Step 4

Stage:

```
Space
```

### Step 5

Commit:

```
c
```

Message:

```
feat: implement login page
```

### Step 6

Push:

```
Shift+P
```

Done.

---

# Memorize Only These

```
?          Help

1 2 3 4 5  Switch panels

j k        Move

Space      Stage file

a          Stage all

c          Commit

Shift+P    Push

p          Pull

n          New branch

d          Discard/Delete

Enter      View diff

/          Search

q          Quit
```

If you master only those shortcuts, you'll already be more productive than most developers who use LazyGit casually. After a week, opening a terminal and typing long Git commands for everyday commits will start to feel slow.