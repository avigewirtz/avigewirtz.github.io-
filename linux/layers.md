# Layers

When a command is executed in a terminal, what might be perceived as a simple action is actually the culmination of many complex processes involving several layers of abstraction within the computer system. This process ultimately leads to the command being executed by the computer hardware.

But let's take a step back to look at these layers, starting from the bottom up, and see how they interact with each other to make the command execution possible.

The general idea is that you start with the services offered by the underlying hardware and then add a sequence of layers, each providing a higher (more abstract) level of service. The services provided at the high layers are implemented in terms of the services provided by the low layers.

## **Hardware**

At the lowest level, there is the hardware, which provides the raw computing resources, including the central processing unit (CPU), memory (RAM), storage devices (like SSDs or HDDs), and input/output devices (like the keyboard, mouse, and display). The CPU carries out the actual computations, RAM holds data that needs to be quickly accessed, and storage devices hold larger amounts of data for long-term storage. At this level, operations are performed in binary, directly manipulating electrical or magnetic signals within the hardware. Hardware is incredibly complex and difficult to work with directly.

## **Instruction Set Architecture (ISA)**

Sitting above the hardware is the Instruction Set Architecture (ISA), which is the lowest level software interface. The ISA abstracts the hardware by providing a software interface. It's a specification detailing the CPU's functions, including the specific binary codes it understands and how it processes them. ISAs can be complex (CISC - Complex Instruction Set Computer) like x86, or simplified (RISC - Reduced Instruction Set Computer) like ARM.  In essence, it defines the machine language that the CPU can understand and process. It is through this layer that programs can communicate with the hardware

## **Operating System (OS)**

This interface allows user-level applications to request services from the OS, which are typically related to input/output operations, process management, file management, and communication. It's through system calls that a program can access the processor, memory, and other system resources managed by the OS.

An operating system comprises two main parts: the kernel and the system programs.

### **Kernel**

The kernel is the core of the operating system. It's a software layer that resides between the hardware and most other software, performing two critical functions: managing computer hardware resources and providing a straightforward interface to these resources for other software.

Understanding why these functions are essential requires recognizing the challenges the kernel addresses.

#### **Resource Management**

Linux is a multiuser and multitasking operating system, meaning it supports multiple users, each potentially running multiple programs concurrently. This is true even on a single CPU system.

Sharing hardware resources among many users and programs presents numerous challenges. For example:

* How can we isolate executing programs in separate memory regions?
* How do we protect each user's personal files from unauthorized access?
* How do we prevent simultaneous usage of an I/O device by different programs, which could result in incoherent output?

The kernel is the sophisticated software solution to these issues. It manages hardware resources, allocating memory, disk space, and CPU cycles to all running programs. It also controls file access for each user and manages interprocess communication.

#### **Hardware Interface**

Programs need to interact with the CPU and various peripheral devices like mice, keyboards, hard drives, cameras, microphones, speakers, and more. This presents another set of challenges:

* Direct communication with a hardware device requires a programmer to understand its low-level machine language interface, which could involve reading hundreds of pages of manuals. How can we simplify this process?
* New peripherals constantly enter the market, often after a program is written. How can we ensure programs remain functional when new devices are added to the system?

The kernel addresses these issues by abstracting the complexities of hardware interfaces, providing a simpler, cleaner interface for programmers. This is the kernel's second major function, allowing software to interact with hardware in a standardized and simplified way.

The Linux kernel addresses the complexities of hardware devices' low-level interfaces by providing a simplified, standardized interface for programmers. This is known as the system call interface.

### **System Calls**

System calls form the primary interface between a program and the kernel. When a program requires a service from the kernel, it issues a request through a system call. Linux provides several hundred system calls, each designed for a unique purpose. For instance, the `read` and `write` system calls are used for interaction with I/O devices, while `fork` and `exec` are utilized to manage executing programs. Although these system calls are primarily written in C, they can be invoked by programs written in other languages.

Major categories of system calls include:

1. Process Control (e.g., `fork`, `exit`)
2. File Manipulation (e.g., `open`, `read`, `write`)
3. Device Management (e.g., `ioctl`)
4. Information Maintenance (e.g., `getpid`, `time`)
5. Communications (e.g., `pipe`, `socket`)

##

Up next is the Operating System (OS) layer, which further abstracts the complexities of the ISA, providing a cleaner, safer, and more efficient interface to the hardware.

An operating system is a program that, from the programmer’s point of view, adds a variety of new instructions and features, above and beyond what the ISA level provides.

This level provides the complete set of instructions available to application programmers. The new instructions are called system calls. A system call invokes a predefined operating system service. A typical system call might be to read some data from a file or to…

OS Features:

* time-sharing. Does this by managing the hardware resources like memory, CPU, and peripherals. The Operating System provides an interface between the hardware and user-level software, primarily through a feature known as the system call interface. This interface allows user-level applications to request services from the OS, which are typically related to input/output operations, process management, file management, and communication. It's through system calls that a program can access the processor, memory, and other system resources managed by the OS.

## **Libraries:**&#x20;

Above the OS Kernel, there is the Standard C Library. This library, among other things, provides a higher-level interface to system calls. In doing so, it simplifies the process of writing software and reduces the chance of errors. It essentially wraps the somewhat arcane system calls in more user-friendly functions. The next layer is utilities, which are built on top of the standard library. These utilities are pre-packaged programs that further reduce the need to write your own software for many common tasks. They provide a set of common operations that are used frequently, reducing the need for repetitive coding.

