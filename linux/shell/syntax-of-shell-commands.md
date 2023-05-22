# Syntax of Shell Commands

Commands issued in the shell typically consist of _fields_, which consist of a _command name_ followed by one or more _arguments_.&#x20;

## **Command name**

A command name typically represents either an executable file, a shell built-in, or a function.&#x20;

* **Executable file**: The executable file can represent any program on the filesystem. It typically represents a utility or a user-written program. There is no fundamental distinction between the two, except that a utility represents a program that can be called by name (rather than _pathname_) and user-written programs must (by default) be called with a pathname. &#x20;
* **Built-In**: A built-in utility is a utility implemented within the shell. The difference between a shell built-in and another program is that a shell built-in is a service provided by the shell itself, while other programs represent services provided by external programs. The practical implications of this are typically not of concern to the programmers, so we will not cover it here. However, whenever the distinction is pertinent, we will clearly point it out.&#x20;
* **Function**: A function is essentially a group of commands that are defined for reuse. You need now be familiar with them in COS217.&#x20;

## **Argument**

An argument is a parameter passed to the executable file, shell built-in, or function represented by the command name. An argument is typically an _option_ or an _operand_, but it can also be an _option argument_.&#x20;

*   **Option**: An option is an argument that changes the command's default behavior. An option normally consists of a single character prefixed by a hyphen (e.g., `-a`), but it can also consist of a full word prefixed by two hyphens (i.e., `--list`). The former is called a _short option_, and the latter is called a _long option_. &#x20;

    Options are defined and interpreted by the program they are supplied to. Thus, the precise syntax and behavior of an option are dependent on the program, not the shell. Many commands allow several short options to be combined.&#x20;
* **Option-Argument**: An option-argument is a parameter that follows certain options. For example, the `-o` option in the `gcc` command uses an argument—an output filename such as `hello`.
* **Operand**: An operand specifies the data the command should manipulate or operate on, which normally represents either a filename, literal, or variable. Many commands allow multiple operands to be supplied together. Operands generally follow options.

The syntax of a shell command can be summarized as follows:

```css
COMMAND_NAME OPTION(S) OPERAND(S)
```

The complete syntactical structure is illustrated in Figure 1.&#x20;

<figure><img src="../../.gitbook/assets/tree.svg" alt="" width="563"><figcaption></figcaption></figure>
