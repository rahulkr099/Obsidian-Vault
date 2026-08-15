Since `dog` is no longer compatible with your Linux Mint setup and you've confirmed that **`doggo`** is working, here's a revised version with all `dog` content removed and the `doggo` sections improved.

---

# `doggo` – A Modern DNS Lookup Tool

[Image](https://images.openai.com/static-rsc-4/11qjDlUhiueu50GcfNj24vnYm3mM2olvKyHlH6tgKpTnRHd9m4JW06BVfPDEZmQqUJLW_Nx468549EeEye-m2rFBg4tyJBKxYyQ2OuxL9OTH0dxjJCCfSLwNM-IOoWsQzQjSAyKyhuQDBF5Ba0yTxLNBHmwWqiESx7bhqkcSPWEah56Zjw3QJAtlGOuqKyCH?purpose=fullsize)

[Image](https://images.openai.com/static-rsc-4/4eEgzblAAZKNJLyxbll6weIBplCgGkZIugtsaepkUyouOd-4x7wPKdgGh-1Tsj5WoLhfeJgfi8CL29SbjLk2XGpFlTZ5PRfR4VhJRCjAyCRRqOgeJGTnxfsk_MpgPA4aVZ8vVeq6J8B-b9MHagB1B2rtSoCHjyhHspsN-fB-C_A9DriMfqrFcvkUZxFl1juU?purpose=fullsize)

[Image](https://images.openai.com/static-rsc-4/OJuqpkH_pVN194AXsE201Acw2SUN3NcK6NvP5F0TYCwnQ9hkcWnmpgF4IX68XG0Soqq0u3yGv2mu76UpOtmorRj4r-l8HbdWbwN8xRzUHteZN6WNdTdwujVj0UQb1x0b104qmescqhshNR42-gMBx2oXlIUp0p_8D_UBirwihr0A7FqyuqQ3MKInIN4xziUK?purpose=fullsize)

[Image](https://images.openai.com/static-rsc-4/p6rck5_RNn2yijA0e_jXPsxiCS1NDHY_jR9kPmju1qn6AwXA1Nh4SYgcBU9gghgwlUD05FdPcAHJcbhgFW4RXb_9ZeOplOCXRHRCPlYwG0HtagPFhxMg4rflBvVsxr3N-_jeQj8RGHDd1SOtOJKR37ne8Dk9NcGZWwJcLOMDiOIvjh5Ti2fR4OLWaPfCFUzb?purpose=fullsize)

`doggo` is a modern DNS client written in **Go**. It's fast, lightweight, and works well for both interactive use and automation.

## Why use `doggo`?

|Feature|`doggo`|
|---|---|
|Language|Go|
|DNS Record Types|✅|
|DNS over HTTPS (DoH)|✅|
|DNS over TLS (DoT)|✅|
|JSON Output|✅|
|Batch Queries|✅|
|Script-Friendly|✅|
|Performance|Very fast|
|Maintenance|Actively maintained|

`doggo` is an excellent choice for developers, DevOps engineers, and anyone who frequently works with DNS.

---

# Basic Usage

Lookup a domain:

```bash
doggo google.com
```

Lookup a specific record type:

```bash
doggo google.com A
doggo google.com AAAA
doggo google.com MX
doggo google.com TXT
doggo google.com NS
doggo google.com SOA
```

Query a specific DNS server:

```bash
doggo google.com @8.8.8.8
doggo google.com @1.1.1.1
```

Get JSON output:

```bash
doggo google.com --json
```

JSON output is especially useful when writing shell scripts or backend tools.

---

# What is DNS?

DNS (Domain Name System) is the Internet's phonebook.

When you type:

```
google.com
```

your computer first asks a DNS server:

> "What is the IP address of `google.com`?"

The DNS server replies with something like:

```
142.250.xxx.xxx
```

Only then can your browser connect to the website.

`doggo` lets you query DNS servers directly, making it easier to troubleshoot networking and deployment issues.

---

# When Should You Use `doggo`?

Most developers only think about DNS when something stops working. Here are some common situations.

## 1. Website isn't opening

Suppose you deployed:

```
myapp.com
```

Run:

```bash
doggo myapp.com
```

If no IP address is returned, your DNS configuration may be incorrect.

---

## 2. After buying a custom domain

Example:

```
rahul.dev
```

Check:

```bash
doggo rahul.dev
```

If an **A** record appears, your domain is pointing somewhere.

---

## 3. Debugging Vercel

Browser shows:

```
ERR_NAME_NOT_RESOLVED
```

Run:

```bash
doggo mywebsite.vercel.app
```

If DNS records don't appear, the issue is with DNS rather than React or Express.

---

## 4. Debugging Render

Backend:

```
api.myapp.com
```

Check:

```bash
doggo api.myapp.com
```

Verify that the DNS record points to the correct server.

---

## 5. Checking Hostinger Nameservers

```bash
doggo mydomain.com NS
```

Verify that your domain is using the expected nameservers.

---

## 6. Email Configuration

When using Gmail Workspace, Zoho Mail, Resend, or similar services:

```bash
doggo mydomain.com MX
```

Verify that your mail server records are correctly configured.

---

## 7. Domain Verification

Many services require TXT records.

Examples:

- Google Site Verification
- SPF
- DKIM
- DMARC

Check them with:

```bash
doggo example.com TXT
```

---

## 8. SSL Certificate Issues

If HTTPS isn't working:

```bash
doggo example.com
```

Ensure DNS is correctly configured before investigating SSL certificate problems.

---

# Common DNS Record Types

|Record|Purpose|
|---|---|
|**A**|Maps a domain to an IPv4 address|
|**AAAA**|Maps a domain to an IPv6 address|
|**MX**|Mail server records|
|**TXT**|Verification and security records (SPF, DKIM, DMARC)|
|**NS**|Nameservers for the domain|
|**CNAME**|Alias from one hostname to another|
|**SOA**|Administrative information about the DNS zone|

Examples:

```bash
doggo google.com A
doggo google.com AAAA
doggo google.com MX
doggo google.com TXT
doggo google.com NS
doggo google.com SOA
```

---

# Useful `doggo` Commands

Normal lookup:

```bash
doggo google.com
```

IPv4:

```bash
doggo google.com A
```

IPv6:

```bash
doggo google.com AAAA
```

Mail server:

```bash
doggo google.com MX
```

TXT records:

```bash
doggo google.com TXT
```

Nameservers:

```bash
doggo google.com NS
```

SOA record:

```bash
doggo google.com SOA
```

Use Google's DNS server:

```bash
doggo google.com @8.8.8.8
```

Use Cloudflare's DNS server:

```bash
doggo google.com @1.1.1.1
```

Machine-readable JSON:

```bash
doggo google.com --json
```

---

# Real MERN Development Examples

### Example 1: Render API isn't reachable

```
api.myapp.com
```

Check:

```bash
doggo api.myapp.com
```

If no IP address is returned, fix the DNS before debugging Express or Node.js.

---

### Example 2: Vercel Custom Domain

```
rahulportfolio.com
```

Run:

```bash
doggo rahulportfolio.com
```

Ensure the domain resolves correctly before checking your Vercel configuration.

---

### Example 3: Email Verification

After adding a TXT record for Resend, Google Workspace, or another email provider:

```bash
doggo rahulportfolio.com TXT
```

Verify that the TXT record is visible before completing the verification process.

---

# Why `doggo` Fits Your Workflow

Since you're learning **Linux**, **backend development**, and the **MERN stack**, `doggo` fits naturally into your toolkit.

Use it when you are:

- Debugging deployment issues
- Checking custom domains
- Verifying DNS propagation
- Configuring email services
- Troubleshooting SSL problems
- Writing deployment or monitoring scripts
- Automating DNS checks with JSON output

---

# Practice Challenge

Create a file named `dns-practice.md` and run the following commands for each of these domains:

- `google.com`
- `github.com`
- `vercel.com`
- Your own domain (if you have one)

```bash
doggo google.com
doggo google.com A
doggo google.com AAAA
doggo google.com MX
doggo google.com TXT
doggo google.com NS
doggo google.com SOA
doggo google.com @1.1.1.1
doggo google.com @8.8.8.8
doggo google.com --json
```

For each command, answer these questions:

1. What question did you ask the DNS server?
2. What information did the server return?
3. In what real-world situation would this record be useful?
4. Would you use this during development, deployment, or troubleshooting?

Completing this exercise will give you a practical understanding of DNS that you'll use regularly when deploying MERN applications to platforms like Vercel, Render, or Hostinger.