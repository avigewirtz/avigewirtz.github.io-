---
description: This page introduces Bash commands.
---

# Getting Started

We'll begin our command line journey by executing a few simple Bash commands on Armlab.&#x20;

### The Big Picture

Bash operates in a simple loop: It accepts a command, interprets the command, executes the command, and then waits for another command. See Fig. 3. Bash indicates its readiness to accept a command by displaying a prompt.&#x20;

<figure><img src="../.gitbook/assets/Group 12 (2).png" alt="" width="188"><figcaption></figcaption></figure>

### Shell prompt

When you begin a bash session, the first thing you'll notice is the shell prompt. On Armlab, it looks like the following:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 3.08.46 PM.png" alt=""><figcaption></figcaption></figure>

In addition to indicating its readiness to accept a command, the prompt provides us with a couple of useful pieces of information:

* The name of the computer we are logged into (armlab02)
* The current working directory ([\~](useful-command-line-features.md#tilde-expansion))&#x20;

Generalizing, the prompt on Armlab has the following format:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-05-24 at 9.53.35 PM.png" alt=""><figcaption></figcaption></figure>

## What's in a command?

A commands typically consists of a program name followed by options and operands. The program name is essentially the name of an executable file, located somewhere in your filesystem.&#x20;

The simplest commands consist of just a command name. As we mentioned earlier, a command name can represent a shell-builtin or an external program. For now, it doesn't make a difference which are which.&#x20;

Here are a few examples:&#x20;

1. `uname`, which displays the name of your OS:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-09 at 2.59.46 PM.png" alt=""><figcaption></figcaption></figure>

4. `date`, which displays the current date and time:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-09 at 2.59.54 PM.png" alt=""><figcaption></figcaption></figure>

5. `cal`, which displays a calendar for the current month:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-09 at 3.00.07 PM.png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Note that Linux is case-specific.&#x20;
{% endhint %}

### Options

Many commands accept arguments known as options, which modify the default behavior of the command. An option normally consists of a single character prefixed by a hyphen (e.g., `-a`), but it can also consist of a full word prefixed by two hyphens (i.e., `--list`). The complete list of a command's available options can typically be found in its [_manpage_](getting-help.md).

An example of an option is the `-w` option for the `cal` command, which modifies its output by prefixing each week with its... to the first column of the calendar. To use this option, simply invoke `cal` like so:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-09 at 3.11.55 PM.png" alt=""><figcaption></figcaption></figure>

Another example of an option is `-m` for cal, which displays the calendar with the weeks starting from Monday instead of Sunday:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-09 at 3.13.46 PM.png" alt=""><figcaption></figcaption></figure>

### Combining options

You can typically combine multiple options together, using both in a single command line invocation. For example, we can combine the `-m` and `-w` options of the cal command:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-09 at 3.16.28 PM.png" alt=""><figcaption></figcaption></figure>

### Operands

Many commands also take operandsAn argument is a token that a command acts on, such as a filename, a string of characters, or a number. An argument usually tells a command to act upon a certain object:

We will illustrate arguments using the `sort` command, which sorts lines of text files. For example, say you have the file numbers.txt, with the numbers `5 7 3 4 8 3`, each on a separate line.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 6.59.10 PM.png" alt=""><figcaption></figcaption></figure>

Many programs can take multiple arguments. For example, you can provide `sort` two files, and it will print a sorted concatenation of both files, like so (note that numbers2.txt contains the numbers `2 5 1 9 0 5 2`):&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 7.00.46 PM.png" alt=""><figcaption></figcaption></figure>

#### Commands with options and operands

Finally, many commands take both options and operands. &#x20;

For example, `sort numbers1.txt` with the `-r` option tells `sort` to reverse the order of the output:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 7.19.34 PM.png" alt=""><figcaption></figcaption></figure>

\




















Shell commands typically consist of _fields_, which represent a _command name_ followed by one or more _arguments_.&#x20;

## **Command name**

A command name typically represents an executable file or a shell _built-in_, but it can also represent a _function_.&#x20;

* **Executable file**: An executable file represent any programs on the filesystem, though it typically represents a utility. There is no fundamental distinction between a utility and a regular program, except that a utility can be called by name alone (rather than _pathname_).
* **Shell built-In**: A shell built-in is a utility implemented within the shell. The difference between a shell built-in and another program is that a shell built-in represents a service provided by the shell itself, while other programs represent services provided by external programs. The practical implications of this distinction are typically not of concern to programmers, so we will not cover them here. However, whenever the distinction is pertinent, we will point it out.&#x20;
* **Function**: A function is essentially a group of commands that are defined for reuse.&#x20;

## **Argument**

An argument is a parameter passed to the executable file, shell built-in, or function. It typically represents an _option_ or an _operand_, but it can also represent an _option-argument_.&#x20;

*   **Option**: An option is an argument that changes the command's default behavior. An option normally consists of a single character prefixed by a hyphen (e.g., `-a`), but it can also consist of a full word prefixed by two hyphens (i.e., `--list`). The former is called a _short option_, and the latter is called a _long option_. &#x20;

    Options are defined and interpreted by the program they are supplied to. Thus, the precise syntax and behavior of an option are dependent on the program, not the shell. Many commands allow several short options to be combined.&#x20;
* **Option-Argument**: An option-argument is a parameter that follows certain options. For example, the `-o` option in the `gcc` command uses an argument—an output filename such as `hello`.
* **Operand**: An operand specifies the data that the command manipulates or operates on, usually representing a literal, variable, or filename. (Note that in this context we use the term _file_ broadly to include directories.) Commands often allow multiple operands to be supplied together. The order of options and operands can be significant, depending on the command.&#x20;

The syntax of a shell command can generally be summarized as follows:
