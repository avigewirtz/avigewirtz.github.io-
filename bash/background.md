# What is Bash?

BASH, short for "Bourne-Again SHell," is a popular Unix-shell developed by the [GNU Project](https://en.wikipedia.org/wiki/GNU\_Project). It is the default shell on many Linux distributions.&#x20;

Bash is a user-program, and hence can be awapped for any other shell.&#x20;



Bash typically runs in a terminal and executes commands interactively.&#x20;

The purpose of Bash, like all shells, is to implement the command line interface. It is also possible to create a file known as a shell script which bash executes. We will not do that here.&#x20;







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

The basic form of a Unix command is:&#x20;

```
commandname options operands
```

The easiest way to explain is by example.&#x20;

```
gcc -c hello.c
```

In this case, the command name is gcc, which represents the gcc compiler. The -c option alters the default behavior of gcc



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
