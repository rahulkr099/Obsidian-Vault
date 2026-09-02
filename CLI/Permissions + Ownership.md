# Linux Permissions & Ownership 🔐

This is one of the most important Linux concepts. You'll use it when working with:

- Servers
    
- SSH
    
- Node.js deployments
    
- Docker
    
- Git
    
- Shell scripts
    
- Configuration files
    
- SSH keys
    

Let's understand it properly.

---

# 1. Viewing Permissions

Run:

```bash
ls -l
```

Example:

```text
-rwxr-xr-- 1 rahul developers 2048 Sep 2 10:00 server.sh
```

The first part is what we care about:

```text
-rwxr-xr--
```

Let's break it down.

---

# 2. Permission Structure 🧠

```text
-rwxr-xr--
│││ │││ │││
│││ │││ ││└── Others permissions
│││ │││ └┴───
│││ │└┴────── Group permissions
│└┴────────── Owner permissions
└──────────── File type
```

More clearly:

```text
- rwx r-x r--
│  │   │   │
│  │   │   └── Others
│  │   └────── Group
│  └────────── Owner
└───────────── File type
```

There are **four sections**:

```text
File Type | Owner | Group | Others
    -     | rwx   | r-x   | r--
```

---

# 3. File Types

The first character tells you what type it is.

|Symbol|Meaning|
|---|---|
|`-`|Regular file|
|`d`|Directory|
|`l`|Symbolic link|
|`c`|Character device|
|`b`|Block device|

Most commonly you'll see:

```text
- → file
d → directory
l → symbolic link
```

Example:

```text
-rw-r--r--  file.txt
drwxr-xr-x  my-folder
lrwxrwxrwx  link
```

---

# 4. The Three Permissions

Linux has:

```text
r → Read
w → Write
x → Execute
```

But their meaning changes slightly for files and directories.

---

# 5. Permissions for Files 📄

For a file:

### Read `r`

You can read its content.

```bash
cat file.txt
```

### Write `w`

You can modify the file.

```bash
echo "Hello" >> file.txt
```

### Execute `x`

You can execute it.

Example:

```bash
./script.sh
```

---

# 6. Permissions for Directories 📁

Directories work differently.

### Read `r`

You can list directory contents.

```bash
ls folder
```

### Write `w`

You can create, rename, or delete files inside the directory.

### Execute `x`

You can enter/access the directory.

```bash
cd folder
```

This is a very important distinction.

---

# 7. Owner, Group, Others 👥

Suppose:

```text
-rwxr-xr--
```

Split it:

```text
rwx | r-x | r--
```

|User Type|Permissions|
|---|---|
|Owner|`rwx`|
|Group|`r-x`|
|Others|`r--`|

Meaning:

```text
Owner  → read, write, execute
Group  → read, execute
Others → read only
```

---

# 8. Who is the Owner?

Check:

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 rahul developers file.txt
```

Structure:

```text
Permissions
    │
    ▼
-rw-r--r-- 1 rahul developers file.txt
              │       │
              │       └── Group
              └────────── Owner
