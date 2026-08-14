> **"Regex is the search language behind Linux, programming, databases, editors, and APIs."**

If you know regex, you can search, validate, extract, and transform text with incredible precision.

You'll use regex in:

- Bash (`grep`, `sed`, `awk`)
- JavaScript (`RegExp`)
- Python
- Java
- VS Code Search
- MongoDB
- SQL
- Nginx
- Apache
- Git
- CI/CD pipelines

As a MERN backend developer, regex is a skill you'll use throughout your career.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Understand regex fundamentals
- Match characters, words, and patterns
- Use quantifiers and anchors
- Create capture groups
- Validate common input formats
- Use regex with `grep`, `sed`, and `awk`
- Debug regex effectively

**Estimated Time:** 8–10 hours

**Difficulty:** ⭐⭐⭐⭐⭐

---

# What is a Regular Expression?

A **Regular Expression (Regex)** is a pattern used to match text.

Instead of searching for:

```
error
```

You can search for:

```
ERROR
Error
error
ERROR123
```

using a single pattern.

---

# Your First Regex

Create a file:

```
log.txt
```

Contents:

```
ERROR Database failed
INFO Server started
WARNING Disk space low
ERROR Redis unavailable
```

Search:

```bash
grep "ERROR" log.txt
```

Output:

```
ERROR Database failed
ERROR Redis unavailable
```

---

# Dot (`.`)

Matches **any single character**.

Pattern:

```
c.t
```

Matches:

```
cat
cut
cot
c9t
c-t
```

Does **not** match:

```
cart
ct
```

Example:

```bash
grep "c.t" words.txt
```

---

# Character Classes (`[]`)

Match one character from a set.

Example:

```
gr[ae]y
```

Matches:

```
gray
grey
```

---

Numbers:

```
[0-9]
```

Letters:

```
[a-z]
```

Uppercase:

```
[A-Z]
```

Alphanumeric:

```
[A-Za-z0-9]
```

---

# Negated Character Classes (`[^]`)

Example:

```
[^0-9]
```

Matches anything **except** digits.

---

# Quantifiers

Zero or more.

```
ab*
```

Matches:

```
a
ab
abb
abbb
```

---

## `+`

One or more.

```
ab+
```

Matches:

```
ab
abb
abbbb
```

Not:

```
a
```

With `grep`, use extended regex:

```bash
grep -E "ab+" file.txt
```

---

## `?`

Zero or one.

```
colou?r
```

Matches:

```
color
colour
```

---

## `{n}`

Exactly `n` occurrences.

```
[0-9]{4}
```

Matches:

```
2026
1234
```

---

## `{n,m}`

Between `n` and `m`.

```
[a-z]{3,5}
```

Matches words with 3–5 lowercase letters.

---

# Anchors

## Beginning of Line (`^`)

```
^ERROR
```

Matches only if the line starts with `ERROR`.

```bash
grep "^ERROR" log.txt
```

---

## End of Line (`$`)

```
failed$
```

Matches:

```
Database failed
```

Not:

```
failed yesterday
```

---

# Word Boundaries

Using `grep -w`:

```bash
grep -w "user" file.txt
```

Matches:

```
user
```

Not:

```
username
superuser
```

---

# Common Shorthand Classes (Extended Regex)

Many regex engines support:

```
\d
```

Digit.

Equivalent to:

```
[0-9]
```

---

Whitespace:

```
\s
```

---

Word character:

```
\w
```

---

⚠️ **Note:** Standard `grep` does **not** support `\d`, `\s`, and `\w`. Use:

- `grep -P` (Perl-compatible regex, if available)
- `perl`
- `ripgrep (rg -P)`
- programming languages like JavaScript or Python

For portable shell scripts, prefer `[0-9]`, `[[:space:]]`, and `[[:alnum:]_]`.

---

# Capture Groups

```
(user)-([0-9]+)
```

Matches:

```
user-42
```

Groups:

```
1 → user

2 → 42
```

Capture groups become especially useful in `sed`, JavaScript, and many programming languages.

---

# Alternation (`|`)

Match either pattern.

```
cat|dog
```

Matches:

```
cat

dog
```

Use with:

```bash
grep -E "cat|dog" pets.txt
```

---

# Escaping Special Characters

Want to match:

```
file.txt
```

Regex:

```
file\.txt
```

The dot must be escaped because `.` normally means "any character."

---

# Regex with `grep`

Search phone numbers:

```
9876543210
```

```bash
grep -E "^[0-9]{10}$" numbers.txt
```

---

Search emails (basic example):

```bash
grep -E "^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$" emails.txt
```

---

Search IP addresses (simplified):

```bash
grep -E "^([0-9]{1,3}\.){3}[0-9]{1,3}$" ips.txt
```

---

# Regex with `sed`

Replace years:

```bash
sed -E 's/[0-9]{4}/YEAR/g'
```

Input:

```
2024
2025
2026
```

Output:

```
YEAR
YEAR
YEAR
```

---

# Regex with `awk`

Print lines where the second field is numeric:

```bash
awk '$2 ~ /^[0-9]+$/'
```

---

# Backend Example — Validate Port

```bash
grep -E "^[0-9]{2,5}$"
```

