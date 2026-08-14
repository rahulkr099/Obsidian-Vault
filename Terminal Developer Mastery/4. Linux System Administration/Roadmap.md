That's great to hear! 🎉

You've just finished one of the most important backend skills. Docker is something many developers know at a basic level, but combining it with Linux administration is what starts moving you toward being a production-ready backend engineer.

# Module 4 — Linux System Administration 🐧

> **Goal:** Become comfortable managing a Linux server without relying on a GUI.

**Estimated Duration:** 3–5 weeks

**Difficulty:** ⭐⭐⭐⭐☆

---

# Why Linux Administration?

As a backend engineer, your applications usually run on Linux servers. Whether you're deploying to a VPS, a cloud VM, or working with Docker hosts, Linux is the operating system underneath.

You'll learn to answer questions like:

- Why is my backend server down?
- Which process is using port 5000?
- Why is disk space full?
- How do I create a new user?
- Why can't my application access this file?
- How do I restart a crashed service?
- Where are my logs?

---

# What You'll Build

By the end of this module, you'll be able to:

- Configure a Linux server from scratch
- Manage users and permissions
- Secure SSH access
- Manage services with `systemd`
- Troubleshoot processes and ports
- Analyze logs
- Monitor CPU, RAM, and disk usage
- Automate routine tasks
- Prepare a server for backend deployment

---

# Module Roadmap

## Lesson 1 — Linux File Permissions ⭐⭐⭐⭐⭐

Learn:

- Ownership
- Users
- Groups
- Read, write, execute
- `chmod`
- `chown`
- `chgrp`
- Numeric permissions
- Symbolic permissions
- Special permissions (SUID, SGID, Sticky Bit)

Hands-on:

- Create secure project directories
- Restrict access between users

---

## Lesson 2 — Users & Groups ⭐⭐⭐⭐⭐

Learn:

- `useradd`
- `adduser`
- `usermod`
- `passwd`
- `groupadd`
- `groups`
- `sudo`
- `/etc/passwd`
- `/etc/group`

Hands-on:

- Create developers
- Create deployment users
- Manage permissions

---

## Lesson 3 — Process Management ⭐⭐⭐⭐⭐

Learn:

- `ps`
- `top`
- `htop`
- `btop`
- `pgrep`
- `kill`
- `killall`
- `pkill`
- Process priorities
- Foreground vs background jobs

Hands-on:

- Kill hung processes
- Diagnose CPU spikes

---

## Lesson 4 — Services & systemd ⭐⭐⭐⭐⭐

Learn:

- `systemctl`
- Enable services
- Disable services
- Restart services
- Create custom service files
- Service logs
- Auto-start applications

Hands-on:

Run your Node.js backend as a Linux service.

---

## Lesson 5 — Package Management ⭐⭐⭐⭐☆

Learn:

- `apt`
- `dpkg`
- Repositories
- Updating packages
- Removing packages
- Package search

Hands-on:

Install backend development tools safely.

---

## Lesson 6 — Storage Management ⭐⭐⭐⭐☆

Learn:

- `df`
- `du`
- `lsblk`
- `mount`
- `umount`
- Disk partitions
- File systems

Hands-on:

Investigate why a server is running out of disk space.

---

## Lesson 7 — Log Management ⭐⭐⭐⭐⭐

Learn:

- `/var/log`
- `journalctl`
- `tail`
- `less`
- `grep`
- Log rotation

Hands-on:

Debug a crashing backend application using logs.

---

## Lesson 8 — Networking Basics ⭐⭐⭐⭐⭐

Learn:

- `ip`
- `ss`
- `ping`
- `traceroute`
- `curl`
- `wget`
- DNS tools
- Routing basics

Hands-on:

Find out why your backend API isn't reachable.

---

## Lesson 9 — SSH & Remote Servers ⭐⭐⭐⭐⭐

Learn:

- SSH authentication
- SSH keys
- `scp`
- `rsync`
- SSH config
- Secure server access

Hands-on:

Deploy your backend to another Linux machine.

---

## Lesson 10 — Cron Jobs ⭐⭐⭐⭐☆

Learn:

- `crontab`
- Scheduling
- Automation
- Backups
- Cleanup scripts

Hands-on:

Schedule automatic database backups.

---

## Lesson 11 — Monitoring & Performance ⭐⭐⭐⭐⭐

Learn:

- CPU monitoring
- Memory usage
- Disk I/O
- Network monitoring
- `vmstat`
- `iostat`
- `free`
- `uptime`

Hands-on:

Find performance bottlenecks.

---

## Lesson 12 — Linux Security ⭐⭐⭐⭐⭐

Learn:

- Firewall (`ufw`)
- Fail2Ban
- Secure SSH
- File permissions
- User hardening
- Security updates

Hands-on:

Harden a Linux server for production.

---

## Lesson 13 — Production Backend Server ⭐⭐⭐⭐⭐

Capstone project where you'll:

- Create a deployment user
- Configure SSH
- Install Node.js
- Install PostgreSQL or MongoDB
- Configure Nginx
- Run your backend with `systemd`
- Secure the server
- Monitor logs
- Automate backups

This is very close to what you'd do on a real VPS.

---

# Practical Projects

Throughout Module 4, you'll build and manage:

1. **Multi-user Linux environment** with different permission levels.
2. **Production Node.js service** managed by `systemd`.
3. **Secure remote server** using SSH keys.
4. **Automated backup system** with cron jobs.
5. **Production-ready Linux server** hosting a backend application.

---

# Recommended Practice Routine

For each lesson:

1. Learn the concepts.
2. Practice every command in your terminal.
3. Break something intentionally.
4. Fix it using Linux tools.
5. Complete the hands-on challenge.
6. Review the cheat sheet before moving on.

This "break and fix" approach builds the troubleshooting skills you'll rely on in real production environments.

---

# Before We Begin

You already have a strong setup:

- ✅ Linux Mint
- ✅ Kitty
- ✅ Zsh
- ✅ Oh My Zsh
- ✅ Powerlevel10k
- ✅ Neovim
- ✅ Docker
- ✅ Git
- ✅ Terminal-focused workflow

That means we can focus on **Linux administration itself**, rather than spending time installing tools.

---

# 🏆 End Goal

By the end of Modules 1–4, you'll have mastered:

- ✅ Linux shell scripting
- ✅ Linux command line
- ✅ Docker
- ✅ Linux system administration

These four modules form the foundation for backend engineering, DevOps, cloud platforms, and server management.

---

# 📖 Module 4 — Lesson 1

We'll begin with **Linux File Permissions**, one of the most important topics in Linux. Once you truly understand permissions, many "Permission denied" errors that frustrate developers become straightforward to diagnose and fix.

This lesson will go beyond `chmod 777` and teach you _why_ permissions work the way they do, how to use them safely, and how to manage them in production environments.