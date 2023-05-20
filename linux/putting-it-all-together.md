# Putting it All Together

**1. Hardware**: At the most fundamental level, a computer's hardware provides the raw computing resources, including the central processing unit (CPU), memory (RAM), storage devices (like SSDs or HDDs), and input/output devices (like the keyboard, mouse, and display). The CPU carries out the actual computations, RAM holds data that needs to be quickly accessed, and storage devices hold larger amounts of data for long-term storage. At this level, operations are performed in binary, directly manipulating electrical signals within the hardware.

**2. Instruction Set Architecture (ISA)**: This is the interface between the hardware and the low-level software. It's a specification detailing the CPU's functions, including the specific binary codes it understands and how it processes them. ISAs can be complex (CISC - Complex Instruction Set Computer) like x86, or simplified (RISC - Reduced Instruction Set Computer) like ARM. At this layer, instructions are written in machine language and assembly code. This is the lowest level of code that is still readable by humans (with some training). Machine language is composed of binary instructions that directly control the CPU. Assembly is a thin layer on top of this, representing machine code instructions with human-readable labels.

**3. Operating System (OS):** The Operating System provides an interface between the hardware and user-level software, primarily through a feature known as the system call interface. This interface allows user-level applications to request services from the OS, which are typically related to input/output operations, process management, file management, and communication. It's through system calls that a program can access the processor, memory, and other system resources managed by the OS.

**4. Libraries:** Building off the system call interface, libraries provide a higher-level programming interface to the services provided by the OS. A library is a collection of pre-compiled code that programs can use to perform common tasks. For instance, a standard C library (like glibc in GNU/Linux systems) provides a set of functions (like `printf`, `malloc`, etc.), which in turn use lower-level system calls to interact with the OS.

While a programmer could write a program using just system calls, this can be quite complex and error-prone. Libraries abstract away many of the details and provide a more convenient and efficient means to perform these tasks. They encapsulate system calls and other complex operations in more straightforward, high-level functions.

So, in a way, libraries provide an interface to the system call interface, abstracting the complexity of the system calls and making programming more accessible and efficient. By writing a program that uses library functions, a developer indirectly uses the services provided by the OS through the system call interface.

**5. Core Utilities**:  On top of the libc layer, a set of core utilities or commands are usually built to perform common system tasks, such as copying files (`cp`), listing directory contents (`ls`), or text processing (`grep`, `awk`). These utilities are standalone programs that can be invoked from the command lineThese are the basic tools that come with an OS, which provide a way to interact with the system and perform basic tasks. These can be command-line utilities like 'ls', 'cd', 'mkdir' in Unix-based systems, or GUI tools like Windows Explorer in Windows.

**6. Shell**: A shell is a command interpreter that provides a text-based interface for users to interact with the OS. Shells allow users to launch programs, manage files, and perform other tasks by typing commands. The shell interprets these commands and uses system calls to execute them. Examples of shells include bash, zsh, and PowerShell. The shell interacts with the system call interface, executing system calls based on user input. When you type a command into the shell, like `ls` or `cat`, the shell locates the appropriate utility program, starts a new process, and makes system calls to execute the command.

**7. Terminal**: The terminal (also known as a console or command line) is the interface that allows users to interact with the shell. In a graphical user interface (GUI), a terminal is usually an application like Terminal on macOS, Command Prompt on Windows, or gnome-terminal on Linux. In a non-GUI environment, the terminal may be a text-based screen shown on the monitor.

So, to summarize, the flow of command execution starts from the terminal, where you type a command. This command is interpreted by the shell, which may use core utilities and libraries to execute the command. The libraries interface with the OS, making system calls as necessary. The OS interprets these calls and communicates with the hardware using the language specified by the ISA. Finally, the hardware executes the low-level instructions, thus completing the flow from terminal to hardware and back.

The sequence of interactions between the user, terminal (or terminal emulator), shell, operating system (OS), and hardware to process and execute a command can be outlined as follows:

