Those are excellent recommendations. Since you're becoming a backend developer and you've already built Express APIs, URL Shortener, and Todo backend, both of these will become daily tools rather than "nice to have".

Here's how I'd use them in real projects.

---

# 1. jq — Your JSON Swiss Army Knife ⭐⭐⭐⭐⭐

Think of `jq` as **grep for JSON**.

Whenever an API returns a huge JSON response, `jq` lets you extract exactly what you need.

## Installation

```bash
sudo apt install jq
```

---

## Scenario 1: Debug your Express API

Suppose your backend returns

```json
{
  "success": true,
  "user": {
    "name": "Rahul",
    "email": "rahul@gmail.com",
    "role": "admin"
  }
}
```

Instead of reading everything

```bash
curl localhost:3000/profile
```

use

```bash
curl localhost:3000/profile | jq '.user.email'
```

Output

```
"rahul@gmail.com"
```

---

## Scenario 2: Pretty-print JSON

Without jq

```
{"id":1,"name":"Rahul","age":21}
```

With jq

```bash
curl localhost:3000/user | jq
```

Output

```json
{
  "id": 1,
  "name": "Rahul",
  "age": 21
}
```

---

## Scenario 3: Extract an array

```bash
curl <https://dummyjson.com/users> \
| jq '.users[].firstName'
```

Output

```
"Terry"
"Sheldon"
"Terrill"
...
```

---

## Scenario 4: Multiple fields

```bash
jq '.users[] | {name: .firstName, email: .email}'
```

Output

```json
{
  "name": "Terry",
  "email": "..."
}
```

---

## Scenario 5: Filter data

Users older than 30

```bash
jq '.users[] | select(.age > 30)'
```

---

## Scenario 6: Count objects

```bash
jq '.users | length'
```

Output

```
30
```

---

## Scenario 7: Get the last object

```bash
jq '.users[-1]'
```

---

## Scenario 8: Sort

```bash
jq '.users | sort_by(.age)'
```

---

## Scenario 9: Pipe with fzf

Pick a user interactively

```bash
curl <https://dummyjson.com/users> \
| jq -r '.users[].firstName' \
| fzf
```

---

## Scenario 10: Read local JSON

```bash
cat package.json | jq '.dependencies'
```

Very useful for checking dependency versions.

---

# 2. xh ⭐⭐⭐⭐⭐

Think of it as

> curl + human-friendly syntax

Install

```bash
sudo apt install xh
```

or

```bash
cargo install xh
```

---

## GET request

Instead of

```bash
curl localhost:3000/users
```

Use

```bash
xh :3000/users
```

---

## POST request

Instead of

```bash
curl \
-X POST \
-H "Content-Type: application/json" \
-d '{"email":"abc","password":"123"}'
```

Use

```bash
xh POST :3000/login \
email=abc \
password=123
```

Much cleaner.

---

## Custom Header

```bash
xh GET :3000/profile \
Authorization:"Bearer TOKEN"
```

---

## Send JSON

```bash
xh POST :3000/user \
name=Rahul \
age:=22
```

Notice

```
=
```

means string

```
:=
```

means JSON value

---

## Upload a file

```bash
xh POST :3000/upload \
file@photo.png
```

---

## Download

```bash
xh GET <https://example.com/file.pdf> \
--download
```

---

## Save response

```bash
xh GET :3000/users > users.json
```

---

## Pretty colors

Unlike curl, responses are colorized automatically.

---

## Show request only

```bash
xh --offline POST :3000/login \
email=test \
password=123
```

Very useful while learning APIs.

---

# xh + jq together ❤️

This is where things become really powerful.

```bash
xh :3000/users | jq
```

Pretty response.

---

Extract emails

```bash
xh :3000/users \
| jq '.[].email'
```

---

Interactive picker

```bash
xh :3000/users \
| jq -r '.[].name' \
| fzf
```

---

Get one user's email

```bash
xh :3000/users \
| jq -r '.[0].email'
```

---

# Your backend debugging workflow

Imagine you're testing your Todo backend:

```bash
xh POST :3000/api/auth/login \
email=rahul@gmail.com \
password=secret
```

↓

```bash
xh GET :3000/api/todos \
Authorization:"Bearer $TOKEN"
```

↓

```bash
... | jq
```

↓

```bash
... | jq '.todos[].title'
```

↓

```bash
... | jq '.todos | length'
```

No Postman needed for quick checks.

