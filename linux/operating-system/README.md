# Operating System

Between the shell and the hardware lie multiple layers of software. Together, these layers provide the services that enable shell commands to be executed. Among these layers, the one most pertinent to our discussion is the Operating System (OS). 

You can think of the operating system as the bridge between the computer's hardware (such as the processor, memory, and I/O devices) and the software applications. Whenever applications want to utilize the hardware resources, they do so via the operating system, which ensures that these applications can effectively communicate with the hardware and utilize its resources effectively.

When we issue commands to the shell, begind the scenes the shell communicates with the OS for us. 

To better understand the role rhe OS plays in the computer system, it's helpful to take a step back and briefly discuss the layers below the OS. We will we begin our exploration from the ground up, starting from the computer hardware and building ip to the OS. Note that this coverage is highly simplified.  

## **Hardware**

At the lowest level, there is the hardware, which provides the raw computing resources, including the central processing unit (CPU), memory (RAM), storage devices (like SSDs or HDDs), and input/output devices (such as the keyboard, mouse, and display unit). The CPU carries out the actual computations, RAM holds data that needs to be quickly accessed by the CPU, and the storage devices hold larger amounts of data for long-term storage. At this level, operations are performed in binary, directly manipulating the electrical or magnetic signals within the hardware. Working with computers at this level falls out of the realm of computer programming and into the realm of electrical engineering.

## **Instruction Set Architecture (ISA)**

Sitting above the hardware is the Instruction Set Architecture (ISA). This is typically the lowest level software interface to the hardware. The ISA abstracts the hardware implementation details by providing programmers with a predefined set of intructions that the computer supports. Programmers typically don't have a clue how the hardware inplements the We don't It's a specification detailing the CPU's functions, including the specific binary codes it understands and how it processes them. ISAs can be complex (CISC - Complex Instruction Set Computer) like x86, or simplified (RISC - Reduced Instruction Set Computer) like ARM. In essence, it defines the machine language that the CPU can understand and process. It is through this layer that programs can communicate with the hardware

## **Operating System (OS)**

The problem is that the ISA does not provide the full set of services that we need to efficiently use a computer. Also, the interface that is provides is extremely primitive, making it dificult t communicate with hardware.&#x20;

The solution is we design  a new layer of software, known as the OS, that adds a variety of new instructions and features, above and beyond what the ISA level provides. more convinient to use and offer more services.&#x20;

This level provides the complete set of instructions available to application programmers.&#x20;

The new instructions are called system calls. A system call invokes a predefined operating system service. This interface allows user-level applications to request services from the OS, which are typically related to input/output operations, process management, file management, and communication. It's through system calls that a program can access the processor, memory, and other system resources managed by the OS.&#x20;

You can think of the OS as acting like the "boss" of the computer, managing and coordinating all its activities.  It controls how programs are executed, manages the computer's memory to ensure that different programs don't interfere with each other, and handles input and output operations (like displaying information on the screen or printing documents). Different operating systems exist, such as Windows, macOS, and Linux. Each has its own features and design, but they all serve the same purpose of making the computer usable and providing a platform for running applications.

### **Kernel**

The kernel is the core of the operating system. Its functions can mostly be broken into two categories: Resource management. Hardware interface.
