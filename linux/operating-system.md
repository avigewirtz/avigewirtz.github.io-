# Operating System

Between the shell and the hardware lie multiple layers of software. Together, these layers provide the services that enable shell commands to be executed. Among these layers, the one most pertinent to our discussion is the Operating System (OS).

You can think of the operating system as the bridge between the computer's hardware (such as the processor, memory, and I/O devices) and the software applications. Whenever applications want to utilize the hardware resources, they do so via the operating system, which ensures that these applications can effectively communicate with the hardware and utilize its resources effectively.

When we issue commands to the shell, behind the scenes the shell communicates with the OS for us, requesting the neccessary services from the OS to complete the task. Having the shell as an intermediary to communicate with the OS for us makes programming exponentially easier, as interfacing with the OS directly is no simple feat.&#x20;

To better understand the role the OS plays in the computer system, it's helpful to take a step back and briefly discuss the layers below the OS--the hardware and ISA in particular. We will we begin our exploration from the ground up, starting from the computer hardware and building up to the OS. Note that this coverage is highly simplified.

## **Hardware**

At the lowest level, there is the hardware, which provides the raw computing resources, including the central processing unit (CPU), memory (RAM), storage devices (like SSDs or HDDs), and input/output devices (such as the keyboard, mouse, and display unit). The CPU carries out the actual computations, RAM holds data that needs to be quickly accessed by the CPU, and the storage devices hold larger amounts of data for long-term storage. At this level, operations are performed in binary, directly manipulating the electrical or magnetic signals within the hardware. Working with computers at this level falls out of the realm of computer programming and into the realm of electrical engineering.

## **Instruction Set Architecture (ISA)**

Sitting above the hardware is the Instruction Set Architecture (ISA). The ISA abstracts the hardware implementation details by providing programmers with the complete set of instructions that the CPU supports. In essence, it defines the machine language that the CPU can understand and process. From the programmer's perspective, the ISA is the lowest-level software interface to the computer. ISAs can be complex (CISC - Complex Instruction Set Computer) like x86, or simplified (RISC - Reduced Instruction Set Computer) like ARM.&#x20;

## **Operating System (OS)**

Above the ISA sits another layer--the OS layer. The problem with the ISA level is that the ISA does not provide the full set of services that we need to efficiently use a computer. Also, the interface that is provided is extremely primitive, making it difficult t communicate with the hardware.

The solution is we design a new layer of software, known as the OS, that adds a variety of new instructions and features, above and beyond what the ISA level provides. more convenient to use and offer more services.

This level provides the complete set of instructions available to application programmers.

The new instructions are called system calls. A system call invokes a predefined operating system service. This interface allows user-level applications to request services from the OS, which are typically related to input/output operations, process management, file management, and communication. It's through system calls that a program can access the processor, memory, and other system resources managed by the OS.

You can think of the OS as acting like the "boss" of the computer, managing and coordinating all its activities. It controls how programs are executed, manages the computer's memory to ensure that different programs don't interfere with each other, and handles input and output operations (like displaying information on the screen or printing documents). Different operating systems exist, such as Windows, macOS, and Linux. Each has its own features and design, but they all serve the same purpose of making the computer usable and providing a platform for running applications.

### **Kernel**

The kernel is the core of the operating system. Its functions can mostly be broken into two categories: Resource management. Hardware interface.











Programmers seldom interact with the OS via system calls directly. Instead, they use library functions, often referred to as "wrapper functions", that call the system calls for them. Libraries offer a multitude of benefits over direct system call use.

Llibraries provide a higher-level programming interface to the services provided by the OS. A library is a collection of pre-compiled code that programs can use to perform common tasks. For instance, a standard C library (like glibc in GNU/Linux systems) provides a set of functions (like `printf`, `malloc`, etc.), which in turn use lower-level system calls to interact with the OS.

While a programmer could write a program using just system calls, this can be quite complex and error-prone. Libraries abstract away many of the details and provide a more convenient and efficient means to perform these tasks. They encapsulate system calls and other complex operations in more straightforward, high-level functions.

So, in a way, libraries provide an interface to the system call interface, abstracting the complexity of the system calls and making programming more accessible and efficient. By writing a program that uses library functions, a developer indirectly uses the services provided by the OS through the system call interface.

The key advantage is portability. System calls are specific to an operating system, meaning that a Linux system call interface differs from those on macOS or Windows. Library functions, in contrast, are typically platform-independent, making code using these libraries portable across different operating systems. Library APIs also offer improved efficiency, security, and ease of use.

## **Core Utilities**
