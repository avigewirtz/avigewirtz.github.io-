# Getting Help

Each Bash command typically has associated documentation that can be accessed from the command line. Such documentation is helpful when you need a refresher on how to use a command or want more information about the command’s specifics, such as it's available options. &#x20;

The command you use to retrieve the documentation differs depending on whether the command represents a bash builtin, such as _exit_, or an external program, such as _cal_. For external programs such as _cal_, use the `man` command, like so:&#x20;

```
man cal
```

_cal_'s _manpage_ (manual page) will be displayed via the _less_ pages:

<figure><img src="../.gitbook/assets/Screenshot 2024-03-19 at 3.54.12 PM.png" alt="" width="375"><figcaption><p>Figure 1. cal manpage.</p></figcaption></figure>

For bash builtins such as _exit_, use the `help` command:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 2.04.36 PM.png" alt=""><figcaption></figcaption></figure>
