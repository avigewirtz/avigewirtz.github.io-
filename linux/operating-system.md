# Operating System

It should come as no surprise that commands issued in the shell aren't directly executed by the hardware. This is because the shell doesn't communicate in the language that the hardware comprehends.

Between the hardware and the shell lie multiple layers of software, which together provide the services for the higher-level layers to function. Among these layers, the one most pertinent to our discussion is the Operating System (OS). The shell essentially provides a user interface to the OS services.

You can think of the operating system as a bridge between the computer's hardware (such as the processor, memory, and I/O devices) and the software applications (like web browsers, games, and word processors) that you use. Whenever applications want to utilize the hardware resources, they do so via the operating system, which ensures that these applications can effectively communicate with the hardware and utilize its resources efficiently.

Before we delve into the details of the OS, it's helpful to first understand where the OS resides within the system. To truly comprehend the role the OS plays in a computer system, it's best to start our exploration from the ground up

## **Hardware**

At the lowest level, there is the hardware, which provides the raw computing resources, including the central processing unit (CPU), memory (RAM), storage devices (like SSDs or HDDs), and input/output devices (like the keyboard, mouse, and display unit). The CPU carries out the actual computations, RAM holds data that needs to be quickly accessed, and storage devices hold larger amounts of data for long-term storage. At this level, operations are performed in binary, directly manipulating the electrical or magnetic signals within the hardware. Computer programmers do not work directly with hardware.

## **Instruction Set Architecture (ISA)**

Sitting above the hardware is the Instruction Set Architecture (ISA), which is the lowest level software interface. The ISA abstracts the hardware by providing a software interface. It's a specification detailing the CPU's functions, including the specific binary codes it understands and how it processes them. ISAs can be complex (CISC - Complex Instruction Set Computer) like x86, or simplified (RISC - Reduced Instruction Set Computer) like ARM. In essence, it defines the machine language that the CPU can understand and process. It is through this layer that programs can communicate with the hardware

## **Operating System (OS)**

The problem is that the ISA does not provide the full set of services that we need to efficiently use a computer. Also, the interface that is provides is extremely primitive, making it dificult t communicate with hardware.&#x20;

The solution is we design  a new layer of software, known as the OS, that adds a variety of new instructions and features, above and beyond what the ISA level provides. more convinient to use and offer more services.&#x20;

This level provides the complete set of instructions available to application programmers.&#x20;

The new instructions are called system calls. A system call invokes a predefined operating system service. This interface allows user-level applications to request services from the OS, which are typically related to input/output operations, process management, file management, and communication. It's through system calls that a program can access the processor, memory, and other system resources managed by the OS.&#x20;

You can think of the OS as acting like the "boss" of the computer, managing and coordinating all its activities.  It controls how programs are executed, manages the computer's memory to ensure that different programs don't interfere with each other, and handles input and output operations (like displaying information on the screen or printing documents). Different operating systems exist, such as Windows, macOS, and Linux. Each has its own features and design, but they all serve the same purpose of making the computer usable and providing a platform for running applications.

### **Kernel**

The kernel is the core of the operating system. Its functions can mostly be broken into two categories: Resource management. Hardware interface.
