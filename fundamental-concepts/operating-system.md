# Operating System

Between the shell and the hardware lie multiple layers of software. Together, these layers provide the services that enable shell commands to be executed. Among these layers, the most important one to the application programmer is the Operating System (OS).

You can think of the operating system as the bridge between the computer's hardware (such as the processor, memory, and I/O devices) and the software applications. Whenever applications want to utilize the hardware resources, they do so via the operating system, which ensures that these applications can effectively communicate with the hardware and utilize its resources effectively.&#x20;

To better understand the role the OS plays in the computer system, it's helpful to take a step back and briefly discuss the layers below the OS. For our purposes, we will cover the hardware and ISA layers, beginning our exploration from the ground up and building up to the OS. Note that this coverage is highly simplified.



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
