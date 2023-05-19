# Shell

CLI commands are ultimately executed by the OS. However, the commands are not issued to the OS directly. Instead, they are issued via an intermediary program known as the _shell_, which is the program that implements the CLI.&#x20;

1. **Defining the language of CLI commands**: The shell defines the syntax and semantics of CLI commands, specifying the format that commands must adhere to and the range of possible operations.
2. **Interpreting CLI commands**: The shell reads and interprets textual commands entered in the terminal, executing them by running either built-in functions or by invoking external programs.

## Shell Syntax on the terminal

A command issued in a Unix-like shell typically has several components:

* **Command name**: This is the name of the actual program that you're asking the shell to run. It can be one of two things: a program or a shell builtin.&#x20;
  * **Program**: executable program somewhere in the file system. either an OS utility program or a user-written program. It's located on the filesystem in an executable.  the first thing on the command line. Examples include `ls`, `ssh`, `emacs`, `javac`, `java`, `python`, `gcc`, and so on. The shell attempts to locate this program based on the PATH environment variable or an absolute/relative path if provided. The only difference is whether you have to supply a pathname
  * **Shell Built-in**: In addition to running external programs, the shell has a set of built-in commands that it can execute directly. These include commands like `cd`, `echo`, `exit`, `alias`, `set`, and many others.
* **Options or Flags**: These are usually indicated by a dash `-` or two dashes `--` (for short and long options respectively). They modify the behavior of the command. For example, `ls -l` tells `ls` to use long format listing, while `gcc -O2` tells `gcc` to use level 2 optimization during compilation.
* **Arguments or Operands**: These are the items that the command operates on. For `ls`, the arguments might be the names of files or directories to list. For `gcc`, it's typically the names of the C source files to compile.
* **Redirections and Piping**: These symbols (`<`, `>`, `>>`, `|`, `2>`, etc.) tell the shell to redirect input and/or output from/to files or other commands. For example, `ls > file.txt` directs the output of `ls` to a file named `file.txt`, and `command1 | command2` pipes the output of `command1` into `command2` as input.
* **Variables**:&#x20;
  * Shell variables
  * Environment variables: These are pairs of keys and values stored in the shell's environment and can be accessed by commands. For example, in `PATH=/usr/bin:/bin command`, `PATH` is an environment variable.
* **Command Grouping and Background Execution**: Symbols like `;`, `&&`, `&`, `(`, `)` are used to group commands, control command execution order, and run commands in the background. For example, `command1 ; command2` runs `command1`, waits for it to finish, and then runs `command2`, while `command1 &` runs `command1` in the background.



