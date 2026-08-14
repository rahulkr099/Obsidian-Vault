# 🚀 curl Mastery Course

# Module 4 — File Transfers & Downloads

**Difficulty:** ⭐⭐⭐⭐☆ → ⭐⭐⭐⭐⭐

**Estimated Time:** 12–15 Hours

> **Goal:** Master downloading, uploading, transferring, verifying, and automating files using `curl`. By the end of this module, you'll be able to handle everything from downloading Linux ISOs to uploading backups, interacting with cloud storage, and building production-ready file transfer scripts.

---

# 🎯 Module Objectives

By the end of this module, you'll be able to:

- Download files efficiently
- Resume interrupted downloads
- Upload files using HTTP
- Work with multipart uploads
- Stream large files
- Verify file integrity
- Perform parallel downloads
- Handle authentication for downloads
- Transfer files securely
- Automate file transfer workflows

---

# 📚 Module 4 Roadmap

|Lesson|Topic|Difficulty|
|---|---|---|
|**Lesson 1**|Downloading Files (`-O`, `-o`, `-J`)|⭐⭐☆☆☆|
|**Lesson 2**|Resuming Downloads (`-C -`)|⭐⭐⭐☆☆|
|**Lesson 3**|Uploading Files (PUT & POST)|⭐⭐⭐⭐☆|
|**Lesson 4**|Multipart File Uploads (`-F`)|⭐⭐⭐⭐☆|
|**Lesson 5**|Download Verification (SHA256, MD5, Checksums)|⭐⭐⭐⭐☆|
|**Lesson 6**|Authentication for File Transfers|⭐⭐⭐⭐☆|
|**Lesson 7**|Large Files & Streaming|⭐⭐⭐⭐⭐|
|**Lesson 8**|Parallel Downloads & Batch Transfers|⭐⭐⭐⭐⭐|
|**Lesson 9**|Production Backup & Restore Workflows|⭐⭐⭐⭐⭐|
|**Lesson 10**|File Transfer Toolkit (Capstone Project)|⭐⭐⭐⭐⭐|

---

# 🧠 Skills You'll Gain

After completing this module, you'll know how to:

### Download Files

- Save files with original names
- Save files with custom names
- Resume interrupted downloads
- Follow download redirects
- Limit download speed
- Show progress

---

### Upload Files

- HTTP PUT uploads
- HTTP POST uploads
- Multipart/form-data uploads
- Upload multiple files
- Upload with authentication
- Upload binary files

---

### Verify Downloads

- SHA256
- SHA512
- MD5 (legacy)
- Compare checksums
- Detect corrupted downloads

---

### Stream Data

- Download directly to another program
- Stream logs
- Stream archives
- Pipe responses
- Avoid temporary files

---

### Automate Transfers

- Backup scripts
- Deployment scripts
- Batch downloads
- Scheduled jobs (cron)
- Retry failed transfers
- Logging

---

### Performance

- Resume transfers
- Parallel downloads
- Compression
- Timing
- Speed limits
- Progress meters

---

# 🏗️ Real-World Examples

Throughout this module, you'll build tools like:

## Linux ISO Downloader

```
Download Ubuntu ISO

↓

Resume if interrupted

↓

Verify SHA256

↓

Done
```

---

## Backup Uploader

```
Create Backup

↓

Compress

↓

Upload

↓

Verify

↓

Log Result
```

---

## Artifact Downloader

```
GitHub Release

↓

Download Binary

↓

Verify Checksum

↓

Install
```

---

## Deployment Helper

```
Build Project

↓

Upload Files

↓

Verify Upload

↓

Restart Server
```

---

## Batch Downloader

```
Read URLs

↓

Download in Parallel

↓

Retry Failures

↓

Generate Report
```

---

# 🧰 Tools You'll Use

Besides `curl`, you'll also use common Linux utilities:

|Tool|Purpose|
|---|---|
|`sha256sum`|Verify downloads|
|`md5sum`|Legacy checksum verification|
|`gzip`|Compression|
|`tar`|Archive files|
|`xz`|High-ratio compression|
|`jq`|Parse JSON APIs|
|`tee`|Save logs while displaying output|
|`pv` _(optional)_|Monitor transfer speed|
|`file`|Identify downloaded file types|
|`stat`|Inspect file metadata|

---

# 🎓 Final Capstone Project

By the end of Module 4, you'll build a complete project:

```
curl-file-toolkit/
│
├── downloads/
├── uploads/
├── backups/
├── checksums/
├── logs/
├── scripts/
│   ├── download.sh
│   ├── upload.sh
│   ├── verify.sh
│   ├── backup.sh
│   ├── restore.sh
│   ├── batch-download.sh
│   └── cleanup.sh
├── reports/
├── .env
├── README.md
└── .gitignore
```

This toolkit will be suitable for:

- Backend Development
- DevOps
- Linux Administration
- CI/CD Pipelines
- Server Maintenance
- Cloud Deployments

---

# 💼 Industry Relevance

These skills are used by:

- ✅ Backend Developers
- ✅ DevOps Engineers
- ✅ Site Reliability Engineers (SREs)
- ✅ Linux System Administrators
- ✅ QA Automation Engineers
- ✅ Platform Engineers
- ✅ Cloud Engineers

---

# 📖 Learning Path

```
Lesson 1
↓

Download Files

↓

Lesson 2

Resume Downloads

↓

Lesson 3

Upload Files

↓

Lesson 4

Multipart Uploads

↓

Lesson 5

Verify Downloads

↓

Lesson 6

Authentication

↓

Lesson 7

Streaming

↓

Lesson 8

Parallel Downloads

↓

Lesson 9

Production Workflows

↓

Lesson 10

Complete File Transfer Toolkit
```

---

# 🎯 Prerequisites

Before starting Module 4, you should already be comfortable with:

- HTTP methods (`GET`, `POST`, `PUT`, `DELETE`)
- Headers
- Authentication
- Timeouts
- Retries
- Compression
- Basic Bash scripting

You've covered all of these in the previous modules, so you're ready.

---

# 🚀 What Makes This Module Different?

Until now, you've mainly used `curl` for interacting with APIs.

In this module, you'll learn to use `curl` as a **professional file transfer tool**, including:

- Downloading software releases from GitHub
- Fetching Docker images and artifacts
- Uploading backups to servers
- Restoring files from remote systems
- Automating downloads in CI/CD pipelines
- Handling large production data transfers safely

---

## ⏭️ Next Lesson

**Module 4 – Lesson 1: Downloading Files (`-O`, `-o`, `-J`)**

You'll learn:

- Saving files with custom names
- Preserving the server's filename
- Downloading multiple files
- Following redirects while downloading
- Progress bars and silent mode
- Limiting download speed
- Best practices for production downloads