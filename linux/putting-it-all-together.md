# Putting it All Together

It should be apparent by now that when a command is invoked in a terminal, what might be perceived as a simple action is actually the culmination of many complex processes involving several layers of abstraction within the computer system, which ultimately leads to the task being completed. The layers between the terminal and hardware that work together to complete the task are the ISA, OS, standard libraries, core utilities, and shell. This layered approach--where you start with the services offered by the underlying hardware and then add a sequence of layers, each providing a higher (more abstract) level of service--provides many benefits. First, it decomposes the problem of building a system into more manageable components. Rather than implementing a monolithic piece of software that does everything you will ever want, you can implement several layers, each of which solves one part of the problem. Second, it provides a more modular design. If you decide that you want to add some new service, you may only need to modify the functionality at one layer, reusing the functions provided at all the other layers. The general sequence of layers is illustrated in Figure 2.



<figure><img src="../.gitbook/assets/image (1).png" alt="" width="375"><figcaption><p>Figure 2: Layers of Computer System</p></figcaption></figure>

{% hint style="info" %}
It's important to note thinking of a system as a linear sequence of layers is an oversimplification. In reality, systems are complex and consist of various components that often interact in non-linear and interdependent ways.

For example, an application might interact directly with the OS kernel using system calls, bypassing higher-level abstractions like the standard C library. This is often done when the developer needs more precise control over the system resources than the higher-level libraries provide.


{% endhint %}

## Example of a sequence of interactions&#x20;

We will now illustrate a potential sequence of interactions between all the layers when a command is invoked by the user. For this example, we will use the `ls` command, which displays the contents of the working directory. This is a simplification, but it should give a good impression of the flow:

1. **User input**: The user types `ls` in the terminal and hits the `Enter` key.
2. **Terminal/terminal emulator**: The terminal captures the user's keystrokes and passes the command string `ls` to the shell. The terminal waits for the output to display.
3. **Shell**: The shell, which might be bash or another shell, parses the `ls` command and verifies its syntax. Finding it valid, the shell starts a new process to run the command.
4. **Core utilities**: The `ls` command is part of the Unix core utilities. It looks up the necessary information about the current directory, using functions provided by the standard C library.
5. **Standard C library**: The library functions called by `ls`, such as `opendir`, `readdir`, and `closedir`, make system calls to the OS kernel to perform the actual operations.
6. **OS Kernel**: The kernel receives the system calls, verifies the permissions of the process making the call, and if everything is in order, performs the necessary operations on the file system. It retrieves the list of files and directories in the current directory and passes this information back up to the `ls` command.
7. **ISA (Instruction Set Architecture)**: This is the level at which the OS kernel's instructions are actually executed on the CPU. The ISA is a specification that describes the low-level machine language instructions that the CPU can understand. The CPU uses the ISA to perform the kernel's instructions, such as accessing the file system to retrieve the directory listing.
8. **Hardware**: The actual physical components of the computer carry out the instructions. The CPU performs computations and the hard drive or SSD retrieves the file data.
9. **Output and prompt**: The results of the `ls` command -- the list of files and directories -- are passed back up through the layers to the shell, which hands this data off to the terminal. The terminal then displays this output to the user. After the command has been executed, the shell displays a new prompt, waiting for the next user input.
