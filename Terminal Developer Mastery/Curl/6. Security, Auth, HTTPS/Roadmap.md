# Module 6 — Security, Authentication & HTTPS ⭐⭐⭐⭐⭐

Welcome to **Module 6**, one of the most important modules in the entire `curl` roadmap.

Up to this point, you've mainly worked with **public websites and APIs**. In the real world, however, most backend APIs are **protected**. You'll need to authenticate, securely transmit data, verify certificates, and troubleshoot TLS issues.

This module teaches the security concepts every backend engineer should know.

---

# Module Objectives

By the end of this module, you'll be able to:

- Understand HTTPS and TLS.
- Verify SSL/TLS certificates.
- Use different authentication methods.
- Send API keys securely.
- Work with Bearer (JWT) tokens.
- Understand OAuth 2.0 workflows.
- Use client certificates (mTLS).
- Debug SSL/TLS handshake problems.
- Secure your `curl` commands.

---

# Why This Module Matters

Almost every backend API today requires authentication.

Examples:

```
GitHub API
↓
Bearer Token

Stripe API
↓
API Key

AWS APIs
↓
Signed Requests

Google APIs
↓
OAuth 2.0

Internal Company APIs
↓
JWT / mTLS
```

Without understanding authentication and HTTPS, you'll struggle to work with production APIs.

---

# Skills You'll Gain

## Security

- HTTPS
- TLS
- SSL certificates
- Certificate chains
- Certificate validation
- Self-signed certificates
- Certificate pinning (concept)

---

## Authentication

- Basic Authentication
- Bearer Tokens
- JWT
- API Keys
- OAuth 2.0
- Client Certificates (mTLS)

---

## Debugging

- TLS handshake
- Certificate errors
- Expired certificates
- Hostname mismatch
- Redirect issues
- Authentication failures
- HTTP 401 vs 403

---

## Production Practices

- Secure secret handling
- Environment variables
- Avoid leaking credentials
- Secure logging
- Secure Bash scripting

---

# Module Roadmap (15 Lessons)

## Lesson 1 — HTTPS & TLS Fundamentals

Learn:

- HTTP vs HTTPS
- SSL vs TLS
- Encryption
- Certificates
- Public & Private Keys
- Certificate Authorities (CA)
- TLS Handshake
- Why HTTPS matters

Practice:

```bash
curl <https://example.com>
```

---

## Lesson 2 — SSL/TLS Certificates

Learn:

- View certificates
- Certificate chain
- Expiration
- Issuer
- Subject
- SAN (Subject Alternative Name)

Commands:

```bash
curl -v <https://example.com>
```

```bash
openssl s_client
```

---

## Lesson 3 — Certificate Validation

Learn:

- How certificate validation works
- Trusted CAs
- Self-signed certificates
- Why `curl` sometimes fails

Commands:

```bash
curl --cacert
```

```bash
curl --capath
```

Understand why **`curl -k` (`--insecure`) should almost never be used in production**.

---

## Lesson 4 — Basic Authentication

Learn:

HTTP Basic Auth

Header:

```
Authorization: Basic Base64(username:password)
```

Commands:

```bash
curl -u user:password
```

Practice:

- GET
- POST
- Private APIs

---

## Lesson 5 — Bearer Tokens & JWT

Learn:

```
Authorization: Bearer TOKEN
```

Commands:

```bash
curl \
-H "Authorization: Bearer TOKEN"
```

Topics:

- JWT structure
- Access tokens
- Refresh tokens
- Token expiration

---

## Lesson 6 — API Keys

Methods:

Header:

```
X-API-Key:
```

Authorization header

Query parameters

Learn:

- Good practices
- Secret management
- Environment variables

---

## Lesson 7 — OAuth 2.0

Concepts:

- Resource Owner
- Client
- Authorization Server
- Resource Server

Flows:

- Authorization Code
- Client Credentials
- Device Flow (overview)

Use `curl` to:

- Exchange authorization codes
- Refresh tokens
- Call protected APIs

---

## Lesson 8 — Cookies & Sessions

Topics:

- Session cookies
- Cookie jars
- Login flows
- CSRF (overview)

Commands:

```bash
curl -c cookies.txt
```

```bash
curl -b cookies.txt
```

---

## Lesson 9 — Client Certificates (mTLS)

Learn:

