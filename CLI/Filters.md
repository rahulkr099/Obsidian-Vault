In Linux, **filters** are commands that take input from **standard input (stdin)**, process it, and send the result to **standard output (stdout)**. They are commonly used with pipes (`|`) to manipulate text.

### Common Linux Filters

|Filter|Purpose|Example|
|---|---|---|
|`cat`|Displays file contents|`cat file.txt`|
|`grep`|Searches for patterns in text|`grep "error" log.txt`|
|`sort`|Sorts lines alphabetically or numerically|`sort names.txt`|
|`uniq`|Removes duplicate adjacent lines|`sort file.txt \| uniq`|
|`wc`|Counts lines, words, and characters|`wc file.txt`|
|`head`|Displays the first few lines|`head -5 file.txt`|
|`tail`|Displays the last few lines|`tail -10 file.txt`|
|`cut`|Extracts specific columns or fields|`cut -d',' -f2 data.csv`|
|`paste`|Merges lines from multiple files|`paste file1 file2`|
|`tr`|Translates or deletes characters|`tr 'a-z' 'A-Z' < file.txt`|
|`sed`|Stream editor for searching and replacing text|`sed 's/Linux/Unix/g' file.txt`|
|`awk`|Pattern scanning and text processing|`awk '{print $1}' file.txt`|
|`tee`|Writes output to both a file and the terminal|`ls \| tee output.txt`|

### Example Using Filters with Pipes

```bash
cat students.txt | grep "John" | sort | uniq
```

**Explanation:**

1. `cat` reads the file.
    
2. `grep` finds lines containing "John".
    
3. `sort` sorts the matching lines.
    
4. `uniq` removes duplicate lines.
    

### Advantages of Filters

- Process text efficiently.
    
- Can be combined using pipes (`|`).
    
- Useful for automation and shell scripting.
    
- Work well with large files.
    

**In short:** Linux filters are text-processing commands that read input, transform it, and produce output, making them essential tools for command-line data processing.