---

# More terminal tools I'd recommend

Since your current setup already includes `fzf`, `zoxide`, `ripgrep`, `bat`, `lsd`, `lazygit`, `yazi`, `btop`, `tldr`, `tmux`, and a customized `kitty` + `zsh` environment, these fit naturally into your workflow:

|Tool|Purpose|Rating|
|---|---|---|
|`eza`|Modern replacement for `ls` (successor to `exa`)|⭐⭐⭐⭐⭐|
|`dust`|Better `du` with visual output|⭐⭐⭐⭐⭐|
|`dua`|Interactive disk usage explorer|⭐⭐⭐⭐⭐|
|`procs`|Modern `ps` command|⭐⭐⭐⭐☆|
|`hyperfine`|Benchmark commands and scripts|⭐⭐⭐⭐⭐|
|`delta`|Beautiful colored `git diff` output|⭐⭐⭐⭐⭐|
|`choose`|Lightweight alternative to `awk` for field selection|⭐⭐⭐⭐☆|
|`sd`|Simpler, faster replacement for `sed`|⭐⭐⭐⭐☆|
|`dog`|User-friendly DNS lookup tool|⭐⭐⭐⭐☆|
|`bandwhich`|See which processes are using network bandwidth|⭐⭐⭐⭐⭐|
|`watchexec`|Re-run commands automatically when files change|⭐⭐⭐⭐⭐|
|`httpie`|Another popular human-friendly HTTP client (similar to `xh`)|⭐⭐⭐⭐☆|

## My top five for a MERN backend developer

1. `jq` — inspect and transform JSON.
2. `xh` — fast API testing from the terminal.
3. `hyperfine` — compare the performance of scripts or commands.
4. `delta` — much easier-to-read Git diffs.
5. `watchexec` — automatically rerun tests, linters, or build commands whenever files change.

Learning these alongside the tools you already use will make your terminal feel like a complete development environment and reduce how often you need graphical tools for everyday backend work.

Since you're using **Linux Mint Cinnamon (Ubuntu-based)**, here are the easiest installation methods.

> **First update your package lists:**

```bash
sudo apt update
```

---

# 1. dust ⭐⭐⭐⭐⭐

Better `du` with colorful output.

### Install

```bash
sudo apt install dust
```

If not available:

```bash
cargo install du-dust
```

Check

```bash
dust
```

---

# 2. dua ⭐⭐⭐⭐⭐

Interactive disk usage analyzer.

### Install

```bash
cargo install dua-cli
```

Check

```bash
dua .
```

Interactive mode

```bash
dua i
```

---

# 3. procs ⭐⭐⭐⭐☆

Modern replacement for `ps`.

### Install

```bash
sudo apt install procs
```

or

```bash
cargo install procs
```

Check

```bash
procs
```

---

# 4. hyperfine ⭐⭐⭐⭐⭐

Benchmark commands.

### Install

```bash
sudo apt install hyperfine
```

or

```bash
cargo install hyperfine
```

Example

```bash
hyperfine "ls" "eza"
```

---

# 5. delta ⭐⭐⭐⭐⭐

Beautiful Git diff viewer.

### Install

```bash
sudo apt install git-delta
```

or

```bash
cargo install git-delta
```

Configure Git

```bash
git config --global core.pager delta
git config --global interactive.diffFilter "delta --color-only"
git config --global delta.navigate true
git config --global delta.side-by-side true
git config --global delta.line-numbers true
```

---

# 6. choose ⭐⭐⭐⭐☆

Tiny alternative to `awk`.

### Install

```bash
cargo install choose
```

Example

```bash
echo "Rahul 21 India" | choose 1
```

Output

```
21
```

---

# 7. sd ⭐⭐⭐⭐☆

A modern `sed`.

### Install

```bash
sudo apt install sd
```

or

```bash
cargo install sd
```

Example

```bash
echo "hello world" | sd world Rahul
```

Output

```
hello Rahul
```

---

# 8. dog ⭐⭐⭐⭐☆

Better DNS lookup.

### Install

```bash
cargo install dog
```

or

```bash
sudo apt install dog
```

Example

```bash
dog google.com
```

---

# 9. bandwhich ⭐⭐⭐⭐⭐

Shows which processes are using the network.

### Install

```bash
cargo install bandwhich
```

Run

```bash
sudo bandwhich
```

---

# 10. watchexec ⭐⭐⭐⭐⭐

