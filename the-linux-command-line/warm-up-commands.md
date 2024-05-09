---
description: This page introduces Bash commands.
---

# Getting Started With Bash

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

## What's a command?

Simplest command consists of just a command name. One such command us `uname`, which prints the name of your OS on stdout. To invoke it, simply type `uname` and press ENTER:

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

Sort also provides many options. For example, `sort numbers1.txt` with the `-r` option tells `sort` to reverse the order of the output:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 7.19.34 PM.png" alt=""><figcaption></figcaption></figure>
