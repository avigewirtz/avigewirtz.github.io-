# Operating System

Whether commands are issued via a GUI or a CLI, they are ultimately executed by the _Operating System_ (OS). The OS is perhaps the most important piece of software on the computer, acting like the "boss" of the computer, managing and coordinating all its activities.

Think of the operating system as a bridge between the computer's hardware (such as the processor, memory, and I/O devices) and the software applications (like web browsers, games, and word processors) that you use. Whenever applications want to utilize the hardware resources, they do so via the operating system, which ensures that these applications can effectively communicate with the hardware and utilize its resources efficiently.

The operating system performs several key tasks. It controls how programs are executed, manages the computer's memory to ensure that different programs don't interfere with each other, and handles input and output operations (like displaying information on the screen or printing documents).

Different operating systems exist, such as Windows, macOS, and Linux. Each has its own features and design, but they all serve the same purpose of making the computer usable and providing a platform for running applications.





## Starting from the bottom up



## **Hardware**

&#x20;At the most fundamental level, a computer's hardware provides the raw computing resources, including the central processing unit (CPU), memory (RAM), storage devices (like SSDs or HDDs), and input/output devices (like the keyboard, mouse, and display). The CPU carries out the actual computations, RAM holds data that needs to be quickly accessed, and storage devices hold larger amounts of data for long-term storage. At this level, operations are performed in binary, directly manipulating electrical signals within the hardware.

## **Instruction Set Architecture (ISA)**

This is the interface between the hardware and the low-level software. It's a specification detailing the CPU's functions, including the specific binary codes it understands and how it processes them. ISAs can be complex (CISC - Complex Instruction Set Computer) like x86, or simplified (RISC - Reduced Instruction Set Computer) like ARM. At this layer, instructions are written in machine language and assembly code. This is the lowest level of code that is still readable by humans (with some training). Machine language is composed of binary instructions that directly control the CPU. Assembly is a thin layer on top of this, representing machine code instructions with human-readable labels.

## **Operating System (OS)**

The Operating System provides an interface between the hardware and user-level software, primarily through a feature known as the system call interface. This interface allows user-level applications to request services from the OS, which are typically related to input/output operations, process management, file management, and communication. It's through system calls that a program can access the processor, memory, and other system resources managed by the OS.

## **Libraries**

Building off the system call interface, libraries provide a higher-level programming interface to the services provided by the OS. A library is a collection of pre-compiled code that programs can use to perform common tasks. For instance, a standard C library (like glibc in GNU/Linux systems) provides a set of functions (like `printf`, `malloc`, etc.), which in turn use lower-level system calls to interact with the OS.

While a programmer could write a program using just system calls, this can be quite complex and error-prone. Libraries abstract away many of the details and provide a more convenient and efficient means to perform these tasks. They encapsulate system calls and other complex operations in more straightforward, high-level functions.

So, in a way, libraries provide an interface to the system call interface, abstracting the complexity of the system calls and making programming more accessible and efficient. By writing a program that uses library functions, a developer indirectly uses the services provided by the OS through the system call interface.

## **Core Utilities**

On top of the libc layer, a set of core utilities or commands are usually built to perform common system tasks, such as copying files (`cp`), listing directory contents (`ls`), or text processing (`grep`, `awk`). These utilities are standalone programs that can be invoked from the command lineThese are the basic tools that come with an OS, which provide a way to interact with the system and perform basic tasks. These can be command-line utilities like 'ls', 'cd', 'mkdir' in Unix-based systems, or GUI tools like Windows Explorer in Windows.

<figure><img src="../.gitbook/assets/image (16).png" alt="" width="375"><figcaption></figcaption></figure>