Automatically reruns commands when files change.

### Install

```bash
sudo apt install watchexec
```

or

```bash
cargo install watchexec-cli
```

Example

```bash
watchexec npm test
```

Whenever a file changes, it reruns the command.

---

# 11. HTTPie ⭐⭐⭐⭐☆

Another friendly HTTP client.

### Install

```bash
sudo apt install httpie
```

Check

```bash
http --version
```

Example

```bash
http GET :3000/users
```

---

# Install Rust (Cargo) once

Many modern CLI tools are written in Rust. If you don't already have `cargo`, install it once:

```bash
sudo apt install cargo
```

or, for the latest toolchain:

```bash
curl --proto '=https' --tlsv1.2 -sSf <https://sh.rustup.rs> | sh
```

Then reload your shell:

```bash
source ~/.cargo/env
```

Verify:

```bash
cargo --version
```

---

# Install all Cargo-based tools at once

```bash
cargo install \
dua-cli \
procs \
hyperfine \
git-delta \
choose \
sd \
dog \
bandwhich \
watchexec-cli \
du-dust
```

---

# Verify everything

```bash
dust --version
dua --version
procs --version
hyperfine --version
delta --version
choose --version
sd --version
dog --version
bandwhich --version
watchexec --version
http --version
```

---

## My recommendation for your setup

Given your MERN stack work and heavily customized terminal, I'd install them in this order:

1. ✅ `delta` – makes Git diffs much easier to review.
2. ✅ `hyperfine` – compare command or script performance.
3. ✅ `dust` – quickly find what's using disk space.
4. ✅ `procs` – clearer process listing than `ps`.
5. ✅ `watchexec` – automatically rerun tests or builds during development.
6. ✅ `bandwhich` – inspect network activity.
7. ✅ `dua` – interactive disk cleanup.
8. ✅ `sd` – quick text replacement.
9. ✅ `dog` – DNS debugging.
10. ✅ `httpie` or `xh` – keep one as your primary API client (both are excellent, so choose the one whose syntax you prefer).
11. ✅ `choose` – useful for simple command-line data extraction.

This is the right question.

Most people install dozens of terminal tools and only use `ls`, `cd`, and `grep`. The goal isn't to collect tools—it's to know **when a tool solves a real problem**.

Since you're a **MERN backend developer** who also uses **Git**, **Linux**, **Neovim**, **fzf**, **yazi**, and **tmux**, here's a practical guide.

---

# 1. delta ⭐⭐⭐⭐⭐

> Beautiful Git diffs.

## When?

Whenever you're working with Git.

Instead of

```bash
git diff
```

You'll see

- Better syntax highlighting
- Side-by-side diff
- Easier navigation

### Example

Before committing

```bash
git diff
```

Review

```bash
git add .
git commit
```

### Real-world scenario

You accidentally modified 15 files.

Run

```bash
git diff
```

with delta.

Now you instantly know

- what changed
- where
- whether something broke

You'll use it every single day.

---

# 2. hyperfine ⭐⭐⭐⭐⭐

> Compare speed.

## When?

Whenever you wonder

> Which command is faster?

Example

```bash
hyperfine "npm install" "pnpm install"
```

or

```bash
hyperfine "node app.js" "bun app.js"
```

or

```bash
hyperfine "rg TODO" "grep -R TODO ."
```

### Real-world

You're optimizing your backend.

Should you use

- Express middleware A
- Express middleware B

Benchmark both.

---

# 3. dust ⭐⭐⭐⭐⭐

Better disk usage.

## Instead of

```bash
du -sh *
```

Use

```bash
dust
```

You'll instantly see

```
3.5 GB node_modules
1.2 GB Downloads
800 MB Videos
```

### Real-world

Laptop says

> Disk Full

Run

```bash
dust ~
```

Find the culprit.

---

# 4. dua ⭐⭐⭐⭐⭐

Interactive disk cleanup.

Instead of just viewing

```
Downloads
```

You can explore.

```bash
dua i
```

Navigate

```
Downloads/

Movies/

node_modules/
```

### Real-world

You're wondering

> Why is my SSD full?

Run

```bash
dua i ~
```

Delete unnecessary folders.

---

# 5. procs ⭐⭐⭐⭐☆

Better process viewer.

Instead of

```bash
ps aux
```

Use

```bash
procs
```

Output is much easier to read.

### Real-world

Your laptop fan is loud.

Run

```bash
procs
```

