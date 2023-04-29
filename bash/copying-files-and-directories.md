# Copying Files and Directories

### Syntax:  <mark style="color:red;">`cp`</mark><mark style="color:green;">`OPTION(S)`</mark><mark style="color:blue;">`SOURCE(S) DESTINATION`</mark>&#x20;

The `cp` command is used to copy files and directories from a source to a destination. It is a versatile command with various options to handle different scenarios. Here, I'll explain the basic usage of `cp` in different situations:

1. **Source is a file, destination is a file**: In this case, the source file will be copied to the destination file. If the destination file exists, it will be overwritten. If it doesn't exist, a new file will be created. Syntax: `cp source_file destination_file`
2. **Source is a file, destination is a directory:** The source file will be copied to the destination directory with the same file name. If a file with the same name already exists in the destination directory, it will be overwritten. Syntax: `cp source_file destination_directory`
3. **Source is a directory, destination is a file**: This scenario is invalid, as you cannot copy a directory to a file. You'll get an error stating that the source is a directory, not a file.
4. **Source is a directory, destination is a directory**: The source directory and its contents (including subdirectories and their contents) will be copied to the destination directory. If the destination directory doesn't exist, it will be created. If it exists, the source directory's contents will be merged with the destination directory's contents. In case of duplicate file names, the destination files will be overwritten. Syntax: `cp -r source_directory destination_directory`. Note that in this case, (I.e., when the source is a directory, you must use the `-r` option for the command to succeed). &#x20;

### Common options&#x20;

* &#x20;**`-i`**   —   prompts the user for confirmation before overwriting.&#x20;
* &#x20;**`-f`**   —   overrides `-i` option (i.e., removes confirmation prompt).&#x20;
* &#x20;**`-r`**   —   copy directory recursively.&#x20;

### Examples

1.  Copy `berra_quote.txt` to a new file named `berra_quote_backup.txt`:

    ```bash
    cp berra_quote.txt berra_quote_backup.txt
    ```
2.  Copy `einstein_quote.txt`a new directory named `quotes`:

    First, create the directory `quotes`:

    ```bash
    mkdir quotes
    ```

    Then, use `cp` to copy `einstein_quote.txt` to the `quotes` directory:

    ```bash
    cp einstein_quote.txt quotes/
    ```
3.  Copy both `berra_quote.txt` and `einstein_quote.txt` to the `quotes` directory:

    ```bash
    cp berra_quote.txt einstein_quote.txt quotes/
    ```
4.  Copy the entire quotes directory to your home directory:&#x20;

    ```bash
    cp -r quotes ~
    ```
