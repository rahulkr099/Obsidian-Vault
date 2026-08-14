Since you're becoming comfortable with the terminal, I'd recommend thinking of these three tools like this:

|Tool|Purpose|Best for|
|---|---|---|
|`dust`|Quick overview|"Which folders are biggest?"|
|`ncdu`|Interactive explorer|"Where exactly is my disk space going?"|
|`dua`|Cleanup manager|"What should I delete?"|

Each one solves a different problem.

---

# 1. `dust` — My favorite for a quick overview ⭐⭐⭐⭐⭐

Think of it as a modern version of `du`.

Instead of

```bash
du -sh *
```

you simply run

```bash
dust
```

Example:

```
15G ┌── Projects
10G ├── Downloads
5G  ├── Videos
2G  ├── Pictures
1G  └── Documents
```

Within a second, you know where to investigate.

---

## Most useful commands

### Current directory

```bash
dust
```

---

### Home directory

```bash
dust ~
```

---

### Entire system

```bash
sudo dust /
```

---

### Largest 20 directories

```bash
dust -n 20 ~
```

Output:

```
22G  Downloads
15G  Projects
8G   Videos
```

---

### Show only directories

```bash
dust -d 2
```

Example

```
Projects
Projects/MERN
Projects/Python
```

---

### Ignore hidden files

```bash
dust --ignore-hidden
```

---

### Show filesystem size

```bash
dust --filesize
```

---

## Real-world examples

### Which project is largest?

```bash
cd ~/Projects
dust
```

---

### Which node_modules folder is biggest?

```bash
cd ~/Projects
dust -d 3
```

You'll immediately see:

```
5.2G BlogApp
3.9G Ecommerce
2.1G Portfolio
```

---

### Downloads cleanup

```bash
dust ~/Downloads
```

---

# 2. `ncdu` — Deep investigation ⭐⭐⭐⭐⭐

After `dust` tells you:

```
Projects = 15GB
```

Use

```bash
ncdu ~/Projects
```

Now you can navigate:

```
Projects
    MERN
        BlogApp
            node_modules
                ...
```

until you find

```
node_modules 3.8GB
```

This is why I use:

```
dust
↓
ncdu
```

---

# 3. `dua` — Cleanup expert ⭐⭐⭐⭐⭐

`dua` focuses on helping you free space.

---

## Scan current directory

```bash
dua .
```

---

## Scan home

```bash
dua ~
```

---

## Scan root

```bash
sudo dua /
```

---

## Interactive mode

```bash
dua i
```

or

```bash
dua interactive
```

You'll see something like:

```
Downloads

Projects

Videos

Pictures
```

Navigate with the arrow keys and inspect sizes interactively.

---

## Delete interactively

```bash
dua i
```

Highlight an unwanted directory and delete it from within the interface. Double-check before confirming deletions.

---

# Workflow I use

## Scenario 1

"My SSD is almost full."

```
df -h
```

↓

```
sudo dust /
```

↓

```
sudo ncdu /
```

↓

```
sudo apt clean
```

---

## Scenario 2

"My Projects folder is huge."

```
dust ~/Projects
```

↓

```
ncdu ~/Projects
```

↓

Find

```
node_modules
```

↓

Delete if appropriate:

```bash
rm -rf node_modules
npm install
```

---

## Scenario 3

"My Downloads folder is a mess."

```
dust ~/Downloads
```

↓

```
ncdu ~/Downloads
```

↓

Delete old ISOs, ZIPs, videos, installers, etc.

---

## Scenario 4

"Which cache is consuming space?"

```
dust ~/.cache
```

↓

```
ncdu ~/.cache
```

---

# My favorite aliases

Add these to `~/.zshrc`:

```bash
alias d='dust'
alias dui='dua i'
alias nc='ncdu'
```

Then you can use:

```bash
d
```

```bash
dui
```

```bash
nc ~
```

---

# A practical workflow for a MERN developer

You'll often have large `node_modules`, Docker images, npm caches, and build artifacts. Here's a sequence I recommend every month or so:

```bash
# 1. Overall disk usage
df -h

# 2. Find large top-level folders
dust ~

# 3. Investigate the largest one
ncdu ~

# 4. Inspect your projects
dust ~/Projects

# 5. Check npm cache
dust ~/.npm

# 6. Check Docker storage (if you use Docker)
sudo dust /var/lib/docker

# 7. Remove unused APT packages
sudo apt autoremove
sudo apt clean
```

---

# Your first challenge

Try these commands and see what they reveal:

```bash
dust ~
```

```bash
dust ~/Projects
```

```bash
ncdu ~/Projects
```

```bash
dua i
```

Then answer these questions:

1. Which folder in your home directory is the largest?
2. Which MERN project uses the most disk space?
3. How large is your largest `node_modules` directory?
4. How much space does your `Downloads` folder use?

