---
description: This page introduces Bash commands.
---

# Getting Started With Bash

<figure><img src="../.gitbook/assets/Group 37.png" alt=""><figcaption></figcaption></figure>

One of the most basic functions of Bash is to launch other programs for you. The program it launches might be a program like _date_, which comes with all Unix systems, or it might be a simple user-written program like hello, which writes "Hello, World!" on stdout. From Bash's perspective, there's no real difference between programs like date and hello, except that by default, date can be launched by just typing it's name, whereas to launch hello you must type it's pathname

```bash
$ /bin/date 
Mon Mar 25 21:10:49 EDT 2023
$ ../../bin/date
Mon Mar 25 21:11:47 EDT 2023
$ 
```

```
$ date
Mon Mar 25 21:15:25 EDT 2024
$ 
```







BASH, short for "Bourne-Again SHell," is a popular Unix-shell developed by the [GNU Project](https://en.wikipedia.org/wiki/GNU\_Project). It is the default shell on many Linux distributions.&#x20;

A shell is a command language interpreter. It reads commands entered by the user in the terminal and executes them. An example of a command is:

```
// Some code
```



Bash typically runs in a terminal and executes commands interactively, but it can also read commands from a file, typically called a shell script. In this tutorial, we will only focus on commands entered in the terminal, but the idea is the same.



### The Big Picture

Bash operates in a simple loop: It accepts a command, interprets the command, executes the command, and then waits for another command. See Fig. 3. Bash indicates its readiness to accept a command by displaying a prompt.&#x20;

<figure><img src="../.gitbook/assets/Group 12 (2).png" alt="" width="188"><figcaption></figcaption></figure>

### Shell prompt

When you begin a bash session, the first thing you'll notice is the shell prompt. On Armlab, it looks like the following:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 3.08.46 PM.png" alt=""><figcaption></figcaption></figure>

In addition to indicating its readiness to accept a command, the prompt provides us with a couple of useful pieces of information:

* The name of the computer we are logged into (armlab02)
* The current working directory ([\~](useful-command-line-features/#tilde-expansion))&#x20;

Generalizing, the prompt on Armlab has the following format:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-05-24 at 9.53.35 PM.png" alt=""><figcaption></figcaption></figure>

## What's in a command?

One of the most fundamental functions of the shell is simply to launch other programs. In fact, in early unix shells, this is basically all they did.&#x20;

A command typically has the following form:

```
program_name arguments
```

The program represents some standalone program located somewhere in the filesystem. It's important to recognize that although we refer to this as a "shell command", the program is completely independent of the shell. The job of the shell, then, is simply to launch that program, and pass the arguments to that program.&#x20;

The program it launches can be any program on your computer. It might be a program like hello that you wrote yourself, or a program like ls that is standard on all Unix systems, or it might be a program like gcc.&#x20;

The point to understand is that in many&#x20;



a few things to note:&#x20;

* When the command name is a program, options and operands are a feature of the program being called,  not bash. Hence, -c is a gcc thing, not a bash thing. Bash simply passes it to gcc for you.&#x20;

```
cd
```



```
./hello
```







The simplest type of command consists of just a command name. As we mentioned earlier, a command name can represent a shell-builtin or a standalone program. For now, it doesn't make a difference which are which.&#x20;



#### What's in a Bash command?

Some of these commands are built into bash itself; others are separate programs. For now, it doesn’t make a difference which are which.

Bash, along with most other unix-shells, offer many convenient features beyond launching programs and providing builtins.&#x20;

&#x20;For example, they remember commands that you’ve typed, and let you reuse those commands. Modern shells also let you edit those commands, so they don’t have to be the same each time. And modern shells let you define your own command abbreviations, shortcuts, and other features. For an experienced user, typing commands (e.g., with shorthand, shortcuts, and command completion) is a lot more efficient and effective than dragging things around in a fancy windowed interface.

### The Big Picture

Bash operates in a simple loop: It accepts a command, interprets the command, executes the command, and then waits for another command. See Fig. 3. Bash indicates its readiness to accept a command by displaying a prompt.&#x20;

<figure><img src="../.gitbook/assets/Group 12 (2).png" alt="" width="188"><figcaption></figcaption></figure>

### Shell prompt

When you begin a bash session, the first thing you'll notice is the shell prompt. On Armlab, it looks like the following:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 3.08.46 PM.png" alt=""><figcaption></figcaption></figure>

In addition to indicating its readiness to accept a command, the prompt provides us with a couple of useful pieces of information:

* The name of the computer we are logged into (armlab02)
* The current working directory ([\~](useful-command-line-features/#tilde-expansion))&#x20;

Generalizing, the prompt on Armlab has the following format:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-05-24 at 9.53.35 PM.png" alt=""><figcaption></figcaption></figure>

## What's a command?

* commands often thought of as bash command. that's true, but might give the impression that bash carries out the work. It does not. Simply launches other program for you. There are exceptions.&#x20;

One such command us `uname`, which prints the name of your OS on stdout. To invoke it, simply type `uname` and press ENTER:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-09 at 2.59.46 PM.png" alt=""><figcaption></figcaption></figure>

Another example is the date `command`, which prints the current date and time on stdout:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-09 at 2.59.54 PM.png" alt=""><figcaption></figcaption></figure>

5. `cal`, which displays a calendar for the current month:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-09 at 3.00.07 PM.png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Note that Linux is case-specific.&#x20;
{% endhint %}

### Options

Many commands accept arguments known as options, which modify the default behavior of the command. An option normally consists of a single character prefixed by a hyphen (e.g., `-a`), but it can also consist of a full word prefixed by two hyphens (i.e., `--list`). The complete list of a command's available options can be found in its [_manpage_](getting-help.md).

An example of an option is the `-w` option for the `cal` command, which modifies its output by prefixing each week with its...  To use this option, simply invoke `cal -w`:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-09 at 3.11.55 PM.png" alt=""><figcaption></figcaption></figure>

Another example of an option is `-m` for cal, which displays the calendar with the weeks starting from Monday instead of Sunday:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-09 at 3.13.46 PM.png" alt=""><figcaption></figcaption></figure>

### Combining options

Some commands permit you to group options in that way, and some commands require the options to be named separately, e.g., ls -l -R.

You can typically combine multiple options together, using both in a single command line invocation. For example, we can combine the `-m` and `-w` options of the cal command:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-09 at 3.16.28 PM.png" alt=""><figcaption></figcaption></figure>

### Operands

Many commands take operands, which might represent a filename, string, or number that the command acts upon.

We will illustrate arguments using the `sort` command, which sorts lines of text files. For example, say you have the file numbers.txt, with the numbers `5 7 3 4 8 3`, each on a separate line.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 6.59.10 PM.png" alt=""><figcaption></figcaption></figure>

Many programs can take multiple arguments. For example, you can provide `sort` two files, and it will print a sorted concatenation of both files, like so (note that numbers2.txt contains the numbers `2 5 1 9 0 5 2`):&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 7.00.46 PM.png" alt=""><figcaption></figcaption></figure>

### Commands with options and operands

Finally, many commands take both options and operands. &#x20;

For example, `sort numbers1.txt` with the `-r` option tells `sort` to reverse the order of the output:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 7.19.34 PM.png" alt=""><figcaption></figcaption></figure>