Sitting above utilities and user programs is the shell. The shell provides a language in which commands are issued. It handles tasks like locating programs, handling input and output calls, and starting a new process. The shell essentially provides a cleaner interface and makes it more efficient for users to interact with the system. This is done via the shell's language, which allows programs to be run with simple commands and implements the command-line interface (CLI).

At the top of this abstraction pyramid is the terminal or terminal emulator. This is the interface that users interact with directly. It captures input from the user and passes it to the shell for interpretation and execution.

Programmers seldom interact directly with system calls. Instead, they use library functions, often referred to as "wrapper functions", that call the system calls for them. Libraries offer a multitude of benefits over direct system call use.

The key advantage is portability. System calls are specific to an operating system, meaning that a Linux system call interface differs from those on macOS or Windows. Library functions, in contrast, are typically platform-independent, making code using these libraries portable across different operating systems. Library APIs also offer improved efficiency, security, and ease of use.



Building off the system call interface, libraries provide a higher-level programming interface to the services provided by the OS. A library is a collection of pre-compiled code that programs can use to perform common tasks. For instance, a standard C library (like glibc in GNU/Linux systems) provides a set of functions (like `printf`, `malloc`, etc.), which in turn use lower-level system calls to interact with the OS.

While a programmer could write a program using just system calls, this can be quite complex and error-prone. Libraries abstract away many of the details and provide a more convenient and efficient means to perform these tasks. They encapsulate system calls and other complex operations in more straightforward, high-level functions.

So, in a way, libraries provide an interface to the system call interface, abstracting the complexity of the system calls and making programming more accessible and efficient. By writing a program that uses library functions, a developer indirectly uses the services provided by the OS through the system call interface.

## **Core Utilities**

On top of the libc layer, a set of core utilities or commands are usually built to perform common system tasks, such as copying files (`cp`), listing directory contents (`ls`), or text processing (`grep`, `awk`). These utilities are standalone programs that can be invoked from the command lineThese are the basic tools that come with an OS, which provide a way to interact with the system and perform basic tasks. These can be command-line utilities like 'ls', 'cd', 'mkdir' in Unix-based systems, or GUI tools like Windows Explorer in Windows.

The Linux operating system includes an array of pre-written utility programs. These programs, many of which are contributions from the GNU project, perform common tasks and help the system run efficiently.

These utilities provide essential services to users. Some notable utility programs include:

* `make`: Determines which source files need to be recompiled and/or linked.
* `ssh`: Allows users to log into a remote machine and execute commands.
* `grep`: Searches files for text matching a specified pattern.

To execute these utilities, you can enter their names along with any required parameters into the command line. If you want to combine utilities, you can use pipes (`|`) to direct the output of one command into another. For instance, you might use `grep` to search for a pattern in the output of another command, like this: `ls -l | grep ".txt"`. This will list all the .txt files in the current directory.

## **Shell**

Sitting above utilities and user programs is the shell. The shell provides a language in which commands are issued. It handles tasks like locating programs, handling input and output calls, and starting a new process. The shell essentially provides a cleaner interface and makes it more efficient for users to interact with the system. This is done via the shell's language, which allows programs to be run with simple commands and implements the command-line interface (CLI).

A shell is a command interpreter that provides a text-based interface for users to interact with the OS. Shells allow users to launch programs, manage files, and perform other tasks by typing commands. The shell interprets these commands and uses system calls to execute them. Examples of shells include bash, zsh, and PowerShell. The shell interacts with the system call interface, executing system calls based on user input. When you type a command into the shell, like `ls` or `cat`, the shell locates the appropriate utility program, starts a new process, and makes system calls to execute the command.

## **Terminal**

At the top of this abstraction pyramid is the terminal or terminal emulator. This is the interface that users interact with directly. It captures input from the user and passes it to the shell for interpretation and execution.

The terminal (also known as a console or command line) is the interface that allows users to interact with the shell. In a graphical user interface (GUI), a terminal is usually an application like Terminal on macOS, Command Prompt on Windows, or gnome-terminal on Linux. In a non-GUI environment, the terminal may be a text-based screen shown on the monitor.

So, to summarize, the flow of command execution starts from the terminal, where you type a command. This command is interpreted by the shell, which may use core utilities and libraries to execute the command. The libraries interface with the OS, making system calls as necessary. The OS interprets these calls and communicates with the hardware using the language specified by the ISA. Finally, the hardware executes the low-level instructions, thus completing the flow from terminal to hardware and back.

## Notes

1. While these layers provide a simplified view of how commands are issued and executed, it's important to note thinking of a system as a linear sequence of layers is an oversimplification. Many times there are multiple abstractions provided at any given level of the system. Additionally, the division between the layers isn't always clear-cut. For instance, user programs can interact directly with the kernel via system calls without using C library functions or utilities.
2. This system is a simplification. In reality there are more layers.
3. There is a fundamental break between levels 3 and 4. Software in Level 3 and below level mode privileges. Software from level 4 and above is user level. As such, there isn't a fundamental difference between a user-level programs, such as user-written programs and programs such as ssh, emacs, or even Bash. Both are software that interacts with the lower layers of the system, and both are subject to the same rules and limitations.

## Diagram

<figure><img src="../.gitbook/assets/image (1).png" alt="" width="375"><figcaption></figcaption></figure>



## Benefits of layering

1. Layering provides two useful features. First, it decomposes the problem of building a system into more manageable components. Rather than implementing a monolithic piece of software that does everything you will ever want, you can implement several layers, each of which solves one part of the problem.
2. Second, it provides a more modular design. If you decide that you want to add some new service, you may only need to modify the functionality at one layer, reusing the functions provided at all the other layers.
