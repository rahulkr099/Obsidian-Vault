The next module after **Module 9 — Observability (Logging, Monitoring & Metrics)** is:

# Module 10 — Linux Security & Hardening ⭐⭐⭐⭐⭐

> Learn how to secure Linux servers, protect backend applications, manage users and permissions, harden SSH, detect intrusions, and defend production systems.

**Difficulty:** Intermediate → Advanced

**Goal:** By the end of this module, you'll be able to secure Linux servers for production, reduce attack surfaces, implement access controls, and respond to common security threats.

---

# Part 1 — Linux Security Fundamentals

## Lesson 1: Introduction to Linux Security

- CIA Triad (Confidentiality, Integrity, Availability)
- Threats and attack surfaces
- Principle of least privilege
- Defense in depth
- Security lifecycle
- Common Linux attacks

---

## Lesson 2: Linux Users, Groups & Permissions Review

- User accounts
- Groups
- File permissions
- Ownership
- Special permission bits
- `sudo`
- Privilege separation

---

## Lesson 3: Authentication & Authorization

- Password authentication
- SSH key authentication
- PAM (Pluggable Authentication Modules)
- Multi-factor authentication (MFA)
- Account locking
- Password policies

---

# Part 2 — Securing SSH

## Lesson 4: SSH Hardening

- Disable root login
- Disable password authentication
- Use SSH keys
- Restrict users
- Change SSH port (pros and cons)
- Connection limits
- Idle session timeout

---

## Lesson 5: SSH Security Best Practices

- `authorized_keys`
- Key restrictions
- SSH agent forwarding
- Secure key storage
- Logging SSH activity
- SSH auditing

---

# Part 3 — File System Security

## Lesson 6: File Permissions in Depth

- `chmod`
- `chown`
- `umask`
- ACLs
- Sticky bit
- SUID
- SGID
- Secure file sharing

---

## Lesson 7: Disk Encryption

- Why encrypt disks?
- LUKS overview
- Encrypting partitions
- Key management
- Backup considerations
- Swap encryption

---

# Part 4 — Network Security

## Lesson 8: Firewall Hardening

- `nftables`
- `iptables` review
- `ufw`
- Allow vs deny policies
- Port restrictions
- Service-specific rules

---

## Lesson 9: Intrusion Prevention

- `fail2ban`
- Brute-force protection
- SSH attack prevention
- Log-based banning
- Custom jails
- Whitelisting

---

## Lesson 10: Secure Networking

- Secure ports
- TLS best practices
- Certificate management
- Secure DNS basics
- VPN overview
- Network segmentation

---

# Part 5 — Process & Service Security

## Lesson 11: System Services

- `systemd` security
- Service isolation
- Capabilities
- Running services as non-root
- Service permissions
- Sandboxing basics

---

## Lesson 12: Process Security

- Process ownership
- Signals
- Capabilities
- Secure environment variables
- Resource limits
- Seccomp overview

---

# Part 6 — Auditing & Logging

## Lesson 13: Security Auditing

- `auditd`
- Audit rules
- Monitoring file changes
- Login auditing
- Command auditing
- Compliance basics

---

## Lesson 14: Malware & Rootkit Detection

- Linux malware overview
- Rootkits
- `rkhunter`
- `chkrootkit`
- File integrity monitoring
- Detecting suspicious behavior

---

# Part 7 — Security Operations

## Lesson 15: Incident Response Basics

- Detecting incidents
- Containment
- Evidence collection
- Recovery
- Post-incident review
- Communication during incidents

---

## Lesson 16: Backup & Disaster Recovery

- Backup strategies
- Full vs incremental backups
- Restore testing
- Recovery Point Objective (RPO)
- Recovery Time Objective (RTO)
- Off-site backups

---

## Lesson 17: Linux Hardening Checklist

- Remove unnecessary packages
- Disable unused services
- Secure boot process
- Kernel updates
- Time synchronization
- Configuration review

---

## Lesson 18: Security Automation

- Automatic updates
- Security scanning
- Scheduled audits
- Compliance scripts
- Backup automation
- Alerting

---

## Lesson 19: Production Server Hardening

Build a secure Linux server with:

- Secure SSH
- Firewall rules
- Fail2ban
- User management
- Service isolation
- Secure logging
- Automated backups
- Security monitoring

---

## Lesson 20: Final Security Project

Create and audit a production-ready Linux server by:

- Creating secure users and groups
- Configuring SSH key-only authentication
- Implementing firewall policies
- Installing intrusion prevention
- Enabling auditing
- Hardening services
- Testing backup and recovery
- Performing a security review against a hardening checklist

---

# Tools You'll Master

- `chmod`
- `chown`
- `umask`
- `setfacl`
- `getfacl`
- `sudo`
- `visudo`
- `ssh`
- `sshd`
- `fail2ban`
- `ufw`
- `iptables`
- `nft`
- `auditd`
- `journalctl`
- `rkhunter`
- `chkrootkit`
- `gpg`
- `openssl`
- `systemctl`

---

# Mini Projects

1. Harden an Ubuntu server for production.
2. Configure SSH with key-only authentication.
3. Build firewall rules using `nftables`.
4. Protect against SSH brute-force attacks with `fail2ban`.
5. Configure file permissions and ACLs for a shared project.
6. Encrypt a test partition using LUKS.
7. Create audit rules to monitor sensitive files.
8. Detect and investigate simulated suspicious activity.
9. Automate backups and verify successful restoration.
10. Perform a complete security audit of your Linux server.

---

# What You'll Be Able to Explain in Interviews

- How to secure a Linux server before deploying an application.
- Why SSH keys are preferred over passwords.
- The difference between authentication and authorization.
- How Linux permissions, SUID, SGID, and ACLs work.
- How `fail2ban` protects against brute-force attacks.
- When to use `ufw`, `iptables`, or `nftables`.
- How `auditd` helps with security auditing.
- How to respond to a security incident.
- How to design a secure production environment.

---

## Next Module

After completing Linux Security & Hardening, you'll move to **Module 11 — System Design Fundamentals**, where you'll learn how to design scalable, reliable backend systems and prepare for backend engineering interviews.