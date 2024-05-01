# What is Bash?

BASH, short for "Bourne-Again SHell," is a popular Unix-shell developed by the [GNU Project](https://en.wikipedia.org/wiki/GNU\_Project). It is the default shell on many Linux distributions.&#x20;

A shell is a command language interpreter. It reads commands entered by the user in the terminal and executes them. An example of a command is:

```
// Some code
```



Bash typically runs in a terminal and executes commands interactively, but it can also read commands from a file, typically called a shell script. In this tutorial, we will only focus on commands entered in the terminal, but the idea is the same.



### The Big Picture

Bash operates in a simple loop: It accepts a command, interprets the command, executes the command, and then waits for another command. See Fig. 3. Bash indicates its readiness to accept a command by displaying a prompt.&#x20;

<figure><img src="../../.gitbook/assets/Group 12 (2).png" alt="" width="188"><figcaption></figcaption></figure>

### Shell prompt

When you begin a bash session, the first thing you'll notice is the shell prompt. On Armlab, it looks like the following:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 3.08.46 PM.png" alt=""><figcaption></figcaption></figure>

In addition to indicating its readiness to accept a command, the prompt provides us with a couple of useful pieces of information:

* The name of the computer we are logged into (armlab02)
* The current working directory ([\~](useful-command-line-features.md#tilde-expansion))&#x20;

Generalizing, the prompt on Armlab has the following format:&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-24 at 9.53.35 PM.png" alt=""><figcaption></figcaption></figure>

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
