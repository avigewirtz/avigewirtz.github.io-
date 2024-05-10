# Redirection and Piping

When a program is started up, it by default has three data streams attached to it: one for reading input, one for writing normal output, and one for writing error messages. These data streams are known as _standard input_ (stdin), _standard output_ (stdout), and _standard error_ (stderr) respectively. By default, stdin is connected to the keyboard, while stdout and stderr are connected to the terminal window. &#x20;

## **Redirection**

Redirection lets you change where input comes from and where output goes. The key symbols are:

* **`>`** and **`>>`**  : These symbols redirect _stdout_. Examples:

```bash
ls > output.txt  # Redirects stdout of 'ls' to output.txt, overwriting existing content
ls -l >> output.txt  # Redirects stdout of 'ls -l' to output.txt, appending to existing content
```

The difference between these two symbols is > overwrites the contents while >> appends.

* **`2>`** and **`2>>`** : These symbols work the same as `>` and `>>`, except they redirect _stderr_. Examples:

```bash
cat nonexistent_file 2> errors.txt  # Redirects stderr of 'cat nonexistent_file' to errors.txt, overwriting existing content. 
cat another_nonexistent_file 2>> errors.txt  # Redirects stderr of 'cat another_nonexistent_file' to errors.txt, appending to existing content. 
# Suggestion: view the contents of errors.txt 
```

* `<`: This symbol redirects _stdin_. Example:

```
```

## Piping

Piping chains commands together, using the output of one command as the input to another. The symbol is **|** . Example:

```bash
~$ cat numbers.txt | sort
1
1
2
3
6
~$ 
```

The takes the output of `cat numbers.txt` and feeds it as input to `sort`, which sorts its contents and displays the sorted version on the screen.&#x20;
