# Important Terminology

Linux is an operating system kernel.&#x20;

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

## Command line Interface

The command-line interface (CLI) is a text-based method of interacting with your computer. Unlike the graphical user interfaces (GUIs) that allow you to issue commands by clicking buttons and icons, a CLI requires you to issue commands by typing typing sequences of text in a [terminal](broken-reference).&#x20;

Imagine using a CLI as if you're texting with your computer: you type in your request, and it responds directly with text output. Let's consider a couple of examples of computer interaction to highlight the distinction between a GUI and CLI:

1. **Opening an application:**
   * **GUI**: You might simply double-click on the application's icon.
   * **CLI**: You would issue a command like `open -a "application_name"`.
2. **Moving a file:**
   * **GUI**: This could involve using the drag-and-drop paradigm.
   * **CLI**: You'd invoke a command like `mv file.txt ~`.

Given the much steeper learning curve of the CLI compared to the GUI, you might wonder why it isn't obsolete. Well, there are a few reasons:

* **Speed:** Once you're familiar with commands, the CLI can be much faster than using a mouse.
* **Automation:** The CLI makes it easy to automate repetitive tasks.
* **Remote Access:** Remote computer interaction is much more efficient in a CLI.&#x20;
* **Power:** Some CLI commands have no GUI equivalent.

## Terminal

CLI commands are issued via a _terminal_. In the nascent days of interactive computing, terminals were hardware devices, consisting of a keyboard and a display unit. The first terminals were teletype machines, such as the Model 33 ASR shown in Figure 1, whose display unit was a paper-roll printer.

<figure><img src="https://lh4.googleusercontent.com/Sui_O3OmVfRuG7TS5Ro-pkF7IOJAAbL3Wxb5wHU2xvDIbpFmwGSHkM35HSD2Eic31K5unT9XBYsh63ta-eK33dyWUfQrfJKI48zSJjDUxw2m3LaRKU73PD2WRTUNqETK1FU1RoFPWQSqlph9K8Zoqc4" alt="" width="375"><figcaption><p>Figure 1: Teletype Model 33 ASR</p></figcaption></figure>

Teletypes fell out of use in the 1970s with the advent of video display terminals, such as the DEC VT100 shown in Figure 2. These terminals provided instant user-feedback and editing capabilities, making the CLI far more efficient and user-friendly.&#x20;

<figure><img src="../../.gitbook/assets/1200px-DEC_VT100_terminal_transparent.png" alt="" width="375"><figcaption></figcaption></figure>

Today, hardware terminals are largely obsolete. The predominant method for accessing the CLI is through a _terminal emulator_, which is a GUI program that simulates the functionality of a hardware terminal, such as the VT-100. An example of such a terminal emulator is macOS's Terminal, shown in Figure 3.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-19 at 5.46.26 PM.png" alt="" width="563"><figcaption><p>Figure 3: macOS Terminal Application</p></figcaption></figure>



## Shell

Have you ever thought about what happens when you type a command and press enter? In other words,&#x20;

When you type commands, how are the commands implemented?&#x20;

The shell is a program that implements a command line interface.&#x20;













While Unix shells such as Bash and Zsh have slight differences in their syntax and capabilities, they share many similarities, making transitioning from one to the other (such as from Bash to Zsh or vice versa) relatively seamless.

##
