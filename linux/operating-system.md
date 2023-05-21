# Operating System

When a command is executed in a terminal, ultimately leads to the command being executed by the computer hardware.

getting from the shell to the hardware is no small feat. It is actaully the culmination of many complex processes involving several layers of abstraction within the computer system.&#x20;

The most important layer, for our purposes, is the operating system (OS) layer. To understand the role of the OS is the computer system, we will diverge slightly&#x20;

But let's take a step back to look at these layers, starting from the bottom up, and see how they interact with each other to make the command execution possible.

The general idea is that you start with the services offered by the underlying hardware and then add a sequence of layers, each providing a higher (more abstract) level of service, until you reach the highest layer--the computer user. Each service is implemented in terms of the services provided by the layers below.

## **Hardware**

At the lowest level, there is the hardware, which provides the raw computing resources, including the central processing unit (CPU), memory (RAM), storage devices (like SSDs or HDDs), and input/output devices (like the keyboard, mouse, and display unit). The CPU carries out the actual computations, RAM holds data that needs to be quickly accessed, and storage devices hold larger amounts of data for long-term storage. At this level, operations are performed in binary, directly manipulating the electrical or magnetic signals within the hardware. Computer programmers do not work directly with hardware.&#x20;

## **Instruction Set Architecture (ISA)**

Sitting above the hardware is the Instruction Set Architecture (ISA), which is the lowest level software interface. The ISA abstracts the hardware by providing a software interface. It's a specification detailing the CPU's functions, including the specific binary codes it understands and how it processes them. ISAs can be complex (CISC - Complex Instruction Set Computer) like x86, or simplified (RISC - Reduced Instruction Set Computer) like ARM. In essence, it defines the machine language that the CPU can understand and process. It is through this layer that programs can communicate with the hardware

## **Operating System (OS)**

As mentioned above, there is a large gap between what is convenient for peo- ple and what is convenient for computers. People want to do X, but computers can only do Y. This leads to a problem. The goal of this book is to explain how this problem can be solved.


The problem can be attacked in two ways: both involve designing a new set of instructions that is more convenient for people to use than the set of built-in ma- chine instructions.


As mentioned above, there is a large gap between what is convenient for peo- ple and what is convenient for computers. People want to do X, but computers can only do Y. This leads to a problem. The goal of this book is to explain how this problem can be solved.



The services provided by the ISA are not ideal to work with. Don't provide enough services. Hard to work with.&#x20;

An operating system is a program that, from the programmer’s point of view, adds a variety of new instructions and features, above and beyond what the ISA level provides.

The solution is that we add a new layer that essentially adds more instructions and services. Of course,&#x20;

This level provides the complete set of instructions available to application programmers. The new instructions are called system calls. A system call invokes a predefined operating system service. A typical system call might be to read some data from a file or to…

This interface allows user-level applications to request services from the OS, which are typically related to input/output operations, process management, file management, and communication. It's through system calls that a program can access the processor, memory, and other system resources managed by the OS.

The OS has two definitions. The narrow definition. Just kernel. Loose defintion. kernel + ...

We will now focus on the kernel, since even by the loose definition, the kernel is the core of the OS.

### **Kernel**



The OS is perhaps the most important piece of software on the computer, acting like the "boss" of the computer, managing and coordinating all its activities.

Think of the operating system as a bridge between the computer's hardware (such as the processor, memory, and I/O devices) and the software applications (like web browsers, games, and word processors) that you use. Whenever applications want to utilize the hardware resources, they do so via the operating system, which ensures that these applications can effectively communicate with the hardware and utilize its resources efficiently.

The operating system performs several key tasks. It controls how programs are executed, manages the computer's memory to ensure that different programs don't interfere with each other, and handles input and output operations (like displaying information on the screen or printing documents).

Different operating systems exist, such as Windows, macOS, and Linux. Each has its own features and design, but they all serve the same purpose of making the computer usable and providing a platform for running applications.

The kernel is the core of the operating system. Its functions can mostly be broken into two categories: Resource management. Hardware interface.&#x20;

#### **Resource Management**

time-sharing. Does this by managing the hardware resources like memory, CPU, and peripherals. The Operating System provides an interface between the hardware and user-level software, primarily through a feature known as the system call interface.&#x20;

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



## Notes

1. While these layers provide a simplified view of how commands are issued and executed, it's important to note thinking of a system as a linear sequence of layers is an oversimplification. Many times there are multiple abstractions provided at any given level of the system. Additionally, the division between the layers isn't always clear-cut. For instance, user programs can interact directly with the kernel via system calls without using C library functions or utilities.
2. This system is a simplification. In reality there are more layers.
3. There is a fundamental break between levels 3 and 4. Software in Level 3 and below level mode privileges. Software from level 4 and above is user level. As such, there isn't a fundamental difference between a user-level programs, such as user-written programs and programs such as ssh, emacs, or even Bash. Both are software that interacts with the lower layers of the system, and both are subject to the same rules and limitations.

## Diagram

<figure><img src="../.gitbook/assets/image (1).png" alt="" width="375"><figcaption></figcaption></figure>

## Benefits of layering

1. Layering provides two useful features. First, it decomposes the problem of building a system into more manageable components. Rather than implementing a monolithic piece of software that does everything you will ever want, you can implement several layers, each of which solves one part of the problem.
2. Second, it provides a more modular design. If you decide that you want to add some new service, you may only need to modify the functionality at one layer, reusing the functions provided at all the other layers.



