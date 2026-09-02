# Regular Expressions (Regex) in Linux 🔥

Regex (Regular Expression) is a **pattern language used to search and match text**.

You've already used:

```bash
grep "ERROR" server.log
```

But Regex lets you search much more intelligently.

For example:

```bash
grep '^ERROR' server.log
```

This means:

> Find lines that **start with `ERROR`**.

---

# Why Regex Matters?

Regex is used everywhere in development:

- `grep`
    
- `sed`
    
- `awk`
    
- JavaScript
    
- Python
    
- VS Code search
    
- Validation
    
- Log analysis
    
- Database queries
    
- Form validation
    

As a MERN developer, Regex is especially useful because JavaScript has built-in regex support.

---

# Basic Mental Model 🧠

Suppose we have:

```text
hello
hello world
world hello
hello123
```

Regex lets us ask questions like:

```text
Starts with hello?
Ends with hello?
Contains digits?
Contains only letters?
Has repeated characters?
```

---

# 1. Literal Text

The simplest regex is normal text.

```bash
grep "hello" file.txt
```

Matches:

```text
hello
hello world
world hello
```

---

# 2. `^` — Start of Line

The caret `^` means:

> Starts with

Example:

```bash
grep '^hello' file.txt
```

Matches:

```text
hello
hello world
hello123
```

But not:

```text
world hello
```

### Visual

```text
^hello
│
Start
```

---

# 3. `$` — End of Line

```bash
grep 'world$' file.txt
```

Means:

> Find lines ending with `world`.

Matches:

```text
hello world
```

Visual:

```text
world$
     │
    End
```

---

# 4. `.` — Any Single Character

The dot matches any single character.

Regex:

```text
c.t
```

Matches:

```text
cat
cut
cot
c9t
c@t
```

Example:

```bash
grep 'c.t' file.txt
```

---

# 5. `[]` — Character Classes

Square brackets match **one character from a set**.

Example:

```text
[abc]
```

Matches:

```text
a
b
c
```

---

## Range

```text
[a-z]
```

Any lowercase letter.

```text
[A-Z]
```

Any uppercase letter.

```text
[0-9]
```

Any digit.

Example:

```bash
grep '[0-9]' file.txt
```

Finds lines containing at least one number.

---

# 6. Negation: `[^...]`

`^` inside square brackets means **NOT**.

```text
[^0-9]
```

Means:

> Any character that is NOT a digit.

Example:

```text
^[0-9]$
```

Means:

```text
Start
 ↓
One digit
 ↓
End
```

Matches:

```text
5
```

But not:

```text
55
a
```

---

# 7. `*` — Zero or More 🔥

Example:

```text
ab*
```

Matches:

```text
a
ab
abb
abbb
```

Because:

```text
b*
```

means zero or more `b`s.

Example:

```bash
grep 'ab*' file.txt
```

---

# 8. `+` — One or More 🔥

This has an important Linux detail.

In **Extended Regex (ERE)**:

```text
ab+
```

Means:

```text
a
ab
abb
abbb
```

But with standard/basic `grep`, `+` may need escaping.

Use:

```bash
grep -E 'ab+' file.txt
```

Or:

```bash
grep 'ab\+' file.txt
```

I strongly recommend using:

```bash
grep -E
```

when learning modern regex.

---

# 9. `?` — Zero or One

Using Extended Regex:

```bash
grep -E 'colou?r' file.txt
```

Matches both:

```text
color
colour
```

Because:

```text
u?
```

means:

> `u` is optional.

---

# 10. `{}` — Exact Repetition

Extended Regex.

### Exactly 3 digits

```bash
grep -E '[0-9]{3}' file.txt
```

Matches:

```text
123
456
```

---

### Between 2 and 4 digits

```bash
grep -E '[0-9]{2,4}' file.txt
```

Matches:

```text
12
123
1234
```

---

### At least 2

```bash
grep -E '[0-9]{2,}' file.txt
```

Matches:

```text
12
123
12345
```

---

# 11. `|` — OR

Extended Regex:

```bash
grep -E 'ERROR|WARNING' server.log
```

Matches lines containing:

```text
ERROR
```

OR:

```text
WARNING
```

---

# 12. Grouping with `()`

Example:

```bash
grep -E '(ERROR|WARNING)' server.log
```

Useful when grouping patterns.

Example:

```text
(ha)+
```

Matches:

```text
ha
haha
hahaha
```

---

# 13. `\d`, `\w`, `\s` — Important Caveat ⚠️

In JavaScript and Python regex, you often see:

```text
\d → digit
\w → word character
\s → whitespace
```

But traditional Linux `grep -E` portability differs.

For Linux CLI, prefer POSIX character classes:

```text
[[:digit:]]
[[:alpha:]]
[[:alnum:]]
[[:space:]]
```

Examples:

```bash
grep -E '[[:digit:]]+' file.txt
```

Find lines containing digits.

```bash
grep -E '[[:space:]]+' file.txt
```

Find lines containing whitespace.

This is more portable across Linux tools.

---

# 14. Anchors + Character Classes 🔥

Suppose:

```text
123
456
abc
123abc
```

Find lines containing **only numbers**:

```bash
grep -E '^[0-9]+$' file.txt
```

Explanation:

```text
^       Start
[0-9]+  One or more digits
$       End
```

Matches:

```text
123
456
```

Does NOT match:

```text
abc
123abc
```

---

