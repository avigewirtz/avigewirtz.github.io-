# Getting Help

Almost all commands come with some form of documentation that can be accessed from the command line. Such documentation is helpful when you need information on how to use a command or want more information about the command’s specifics, such as it's options. &#x20;

The command you use to retrieve the documentation depends on whether the command represents a shell builtin, such as _exit_, or an external program, such as _cal_. You can tell whether a command is a shell built-in or an external program by using the `type` command.  For example, if we invoke:

```bash
~> type exit
exit is a shell builtin
~> 
```

It tells us that _exit_ is a shell builtin. However, if we invoke type on cal, which is a standalone program, we get the following output:

```bash
~> type cal
cal is /usr/bin/cal
~> 
```

Which is it's absolute pathname.

### man

For an external program such as _cal_, you can get its _manpage_ (manual page) by invoking the  `man` command. Note that the output will be displayed via the _less_ pager:

```bash
man cal
```

<figure><img src="../.gitbook/assets/Screenshot 2024-03-19 at 3.54.12 PM.png" alt="" width="375"><figcaption><p>Figure 1: <em>cal</em> manpage</p></figcaption></figure>

### help

For bash builtins such as _exit_, use the `help` command:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 2.04.36 PM.png" alt=""><figcaption></figcaption></figure>
