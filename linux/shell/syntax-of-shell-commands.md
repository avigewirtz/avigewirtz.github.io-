# Syntax of Shell Commands

Commands issued in the shell typically consist of a _command name_ followed by one or more _arguments_.&#x20;

## **Command name**

A command name normally represents either an executable file somewhere in the filesystem or a shell builtin. However, it can also represent a function.&#x20;

* **Executable file**: The executable file can either be a OS utility program or a user-written program. Fundamentally there is no difference between the two. expect when invoking a user-written program, you typicaslly need to provide the pathname of the program, instead of just its name like with utility programs. More on that later.&#x20;
* **Shell Built-in**: A shell builtin is a utility implemented within the shell. The practical distinction between the two is normally irelevant,.

## **Argument**

An argument is a parameter passed to the executable file or shell built-in.  An argument is typically an _option_ or an _operand_, but it can also be an option argument.&#x20;

* **Option**: An option is generally a character prefixed by a dash that changes the command's default behavior. Many commands allow several options to be used together.&#x20;
* **Operand**: An operand generally specifies the data the command should manipulate or operate on. An operand normally represents either a filename, literal, or variable. Many commands allow multiple operands to be supplied together.&#x20;

The syntax is summarized in Figure 1.&#x20;

<figure><img src="../../.gitbook/assets/new tree.svg" alt="" width="450"><figcaption><p>Figure 1: Common Shell Syntax</p></figcaption></figure>



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
