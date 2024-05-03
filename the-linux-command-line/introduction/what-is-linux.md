# What is Linux?

## Operating System

Like all things programing, the term "operating system" isn't well defined. There's two definitions in common usage:

Narrow definition: A piece of software that controls the interaction between programs and hardware (CPU, memory, storage, peripherals). Also called a “kernel”. Modern Kernel Examples: Unix lineage: Linux, XNU • VMS lineage: Windows NT

Looser definition: The kernel plus a variety of libraries and tools built upon it, that provide a specific experience to users (e.g., GUI). Modern OS Examples. Linux/GNU, Android. macOS, iOS, and Windows

You can think of the operating system as the bridge between the computer's hardware (such as the processor, memory, and I/O devices) and the software applications. Whenever applications want to utilize the hardware resources, they do so via the operating system, which ensures that these applications can effectively communicate with the hardware and utilize its resources effectively.&#x20;

The study of operating systems is an advanced topic, so detailed coverage is beyond the scope of COS217. For now, it is sufficient to think of the OS as acting like the "boss" of the computer, managing and coordinating all its activities. It controls how programs are executed, manages the computer's memory to ensure that different programs don't interfere with each other, and handles input and output operations (like displaying information on the screen or printing documents). Different operating systems exist, such as Windows, macOS, and Linux. Each operating system has its own unique features and design, but they all share the common purpose of making the computer usable and providing a platform for applications to run.

{% hint style="info" %}
## Libraries

Programmers rarely invoke system calls directly. Instead, they invoke them via library functions, often called "wrapper functions," that "wrap" the system calls with a higher programming interface. For instance, a standard C library (like _glibc_ in Linux/GNU systems) provides a set of functions (like `printf`, `malloc`, etc.). So, in a way, libraries provide an interface to the system call interface, abstracting the complexity of the system calls and making programming more accessible and efficient.&#x20;

While a programmer could write a program using just system calls, libraries offer many advantages. For example, one key advantage is portability. System calls are specific to an operating system, meaning that a Linux system call interface differs from those on macOS or Windows. Library functions, in contrast, are typically platform-independent, making code using these libraries portable across different operating systems. Library APIs also offer improved efficiency, security, and ease of use.
{% endhint %}
