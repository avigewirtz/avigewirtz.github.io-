# Bash Cheat Sheet

{% hint style="info" %}
Uppercase terms (e.g., SOURCE, DESTINATION) indicate placeholders for text that should be replaced with user-specified values.
{% endhint %}

### Basic Commands

* `pwd`: Print working directory.
* `cd DIRECTORY`: Make DIRECTORY the working directory.&#x20;
* `cd ..`:  Change the working directory to its parent.&#x20;
* `cd -`: Change the working directory to the previous working directory.
* `ls`: List files and directories in the working directory.
* `ls -a`: List all files and directories, including hidden ones.
* `ls -l`: List files and directories in long format.
* `ls -t`: List files and directories sorted by modification time.
* `mkdir DIRECTORY`: Create a new directory.
* `rmdir DIRECTORY`: Delete an empty directory.
* `rm FILE`: Delete a file.
* `rm -r DIRECTORY`: Delete a non-empty directory.
* `rm -f FILE`: Forcefully delete a file (I.e., remove confirmation, if it exists).
* `cp SOURCE DESTINATION`: Copy a file or directory.
* `cp -r SOURCE DESTINATION`: Copy a directory and its contents.
* `mv SOURCE DESTINATION`: Move a file or directory.
* `touch FILE`: Create an empty file or update its modification time.
* `cat FILE`: Display the contents of a file.
* `less FILE`: View the contents of a file one page at a time.
* `head FILE`: Display the first 10 lines of a file.
* `tail FILE`: Display the last 10 lines of a file.
* `grep PATTERN FILE`: Search for a pattern in a file.
* `grep -r PATTERN DIRECTORY`: Search for a pattern recursively in a directory.
* `echo "TEXT"`: Print text to the console.
* `echo $VARIABLE`: Print the value of a variable.
* `export VARIABLE=value`: Set an environment variable.
* `man COMMAND`: Display the manual page for a command.

### I/O Redirection

1. `COMMAND > FILE`: Redirect the output of a command to a file (overwrite).
2. `COMMAND >> FILE`: Redirect the output of a command to a file (append).
3. `COMMAND < FILE`: Redirect the contents of a file to a command as input.
4. `COMMAND 2> FILE`: Redirect the error output of a command to a file.
5. `COMMAND1 | COMMAND2`: Pipe the output of one command as input to another command.
