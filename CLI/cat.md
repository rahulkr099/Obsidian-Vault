## `cat` Command in Linux

`cat` stands for **concatenate**. It is one of the most commonly used Linux commands for **reading, combining, and displaying file contents**.

### Basic Syntax

```bash
cat [OPTIONS] [FILE...]
```

---

## 1. Display contents of a file

Suppose you have a file called `hello.txt`.

```bash
cat hello.txt
```

Output:

```text
Hello Rahul
Welcome to Linux
```

---

## 2. Display multiple files

You can display multiple files together:

```bash
cat file1.txt file2.txt
```

`cat` will print the contents sequentially.

Example:

```text
Contents of file1
Contents of file2
```

This is where the name **concatenate** comes from—it joins file contents together.

---

## 3. Create a file using `cat`

You can create a file interactively:

```bash
cat > notes.txt
```

Now type:

```text
Linux is awesome
I am learning terminal commands
```

Press:

```text
Ctrl + D
```

This signals **EOF (End of File)** and saves the input.

---

## 4. Append content to a file

Use `>>` instead of `>`:

```bash
cat >> notes.txt
```

Type additional content and press `Ctrl + D`.

### Important difference

```bash
cat > file.txt
```

⚠️ Overwrites the file.

```bash
cat >> file.txt
```

✅ Appends content without removing existing data.

---

## 5. Combine multiple files into a new file

```bash
cat file1.txt file2.txt > combined.txt
```

This creates:

```text
combined.txt
```

containing:

```text
[file1 contents]
[file2 contents]
```

---

## 6. Display line numbers

Use `-n`:

```bash
cat -n file.txt
```

Example:

```text
     1  Hello
     2  Linux
     3  MERN Stack
```

Very useful when debugging configuration files or source code.

---

## 7. Remove repeated blank lines

Use `-s`:

```bash
cat -s file.txt
```

If a file has:

```text
Hello



Linux


World
```

It squeezes multiple blank lines into one.

---

## 8. Show special characters

Use `-A`:

```bash
cat -A file.txt
```

This can help debug hidden characters.

For example:

```text
Hello$
Linux$
```

`$` represents the end of a line.

---

# Using `cat` with Pipes

`cat` is often used with other Linux commands.

### Search text

```bash
cat file.txt | grep "error"
```

Better version:

```bash
grep "error" file.txt
```

The second version is generally preferred because `cat` isn't necessary.

### Count lines

```bash
cat file.txt | wc -l
```

Better:

```bash
wc -l file.txt
```

---

# A Useful Real Developer Example

Suppose you want to inspect your `.env` file:

```bash
cat .env
```

Or view a JSON file:

```bash
cat package.json
```

Or combine logs:

```bash
cat app.log error.log > combined.log
```

---

## Important Tip

For **small files**, `cat` is perfect.

For large files, prefer:

```bash
less largefile.log
```

because `cat` dumps the entire file into the terminal at once.

### Quick mental model

> **`cat` = Read → Display → Combine text files**

For your terminal-first developer journey, `cat` is especially useful for quickly inspecting files like:

```bash
cat package.json
cat .env.example
cat docker-compose.yml
cat README.md
```

A good next command to learn after `cat` is **`less`**, because together they teach you when to quickly print a file versus navigate through a large file.