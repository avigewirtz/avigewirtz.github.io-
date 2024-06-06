# Getting Documentation for Commands

Almost all Linux commands come with a manual page (manpage) that can be accessed directly from the command line. The manual page describes the basics of the command. To obtain a manual page, type man followed by the name of the command. For example, For standalone programs such as `cal`, you can obtain a manual page (manpage) via the command command:&#x20;

```bash
man cal
```

<figure><img src="../.gitbook/assets/Screenshot 2024-03-19 at 3.54.12 PM.png" alt="" width="375"><figcaption><p>Figure 1: <code>cal</code> manpage</p></figcaption></figure>

Sometimes, instead of a manpage, you'll get a shell builtin response. This happens when the command is not a standalone program but built into the shell. For shell builtins such as `exit`, use the `help` command:&#x20;

```bash
~$ help exit
exit: exit [n]
    Exit the shell with a status of N.  If N is omitted, the exit status
    is that of the last command executed.
~$
```

{% hint style="info" %}
You can determine whether a command is a shell built-in or a standalone program by invoking `type COMMAND_NAME`. For example:

```bash
~$ type exit
exit is a shell builtin
~$
```

If the command is a standalone program, `type` will return its absolute pathname:&#x20;

```bash
~> type cal
cal is /usr/bin/cal
~> 
```
{% endhint %}