```

Here:

```text
Owner → rahul
Group → developers
```

---

# 9. Changing Permissions with `chmod` 🔥

`chmod` means:

> Change Mode

Example:

```bash
chmod +x script.sh
```

This adds execute permission.

Now you can run:

```bash
./script.sh
```

---

# 10. Symbolic Mode

You can modify permissions using symbols.

```text
u → user/owner
g → group
o → others
a → all
```

Operations:

```text
+ → add
- → remove
= → set exactly
```

---

## Add Execute Permission

```bash
chmod u+x script.sh
```

Add execute for owner.

---

## Add Write for Group

```bash
chmod g+w file.txt
```

---

## Remove Read for Others

```bash
chmod o-r file.txt
```

---

## Add Execute for Everyone

```bash
chmod a+x script.sh
```

Equivalent:

```bash
chmod +x script.sh
```

---

# 11. Numeric Permissions 🔥🔥

You'll see commands like:

```bash
chmod 755 script.sh
```

Where do these numbers come from?

Each permission has a value:

```text
r = 4
w = 2
x = 1
```

Add them together.

---

## Permission Values

|Permission|Value|
|---|--:|
|`r`|4|
|`w`|2|
|`x`|1|

---

### `7`

```text
4 + 2 + 1 = 7
```

Means:

```text
rwx
```

---

### `6`

```text
4 + 2 = 6
```

Means:

```text
rw-
```

---

### `5`

```text
4 + 1 = 5
```

Means:

```text
r-x
```

---

### `4`

```text
4
```

Means:

```text
r--
```

---

### Full Table

|Number|Permission|
|---|---|
|`0`|`---`|
|`1`|`--x`|
|`2`|`-w-`|
|`3`|`-wx`|
|`4`|`r--`|
|`5`|`r-x`|
|`6`|`rw-`|
|`7`|`rwx`|

---

# 12. Understanding `chmod 755`

```bash
chmod 755 script.sh
```

Split:

```text
7 | 5 | 5
│   │   │
│   │   └── Others
│   └────── Group
└────────── Owner
```

Convert:

```text
7 → rwx
5 → r-x
5 → r-x
```

Result:

```text
rwxr-xr-x
```

Meaning:

```text
Owner  → Read + Write + Execute
Group  → Read + Execute
Others → Read + Execute
```

---

# 13. Common Permission Modes 🔥

## `644`

```text
rw-r--r--
```

Common for normal files.

```bash
chmod 644 file.txt
```

Meaning:

```text
Owner  → read + write
Others → read
```

---

## `755`

```text
rwxr-xr-x
```

Common for:

- Directories
    
- Executable scripts
    

```bash
chmod 755 script.sh
```

---

## `700`

```text
rwx------
```

Only the owner has access.

Common for private directories.

```bash
chmod 700 private-folder
```

---

## `600`

```text
rw-------
```

Only the owner can read/write.

Common for:

- Private keys
    
- Secret files
    
- Credentials
    

Example:

```bash
chmod 600 ~/.ssh/id_ed25519
```

---

# 14. `chmod` Examples

### Make script executable

```bash
chmod +x script.sh
```

### Owner full access, everyone else read

```bash
chmod 744 file.txt
```

### Private file

```bash
chmod 600 secrets.txt
```

### Public directory

```bash
chmod 755 public
```

---

# 15. Directory Permissions Deep Dive 🔥

Suppose:

```text
drwxr-xr-x myfolder
```

Meaning:

```text
Owner  → rwx
Group  → r-x
Others → r-x
```

For a directory:

|Permission|Meaning|
|---|---|
|`r`|List filenames|
|`w`|Create/delete/rename entries|
|`x`|Enter/traverse directory|

Example:

```bash
mkdir private
chmod 700 private
```

Only you can access it.

---

# 16. Changing Ownership with `chown`

`chown` means:

> Change Owner

Syntax:

```bash
sudo chown user file
```

Example:

```bash
sudo chown rahul file.txt
```

Change owner and group:

```bash
sudo chown rahul:developers file.txt
```

Structure:

```text
chown OWNER:GROUP FILE
```

---

# 17. Change Group with `chgrp`

```bash
sudo chgrp developers file.txt
```

Now the file belongs to:

```text
Group → developers
```

---

# 18. Recursive Permissions ⚠️

You can apply changes recursively.

```bash
chmod -R 755 folder
```

Or:

```bash
sudo chown -R rahul:developers project
```

But be careful.

### This is often NOT recommended:

```bash
chmod -R 755 project
```

Why?

It makes every file executable.

For example:

```text
project/
├── app.js
├── config.json
└── README.md
```

These files generally don't need execute permission.

A better approach:

```bash
find project -type d -exec chmod 755 {} +
find project -type f -exec chmod 644 {} +
```

This sets:

```text
Directories → 755
Files       → 644
```

Much cleaner.

---

# 19. The Famous `chmod 777` ⚠️

You'll sometimes see:

```bash
chmod 777 folder
```

Meaning:

```text
rwxrwxrwx
```

Everyone can:

- Read
    
- Write
    
- Execute
    

This is usually a bad idea.

Especially on:

- Servers
    
- Production systems
    
- Shared systems
    
- Sensitive directories
    

Don't use `777` as a quick fix.

Instead, understand:

```text
Who needs access?
What access do they need?
```

Then assign the minimum required permission.

This is called the **Principle of Least Privilege**.

---

# 20. Practical Node.js Example 🚀

Suppose your project belongs to root because you accidentally ran:

```bash
sudo npm install
```

Now:

```bash
ls -l
```

might show:

```text
root root node_modules
```

Then running:

```bash
npm install
```

as your normal user can cause permission errors.

A possible fix for that project directory is:

```bash
sudo chown -R "$USER":"$USER" .
```

Then verify:

```bash
ls -ld .
```

⚠️ Better long-term habit: avoid using `sudo npm install` inside normal development projects.

---

# 21. `umask` — Default Permissions 🌱

When you create a file:

```bash
touch file.txt
```

It gets default permissions.

Check:

```bash
umask
```

You might see:

```text
0022
```

A common conceptual result is:

```text
Files       → 666 - 022 = 644
Directories → 777 - 022 = 755
```

That's why you often see:

```text
Files       → rw-r--r--
Directories → rwxr-xr-x
```

Important detail: normal files are usually created **without execute permission by default**.

---

# 22. Special Permissions (Introduction)

There are advanced permissions:

```text
setuid
setgid
sticky bit
```

You don't need to master them yet, but here's the idea.

---

## Sticky Bit

Common on:

```text
/tmp
```

Check:

```bash
ls -ld /tmp
```

You may see something like:

```text
drwxrwxrwt
```

The `t` is the sticky bit.

Meaning:

> Users can create files there, but generally cannot delete files owned by other users.

We'll cover special permissions separately later.

---

# 23. Practical Permission Debugging 🔍

When you get:

```text
Permission denied
```

Follow this process.

### Step 1: Check file

```bash
ls -l filename
```

### Step 2: Check directory

```bash
ls -ld directory
```

### Step 3: Check owner

```bash
stat filename
```

### Step 4: Check your user

```bash
whoami
```

### Step 5: Check groups

```bash
groups
```

Don't immediately use:

```bash
sudo
```

Understand the permission problem first.

---

# Permission Cheat Sheet 🧠

```text
r = 4
w = 2
x = 1
```

```text
7 = rwx
6 = rw-
5 = r-x
4 = r--
0 = ---
```

Common modes:

```text
644 → rw-r--r--
755 → rwxr-xr-x
700 → rwx------
600 → rw-------
```

Commands:

```bash
# View permissions
ls -l

