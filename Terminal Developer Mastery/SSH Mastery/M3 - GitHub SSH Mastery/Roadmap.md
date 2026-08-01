# SSH Mastery — Module 3

# GitHub SSH Mastery

Welcome to **Module 3**. This module focuses on using SSH with GitHub—the method used by professional backend engineers to authenticate securely without repeatedly entering usernames and passwords.

By the end of this module, you'll be able to:

- ✅ Authenticate to GitHub using SSH
- ✅ Clone, push, and pull repositories securely
- ✅ Manage multiple GitHub accounts
- ✅ Understand SSH commit signing
- ✅ Troubleshoot GitHub SSH issues

We'll follow the same format as before:

- 📘 15 lessons
- 💻 Hands-on terminal practice
- ⚠️ Common mistakes
- 🎯 Mini challenges
- 🏗️ Real backend examples

---

# Module 3 Roadmap

## Lesson 1 — Why GitHub SSH?

- HTTPS vs SSH
- Why professionals prefer SSH
- How GitHub authentication works
- The SSH authentication flow

---

## Lesson 2 — SSH Keys Recap

- Public key
- Private key
- Ed25519 vs RSA
- Checking existing keys
- Generating a new key (if needed)

---

## Lesson 3 — Adding Your SSH Key to GitHub

- Copy the public key
- Add it to GitHub
- Name your key
- Best practices

---

## Lesson 4 — Testing GitHub Authentication

```bash
ssh -T git@github.com
```

- Understanding the output
- First-time connection
- Host key verification

---

## Lesson 5 — Cloning with SSH

```bash
git clone git@github.com:user/repo.git
```

- SSH URLs vs HTTPS URLs
- Choosing the right URL
- Existing repositories

---

## Lesson 6 — Push & Pull over SSH

- `git push`
- `git pull`
- Authentication without passwords
- Daily workflow

---

## Lesson 7 — Changing an Existing Repository from HTTPS to SSH

```bash
git remote set-url origin ...
```

- Inspect remotes
- Replace HTTPS with SSH
- Verify the change

---

## Lesson 8 — Managing Multiple GitHub Accounts

- Personal account
- Work account
- Multiple SSH keys
- `~/.ssh/config` for GitHub identities

---

## Lesson 9 — SSH Agent

```bash
ssh-agent
ssh-add
```

- Why it's useful
- Loading keys
- Persisting keys during a session

---

## Lesson 10 — GitHub SSH Troubleshooting

Common errors:

- Permission denied (publickey)
- Repository not found
- Host key verification failed
- Too many authentication failures

---

## Lesson 11 — GitHub Commit Signing with SSH

- What commit signing is
- Why signed commits matter
- Configure Git to sign commits using SSH
- Verify signatures on GitHub

---

## Lesson 12 — GitHub SSH Security

- Protecting private keys
- Using passphrases
- Rotating keys
- Removing old keys
- Lost or compromised keys

---

## Lesson 13 — Real Backend Workflows

Typical daily tasks:

- Clone a new project
- Create a feature branch
- Push changes
- Open a Pull Request
- Pull teammate updates

All using SSH.

---

## Lesson 14 — Mini Project

You'll simulate joining a new company:

- Configure GitHub SSH
- Clone the project
- Push your first commit
- Resolve an authentication issue
- Verify everything works

---

## Lesson 15 — Final Review & Interview Preparation

We'll cover:

- Complete GitHub SSH cheat sheet
- Interview questions
- Common mistakes
- Practical assessment
- Best practices

---

# Prerequisites

Before starting this module, make sure you have:

- ✅ Git installed
- ✅ OpenSSH installed
- ✅ An existing GitHub account
- ✅ An SSH key (or we'll generate one in Lesson 2)

---

# What You'll Build

By the end of this module, you'll have a professional GitHub SSH setup like this:

```
~/.ssh/
├── id_ed25519
├── id_ed25519.pub
├── work_ed25519
├── work_ed25519.pub
└── config
```

With a configuration similar to:

```
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519

Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/work_ed25519
```

You'll be able to work with multiple GitHub accounts cleanly and securely.

---

# Why This Matters for You

Since you're pursuing **backend development with Node.js**, GitHub SSH is something you'll use almost every day:

- Cloning new repositories
- Contributing to open source
- Working with private company repositories
- Deploying code from GitHub to servers
- Collaborating with teammates

Using SSH instead of HTTPS removes repeated authentication prompts and integrates smoothly with professional development workflows.

---

## Learning Outcomes

After completing Module 3, you'll be able to:

- Authenticate to GitHub without passwords
- Use SSH for all Git operations
- Manage multiple GitHub identities
- Sign commits with SSH
- Troubleshoot GitHub authentication issues confidently

---

# Next Step

We'll begin with **Lesson 1: Why GitHub SSH?**

In that lesson, you'll learn:

- Why experienced developers almost always choose **SSH over HTTPS**
- How GitHub authenticates you using SSH keys
- The complete authentication flow from your computer to GitHub
- When HTTPS is still the better choice in certain situations