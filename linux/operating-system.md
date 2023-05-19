# Operating System

Whether commands are issued via a GUI or a CLI, they are ultimately executed by the _Operating System_ (OS). The OS is perhaps the most important piece of software on the computer, acting like the "boss" of the computer, managing and coordinating all its activities.

Think of the operating system as a bridge between the computer's hardware (such as the processor, memory, and I/O devices) and the software applications (like web browsers, games, and word processors) that you use. Whenever applications want to utilize the hardware resources, they do so via the operating system, which ensures that these applications can effectively communicate with the hardware and utilize its resources efficiently.

The operating system performs several key tasks. It controls how programs are executed, manages the computer's memory to ensure that different programs don't interfere with each other, and handles input and output operations (like displaying information on the screen or printing documents).

Different operating systems exist, such as Windows, macOS, and Linux. Each has its own features and design, but they all serve the same purpose of making the computer usable and providing a platform for running applications.

## **Hardware**

&#x20;At the most fundamental level, a computer's hardware provides the raw computing resources, including the central processing unit (CPU), memory (RAM), storage devices (like SSDs or HDDs), and input/output devices (like the keyboard, mouse, and display). The CPU carries out the actual computations, RAM holds data that needs to be quickly accessed, and storage devices hold larger amounts of data for long-term storage. At this level, operations are performed in binary, directly manipulating electrical signals within the hardware.

## **Instruction Set Architecture (ISA)**

This is the interface between the hardware and the low-level software. It's a specification detailing the CPU's functions, including the specific binary codes it understands and how it processes them. ISAs can be complex (CISC - Complex Instruction Set Computer) like x86, or simplified (RISC - Reduced Instruction Set Computer) like ARM. At this layer, instructions are written in machine language and assembly code. This is the lowest level of code that is still readable by humans (with some training). Machine language is composed of binary instructions that directly control the CPU. Assembly is a thin layer on top of this, representing machine code instructions with human-readable labels.

## **Operating System (OS)**

The Operating System provides an interface between the hardware and user-level software, primarily through a feature known as the system call interface. This interface allows user-level applications to request services from the OS, which are typically related to input/output operations, process management, file management, and communication. It's through system calls that a program can access the processor, memory, and other system resources managed by the OS.

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

## **Libraries**

Programmers seldom interact directly with system calls. Instead, they use library functions, often referred to as "wrapper functions", that call the system calls for them. Libraries offer a multitude of benefits over direct system call use.

The key advantage is portability. System calls are specific to an operating system, meaning that a Linux system call interface differs from those on macOS or Windows. Library functions, in contrast, are typically platform-independent, making code using these libraries portable across different operating systems. Library APIs also offer improved efficiency, security, and ease of use.

## **Utility Programs**

The Linux operating system includes an array of pre-written utility programs. These programs, many of which are contributions from the GNU project, perform common tasks and help the system run efficiently.

These utilities provide essential services to users. Some notable utility programs include:

* `make`: Determines which source files need to be recompiled and/or linked.
* `ssh`: Allows users to log into a remote machine and execute commands.
* `grep`: Searches files for text matching a specified pattern.

To execute these utilities, you can enter their names along with any required parameters into the command line. If you want to combine utilities, you can use pipes (`|`) to direct the output of one command into another. For instance, you might use `grep` to search for a pattern in the output of another command, like this: `ls -l | grep ".txt"`. This will list all the .txt files in the current directory.

## **Libraries**

Building off the system call interface, libraries provide a higher-level programming interface to the services provided by the OS. A library is a collection of pre-compiled code that programs can use to perform common tasks. For instance, a standard C library (like glibc in GNU/Linux systems) provides a set of functions (like `printf`, `malloc`, etc.), which in turn use lower-level system calls to interact with the OS.

While a programmer could write a program using just system calls, this can be quite complex and error-prone. Libraries abstract away many of the details and provide a more convenient and efficient means to perform these tasks. They encapsulate system calls and other complex operations in more straightforward, high-level functions.

So, in a way, libraries provide an interface to the system call interface, abstracting the complexity of the system calls and making programming more accessible and efficient. By writing a program that uses library functions, a developer indirectly uses the services provided by the OS through the system call interface.

## **Core Utilities**

On top of the libc layer, a set of core utilities or commands are usually built to perform common system tasks, such as copying files (`cp`), listing directory contents (`ls`), or text processing (`grep`, `awk`). These utilities are standalone programs that can be invoked from the command lineThese are the basic tools that come with an OS, which provide a way to interact with the system and perform basic tasks. These can be command-line utilities like 'ls', 'cd', 'mkdir' in Unix-based systems, or GUI tools like Windows Explorer in Windows.

<figure><img src="../.gitbook/assets/image (1).png" alt="" width="375"><figcaption></figcaption></figure>

