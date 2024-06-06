# Understanding the CLI

Three parts under the hood

## The shell







General outline:

* explain what terminal emulators are. emulate&#x20;



* back in the day, people interacted with computers primarily through terminals. Terminal is a hardware device consisting of a keyboard and display unit. first terminals were teletype writers, whose display unit was a paper roll printer. as computing modernized, teletypes were replaced video display terminals. basic mode of operation was the same, however.&#x20;

When the system prints the prompt and you type commands that get executed, it's not the kernel that is talking to you, but a go-between program called _the shell_. It's job is to interpret and execute the commands you type in the terminal. The shell is a command interpreter that provides a command-line interface to the system. The shell operates in a simple loop (Figure 2). Here's how it works:

1.  The shell displays a prompt, which is its way of saying "hey user, I'm ready to accept a command". On Armlab, the shell prompt looks like the following:&#x20;

    <figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 3.08.46 PM.png" alt=""><figcaption></figcaption></figure>
2. After the user enters a command and presses RETURN, the shell interprets the command, figuring out what exactly the user is asking it to do.&#x20;
3. After the shell finishes parsing the command line, it executes the command. It does this by invoking the proper system calls to execute the command.&#x20;
4. Prompts the user for another command, repeating steps 1-3.

<figure><img src="../.gitbook/assets/Group 12 (3).png" alt="" width="188"><figcaption><p>Figure 2.</p></figcaption></figure>

{% hint style="info" %}
The shell can also accept commands from a file. Such files typically have .sh suffix and are referred to as shell scripts.&#x20;
{% endhint %}

Job of the shell is to interpret users commands. Called command language interpreter. Kind of like an interpreter like Python, except that the expectation.&#x20;

## The Kernel

The term operating system is commonly used with two different meanings:

* To denote the entire package consisting of the central software managing a computer’s resources and all of the accompanying standard software tools, such as command-line interpreters, graphical user interfaces, file utilities, and editors.
* More narrowly, to refer to the central software that manages and allocates computer resources (i.e., the CPU, RAM, and devices).

The term kernel is often used as a synonym for the second meaning, and it is withhis meaning of the term operating system that we are concerned in this book.Although it is possible to run programs on a computer without a kernel, the presence of a kernel greatly simplifies the writing and use of other programs, and increases the power and flexibility available to programmers. The kernel does this by providing a software layer to manage the limited resources of a computer.

First program that runs when you turn on your computer. You can think of the kernel as the bridge between the computer's hardware (such as the processor, memory, and I/O devices) and the software applications. Whenever applications want to utilize the hardware resources, they do so via the operating system, which ensures that these applications can effectively communicate with the hardware and utilize its resources effectively.&#x20;



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

{% hint style="info" %}
## Libraries

Programmers rarely invoke system calls directly. Instead, they invoke them via library functions, often called "wrapper functions," that "wrap" the system calls with a higher programming interface. For instance, a standard C library (like _glibc_ in Linux/GNU systems) provides a set of functions (like `printf`, `malloc`, etc.). So, in a way, libraries provide an interface to the system call interface.
{% endhint %}

## The utility programs

Core utilities, often referred to as "coreutils," are standalone programs that use these library functions to provide a standard set of features to programmers. The core utilities essentially act as a toolbox, providing programmers with ready-to-use tools for most of the basic tasks they might need to perform, such as file management and text processing.&#x20;

Utilities are usually packaged with the operating system and installed by default. However, they are generally not considered part of the operating system itself. The operating system's core is the kernel, which interacts directly with the hardware. Core utilities, on the other hand, operate at a higher level.

## The shell

When the system prints the prompt and you type commands that get executed, it's not the kernel that is talking to you, but a go-between program called _the shell_. It's job is to interpret and execute the commands you type in the terminal. The shell is a command interpreter that provides a command-line interface to the system. The shell operates in a simple loop (Figure 2). Here's how it works:

1.  The shell displays a prompt, which is its way of saying "hey user, I'm ready to accept a command". On Armlab, the shell prompt looks like the following:&#x20;

    <figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 3.08.46 PM.png" alt=""><figcaption></figcaption></figure>
2. After the user enters a command and presses RETURN, the shell interprets the command, figuring out what exactly the user is asking it to do.&#x20;
3. After the shell finishes parsing the command line, it executes the command. It does this by invoking the proper system calls to execute the command.&#x20;
4. Prompts the user for another command, repeating steps 1-3.

<figure><img src="../.gitbook/assets/Group 12 (3).png" alt="" width="188"><figcaption><p>Figure 2.</p></figcaption></figure>

{% hint style="info" %}
The shell can also accept commands from a file. Such files typically have .sh suffix and are referred to as shell scripts.&#x20;
{% endhint %}

Job of the shell is to interpret users commands. Called command language interpreter. Kind of like an interpreter like Python, except that the expectation.&#x20;





## What's a command?

A command is a directive to the shell to perform a specific task.&#x20;



Bash, along with most other unix-shells, offer many convenient features beyond launching programs and providing builtins.&#x20;

&#x20;For example, they remember commands that you’ve typed, and let you reuse those commands. Modern shells also let you edit those commands, so they don’t have to be the same each time. And modern shells let you define your own command abbreviations, shortcuts, and other features. For an experienced user, typing commands (e.g., with shorthand, shortcuts, and command completion) is a lot more efficient and effective than dragging things around in a fancy windowed interface.

### Putting it all together

<figure><img src="../.gitbook/assets/Group 8 (1).png" alt="" width="375"><figcaption></figcaption></figure>

#### Example of a sequence of interactions&#x20;

1.
