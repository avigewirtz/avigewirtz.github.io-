# Shell

Commands are issued in the termiank as sequences of text. Just as commands in a programming language like Java, C, or Python must comply with a specific grammatical structure, so must the commands entered in a terminal. Furthermore, just like Java, C, or Python require an interpreter or compiler to translate them into an executable form, commands inputted into the terminal also necessitate a similar translation process.

Enter the shell - a dual-purpose entity serving as both a programming language and a command interpreter.

1. **Defining the language of CLI commands**: The shell defines the syntax and semantics of CLI commands, specifying the format that commands must adhere to and the range of possible operations.
2. **Interpreting CLI commands**: The shell reads and interprets textual commands entered in the terminal, executing them by running either built-in functions or by invoking external programs.

The main difference between a language like Java or C and Bash is that instead of Bash being used to write programs, the shell is primarily used to interact with the operating system. When you type a command into the shell, the shell interprets your command and then instructs the operating system accordingly.

Essential, the shell serves as an intermediary between the user in the terminal and the OS. 


## Shell Syntax

A command issued in a Unix-like shell typically has several components:

#### Field

In the shell command language, a unit of text that is the result of parameter expansion, arithmetic expansion, command substitution, or field splitting. During command processing, the resulting fields are used as the command name and its arguments.

* **Command name**:
  * **Executable file**: executable program somewhere in the file system. either an OS utility program or a user-written program. It's located on the filesystem in an executable.  Examples include `ls`, `ssh`, `emacs`, `javac`, `java`, `python`, `gcc`, and so on. The shell attempts to locate this program based on the PATH environment variable or an absolute/relative path if provided. The only difference is whether you have to supply a pathname
  *   **Shell Built-in**: A utility implemented within the shell. These include commands like `cd`, `echo`, `exit`, `alias`, `set`, and many others.
  * Function
* **Argument**: A parameter passed to a utility. An argument is typically an option or an operand. 
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



