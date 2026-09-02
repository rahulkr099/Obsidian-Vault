## Next Linux Command: `less`

`less` is used to **view large files page by page** in the terminal.

Unlike `cat`, it doesn't dump the entire file at once.

### Basic Syntax

```bash
less filename
```

Example:

```bash
less package.json
```

Or for logs:

```bash
less server.log
```

---

## Why use `less` instead of `cat`?

Imagine a file has 10,000 lines.

```bash
cat huge.log
```

😵 Everything prints immediately.

But:

```bash
less huge.log
```

You can comfortably scroll and search.

> Fun fact: `less` is called "less" because **less is more** 😄

---

# Important `less` Keyboard Shortcuts

Once you're inside `less`:

|Key|Action|
|---|---|
|`Space`|Next page|
|`b`|Previous page|
|`↓`|Move down|
|`↑`|Move up|
|`g`|Go to beginning|
|`G`|Go to end|
|`/text`|Search forward|
|`?text`|Search backward|
|`n`|Next search result|
|`N`|Previous search result|
|`q`|Quit|

---

## Search inside a file

Open:

```bash
less package.json
```

Then type:

```text
/scripts
```

Press `Enter`.

To go to the next match:

```text
n
```

Previous match:

```text
N
```

---

## Developer Superpower: Follow Logs

This command is extremely useful:

```bash
less +F server.log
```

It follows the file like:

```bash
tail -f server.log
```

When new logs are added, you'll see them live.

To stop following mode, press:

```text
Ctrl + C
```

Then you can scroll/search normally.

---

## Useful Options

### Show line numbers

```bash
less -N file.txt
```

### Open directly at a search result

```bash
less +/error server.log
```

This opens the file and searches for `error`.

### View command output with `less`

Very useful when a command produces lots of output:

```bash
npm list | less
```

```bash
git log | less
```

```bash
journalctl | less
```

---

## `cat` vs `less`

|Feature|`cat`|`less`|
|---|---|---|
|Small files|✅ Excellent|✅|
|Large files|❌ Not ideal|✅ Excellent|
|Scroll|❌|✅|
|Search|❌|✅|
|Edit file|❌|❌|
|Quick output|🚀 Fast|Good|

### My recommendation for you

As a developer, get comfortable with this workflow:

```bash
cat package.json       # Quick look
less package-lock.json # Large file
grep "express" package.json # Find something
```

This combination is used constantly in Linux development.

**Next command I recommend: `head` and `tail`** — especially `tail -f`, which is extremely useful for watching backend logs in real time.