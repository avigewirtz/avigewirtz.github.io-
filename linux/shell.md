# Shell

Just as commands issued in a programming language like Java or C must comply with a specific grammatical structure, so too must the commands entered in a terminal. Similarly, just like Java and C require a compiler to translate them into an executable form, commands inputted into the terminal necessitate a similar process.

Enter the shell - a dual-purpose entity serving as both a programming language and a command interpreter.

1. **Defining the language of CLI commands**: The shell defines the syntax and semantics of CLI commands, specifying the format that commands must adhere to and the range of possible operations.
2. **Interpreting CLI commands**: The shell reads and interprets textual commands entered in the terminal, executing them by running either built-in functions or by invoking external programs.

The main difference between a language like Java or C and Bash is compiled vs interpreted. writing programs vs ...&#x20;

Essentially, the shell serves as an intermediary between the user in the terminal and the OS.

## Shell Syntax

A commands issues in the shell generally consists of a command name followed by arguments. Technically referee to as fields.

* **Command name**:
  * **Executable file**: executable program somewhere in the file system. either an OS utility program or a user-written program. It's located on the filesystem in an executable. Examples include `ls`, `ssh`, `emacs`, `javac`, `java`, `python`, `gcc`, and so on. The shell attempts to locate this program based on the PATH environment variable or an absolute/relative path if provided. The only difference is whether you have to supply a pathname
  * **Shell Built-in**: A utility implemented within the shell. These include commands like `cd`, `echo`, `exit`, `alias`, `set`, and many others.
  * Function
* **Argument**: A parameter passed to a utility. An argument is typically an option or an operand.
  * **Option**: An argument to a command that is generally used to specify changes in the utility's default behavior
  * **Operand**: An argument to a command that generally specifies the data to be manipulated or operated on. Operands generally follow the options in a command line.

<figure><img src="../.gitbook/assets/Screenshot 2023-05-19 at 4.10.11 PM.png" alt="" width="375"><figcaption></figcaption></figure>
