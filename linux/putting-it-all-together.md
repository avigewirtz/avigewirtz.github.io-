# Putting it All Together

It should be apparent by now that when a command is invoked in a terminal, what might be perceived as a simple action is actually the culmination of many complex processes involving several layers of abstraction within the computer system which ultimately leads to the task being completed. The layers between the terminal and hardware that work together to complete the task are the ISA, OS, standard libraries, core utilities, and shell. This layered approach--where you start with the services offered by the underlying hardware and then add a sequence of layers, each providing a higher (more abstract) level of service--provides many benefits. First, it decomposes the problem of building a system into more manageable components. Rather than implementing a monolithic piece of software that does everything you will ever want, you can implement several layers, each of which solves one part of the problem. Second, it provides a more modular design. If you decide that you want to add some new service, you may only need to modify the functionality at one layer, reusing the functions provided at all the other layers.

{% hint style="info" %}
It's important to note thinking of a system as a linear sequence of layers is an oversimplification. Many times there are multiple abstractions provided at any given level of the system. Additionally, the division between the layers isn't always clear-cut. For instance, user programs can interact directly with the kernel via system calls without using C library functions or utilities.
{% endhint %}

The general sequence of layers is illustrated in Figure 2.



<figure><img src="../.gitbook/assets/image (1).png" alt="" width="375"><figcaption><p>Figure 2: Layers of Computer System</p></figcaption></figure>

Let's illustrate a potential sequence of interactions The sequence of interactions between all the layers using the ls command:

1. **User input**: The user types a command with an input device, typically a keyboard, in a terminal or terminal emulator window. This command is a text-based instruction directing the computer system to perform a specific action.
2. **Terminal/terminal emulator**: The terminal or terminal emulator captures the user's input and transmits the command to the shell upon the user pressing the 'Enter' key.
3. **Shell**: The shell interprets the user's command, parsing it into its constituent components (e.g., command name, options, arguments), and checks for any syntax errors. The shell then proceeds to execute the command, either by running a built-in function or by invoking an external program.
4. **Utilities/application**:
5. **Standard C library**:
6. **OS Kernel**: The OS takes the commands from the shell and other programs and loads the instructions into memory for execution.
7. **ISA:**&#x20;
8. **Hardware**: The hardware receives the low-level instructions from the OS and performs the necessary operations, including data processing and I/O operations. This involves the CPU, memory, storage devices, and other hardware components working together.
9. **Output and prompt**: Once the operations are completed, the output, if any, is sent back to the terminal and displayed to the user. The shell then reverts to displaying its prompt, signaling to the user that it is ready to accept another command.

{% hint style="info" %}
It should be noted that there is a fundamental break between layers 5 and 6. Software in layer 3 and below-level mode privileges. Software from level 4 and above is user level. As such, there isn't a fundamental difference between a user-level programs, such as user-written programs and programs such as ssh, emacs, or even Bash. Both are software that interacts with the lower layers of the system, and both are subject to the same rules and limitations
{% endhint %}
