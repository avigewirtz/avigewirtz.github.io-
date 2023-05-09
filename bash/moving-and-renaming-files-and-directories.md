# Moving and Renaming Files and Directories

### Syntax:  <mark style="color:red;">`mv`</mark><mark style="color:green;">`OPTION(S)`</mark><mark style="color:blue;">`SOURCE(S) DESTINATION`</mark>

The `mv` command in Bash is used to move or rename files and directories from a source to a destination. It is a flexible command with various options to handle different scenarios. Here, I'll explain the basic usage of `mv` in different situations:

1. **Source is a file, destination is a file**: In this case, the source file will be moved to the destination file. If the destination file exists, it will be overwritten. If it doesn't exist, a new file will be created, and the source file will be removed. Syntax: `mv source_file destination_file`
2. **Source is a file, destination is a directory**: The source file will be moved to the destination directory with the same file name. If a file with the same name already exists in the destination directory, it will be overwritten, and the source file will be removed. Syntax: `mv source_file destination_directory/`
3. **Source is a directory, destination is a file**: This scenario is invalid, as you cannot move a directory to a file. You'll get an error stating that the source is a directory, not a file.
4. **Source is a directory, destination is a directory**: The source directory will be moved to the destination directory. If the destination directory doesn't exist, it will be created, and the source directory will be removed. If it exists, the source directory will be merged with the destination directory, overwriting any files with the same name. Syntax: `mv source_directory/ destination_directory/`

### Common options

* `-i`: Prompts the user for confirmation before overwriting existing files.
* `-n`: Prevents overwriting existing files.
* `-u`: Moves only when the source file is newer than the destination file, or when the destination file is missing.

<details>

<summary>Current version of  <code>bash_practice</code> directory</summary>

Assuming that you have executed the previous `cp` examples, the updated `bash_practice` directory now contains the following files and directories:

```bash
armlab01:~/bash_practice$ ls
.   .git       berra_quote.txt     berra_quote_backup.txt  encyclopaedia.txt  quotes
..  README.md  einstein_quote.txt  the_odyssey.txt
```

And the `quotes` directory contains the following files:

```bash
armlab01:~/bash_practice/quotes$ ls
einstein_quote.txt
```

</details>



### Examples

1.  Move _the\_odyssey.txt_ to a new file named _odyssey.txt_:

    ```bash
    mv the_odyssey.txt odyssey.txt
    ```
2.  Move _encyclopaedia.txt_ to the _quotes_ directory:

    ```bash
    mv encyclopaedia.txt quotes/
    ```
3.  Rename _berra\_quote\_backup.txt_ to _yogi\_berra\_quote.txt_:

    ```bash
    mv berra_quote_backup.txt yogi_berra_quote.txt
    ```
4.  Move both _odyssey.txt_ and _yogi\_berra\_quote.txt_ to the _quotes_ directory:

    ```bash
    mv odyssey.txt yogi_berra_quote.txt quotes/
    ```
5.  Assuming you have a directory named _old\_directory_, use `mv` to rename it to _new\_directory_:

    ```bash
    mv old_directory new_directory
    ```
