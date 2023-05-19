# Shell

CLI commands are ultimately executed by the OS. However, the commands are not issued to the OS directly. Instead, they are issued via an intermediary program known as the _shell_, which is the program that implements the CLI.&#x20;

1. **Defining the language of CLI commands**: The shell defines the syntax and semantics of CLI commands, specifying the format that commands must adhere to and the range of possible operations.
2. **Interpreting CLI commands**: The shell reads and interprets textual commands entered in the terminal, executing them by running either built-in functions or by invoking external programs.

## Command Syntax

A command issued in a Unix-like shell typically has several components:

* **Command name**: This is the name of the actual program that you're asking the shell to run. It can be one of two things: a program or a shell builtin.&#x20;
  * **Program**: executable program somewhere in the file system. either an OS utility program or a user-written program. It's located on the filesystem in an executable.  the first thing on the command line. Examples include `ls`, `ssh`, `emacs`, `javac`, `java`, `python`, `gcc`, and so on. The shell attempts to locate this program based on the PATH environment variable or an absolute/relative path if provided. The only difference is whether you have to supply a pathname
  * **Shell Built-in**: In addition to running external programs, the shell has a set of built-in commands that it can execute directly. These include commands like `cd`, `echo`, `exit`, `alias`, `set`, and many others.

#### Option

An argument to a command that is generally used to specify changes in the utility's default behavior

#### Option-Argument

A parameter that follows certain options. In some cases an option-argument is included within the same argument string as the option-in most cases it is the next argument.

#### Operand

An argument to a command that is generally used as an object supplying information to a utility necessary to complete its processing. Operands generally follow the options in a command line. Defined by utility.&#x20;



<figure><img src="../.gitbook/assets/Screenshot 2023-05-19 at 3.47.43 PM.png" alt="" width="563"><figcaption></figcaption></figure>

#### Example of CLI Commands

```bash
javac hello.java
java Hello
gcc217 hello.c -o hello
./hello
```



