# Operating Systems

The shell is a program that provides a user-friendly interface to the operating system. Before elaborating on this, let’s ensure we understand what an operating system is.&#x20;

Operating system

An operating system has two main parts: the kernel and the system programs.

Kernel

The kernel is the heart of the operating system. It is a layer of software that lies between the hardware and (most) other software. The kernel serves two primary functions: (1) it manages computer hardware resources; (2) it provides programs with a clean interface to these resources.&#x20;

\


To better understand the necessity of these two kernel functions, it is helpful to first understand the challenges they exist to solve. Let’s first discuss the kernel’s role as the manager of hardware resources.&#x20;

\


Linux is a multiuser and multitasking operating system. This means that a Linux system can support many users, all of whom may log in simultaneously. Additionally, each of them may run many programs concurrently. This holds true even if the computer has only one CPU.&#x20;

\


Enabling many users and programs to share the same hardware resources poses many challenges. Here are just a few:

* How do we ensure executing programs are each kept in separate regions of memory?&#x20;
* How do we ensure that each user’s personal files can’t be accessed by unauthorized users?&#x20;
* How do we ensure that executing programs don’t utilize an I/O device—such as a printer, speakers, or keyboard—at the same time, producing incomprehensible output?&#x20;

\


As you can imagine, resolving such challenges requires a large and sophisticated piece of software. That software is the kernel. It manages hardware resources, allocating memory, disk space, CPU cycles, and so on, to all programs that run on the computer. The kernel also dictates which files each user has access to and controls interprocess communication.&#x20;

\


The details are complex and well beyond the scope of COS217. If you take COS318, you’ll learn all the glorious details. For now it is sufficient to have a vague understanding and simply recognize that the kernel enables computers to be multiuser and multitasking.&#x20;

\


Let’s now turn to the kernel’s role of providing an interface to the hardware resources.&#x20;

\


Programs must communicate with the CPU as well as a wide variety of peripheral devices, such as mice, keyboards, hard drives, touchpads, cameras, microphones, speakers, network modems, and so on. This too poses many challenges. Here are a few examples:&#x20;

* To communicate directly with a specific hardware device, a programmer would need an in-depth understanding of its low-level, machine language interface. Acquiring this knowledge would require the programmer to read a several hundred page manual. How do we make the process less tedious and less time-consuming?&#x20;
* New peripheral devices constantly enter the market. Many of them are manufactured after programs are written. How do we ensure programs need not be changed every time a new peripheral device is added to the system?&#x20;

\


The Linux kernel solves these challenges by abstracting away the complexities of the hardware devices' low-level interfaces and instead providing programmers with a simpler and cleaner interface that is much easier to program with. This interface is called the system call interface.

\


System calls

\


System calls define the programmer's interface to the kernel. When an executing program needs a service from the kernel, it requests it by invoking a system call. Linux has several hundred system calls, each tailored for a different purpose. For example, some system calls are used to interact with I/O devices, while others are used to control executing programs. System calls are mostly written in C.&#x20;

\


The major categories of system calls include process control, file management, device management, and information maintenance.&#x20;

\


The device management system call interface  is extremely important and sufficiently simple that it’s worth briefly discussing.&#x20;

\


Device management&#x20;

\


Each peripheral device has an associated file, called a device file, in the filesystem that models the device and serves as the programmer’s interface to the device. When a programmer wants to obtain input or send output to the device, they do so through its device file.&#x20;

\


The interface to device files is identical to the interface of ordinary files. Thus, programmers interact with them in the same manner they interact with ordinary files. For example, to obtain input from the keyboard, a program reads from the keyboard's device file. Similarly, to display output on the screen, the program writes to the monitor’s device file.

\


| int | <p>creat(char *pathname, mode_t mode)</p><p>Creates the file pathname and assigns it a file descriptor. </p>     |
| --- | ---------------------------------------------------------------------------------------------------------------- |
| int | <p>open(char *pathname, int flags, mode_t mode)</p><p>Opens the file pathname and returns a file descriptor.</p> |
| int | <p>close(int fd)</p><p>Closes the file descriptor fd. </p>                                                       |
| int | <p>read(int fd, void *buf, int count)</p><p>Reads up to count bytes into fd, from the buffer at buf. </p>        |
| int | <p>write(int fd, void *buf, int count)</p><p>Writes up to count bytes into fd, from the buffer at buf. </p>      |



