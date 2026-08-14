That's a good refinement. The previous Module 6 I suggested was Linux Networking, but if your goal is to become highly proficient with SSH, it's better to first complete an **SSH Security** module before moving on.

# Module 6 — SSH Security (15 Lessons)

> **Goal:** Learn how to secure SSH servers like a Linux System Administrator or DevOps Engineer.

---

## Lesson 1 — `authorized_keys`

### Learn

- What `authorized_keys` is
- Public key authentication flow
- File format
- Location of `authorized_keys`
- Multiple public keys
- Comments in keys
- Managing keys safely

### Practice

- Generate a new SSH key pair
- Add a public key to `authorized_keys`
- Log in using the new key
- Remove an unused key

---

## Lesson 2 — `authorized_keys` Options

### Learn

Key restrictions such as:

- `command=`
- `from=`
- `no-port-forwarding`
- `no-agent-forwarding`
- `no-X11-forwarding`
- `no-pty`
- `environment=`

### Practice

- Restrict a key to one IP address
- Force a single command
- Disable port forwarding for a specific key

---

## Lesson 3 — Root Login Security

### Learn

- `PermitRootLogin`
- `prohibit-password`
- `forced-commands-only`
- `no`
- Why root SSH login is discouraged
- Using `sudo` instead

### Practice

- Disable root login
- Verify login with a normal user
- Recover safely if locked out

---

## Lesson 4 — Password Authentication

### Learn

- `PasswordAuthentication`
- `PubkeyAuthentication`
- `ChallengeResponseAuthentication`
- `KbdInteractiveAuthentication`
- MFA overview
- Transitioning from passwords to SSH keys

### Practice

- Disable password authentication
- Verify key-based access
- Test recovery methods

---

## Lesson 5 — SSH Key Permissions

### Learn

Correct permissions for:

- `~/.ssh`
- `authorized_keys`
- Private keys
- Public keys

Understand common permission errors.

### Practice

Use:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
```

---

## Lesson 6 — Restricting SSH Users

### Learn

- `AllowUsers`
- `AllowGroups`
- `DenyUsers`
- `DenyGroups`
- Least privilege
- Separate admin accounts

### Practice

Allow only one user to log in via SSH.

---

## Lesson 7 — `fail2ban`

### Learn

- How brute-force attacks work
- How Fail2Ban detects attacks
- Jails
- Filters
- Bans
- Whitelisting trusted IPs

### Practice

- Install Fail2Ban
- Enable the `sshd` jail
- Simulate failed logins
- View banned IPs

---

## Lesson 8 — Hardening `sshd_config`

### Learn

Secure options such as:

- `PermitRootLogin no`
- `PasswordAuthentication no`
- `PermitEmptyPasswords no`
- `MaxAuthTries`
- `LoginGraceTime`
- `MaxSessions`
- `AllowTcpForwarding`
- `X11Forwarding`

### Practice

Build a production-ready `sshd_config`.

---

## Lesson 9 — Modern Cryptography

### Learn

- Ed25519
- RSA (3072+)
- Host keys
- Key exchange (KEX)
- Ciphers
- MAC algorithms
- Deprecated algorithms

### Practice

Inspect supported algorithms:

```bash
ssh -Q cipher
ssh -Q kex
ssh -Q key
```

---

## Lesson 10 — SSH Logging & Auditing

### Learn

- `journalctl`
- `/var/log/auth.log`
- `/var/log/secure`
- Login history
- Failed logins
- Active sessions

### Practice

Analyze SSH login attempts and identify suspicious activity.

---

## Lesson 11 — SSH Certificate Authentication

### Learn

- Difference between SSH keys and SSH certificates
- Certificate Authority (CA)
- User certificates
- Host certificates
- Enterprise SSH

### Practice

Create and use a simple SSH certificate in a lab.

---

## Lesson 12 — Key Rotation & Revocation

### Learn

- Rotating SSH keys
- Revoking compromised keys
- Removing stale access
- Inventory management

### Practice

Replace an old SSH key without causing downtime.

---

## Lesson 13 — Bastion Security

### Learn

- Securing bastion hosts
- MFA
- Audit logging
- Session recording
- Restricting lateral movement
- Network segmentation

### Practice

Harden a bastion host and review access logs.

---

## Lesson 14 — Production SSH Hardening Checklist

### Learn

Create a reusable hardening checklist covering:

- SSH daemon configuration
- Firewall
- Fail2Ban
- Logging
- Updates
- Key management
- User management
- Monitoring

### Practice

Audit an SSH server against the checklist and identify weaknesses.

---

## Lesson 15 — SSH Security Capstone Project

### Project

Build a secure SSH environment with:

- Bastion host
- Private application server
- Key-only authentication
- Root login disabled
- Password authentication disabled
- Restricted users
- `authorized_keys` restrictions
- Fail2Ban enabled
- Hardened `sshd_config`
- Logging and auditing
- Documented security configuration

---

## Skills You'll Master

By the end of this module, you'll be able to:

- ✅ Secure `authorized_keys`
- ✅ Apply per-key restrictions
- ✅ Disable insecure authentication methods
- ✅ Harden an SSH server
- ✅ Configure `fail2ban`
- ✅ Manage SSH users and permissions
- ✅ Audit SSH activity
- ✅ Rotate and revoke SSH keys
- ✅ Secure bastion hosts
- ✅ Deploy a production-grade SSH configuration

This module complements the Advanced SSH module well. After completing it, you'll have both the **operational skills** to use SSH effectively and the **security expertise** to configure and maintain SSH safely in production environments.