1. **User input**: The user types a command with an input device, typically a keyboard, in a terminal or terminal emulator window. This command is a text-based instruction directing the computer system to perform a specific action.
2. **Terminal/terminal emulator**: The terminal or terminal emulator captures the user's input and transmits the command to the shell upon the user pressing the 'Enter' key.&#x20;
3. **Shell**: The shell interprets the user's command, parsing it into its constituent components (e.g., command name, options, arguments), and checks for any syntax errors. The shell then proceeds to execute the command, either by running a built-in function or by invoking an external program.&#x20;
4. **Operating System**: The OS takes the commands from the shell and other programs and loads the instructions into memory for execution.&#x20;
5. **Hardware**: The hardware receives the low-level instructions from the OS and performs the necessary operations, including data processing and I/O operations. This involves the CPU, memory, storage devices, and other hardware components working together.
6. **Output and prompt**: Once the operations are completed, the output, if any, is sent back to the terminal and displayed to the user. The shell then reverts to displaying its prompt, signaling to the user that it is ready to accept another command.

The sequence of interactions is illustrated in Figure 4.

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 3.21.28 PM.png" alt=""><figcaption><p>Figure 4: Sequence of interactions between the user, terminal, shell, OS, and hardware.</p></figcaption></figure>




When a command is issued in a terminal, what we often perceive as a simple action is actually the culmination of a complex process involving several layers of abstraction within a computer system. This process ultimately leads to the command being executed by the computer hardware. 

But let's take a step back to look at these layers, starting from the bottom up, and see how they interact with each other to make the command execution possible.


The general idea is that you start with the services offered by the underlying hardware and then add a sequence of layers, each providing a higher (more abstract) level of service. 
The services provided at the high layers are implemented in terms of the services provided by the low layers. 

At the lowest level, there is the hardware, which includes the central processing unit (CPU), memory, storage devices, and various peripheral devices. All interactions at this level involve electrical or magnetic signals, which are inherently complex and difficult to work with directly.
Sitting above the hardware is the Instruction Set Architecture (ISA). The ISA abstracts the hardware and provides a more user-friendly software interface. In essence, it defines the machine language that the CPU can understand and process. It is through this layer that programs can communicate with the hardware.


Up next is the Operating System (OS) layer, which further abstracts the complexities of the ISA, providing a cleaner, safer, and more efficient interface to the hardware. 

An operating system is a program that, from the programmer’s point of view, adds a variety of new instructions and features, above and beyond what the ISA level provides. 

This level provides the complete set of instructions available to application programmers. The new instructions are called system calls. A system call invokes a predefined operating system service. A typical system call might be to read some data from a file or to…


OS Features: 
- time-sharing. Does this by managing the hardware resources like memory, CPU, and peripherals. 


Above the OS Kernel, there is the Standard C Library. This library, among other things, provides a higher-level interface to system calls. In doing so, it simplifies the process of writing software and reduces the chance of errors. It essentially wraps the somewhat arcane system calls in more user-friendly functions.
The next layer is utilities, which are built on top of the standard library. These utilities are pre-packaged programs that further reduce the need to write your own software for many common tasks. They provide a set of common operations that are used frequently, reducing the need for repetitive coding.

Sitting above utilities and user programs is the shell. The shell provides a language in which commands are issued. It handles tasks like locating programs, handling input and output calls, and starting a new process. The shell essentially provides a cleaner interface and makes it more efficient for users to interact with the system. This is done via the shell's language, which allows programs to be run with simple commands and implements the command-line interface (CLI).


At the top of this abstraction pyramid is the terminal or terminal emulator. This is the interface that users interact with directly. It captures input from the user and passes it to the shell for interpretation and execution.


Notes: 

1. While these layers provide a simplified view of how commands are issued and executed, it's important to note thinking of a system as a linear sequence of layers is an oversimplification. Many times there are multiple abstractions provided at any given level of the system. Additionally, the division between the layers isn't always clear-cut. For instance, user programs can interact directly with the kernel via system calls without using C library functions or utilities.
2. This system is a simplification. In reality there are more layers. 
3. There is a fundamental break between levels 3 and 4. Software in Level 3 and below level mode privileges. Software from level 4 and above is user level. As such, there isn't a fundamental difference between a user-level programs, such as user-written programs and programs such as ssh, emacs, or even Bash. Both are software that interacts with the lower layers of the system, and both are subject to the same rules and limitations.


Benefits of layering 


1. Layering provides two useful features. First, it decomposes the problem of building a network into more manageable components. Rather than implementing a monolithic piece of software that does everything you will ever want, you can implement several layers, each of which solves one part of the problem.
2. Second, it provides a more modular design. If you decide that you want to add some new service, you may only need to modify the funconality at one layer, reusing the func!ons provided at all the other layers.

