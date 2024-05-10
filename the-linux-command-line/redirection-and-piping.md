# Redirection and Piping

When a program is started up, it by default has three data streams attached to it: one for reading input, one for writing normal output, and one for writing error messages. These data streams are known as _standard input_ (stdin), _standard output_ (stdout), and _standard error_ (stderr) respectively. By default, stdin is connected to the keyboard, while stdout and stderr are connected to the terminal window. &#x20;

## **Redirection**

Redirection lets you change where input comes from and where output goes. The key symbols are:

**`>`** and **`>>`**  : These redirect stdout.&#x20;

The difference between the two is that `>` overwrites the file, while `>>` appends to it. In both case, if the file doesn't exist, it will be created. Examples:

```bash
ls > output.txt  # Writes stdout of 'ls' to output.txt
ls -l >> output.txt  # Appends stdout of 'ls -l' to output.txt 
```

**`2>`** and **`2>>`** : Identical to `>` and `>>`, except they redirects stderr. Examples:

```bash
cat nonexistent_file 2> errors.txt  # Writes stderr of 'cat nonexistent_file' to errors.txt
cat another_nonexistent_file 2>> errors.txt  # Appends stderr of 'cat another_nonexistent_file' to errors.txt
# Suggestion: view the contents of errors.txt 
```

**`>`**: Redirects stdin. Example:

## Piping

Piping chains commands together, using the output of one command as the input to another. The symbol is **|** . Example:

```bash
cat file.txt | sort
```

The takes the output of `cat file.txt` and feeds it as input to `sort`, which sorts its contents displays the sorted version on the screen.&#x20;

