# Getting Help

Almost all commands come with some form of documentation that can be accessed from the command line. Such documentation is helpful when you need information on how to use a command or want more information about the command’s specifics, such as it's options. &#x20;

The command you use to retrieve the documentation differs depending on whether the command represents a shell builtin, such as _exit_, or an external program, such as _cal_. You can tell whether a command is a shell built-in or an external program by using the `type` command.  For example, if we invoke:

```bash
~> type exit
exit is a shell builtin
~> 
```

It tells us that _exit_ is a shell builtin. If the argument is an external program, type will print it's absolute pathname on stdout:

```bash
~> type cal
cal is /usr/bin/cal
~> 
```

### man

For an external program such as _cal_, you can get its _manpage_ (manual page) via the  `man` command:

```bash
man cal
```

The manpage will be displayed via the _less_ pager:

<figure><img src="../.gitbook/assets/Screenshot 2024-03-19 at 3.54.12 PM.png" alt="" width="375"><figcaption><p>Figure 1: <em>cal</em> manpage</p></figcaption></figure>

### help

For bash builtins such as _exit_, use the `help` command:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 2.04.36 PM.png" alt=""><figcaption></figcaption></figure>









* Almost all commands come with some form of help on how to use them. Usually there is online documentation called manpages, where “man” is short for manual. These are accessed using the man command, so man ls will give you documentation about the ls command.
* One problem with builtin commands is that you generally can’t use a -h or --help option to get usage reminders, and if a manpage exists it’s often just a pointer to the large bash manpage. That’s where the help command, which is itself a builtin, comes in handy. help displays help about shell builtins:
