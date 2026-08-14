Excellent! Module 4 builds directly on your SSH knowledge. Since you've already learned SSH, this module focuses on **moving files safely and efficiently**—a skill you'll use almost every day as a backend developer, DevOps engineer, or system administrator.

---

# Module 4 — Secure File Transfer

## Goal

By the end of this module, you'll be able to:

- Upload project files to a Linux server
- Download logs and backups
- Sync thousands of files efficiently
- Deploy applications using `rsync`
- Transfer files securely over SSH
- Troubleshoot transfer problems

---

# Module Roadmap

|Lesson|Topic|Importance|
|---|---|---|
|1|Introduction to SCP|⭐⭐⭐⭐⭐|
|2|Copy files to remote server|⭐⭐⭐⭐⭐|
|3|Copy files from remote server|⭐⭐⭐⭐⭐|
|4|Recursive directory transfers|⭐⭐⭐⭐⭐|
|5|SFTP interactive mode|⭐⭐⭐⭐|
|6|SFTP commands|⭐⭐⭐⭐|
|7|rsync fundamentals|⭐⭐⭐⭐⭐|
|8|Efficient synchronization|⭐⭐⭐⭐⭐|
|9|Preserve permissions & timestamps|⭐⭐⭐⭐|
|10|Incremental backups|⭐⭐⭐⭐⭐|
|11|Remote deployment workflows|⭐⭐⭐⭐⭐|
|12|Troubleshooting|⭐⭐⭐⭐|
|13|Security best practices|⭐⭐⭐⭐|
|14|Real-world DevOps workflows|⭐⭐⭐⭐⭐|
|15|Mastery Lab|⭐⭐⭐⭐⭐|

---

## What you'll build during this module

By Lesson 15 you'll have practiced:

- Uploading a Node.js project to a VPS
- Downloading server logs
- Syncing websites
- Creating automatic backups
- Deploying applications with one command
- Updating only changed files
- Keeping permissions intact

These are common tasks in real backend and DevOps work.

---

## Skills you'll gain

### SCP

- Secure file copy
- Uploads
- Downloads
- Recursive copy

### SFTP

- Interactive file management
- Navigation
- Upload/download sessions

### rsync

- Fast synchronization
- Incremental transfer
- Compression
- Backup creation
- Deployment automation

---

## Real-world examples

After this module, commands like these will make sense:

```bash
scp app.js user@server:/home/user/
```

```bash
scp -r project/ user@server:/var/www/
```

```bash
rsync -avz project/ user@server:/var/www/project/
```

```bash
rsync -av --delete build/ server:/var/www/html/
```

---

## Prerequisites

You should already know:

- ✅ Linux commands
- ✅ File permissions
- ✅ SSH login
- ✅ Terminal navigation
- ✅ Basic networking

You're ready.

---

## Job relevance

You'll use these skills to:

- Deploy MERN applications
- Upload Docker files
- Download production logs
- Backup databases
- Sync project folders
- Update websites without re-uploading everything

---

# Final Goal

At the end of Module 4, you'll be able to manage files between your Linux machine and remote servers confidently and efficiently.

---

### Next lesson

**Lesson 1 — Introduction to SCP**

You'll learn:

- What SCP is
- How SCP works
- SCP syntax
- SCP vs `cp`
- SCP vs SFTP
- SCP vs `rsync`
- When to use each tool

This lesson lays the foundation for the rest of the module.