# Add execute
chmod +x script.sh

# Set permissions
chmod 755 script.sh

# Change owner
sudo chown user file

# Change group
sudo chgrp group file

# Check details
stat file

# View current user
whoami

# View groups
groups

# Default permission mask
umask
```

---

# Practical Exercise 💪

Create a safe practice directory:

```bash
mkdir ~/permission-lab
cd ~/permission-lab
```

Create a script:

```bash
printf '#!/usr/bin/env bash\necho "Hello from script"\n' > hello.sh
```

Check permissions:

```bash
ls -l hello.sh
```

Try running:

```bash
./hello.sh
```

You may get:

```text
Permission denied
```

Now fix it:

```bash
chmod +x hello.sh
```

Run again:

```bash
./hello.sh
```

Then experiment:

```bash
chmod 600 hello.sh
ls -l hello.sh
```

Try to understand how the permission string changes.

---

# What You've Learned 🚀

```text
Linux Permissions
│
├── File Types
│   ├── -
│   ├── d
│   └── l
│
├── Permission Types
│   ├── r → read
│   ├── w → write
│   └── x → execute
│
├── Permission Groups
│   ├── Owner
│   ├── Group
│   └── Others
│
├── chmod
│   ├── Symbolic
│   └── Numeric
│
├── chown
├── chgrp
└── umask
```

## Next Topic: Processes & Job Control ⚙️

This is the natural next step.

You'll learn:

```bash
ps
top
htop
pgrep
pkill
kill
jobs
bg
fg
&
```

And understand:

```text
Terminal
   │
   ├── Foreground Process
   │
   └── Background Process
```

This is essential for running Node.js servers, debugging stuck processes, managing ports, and becoming truly comfortable with Linux process management.