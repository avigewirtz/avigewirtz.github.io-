# Linux kernel

The term operating system is commonly used with two different meanings:

* To denote the entire package consisting of the central software managing a computer’s resources and all of the accompanying standard software tools, such as command-line interpreters, graphical user interfaces, file utilities, and editors.
* More narrowly, to refer to the central software that manages and allocates computer resources (i.e., the CPU, RAM, and devices).

The term kernel is often used as a synonym for the second meaning, and it is withhis meaning of the term operating system that we are concerned in this book.Although it is possible to run programs on a computer without a kernel, the presence of a kernel greatly simplifies the writing and use of other programs, and increases the power and flexibility available to programmers. The kernel does this by providing a software layer to manage the limited resources of a computer.

#### Tasks performed by the kernel

Among other things, the kernel performs the following tasks:

* 􏰀  Process scheduling: A computer has one or more central processing units (CPUs), which execute the instructions of programs. Like other UNIX systems, Linux is a preemptive multitasking operating system, Multitasking means that multiple processes (i.e., running programs) can simultaneously reside in mem- ory and each may receive use of the CPU(s). Preemptive means that the rules governing which processes receive use of the CPU and for how long are deter- mined by the kernel process scheduler (rather than by the processes them- selves).
* 􏰀  Memory management: While computer memories are enormous by the stan- dards of a decade or two ago, the size of software has also correspondingly grown, so that physical memory (RAM) remains a limited resource that the ker- nel must share among processes in an equitable and efficient fashion. Like most modern operating systems, Linux employs virtual memory management (Section 6.4), a technique that confers two main advantages:
  * –  Processes are isolated from one another and from the kernel, so that one process can’t read or modify the memory of another process or the kernel.
  * –  Only part of a process needs to be kept in memory, thereby lowering the memory requirements of each process and allowing more processes to be held in RAM simultaneously. This leads to better CPU utilization, since it increases the likelihood that, at any moment in time, there is at least one process that the CPU(s) can execute.
* 􏰀  Provision of a file system: The kernel provides a file system on disk, allowing files to be created, retrieved, updated, deleted, and so on.
* 􏰀  Creation and termination of processes: The kernel can load a new program into memory, providing it with the resources (e.g., CPU, memory, and access to files) that it needs in order to run. Such an instance of a running program is termed a process. Once a process has completed execution, the kernel ensures that the resources it uses are freed for subsequent reuse by later programs.
* 􏰀  Access to devices: The devices (mice, monitors, keyboards, disk and tape drives, and so on) attached to a computer allow communication of information between the computer and the outside world, permitting input, output, or both. The kernel provides programs with an interface that standardizes and simplifies access to devices, while at the same time arbitrating access by multiple processes to each device.
* 􏰀  Networking: The kernel transmits and receives network messages (packets) on behalf of user processes. This task includes routing of network packets to the target system.
*   􏰀  Provision of a system call application programming interface (API): Processes can request the kernel to perform various tasks using kernel entry points known as system calls. The Linux system call API is the primary topic of this book. Section 3.1 details the steps that occur when a process performs a system call.

    In addition to the above features, multiuser operating systems such as Linux gener- ally provide users with the abstraction of a virtual private computer; that is, each user can log on to the system and operate largely independently of other users. For example, each user has their own disk storage space (home directory). In addition, users can run programs, each of which gets a share of the CPU and operates in its own virtual address space, and these programs can independently access devices and transfer information over the network. The kernel resolves potential conflicts in accessing hardware resources, so users and processes are generally unaware of the conflicts.

Like all things programing, the term "operating system" isn't well defined. There's two meanings in common usage:

* Narrow definition: A piece of software that controls the interaction between programs and hardware (CPU, memory, storage, peripherals). Also called a “kernel”.&#x20;
* Looser definition: The kernel plus a variety of libraries and tools built upon it, that provide a specific experience to users (e.g., GUI).&#x20;

By far, the narrow definition is far more common definition in academia, so if you hear someone say operating system, you can assume they probably mean the kernel.&#x20;

Linux is the kernel; The other components are&#x20;

You can think of the kernel as the bridge between the computer's hardware (such as the processor, memory, and I/O devices) and the software applications. Whenever applications want to utilize the hardware resources, they do so via the operating system, which ensures that these applications can effectively communicate with the hardware and utilize its resources effectively.&#x20;

Tasks performed by Linux kernel:

* Interface to hardware. Evrything is done through os. can be thought of as assistant
* Multitasking - abstraction of each program computer to itself. thought of as manager that ensures processes don't interfere with each other.&#x20;
* Provides a file system, abstracted view of computer storage
* multiuser - abstraction of each user having computer to itself. file permissions, ensures security.
* Interface to I/O devices

{% hint style="info" %}
## Libraries

Programmers rarely invoke system calls directly. Instead, they invoke them via library functions, often called "wrapper functions," that "wrap" the system calls with a higher programming interface. For instance, a standard C library (like _glibc_ in Linux/GNU systems) provides a set of functions (like `printf`, `malloc`, etc.). So, in a way, libraries provide an interface to the system call interface.
{% endhint %}

