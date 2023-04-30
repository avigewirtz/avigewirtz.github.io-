# Shell

When you enter commands on the command line, you are ultimately issuing commands to the operating system, which provides an interface to the computer hardware. However, you are not directly interacting with the OS. Instead, you do so via an intermediary known as the _Shell_.&#x20;

The shell is the program that lies between the terminal and OS and implements the command line interface.&#x20;

The **shell** is a command interpreter and programming language that provides a command line interface to the operating system kernel and utilities.&#x20;

As a programming language, it specifies the syntax and semantics of CLI commands—that is, the format commands must follow and what sort of operations are possible.&#x20;

As a command interpreter, it reads and interprets textual commands and executes them by invoking the appropriate calls to the operating system (OS) kernel—either directly or by calling other programs that make the calls. The OS kernel then invokes the necessary low-level hardware instructions to complete the task. If there is output for the user, it will be sent back and displayed on the terminal. The relationship between the user, terminal, shell, OS kernel, and hardware looks like the following:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 3.21.28 PM.png" alt=""><figcaption></figcaption></figure>
