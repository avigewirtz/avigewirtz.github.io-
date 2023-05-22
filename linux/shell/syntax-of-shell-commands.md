# Syntax of Shell Commands

Commands issued in the shell typically consist of a _command name_ followed by one or more _arguments_.&#x20;

## **Command name**

A command name typically represents either an executable file, a shell built-in, or a function.&#x20;

* **Executable file**: The executable file can be any executable file on the filesystem, be it a pre-installed program, called a utility, or a user-written program. However, in the context of Fundamentally there is no difference between the two, except that when invoking a user-written program, you typically need to provide the pathname of the program so the shell can locate it. More on this later.&#x20;
* **Shell built-in**: A shell built-in is a utility implemented within the shell. The difference between a shell built-in and an executable file is that a built-in is a feature of the shell itself, while an executable is written by others. The practical implications of this are typically not of concern to the programmers, so we will not cover it here. However, whenever the distinction is pertinent, we will clearly point it out.&#x20;
* **Function**:&#x20;

## **Argument**

An argument is a parameter passed to the executable file or shell built-in.  An argument is typically an _option_ or an _operand_, but it can also be an option argument.&#x20;

* **Option**: An option is generally a character prefixed by a dash that changes the command's default behavior. Many commands allow several options to be used together. Arguments are options if they begin with a hyphen delimiter (‘-’).
* **Operand**: An operand generally specifies the data the command should manipulate or operate on. An operand normally represents either a filename, literal, or variable. Many commands allow multiple operands to be supplied together. The argument -- terminates all options
* **Option argument**:&#x20;
  * Certain options require an argument. For example, the -o option of the `ld` command requires an argument—an output file name.

The syntax can be summarized as follows:

```css
COMMAND_NAME OPTION(S) OPERAND(S)
```

The complete syntactical structure is illustrated in Figure 1.&#x20;

<figure><img src="../../.gitbook/assets/tree.svg" alt="" width="563"><figcaption></figcaption></figure>



## Examples of Shell Commands&#x20;

Before we begin executing commands, we need to cover a few more topics—most notably the Linux filesystem. However, to make the idea of a shell more concrete, let’s first give a high-level overview of some commands you're certainly familiar with.



Recall from COS126 that to compile Java programs:

```bash
javac program.java
```

`javac` is the Java compiler that translates Java source code into Java Bytecode. The shell interprets `javac` as an executable program, and `hello.java` as the argument to this program. The shell runs javac and supplies it with the hello.java argument. `javac` then compiles it into Java Bytecode, creating a file named `Hello.class`. Of course you then run the program by invoking `java Hello`.

Let's now use an example from COS217. Recall that to compile a C program, you invoke:

```bash
gcc hello.c -o hello # For simplicity, we're using 'gcc' instead of 'gcc217'
```

`gcc` is the GNU Compiler Collection. The shell interprets `gcc` as an executable program, and `hello.c`, `-o`, and `hello` as arguments to this program. The shell runs gcc and supplies it with the hello.c, -o, and hello as arguments. gcc then compiles hello.c into machine code, creating an executable file hello. &#x20;

.