Find

```
chrome
node
docker
```

using lots of CPU.

Kill the one you don't need.

---

# 6. bandwhich ⭐⭐⭐⭐⭐

Shows live network usage.

Run

```bash
sudo bandwhich
```

You'll see

```
Chrome
Firefox
Node
Discord
```

and how much bandwidth each uses.

### Real-world

Internet is slow.

Is it

- npm?
- Docker?
- Chrome?
- VS Code?
- Dropbox?

bandwhich tells you.

---

# 7. sd ⭐⭐⭐⭐☆

Simpler `sed`.

Instead of

```bash
sed -i 's/localhost/127.0.0.1/g'
```

Use

```bash
sd localhost 127.0.0.1 file.txt
```

### Real-world

Rename

```
localhost
```

to

```
api.local
```

across configuration files.

---

# 8. choose ⭐⭐⭐⭐☆

Extract fields.

Example

```
Rahul 21 India
```

Need only age?

```bash
echo "Rahul 21 India" | choose 1
```

Output

```
21
```

### Real-world

You're processing logs.

Instead of using `awk`, `choose` is convenient for simple field extraction.

---

# 9. dog ⭐⭐⭐⭐☆

Modern DNS lookup.

Instead of

```bash
dig google.com
```

Use

```bash
dog google.com
```

### Real-world

Your deployed backend isn't reachable.

Check

```
A record

AAAA record

MX record

TXT record
```

Very useful when configuring domains.

---

# 10. watchexec ⭐⭐⭐⭐⭐

Runs commands whenever files change.

Example

```bash
watchexec npm test
```

Every time you save

```
app.js
```

Tests rerun automatically.

### MERN Example

Instead of

```bash
npm run lint
```

again and again

Use

```bash
watchexec npm run lint
```

Save

↓

Runs automatically

↓

Fix errors

↓

Save again

↓

Runs again

---

# 11. xh ⭐⭐⭐⭐⭐

Your API tester.

Instead of Postman.

Example

Login

```bash
xh POST :3000/login \
email=rahul@gmail.com \
password=123
```

### Real-world

Testing

```
GET /users

POST /login

DELETE /todo

PATCH /profile
```

No browser needed.

---

# 12. jq ⭐⭐⭐⭐⭐

JSON processor.

Suppose

```bash
xh :3000/users
```

returns

1000 lines.

Need only names.

```bash
xh :3000/users | jq '.users[].name'
```

Perfect.

---

# A Typical Backend Development Session

Imagine you're building your Todo API.

### Step 1 — Start server

```bash
npm run dev
```

---

### Step 2 — Test endpoint

```bash
xh POST :3000/login \
email=rahul@gmail.com \
password=123
```

---

### Step 3 — Format response

```bash
... | jq
```

---

### Step 4 — Find a bug

```bash
git diff
```

(delta makes this much easier to read)

---

### Step 5 — Run tests automatically

```bash
watchexec npm test
```

---

### Step 6 — Check if another Node process is still running

```bash
procs
```

---

### Step 7 — Laptop is running out of space

```bash
dust ~
```

---

### Step 8 — Drill into large folders

```bash
dua i
```

---

### Step 9 — Compare two implementations

```bash
hyperfine \
"node old.js" \
"node new.js"
```

---

### Step 10 — Push changes

```bash
git add .
git commit
git push
```

---

# When should you use each one?

|Situation|Tool|
|---|---|
|Testing REST APIs|`xh`|
|Reading JSON responses|`jq`|
|Reviewing Git changes|`delta`|
|Benchmarking commands|`hyperfine`|
|Disk almost full|`dust`|
|Finding huge folders|`dua`|
|Finding CPU-hungry processes|`procs`|
|Finding network-heavy apps|`bandwhich`|
|Replacing text in files|`sd`|
|Checking DNS records|`dog`|
|Automatically rerunning commands|`watchexec`|
|Extracting simple whitespace-separated fields|`choose`|

## One more suggestion

Because you're already comfortable with `fzf`, `ripgrep`, `bat`, `yazi`, `tmux`, and Neovim, the next level is **combining tools**. For example:

```bash
rg "TODO" . | fzf | bat
```

or

```bash
xh :3000/users | jq -r '.users[].email' | fzf
```

These pipelines let small tools work together, which is one of the biggest strengths of the Linux terminal. Once you start thinking in pipelines instead of standalone commands, you'll find yourself solving many development tasks much faster.