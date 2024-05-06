# Getting Documentation

Almost all commands come with some form of documentation that can be accessed from the command line. Such documentation is helpful when you need information on how to use a command or want more information about the command’s specifics, such as it's options. &#x20;

The command you use to retrieve the documentation depends on whether the command is a shell builtin, such as `exit`, or an external program, such as `cal`. For standalone programs such as `cal`,  use the `man` command, which outputs the command's _manpage_ (manual page) via the [`less`](basic-file-and-directory-operations/viewing-files.md#less) pager :&#x20;

```bash
man cal
```

<figure><img src="../.gitbook/assets/Screenshot 2024-03-19 at 3.54.12 PM.png" alt="" width="375"><figcaption><p>Figure 1: <code>cal</code> manpage</p></figcaption></figure>

For shell builtins such as `exit`, use the `help` command:&#x20;

```bash
~$ help exit
exit: exit [n]
    Exit the shell with a status of N.  If N is omitted, the exit status
    is that of the last command executed.
~$
```

{% hint style="info" %}
You can determine whether a command is a shell built-in or a standalone program by invoking `type command_name`. For example:

```bash
~$ type exit
exit is a shell builtin
~$
```

If the command is a standalone program, it'll return its absolute pathname:&#x20;

```bash
~> type cal
cal is /usr/bin/cal
~> 
```
{% endhint %}
