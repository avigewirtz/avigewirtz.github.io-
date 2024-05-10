# Introduction

When Linus Torvalds introduced Linux and for a long time thereafter, Linux did not have a graphical user interface (GUI): It ran on character-based terminals only, using a command-line interface (CLI), also referred to as a textual interface. All the tools ran from a command line. Today the Linux GUI is important, but many people— especially system administrators—run many command-line utilities. Command-line utilities are often faster, more powerful, or more complete than their GUI counter- parts. Sometimes there is no GUI counterpart to a textual utility; some people just prefer the hands-on feeling of the command line.

When you work with a command-line interface, you are working with a shell (Chapters 5, 8, and 10). Before you start working with a shell, it is important that you understand something about the characters that are special to the shell, so this chapter starts with a discussion of special characters. The chapter then describes five basic utilities: ls, cat, rm, less, and hostname. It continues by describing several other file manipulation utilities as well as utilities that compress and decompress files, pack and unpack archive files, locate utilities, display system information, communicate with other users, and print files.





Before the introduction of the graphical user interface, UNIX and then Linux pro- vided only a textual (command-line) interface. Today, a textual interface is available when you log in from a terminal, a terminal emulator, or a textual virtual console, or when you use ssh or telnet to log in on a system.

Although the concept might seem antiquated, the textual interface has a place in modern computing. In some cases an administrator might use a command-line tool either because a graphical equivalent does not exist or because the graphical tool is not as powerful or flexible as the textual one. For example, chmod (pages 102 and 759) is more powerful and flexible than its GUI counterpart. Frequently, on a server system, a graphical interface might not even be installed. The first reason for this omission is that a GUI consumes a lot of system resources; on a server, those resources are better dedicated to the main task of the server. Additionally, security considerations mandate that a server system run as few tasks as possible because each additional task can make the system more vulnerable to attack.

You can also write scripts using the textual interface. Using scripts, you can easily reproduce tasks on multiple systems, enabling you to scale the tasks to larger environ- ments. When you are the administrator of only a single system, using a GUI is often the easiest way to configure the system. When you act as administrator for many sys- tems, all of which need the same configuration installed or updated, a script can make the task go more quickly. Writing a script using command-line tools is frequently easy, whereas the same task can be difficult to impossible using graphical tools.

Before the introduction of GUIs, resourceful programmers created textual interfaces that included graphical elements such as boxes, borders outlining rudimentary win- dows, highlights, and, more recently, color. These textual interfaces, called pseudographical interfaces, bridge the gap between textual and graphical interfaces. The Midnight Commander file management utility (mc; page 902) is a good example of a utility with a well-designed pseudographical interface.



Before icons and windows took over computer screens, you typed commands to run most computers. On UNIX systems, from which Linux was derived, the progra



{% hint style="info" %}
What's an Operating System?



The term operating system is commonly used with two different meanings:

* To denote the entire package consisting of the central software managing a computer’s resources and all of the accompanying standard software tools, such as command-line interpreters, graphical user interfaces, file utilities, and editors.
* More narrowly, to refer to the central software that manages and allocates computer resources (i.e., the CPU, RAM, and devices).

The term kernel is often used as a synonym for the second meaning, and it is withhis meaning of the term operating system that we are concerned in this book.Although it is possible to run programs on a computer without a kernel, the presence of a kernel greatly simplifies the writing and use of other programs, and increases the power and flexibility available to programmers. The kernel does this by providing a software layer to manage the limited resources of a computer.

You can think of the kernel as the bridge between the computer's hardware (such as the processor, memory, and I/O devices) and the software applications. Whenever applications want to utilize the hardware resources, they do so via the operating system, which ensures that these applications can effectively communicate with the hardware and utilize its resources effectively.&#x20;



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
{% endhint %}



#### Outline of this chapter





The command-line interface (CLI) is a text-based method of interacting with your computer. Unlike the graphical user interfaces (GUIs) that allow you to issue commands by clicking buttons and icons, a CLI requires you to issue commands by typing typing sequences of text in a [terminal](broken-reference).&#x20;

Imagine using a CLI as if you're texting with your computer: you type in your request, and it responds  with text output. Let's consider a couple of examples of computer interaction to highlight the distinction between a GUI and CLI.&#x20;

In this chapter, will focus on command line interface to Linux.

{% hint style="info" %}
Given the much steeper learning curve of the CLI compared to the GUI, you might wonder why anyone uses the CLI over a GUI. Here's a few reasons:

* **Speed:** Once you're familiar with commands, the CLI can be much faster than using a mouse.
* **Automation:** The CLI makes it easy to automate repetitive tasks.
* **Remote Access:** Remote computer interaction is much more efficient in a CLI environment.&#x20;
* **Necessity:** Some CLI commands have no GUI equivalent.
{% endhint %}

## Terminal

CLI commands are issued via a _terminal_. In the nascent days of interactive computing, terminals were hardware devices, consisting of a keyboard and a display unit. The first terminals were teletype machines, such as the Model 33 ASR shown in Figure 1, whose display unit was a paper-roll printer.

<figure><img src="../.gitbook/assets/560px-Teletype-IMG_7287.jpg" alt="" width="280"><figcaption><p>Figure 1: Teletype Model 33 ASR</p></figcaption></figure>

Teletypes fell out of use in the 1970s with the advent of video display terminals, such as the DEC VT100 shown in Figure 2, which provided instant user-feedback and editing capabilities.&#x20;

<figure><img src="../.gitbook/assets/1200px-DEC_VT100_terminal_transparent.png" alt="" width="375"><figcaption></figcaption></figure>

Today, hardware terminals are largely obsolete. The predominant method for accessing the CLI is through a _terminal emulator_, which is a GUI program that simulates the functionality of a hardware terminal. An example of a terminal emulator is macOS's Terminal, shown in Figure 3.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-05-19 at 5.46.26 PM.png" alt="" width="375"><figcaption><p>Figure 3: macOS Terminal Application</p></figcaption></figure>



## Shell





## What's a command?
