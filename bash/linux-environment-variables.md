# Linux Environment Variables

In Linux, environment variables are a type of variable used to store information about the system environment, such as the current user's name, the current system's directory path, or settings for software applications. Standard environment variables on Linux include:

* `PATH`: Stores a list of directories where the shell looks for executable programs when a command is entered. Directories in the `PATH` variable are separated by colons (:) on Linux and semicolons (;) on Windows.
* `HOME`: Specifies the home directory of the current user. &#x20;
* `USER`: Contains the username of the currently logged-in user.
* `PWD`: Represents the current working directory of the shell.
* `LANG`: Specifies the default language and character encoding used by the system.
* `EDITOR`: Defines the default text editor to be used by certain command-line programs.
* `SHELL`: Indicates the user's preferred shell program, such as Bash or Zsh.

To print the value of an environment variable, you can use the `echo` command with the variable name prefixed by a dollar sign ($), as so:

```bash
echo $PATH
```
