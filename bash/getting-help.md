# Getting Help

Each Bash command has associated documentation that can be accessed from the command line. Such documentation is helpful when you need a refresher for a command or want more information about the command’s specifics.&#x20;

Retrieving documentation is one context where there is a distinction between OS utility programs and shell builtins. Specifically, the commands used to retrieve documentation for utility programs are different than the ones used for shell builtins, and vice versa.



Before moving foraward, let's briefly discuss what the command name represents.

#### External Programs and Shell Built-ins

The command name normally represents one of two things:

1. &#x20;A shell _built-in_, which is a utility that is implemented within Bash. &#x20;
2. An external program--either an OS utility program or a user-written program.&#x20;

The practical distinction between the two is normally irrelevant, but it does matter in certain contexts, such as when [retrieving documentation](getting-help.md) for a command, which will be covered soon.

## Documentation for utility programs

To retrieve documentation for a utility program, you can use the `man` command followed by the name of the utility. For example, `man cal` will display the manual page (_manpage_) for the `cal` utility. The output will be sent through the [`less`](broken-reference) pager, which displays the output one screen at a time. On armlab, the following page will be displayed:&#x20;

<figure><img src="https://lh6.googleusercontent.com/jicQ9FFUnwtJyablwzlVk-dSwXGuFimIJoeFH8-uEp5P_oiUJHuuNGu2Jzdb6gC6j4FmTGsOAgdxexY6LfjJIAhEOzmv0mwn-mejK4H9RwKrUpq2jBrHCBa-6TbqaKumyFhY_PdFswbRjUPcAFRuHkY" alt=""><figcaption></figcaption></figure>

## Documentation for Bash built-ins

If you want documentation for a Bash built-in, you must use the `help` instead of the `man`. For example, to retrieve documentation for the bash built-it `exit`, invoke:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 2.04.36 PM.png" alt=""><figcaption></figcaption></figure>

### How to determine if a command is a Bash built-in or a utility program

There are two ways you can determine if a command is a Bash built-in or a utility program.&#x20;

1. You can simply try the `man` command, and if the argument is a Bash built-in, Bash will return the following page, with `BASH_BUILTINS` written on the top corners:&#x20;

<figure><img src="https://lh4.googleusercontent.com/5k7q2Hl7hgogOQytiVUs5j1rgyHocnot1xIbIO-FFAaVkpOZy2e9Cm-APpoccvWTyjw1Yx6GCZCBydMULp9QvjzWFh1aB3tju7oNRUJktapPZwJzNMMycoWxH296Ez0BdCO_pjIz7TSszFff65CWH3g" alt=""><figcaption></figcaption></figure>

2. You can use the `type` command. For example, to check if the `exit` command is a Bash built-in, you can run `help exit`, and you will get the following output: &#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 8.00.25 PM.png" alt=""><figcaption></figcaption></figure>

\
\
