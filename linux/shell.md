# Shell

When you enter commands on the command line, you are ultimately issuing commands to the operating system. However, you are not directly communicating with the OS; rather, you interact with it through an intermediary known as the _shell_.&#x20;

The shell is a program residing between the terminal and the OS that implements the command line interface. It consists of a command interpreter and a programming language.&#x20;

As a programming language, it specifies the syntax and semantics of CLI commands—that is, the format commands must follow and what sort of operations are possible.&#x20;

As a command interpreter, it reads and interprets textual commands and executes them by invoking the appropriate calls to the operating system (OS) kernel—either directly or by calling other programs that make the calls. The OS kernel then invokes the necessary low-level hardware instructions to complete the task. If there is output for the user, it will be sent back and displayed on the terminal. The relationship between the user, terminal, shell, OS kernel, and hardware looks like the following:

The relationship between the user, terminal, shell, OS kernel, and hardware can be summarized as follows:

1. User: Interacts with the terminal by entering text-based commands.
2. Terminal: Acts as an interface to the shell, allowing the user to input text-based commands and receive output.
3. Shell: Interprets and executes commands from terminal, communicating with the OS kernel and utilities as needed.
4. OS Kernel: Receives instructions from the shell, translating them into low-level hardware operations.
5. Hardware: Executes the low-level instructions, completing the task requested by the user.

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 3.21.28 PM.png" alt=""><figcaption></figcaption></figure>
