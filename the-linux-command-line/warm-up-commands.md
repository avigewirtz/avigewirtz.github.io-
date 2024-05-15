---
description: This page introduces Bash commands.
---

# First Command-Line Session

### History

Bash keeps a record of the commands you've entered in a file named `.bash_history`, typically stored in your home directory. You can view This allows you to perform a few extremely useful operations:&#x20;

* **Display your command history:**  Invoke `history`.&#x20;
* **Search your command history**: Press`Ctrl-r` and type a few characters of the command you're looking for. Press `Ctrl-r` again to cycle through matching commands.
* **Navigate your command history**: Use the up and down arrow keys.
* **Reuse commands**: Use the `!` (bang) operator followed by a number (e.g., `!125`), to execute the command with that number in the history.&#x20;



When you begin a Bash session on Armlab, the first thing you'll notice is the shell prompt, which looks like this:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 3.08.46 PM.png" alt=""><figcaption></figcaption></figure>

The prompt is Bash's way of telling us it's ready to accept a command.  It addition, it provides us with a couple of useful pieces of information:

* The name of the computer we are logged into (armlab02)
* The current working directory ([\~](useful-command-line-features.md#tilde-expansion))&#x20;

Generalizing, the prompt on Armlab has the following format:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-05-24 at 9.53.35 PM.png" alt=""><figcaption></figcaption></figure>

#### A Few Simple Commands

The simplest type of command consists of just a command name. One such command us `uname`, which prints the name of your OS on stdout. To invoke it, simply type `uname` and press ENTER:

Another example is the date `command`, which prints the current date and time on stdout:

5. `cal`, which displays a calendar for the current month:

{% hint style="warning" %}
Note that Linux is case-specific.&#x20;
{% endhint %}

### Options

Many commands accept arguments known as options , which modify the default behavior of the command. An option normally consists of a single character prefixed by a hyphen (e.g., `-a`), but it can also consist of a full word prefixed by two hyphens (i.e., `--list`). The complete list of a command's available options can be found in its [_manpage_](getting-help.md).

An example of an option is the `-w` option for the `cal` command, which modifies its output by prefixing each week with its...  To use this option, simply invoke `cal -w`:

Another example of an option is `-m` for cal, which displays the calendar with the weeks starting from Monday instead of Sunday:

### Combining options

Some commands permit you to group options in that way, and some commands require the options to be named separately, e.g., ls -l -R.

You can typically combine multiple options together, using both in a single command line invocation. For example, we can combine the `-m` and `-w` options of the cal command:

### Operands

Many commands take operands, which might represent a filename, string, or number that the command acts upon.

We will illustrate arguments using the `sort` command, which sorts lines of text files. For example, say you have the file numbers.txt, with the numbers `5 7 3 4 8 3`, each on a separate line.&#x20;

Many programs can take multiple arguments. For example, you can provide `sort` two files, and it will print a sorted concatenation of both files, like so (note that numbers2.txt contains the numbers `2 5 1 9 0 5 2`):&#x20;

Sort also provides many options. For example, `sort numbers1.txt` with the `-r` option tells `sort` to reverse the order of the output:&#x20;