These exercises will help you become comfortable using the tools in situations you'll encounter regularly as a developer.

`ncdu` is one of the best terminal tools for finding out **what is using your disk space**. Think of it as a fast, terminal-based version of Windows' "Storage" settings.

Since you enjoy terminal workflows, I think you'll really like it.

---

# Step 1: Install

```bash
sudo apt update
sudo apt install ncdu
```

Check the version:

```bash
ncdu --version
```

---

# Step 2: Scan your entire system

```bash
sudo ncdu /
```

Why `sudo`?

Without it, `ncdu` can't read many system directories like `/root` or parts of `/var`.

The first time you run it, you'll see something like:

```
--- / --------------------------------------------------------------------
  35.6 GiB [##########] /
```

It scans your filesystem. On a large drive, this can take a minute or two.

---

# Step 3: Understanding the interface

After scanning, you'll see something like:

```
--- / ---------------------------------------------------------------------
   18.2 GiB [##########] home/
    7.4 GiB [####      ] var/
    6.1 GiB [###       ] usr/
    2.8 GiB [#         ] opt/
  500.0 MiB [          ] etc/
```

Each row shows:

- Directory name
- Size
- Visual usage bar

The largest folders are usually at the top.

---

# Step 4: Navigation

|Key|Action|
|---|---|
|↑ ↓|Move up/down|
|Enter / →|Open folder|
|← / Backspace|Go back|
|q|Quit|
|g|Go to top directory|
|?|Help|
|n|Sort by name|
|s|Sort by size|
|C|Sort by number of items|

---

# Step 5: Example

Suppose you run:

```bash
sudo ncdu /
```

You might see:

```
/
├── home
├── var
├── usr
├── opt
└── etc
```

Press **Enter** on `home`.

```
home
├── rahul
```

Press **Enter** again.

```
rahul
├── Downloads
├── Videos
├── Projects
├── .cache
└── Pictures
```

Now you can immediately see where your space is going.

---

# Step 6: Scan only your home directory

If you only care about your personal files:

```bash
ncdu ~
```

or

```bash
ncdu /home/rahul
```

No `sudo` is needed for your own files.

---

# Step 7: Scan a specific folder

Downloads:

```bash
ncdu ~/Downloads
```

Projects:

```bash
ncdu ~/Projects
```

Node projects:

```bash
ncdu ~/Projects/MERN
```

This is much faster than scanning the whole system.

---

# Step 8: Delete files (use carefully)

Highlight a file or directory and press:

```
d
```

It asks:

```
Delete?
```

Press:

```
y
```

Only delete items you recognize. Avoid deleting system directories unless you're certain of their purpose.

---

# Step 9: Show hidden folders

Hidden folders like `.cache` and `.config` are included automatically.

You may find:

```
.cache
```

taking several gigabytes.

Often, browser caches or build caches live here.

---

# Step 10: Useful directories to inspect

```
/
├── home
├── var
├── usr
├── opt
├── tmp
└── boot
```

If you're a MERN developer, also check:

```
~/Projects
~/Downloads
~/.cache
~/.local
~/.npm
```

These are common places where space accumulates.

---

# Step 11: Save a report

You can export a scan:

```bash
ncdu -o report.ncdu /
```

Open it later:

```bash
ncdu -f report.ncdu
```

This is handy if you want to compare disk usage over time.

---

# Step 12: Common workflow

Here's a simple workflow I use:

1. Check overall disk usage:
    
    ```bash
    df -h
    ```
    
2. If a partition is getting full:
    
    ```bash
    sudo ncdu /
    ```
    
3. Drill down into the largest directories.
    
4. Remove unnecessary files.
    
5. Run:
    
    ```bash
    sudo apt autoremove
    sudo apt clean
    ```
    

---

# A few examples

**Find what's taking space in Downloads:**

```bash
ncdu ~/Downloads
```

**Check Docker data:**

```bash
sudo ncdu /var/lib/docker
```

**Check log files:**

```bash
sudo ncdu /var/log
```

**Inspect Node.js caches:**

```bash
ncdu ~/.npm
```

**Inspect your project directory:**

```bash
ncdu ~/Projects
```

---

## Practice challenge

Try these commands one by one:

```bash
df -h
```

```bash
ncdu ~
```

```bash
sudo ncdu /
```

Navigate to:

```
/
→ home
→ rahul
→ Downloads
```

Then:

- Sort by **size** (`s`).
- Open the largest folder.
- Keep drilling down until you find the largest files.

This is one of the fastest ways to understand where your disk space is going.

Since you're building a strong Linux terminal toolkit, I'd also recommend learning `dust` (a modern replacement for `du`) and `dua` (an interactive disk usage analyzer). Together with `ncdu`, they make an excellent set of tools for managing disk space efficiently.