# 15. Find Lines with Only Letters

```bash
grep -E '^[a-zA-Z]+$' file.txt
```

Matches:

```text
Rahul
Developer
Linux
```

---

# 16. Simple Email Pattern

For basic searching:

```bash
grep -E '[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}' file.txt
```

⚠️ This is useful for finding email-like strings, but **email validation is more complicated** than a simple regex.

---

# 17. Regex with `grep` 🔥

Suppose `server.log`:

```text
INFO Server started
ERROR Database failed
WARNING Memory high
ERROR Authentication failed
INFO User logged in
```

### Lines starting with ERROR

```bash
grep '^ERROR' server.log
```

### ERROR or WARNING

```bash
grep -E 'ERROR|WARNING' server.log
```

### Lines ending with failed

```bash
grep 'failed$' server.log
```

---

# 18. Regex with `sed`

Suppose:

```text
Rahul
Aman
Rahul Kumar
```

Replace lines starting with Rahul:

```bash
sed 's/^Rahul/Developer/' file.txt
```

Output:

```text
Developer
Aman
Developer Kumar
```

---

# 19. Regex with `awk`

Find lines starting with `ERROR`:

```bash
awk '/^ERROR/' server.log
```

Find lines containing digits:

```bash
awk '/[0-9]/' file.txt
```

Regex integrates naturally with `awk`.

---

# 20. Greedy Matching Concept

Consider:

```text
hello12345
```

Pattern:

```text
[0-9]+
```

Matches:

```text
12345
```

The `+` tries to match as many consecutive digits as possible.

This concept becomes especially important in JavaScript regex.

---

# Basic Regex Cheat Sheet 🧠

|Pattern|Meaning|
|---|---|
|`hello`|Literal text|
|`^hello`|Starts with hello|
|`world$`|Ends with world|
|`.`|Any one character|
|`[abc]`|a, b, or c|
|`[a-z]`|Lowercase letter|
|`[A-Z]`|Uppercase letter|
|`[0-9]`|Digit|
|`[^0-9]`|Not a digit|
|`*`|Zero or more|
|`+`|One or more|
|`?`|Zero or one|
|`{3}`|Exactly 3|
|`{2,5}`|Between 2–5|
|`a|b`|
|`(abc)`|Group|

---

# The Most Important Patterns to Memorize 🔥

### Only digits

```text
^[0-9]+$
```

### Only letters

```text
^[a-zA-Z]+$
```

### Starts with

```text
^word
```

### Ends with

```text
word$
```

### Contains number

```text
[0-9]
```

### Optional character

```text
colou?r
```

### Multiple choices

```text
cat|dog
```

---

# BRE vs ERE ⚠️ Important Linux Concept

Linux has two major regex styles.

## Basic Regular Expression (BRE)

```bash
grep 'pattern'
```

Some special characters need escaping.

## Extended Regular Expression (ERE)

```bash
grep -E 'pattern'
```

Supports naturally:

```text
+
?
|
()
{}
```

### My recommendation

For practical learning, mostly use:

```bash
grep -E
```

It makes regex easier to read.

---

# A Practical Developer Example 🚀

Suppose you have logs:

```text
INFO GET /api/users 200
ERROR POST /api/login 401
INFO GET /api/products 200
ERROR GET /api/users 500
WARNING GET /api/cache 503
```

Find HTTP errors:

```bash
grep -E ' [45][0-9]{2}$' server.log
```

Explanation:

```text
[45]        4 or 5
[0-9]{2}    followed by two digits
$           at end of line
```

Matches:

```text
ERROR POST /api/login 401
ERROR GET /api/users 500
WARNING GET /api/cache 503
```

That's a realistic log-analysis use case. 🔥

---

# Regex Learning Strategy 🎯

Don't try to memorize every regex symbol.

Learn in this order:

```text
Level 1
├── Literal text
├── ^ start
├── $ end
├── .
└── []

Level 2
├── *
├── +
├── ?
└── {}

Level 3
├── |
├── ()
└── Negation [^]

Level 4
├── grep regex
├── sed regex
├── awk regex
└── JavaScript regex
```

---

# Practice Challenge 💪

Given:

```text
Rahul
rahul123
12345
hello_world
test@email.com
ERROR Database failed
```

Try to write regex for:

### 1. Lines containing only numbers

```text
?
```

Answer:

```text
^[0-9]+$
```

### 2. Lines starting with ERROR

```text
?
```

Answer:

```text
^ERROR
```

### 3. Lines containing an email-like pattern

Try:

```text
.+@.+\..+
```

### 4. Lines containing at least one digit

```text
[0-9]
```

---

# Your Linux Learning Roadmap 🚀

You've now covered:

```text
Linux Text Processing
│
├── cat
├── less
├── head
├── tail
├── grep
├── sort
├── uniq
├── wc
├── cut
├── tr
├── tee
├── paste
├── sed
├── awk
│
├── Pipes
├── Redirection
├── Command Chaining
├── xargs
├── find
└── Regex 🔥
```

## Next Topic Recommendation: `stdin`, `stdout`, and `stderr` Deep Dive

You already saw them briefly during redirection, but understanding them properly is a **major Linux concept**.

You'll learn why this works:

```bash
command > output.txt 2> errors.txt
```

and exactly what these mean:

```text
0 → stdin
1 → stdout
2 → stderr
```

After that, shell scripting will become much easier because you'll understand how Linux processes communicate. 🚀