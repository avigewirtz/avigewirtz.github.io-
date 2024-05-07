# A Bit of Background

This chapter introduces a range of concepts related to Linux system programming. It is intended for readers who have worked primarily with other operating systems, or who have only limited experience with Linux or another UNIX implementation.

## Terminal

CLI commands are issued via a _terminal_. In the nascent days of interactive computing, terminals were hardware devices, consisting of a keyboard and a display unit. The first terminals were teletype machines, such as the Model 33 ASR shown in Figure 1, whose display unit was a paper-roll printer.

<figure><img src="../../.gitbook/assets/560px-Teletype-IMG_7287.jpg" alt="" width="280"><figcaption><p>Figure 1: Teletype Model 33 ASR</p></figcaption></figure>

Teletypes fell out of use in the 1970s with the advent of video display terminals, such as the DEC VT100 shown in Figure 2, which provided instant user-feedback and editing capabilities.&#x20;

<figure><img src="../../.gitbook/assets/1200px-DEC_VT100_terminal_transparent.png" alt="" width="375"><figcaption></figcaption></figure>

Today, hardware terminals are largely obsolete. The predominant method for accessing the CLI is through a _terminal emulator_, which is a GUI program that simulates the functionality of a hardware terminal. An example of a terminal emulator is macOS's Terminal, shown in Figure 3.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-19 at 5.46.26 PM.png" alt="" width="375"><figcaption><p>Figure 3: macOS Terminal Application</p></figcaption></figure>



## Shell

\






























## Putting it all together





<figure><img src="../../.gitbook/assets/image (1).png" alt="" width="375"><figcaption><p>Figure 2: Layers of Computer System</p></figcaption></figure>

{% hint style="info" %}
It's important to note that thinking of a system as a linear sequence of layers is an oversimplification. In reality, systems are complex and consist of various components that often interact in non-linear and interdependent ways.

For example, the shell or any other program might interact directly with the OS kernel using system calls, bypassing higher-level abstractions like the standard C library. This is often done when the developer needs more precise control over the system resources than the higher-level libraries provide.
{% endhint %}

## Example of a sequence of interactions&#x20;

We will now illustrate a potential sequence of interactions between all the layers when a command is invoked by the user. For this example, we will use the `ls` command, which when invoked in the terminal results in the contents of the working directory being displayed on the screen. The following sequence is an oversimplification, but it should give you a good idea of the flow:

1. **User input**: The user types `ls` in the terminal and hits the `Enter` key.
2. **Terminal/terminal emulator**: The terminal captures the user's keystrokes and passes the command string `ls` to the shell.&#x20;
3. **Shell**: The shell, which might be bash or another shell, parses the `ls` command and verifies its syntax. Finding it valid, the shell starts a new process to run the command.
4. **Core utilities**: The `ls` command is part of the Unix core utilities. `ls` looks up the necessary information about the current directory, using functions provided by the standard C library.
5. **Standard C library**: `ls` calls the relevant library functions, such as `opendir`, `readdir`, and `closedir`, which make system calls to the OS kernel to perform the actual operations.
6. **OS Kernel**: The kernel receives the system calls, verifies the permissions of the process making the call, and if everything is in order, performs the necessary operations on the file system. It retrieves the list of files and directories in the current directory and passes this information back up to the `ls` command.
7. **Hardware**: The actual physical components of the computer carry out the instructions. The CPU performs the necessary computations to complete the kernel's instructions, accessing the relevant memory locations and retrieving the directory's listing.
8. **Output and prompt**: The results of the `ls` command -- the list of files and directories -- are passed back up through the layers to the shell, which hands this data off to the terminal. The terminal then displays this output to the user. After the command has been executed, the shell displays a new prompt, indicating that it is prepared to accept a new command.