Mutual TLS authentication.

Commands:

```bash
curl \
--cert client.crt \
--key client.key
```

Used in:

- Banking
- Enterprise APIs
- Internal microservices

---

## Lesson 10 — Secure Secret Handling

Learn:

Never hardcode:

```bash
API_KEY="abcd123"
```

Instead:

```bash
export API_KEY="..."
```

Topics:

- `.env`
- Environment variables
- File permissions
- Secret managers (overview)

---

## Lesson 11 — Debugging HTTPS Problems

Learn to debug:

- Expired certificate
- Wrong hostname
- TLS handshake failures
- Proxy problems
- Certificate chain issues

Useful commands:

```bash
curl -v
```

```bash
curl --trace
```

```bash
openssl s_client
```

---

## Lesson 12 — Mini Project: Authenticated API Client

Build a Bash tool that:

- Stores a Bearer token securely
- Makes authenticated API requests
- Handles token expiration
- Logs errors
- Generates reports

---

## Lesson 13 — Mini Project: Secure File Downloader

Build:

- Certificate validation
- Resume downloads
- Retry logic
- SHA-256 checksum verification
- Secure logging

---

## Lesson 14 — Security Best Practices

Topics:

- Secure scripting
- HTTPS only
- Secret management
- Least privilege
- Logging safely
- Avoiding credential leaks
- Production security checklist

---

## Lesson 15 — Module Challenge

Build a complete secure API automation tool that includes:

- HTTPS
- Authentication
- Logging
- Error handling
- Configuration
- Token management
- Report generation

---

# Tools You'll Learn

|Tool|Purpose|
|---|---|
|`curl`|HTTPS requests|
|`openssl`|Inspect certificates|
|`base64`|Basic Auth encoding|
|`jq`|Parse authenticated JSON responses|
|`env`|Environment variables|
|`sha256sum`|Verify downloads|

---

# Prerequisites

You already know:

- ✅ HTTP methods
- ✅ Headers
- ✅ JSON
- ✅ APIs
- ✅ Bash
- ✅ Logging
- ✅ Error handling
- ✅ Automation

Those skills will be used throughout this module.

---

# Real-World Backend Examples

By the end of Module 6, you'll be able to interact with APIs like:

- GitHub REST API
- GitLab API
- Stripe API
- OpenAI API
- Docker Hub API
- Kubernetes API
- AWS services (introductory level)
- Internal company REST APIs

---

# What You'll Build

During this module, you'll create:

1. **Authenticated API Client**
2. **Secure File Downloader**
3. **Secure API Automation Tool (Final Challenge)**

These projects emphasize secure communication and credential handling.

---

# Success Criteria

By the end of Module 6, you should be able to:

- Explain how HTTPS protects data in transit.
- Inspect and troubleshoot TLS certificates.
- Authenticate using Basic Auth, API Keys, Bearer Tokens, and understand OAuth 2.0.
- Use `curl` securely with authenticated APIs.
- Store secrets safely instead of hardcoding them.
- Debug common HTTPS and authentication issues.

---

# Module 6 Progress

```
Module 6 Progress

░░░░░░░░░░░░░░ 0%

⏳ Lesson 1 — HTTPS & TLS Fundamentals
Lesson 2 — SSL/TLS Certificates
Lesson 3 — Certificate Validation
Lesson 4 — Basic Authentication
Lesson 5 — Bearer Tokens & JWT
Lesson 6 — API Keys
Lesson 7 — OAuth 2.0
Lesson 8 — Cookies & Sessions
Lesson 9 — Client Certificates (mTLS)
Lesson 10 — Secure Secret Handling
Lesson 11 — Debugging HTTPS Problems
Lesson 12 — Authenticated API Client
Lesson 13 — Secure File Downloader
Lesson 14 — Security Best Practices
Lesson 15 — Module Challenge
```

---

## 🎯 Why This Module Is Critical for Backend Engineers

In backend development, you'll spend much of your time interacting with **protected APIs** rather than public ones. Whether you're integrating payment gateways, cloud services, third-party platforms, or internal microservices, understanding **HTTPS, authentication, and secure credential handling** is essential.

This module bridges the gap between making simple HTTP requests and working confidently with production-grade APIs.

**Next Lesson:** **Lesson 1 — HTTPS & TLS Fundamentals**