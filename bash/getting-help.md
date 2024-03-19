# Getting Help

Each Bash command typically has associated documentation that can be accessed from the command line. Such documentation is helpful when you need a refresher on how to use a command or want more information about the command’s specifics, such as it's available options. &#x20;

The command you use to retreive the documentation differes depending on whether the command is a bash builtin, such as exit, or an external program, such as cal. For external programs, use the man command followed by the name of the program. For example, in you invoke:

```
man cal
```

the manpage for cal will be displayed on the screen:

<figure><img src="../.gitbook/assets/Screenshot 2024-03-19 at 3.54.12 PM.png" alt="" width="375"><figcaption><p>Figure 1. cal manpage.</p></figcaption></figure>

Note that the output will be displayed via the less utility. For documentation on bash built-ins, use the help command. For example, to retrieve documentation for `exit,` which is a bash built-it, invoke:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 2.04.36 PM.png" alt=""><figcaption></figcaption></figure>