This abstraction greatly simplifies I/O, since all devices use a subset of the same file interface. interfaces are the same. Thus, a programmer needs to only know one API that they can use for all hardware devices. This is much easier than studying device-specific interfaces. This flexibility also allows old utilities to work with devices that did not exist when the utilities were written.

\


System programs&#x20;

The system programs include device drivers, libraries, utility programs, shells (command interpreters), configuration scripts and files, application programs, servers, and documentation. They perform higher-level housekeeping tasks, often acting as servers in a client/server relationship. For Linux and macOS, many of the libraries, servers, and utility programs were written by the GNU Project, which is discussed shortly.

Wrapper functions

In practice, programmers rarely invoke system calls directly. Instead, they invoke library functions, called wrapper functions, that invoke the system calls on their behalf. Library APIs provide several benefits over system calls and are therefore the favored choice.&#x20;

\


The first is portability. System calls are operating system specific; that is, the system call interface on Linux is different from the one on macOS and Windows. Library functions, however, are platform independent; that is, Linux, macOS, and Windows generally share the same library APIs. Thus, the code is portable. Library APIs also provide efficiency, security, and are easier to use.&#x20;

\


Utility programs

\


The Linux operating system comes with many pre-written programs, called utility programs, that perform common tasks and enable the system to run smoothly and efficiently. Most Linux utility programs were written by the GNU project.&#x20;

\


Utility programs save programmers a lot of time; for example, if a programmer wants to display the content of a file on the screen, they need not write a program like the one in Figure 4; instead, they can invoke the cat utility, which is almost certainly far superior to&#x20;

\
Figure 1: Program to display the contents of a file on standard output

\
\
\
\


These programs provide common and necessary services to users. Here are just a few extremely important utility programs:

\


* GCC. A compiler supporting many programming languages.
* Emacs. A powerful text editor.&#x20;
* Make. Automatically determines which source files need to be recompiled and/or linked.
* SSH. Enables users to log into a remote machine and execute commands on it.&#x20;
* Grep. Searches files for text matching a given pattern.&#x20;

\
\


One of the most important utility programs is the shell.&#x20;

\


How do we execute these utilities? What if we want to combine utilities together?&#x20;

\


Shell

\


The shell is a program that provides a user-friendly interface to the operating system.&#x20;

\


It does this by (1) providing a programming language through which users can efficiently write commands; and (2) by interpreting these commands and executing these commands.&#x20;

\


The programming language the shell provides is a programming language like any other—it has variables, functions, comments, and offers redirection and piping. Unlike languages such as Java or C, however, the shell is designed for invoking commands interactively.&#x20;

\


That is, unlike Java programs that are normally written in a file for later execution, shell commands are generally invoked one command at a time, normally consisting of less than a line of.&#x20;

\
\
\
\


For this we offer another interface: the shell. It offers an interface to OS utilities. Sometimes, however, the shell executes the command itself. In this case the shell serves as a direct interface to the OS system calls.&#x20;

\


The shell is one of the most used user programs. The shell is a program like any other; it is not part of the OS kernel. Thus, users are not bound to one type of shell. There are many shells on linux. In fact, a user can write their own shell.&#x20;

\


All in all, the utility programs, libraries, application programs, shells, etc., make up the System programs. Which programmers use as their interface.&#x20;

\


The set of systems programs commonly available defines the user interface. Most systems programs are written in C, and the UNIX Programmer’s Manual presents all system calls as C functions. They perform higher-level housekeeping tasks.&#x20;

\
\


The shell executes the commands by either invoking other programs that make the appropriate system-calls or by making the system-calls itself using its builtin functions (I.e., code contained within the shell itself). Shell commands can be arranged in a file for later execution. (Linux calls these files shell scripts.)

\
