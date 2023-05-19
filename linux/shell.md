# Shell

CLI commands are ultimately executed by the OS. However, the commands are not issued to the OS directly. Instead, they are issued via an intermediary program known as the _shell_, which is the program that implements the CLI.&#x20;

1. **Defining the language of CLI commands**: The shell defines the syntax and semantics of CLI commands, specifying the format that commands must adhere to and the range of possible operations.
2. **Interpreting CLI commands**: The shell reads and interprets textual commands entered in the terminal, executing them by running either built-in functions or by invoking external programs.

## Command Syntax

A command issued in a Unix-like shell typically has several components:

#### Field

In the shell command language, a unit of text that is the result of parameter expansion, arithmetic expansion, command substitution, or field splitting. During command processing, the resulting fields are used as the command name and its arguments.

* **Command name**:
  * **Executable file**: executable program somewhere in the file system. either an OS utility program or a user-written program. It's located on the filesystem in an executable.  Examples include `ls`, `ssh`, `emacs`, `javac`, `java`, `python`, `gcc`, and so on. The shell attempts to locate this program based on the PATH environment variable or an absolute/relative path if provided. The only difference is whether you have to supply a pathname
  *   **Shell Built-in**: Built-In Utility (or Built-In)

      A utility implemented within the shell.  In addition to running external programs, the shell has a set of built-in commands that it can execute directly. These include commands like `cd`, `echo`, `exit`, `alias`, `set`, and many others.
  * Function
* **Argument**: A parameter passed to a utility as the equivalent of a single string in the _argv_ array created by one of the _exec_ functions. An argument is one of the options, option-arguments, or operands following the command name. A parameter that follows certain options
  * **Option**: An argument to a command that is generally used to specify changes in the utility's default behavior
  * **Operand**: An argument to a command that is generally used as an object supplying information to a utility necessary to complete its processing. Operands generally follow the options in a command line.&#x20;



&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-05-19 at 4.10.11 PM.png" alt="" width="375"><figcaption></figcaption></figure>

#### Example of CLI Commands

```bash
javac hello.java
java Hello
gcc217 hello.c -o hello
./hello
```



