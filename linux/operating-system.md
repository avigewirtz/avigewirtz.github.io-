# Operating System

Between the shell and the hardware lie multiple layers of software. Together, these layers provide the services that enable shell commands to be executed. Among these layers, the most important one to the application programmer is the Operating System (OS).

You can think of the operating system as the bridge between the computer's hardware (such as the processor, memory, and I/O devices) and the software applications. Whenever applications want to utilize the hardware resources, they do so via the operating system, which ensures that these applications can effectively communicate with the hardware and utilize its resources effectively.&#x20;

To better understand the role the OS plays in the computer system, it's helpful to take a step back and briefly discuss the layers below the OS. For our purposes, we will cover the hardware and ISA layers, beginning our exploration from the ground up and building up to the OS. Note that this coverage is highly simplified.

## **Hardware**

At the lowest level, there is the hardware, which provides the raw computing resources, including the central processing unit (CPU), memory (RAM), storage devices (like SSDs or HDDs), and input/output devices (such as the keyboard, mouse, and display unit). The CPU carries out the actual computations, RAM holds data that needs to be quickly accessed by the CPU, and the storage devices hold larger amounts of data for long-term storage. At this level, operations are performed in binary, directly manipulating the electrical or magnetic signals within the hardware. Working with computers at this level falls out of the realm of computer programming and into the realm of electrical engineering.

## **Instruction Set Architecture (ISA)**

Sitting above the hardware is the Instruction Set Architecture (ISA). The ISA abstracts the hardware implementation details by providing programmers with a set of software instructions that the CPU supports. In essence, it defines the machine language that the CPU can understand and process. From the programmer's perspective, the ISA is the lowest-level software interface to the computer. ISAs can be complex (CISC - Complex Instruction Set Computer) like x86, or simplified (RISC - Reduced Instruction Set Computer) like ARM.&#x20;

## **Operating System**

Above the ISA layer sits the OS layer. The motivation for introducing the OS layer is that while the ISA simplifies programming by hiding the low-level details of the hardware, it has limitations that can make certain tasks challenging to perform. For instance, the ISA does not include a standardized I/O interface. As I/O devices are often external and frequently manufactured by different companies, each comes with its unique low-level ISA interface, separate from the CPU’s ISA. The CPU’s ISA doesn't provide a standardized method for interacting with these I/O devices, thus requiring programmers to familiarize themselves with the specific low-level interface of each device.

Another limitation of the ISA is that it does not provide support for time-sharing, referring to the distribution of computational resources, such as memory and CPU, among multiple programs or users. Without inherent support for this feature, the ability to run multiple programs concurrently (a process known as multitasking) is limited.

The solution to these (and many other) limitations is to add another layer--the OS layer--that adds services on top of those supported by the ISA. Among other things, the OS layer includes support for time-sharing and provides a standardized interface for interacting with I/O devices.

Programs request services from the OS via the _system call_ interface. The services typically relate to input/output operations, process management, file management, and communication. It's through system calls that a program can access the processor, memory, and other system resources managed by the OS.

The study of operating systems is an advanced topic, so detailed coverage is beyond the scope of COS217. For now, it is sufficient to think of the OS as acting like the "boss" of the computer, managing and coordinating all its activities. It controls how programs are executed, manages the computer's memory to ensure that different programs don't interfere with each other, and handles input and output operations (like displaying information on the screen or printing documents). Different operating systems exist, such as Windows, macOS, and Linux. Each operating system has its own unique features and design, but they all share the common purpose of making the computer usable and providing a platform for applications to run.

## Libraries

Programmers rarely invoke system calls directly. Instead, they invoke them via library functions, often called "wrapper functions," that "wrap" the system calls with a higher programming interface. For instance, a standard C library (like _glibc_ in Linux/GNU systems) provides a set of functions (like `printf`, `malloc`, etc.). So, in a way, libraries provide an interface to the system call interface, abstracting the complexity of the system calls and making programming more accessible and efficient.&#x20;

While a programmer could write a program using just system calls, libraries offer many advantages. For example, one key advantage is portability. System calls are specific to an operating system, meaning that a Linux system call interface differs from those on macOS or Windows. Library functions, in contrast, are typically platform-independent, making code using these libraries portable across different operating systems. Library APIs also offer improved efficiency, security, and ease of use.

## **Core Utilities**

Core utilities, often referred to as "coreutils," are standalone programs that use these library functions to provide a standard set of features to programmers. The core utilities essentially act as a toolbox, providing programmers with ready-to-use tools for most of the basic tasks they might need to perform, such as file management and text processing.&#x20;

Utilities are usually packaged with the operating system and installed by default. However, they are generally not considered part of the operating system itself. The operating system's core is the kernel, which interacts directly with the hardware. Core utilities, on the other hand, operate at a higher level.

## Kernel Mode and User Mode

The computer system operates in different modes, called _kernel mode_ and _user mode_, which represent different states of the processor and govern the execution privileges of the code that's running. The OS kernel runs in kernel mode, while other programs, such as utilities and application programs, run in user mode. The division between the two modes is a crucial one.&#x20;

#### **Kernel Mode**

In kernel mode (also known as supervisor mode, system mode, or privileged mode), the executing code has full access to all hardware resources and all areas of memory. Kernel mode is typically reserved for low-level operations, such as managing I/O devices or manipulating the file system.

#### **User Mode**

In user mode, the executing code has restricted access to hardware resources and memory. Code running in user mode must request access to hardware or memory through a system call, which may be granted or denied by the kernel. Most application software runs in user mode to prevent a faulty or malicious program from interfering with the operation of the system as a whole. When a user mode program makes a system call, the system switches to kernel mode while the kernel code executes, and then switches back to user mode once the system call is complete.

It should be noted that all user-level programs, whether they're part of the OS distribution or written by users, operate under the same rules and limitations. For example, the system doesn't distinguish between a shell, an editor, a network service, or a user's own program when it comes to enforcing access controls and resource limits.