Matches:

```
3000
8080
5432
```

---

# Backend Example — JWT Secret

Require at least 32 characters:

```
^.{32,}$
```

---

# Backend Example — Semantic Version

Match:

```
1.0.0

2.15.7

10.4.19
```

Regex:

```
^[0-9]+\.[0-9]+\.[0-9]+$
```

---

# Backend Example — Git Branch

Allowed:

```
feature/login

fix/auth

hotfix/api
```

Regex:

```
^(feature|fix|hotfix)/[a-z0-9-]+$
```

Useful in CI/CD validation.

---

# Backend Example — `.env`

Extract variables:

```bash
grep -E "^[A-Z_]+=.*" .env
```

---

# Hands-on Lab

Create:

```
validator.sh
```

Ask the user for:

- Email
- Phone number
- Port number

Validate each using regex.

Print:

```
Valid
```

or

```
Invalid
```

---

# Mini Project

Create:

```
log-filter.sh
```

Given:

```
server.log
```

Generate:

- ERROR count
- WARNING count
- 404 count
- 500 count
- IP addresses
- Email addresses (if present)

Use `grep -E` with regular expressions.

---

# Common Mistakes

## Forgetting `E`

Wrong:

```bash
grep "[0-9]+"
```

`+` is treated as a literal character in basic `grep`.

Correct:

```bash
grep -E "[0-9]+"
```

---

## Not Escaping Dots

Wrong:

```
file.txt
```

Matches:

```
file1txt
filextxt
```

Correct:

```
file\.txt
```

---

## Using `.*` Everywhere

This can become too greedy.

Prefer more specific patterns whenever possible.

---

## Assuming Regex Validates Everything

Example:

```
999.999.999.999
```

A simple IPv4 regex may match it, even though it's not a valid IP address.

Regex validates format, not always correctness.

---

# Interview Questions

1. What is a regular expression?
2. Explain `.`, , `+`, and `?`.
3. What's the difference between `^` and `$`?
4. What is a character class?
5. What are capture groups?
6. How do you search for a valid email?
7. Why is `grep -E` useful?

---

# Cheat Sheet

```
.              Any character
[abc]          One of a, b, c
[^abc]         Not a, b, c
[a-z]          Lowercase letter
[0-9]          Digit
*              Zero or more
+              One or more
?              Zero or one
{3}            Exactly 3
{2,5}          Between 2 and 5
^              Start of line
$              End of line
(...)          Capture group
|              OR
\.             Literal dot
```

---

# Weekly Challenge 🚀

Build:

```
env-auditor.sh
```

Given a project directory, the script should:

1. Find every `.env` file.
2. Verify each required variable:

```
PORT
DATABASE_URL
JWT_SECRET
NODE_ENV
```

1. Ensure:

- `PORT` is numeric.
- `JWT_SECRET` has at least 32 characters.
- `NODE_ENV` is one of:

```
development
production
test
```

1. Generate a report showing which files pass or fail validation.

Use only Bash, `grep -E`, and other standard Linux tools.

---

# ⭐ Pro Challenge (Backend Engineer)

Create:

```
access-security-check.sh
```

Analyze an `access.log` file and report:

- Invalid HTTP methods
- Malformed IP addresses
- Suspicious URL patterns (such as repeated `../`)
- Requests with SQL injection keywords like `UNION`, `SELECT`, or `DROP`
- Requests with `<script>` tags

This introduces the idea of using regex as a lightweight first pass for security monitoring.

---

# ⭐ Module 2 Progress

```
✅ Lesson 1 — Advanced Parameter Expansion
✅ Lesson 2 — Command Substitution & Process Substitution
✅ Lesson 3 — Here Documents & Here Strings
✅ Lesson 4 — Advanced Text Processing
✅ Lesson 5 — Regular Expressions

⬜ Lesson 6 — Signals, Traps & Process Control
⬜ Lesson 7 — Background Jobs & Parallel Processing
⬜ Lesson 8 — Scheduling (cron, at, systemd timers)
⬜ Lesson 9 — Writing Reusable Bash Libraries
⬜ Lesson 10 — API Automation with curl & JSON
⬜ Lesson 11 — Production Automation Projects
⬜ Lesson 12 — Final DevOps Toolkit Capstone
```

---

# 💡 Backend Engineer Insight

Regex is everywhere in backend development:

- **Express.js** route validation
- **Joi** and **Zod** input validation
- **MongoDB** text searches
- **NGINX** URL matching
- **GitHub Actions** workflow filters
- **Log analysis** and monitoring
- **VS Code** search and replace
- **CI/CD** branch naming rules

The goal isn't to memorize every regex pattern. Instead:

1. Learn the building blocks (`[]`, `()`, , `+`, `?`, `^`, `$`).
2. Practice combining them.
3. Test patterns with real data.

Once you're comfortable with regex, you'll find many text-processing tasks become much simpler.

In **Lesson 6**, we'll explore **Signals, Traps & Process Control**, where you'll learn how Linux handles process lifecycle events, clean shutdowns, interrupts (`Ctrl+C`), background services, and graceful cleanup—essential knowledge for writing robust automation scripts and managing long-running backend processes.