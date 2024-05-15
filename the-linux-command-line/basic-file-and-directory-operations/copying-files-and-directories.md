# Copying, Moving, and Renaming Files/Directories

\
Two very similar commands in Unix-like operating systems are `cp` and `mv`. The `cp` command is used to copy files or directories, while the `mv` command is used to move or rename them. Here, we'll cover the usage of both commands, starting with basic operations and progressing to more complex scenarios.&#x20;

{% hint style="info" %}
Wildcards





### **Wildcards**

Wildcards are characters that can represent any number of characters or a specific range of characters in a pattern. They are helpful when you need to perform an operation on multiple files or directories that share a similar naming pattern. Two commonly used wildcards in Bash are:

* `*` (asterisk): This represents any number of characters (including zero characters). For example, `*.txt` will match any file that ends with the `.txt` extension in the current directory, such as `notes.txt`, `chapter1.txt`, and `todo.txt`.&#x20;
* `?` (question mark): This represents exactly one character. For example, `file?.txt` matches with files like `file1.txt`, `file2.txt`, but not `file12.txt`.
{% endhint %}

#### Copying files in the current directory

When you make a copy of a file, you can store the copy in the same directory, or you can store it in a different directory. When you store the copies in the same directory It goes without saying that the copy must have a different name, since two files in the same directory cannot have the same name. Suppose we want to copy `einstein_quote.txt` to a new file named `einstein_quote_backup.txt` in the same directory. We'd invoke:

```bash
cp einstein_quote.txt einstein_quote_backup.txt
```

Note that if `einstein_quote_backup.txt` already exists, it will be overwritten. To avoid accidentally overwriting files, you can use the `-i` (interactive) option with `cp`, which prompts you for confirmation before overwriting an existing file. For example, suppose we invoke the same command again, but this time with the `-i` option. We will be asked to confirm that we want to overwrite `einstein_quote_backup.txt`, to which we can respond y (yes) or n (no):

```bash
~/CLI_playground$ cp -i einstein_quote.txt einstein_quote_backup.txt
overwrite einstein_quote_backup.txt? (y/n [n]) n
not overwritten
~/CLI_playground$
```

{% hint style="info" %}
On Armlab, '`cp`' is aliased to '`cp -i`', meaning by default you will be prompted for confirmation before overwriting a file. If you are sure about overwriting a file and do not want to be prompted, you can remove the confirmation with the `-f` option.
{% endhint %}

#### Copying a File to Another Directory

Suppose we want to copy `einstein_quote.txt` to a different directory, say our home directory. We now have a choice whether the copy should retain the original name (i.e., `einstein_quote.txt`) or be renamed. To retain its name, we'd invoke:

```bash
cp einstein_quote.txt ~ # recall that ~ = /path/to/home/directory
```

To rename the copy `einstein_quote_backup.txt`, we'd invoke:

```
cp einstein_quote.txt ~/einstein_quote_backup.txt
```

#### Copying Multiple Files to a Directory

To copy multiple files from one directory to another, list all files followed by the destination directory. For example, to copy `einstein_quote.txt` and `berra_quote.txt` to our home directory, we'd invoke:

```bash
cp berra_quote.txt einstein_quote.txt ~
```

If we wanted to rename the copies (e.g., to `berra_quote_backup.txt` and `einstein_quote_backup.txt` and respectively) , this operation would require two commands:

```bash
cp berra_quote.txt ~/berra_quote_backup.txt
cp einstein_quote.txt ~/einstein_quote_backup.txt
```

## Copying Directories

* copy directory to another
* copy to nonexistent directory
* merge with existing directory. address overwriting.

