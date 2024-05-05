# The Terminal and Shell

how do we interact with Linux, or with any computer for that matter? Nowadays, most users intearct with computers via a graphical user interface (GUI).&#x20;

back in the day, used to do it with a device known  as a terminal. the first terminals were hardware&#x20;

## Command line Interface

The command-line interface (CLI) is a text-based method of interacting with your computer. Unlike the graphical user interfaces (GUIs) that allow you to issue commands by clicking buttons and icons, a CLI requires you to issue commands by typing typing sequences of text in a [terminal](broken-reference).&#x20;

Imagine using a CLI as if you're texting with your computer: you type in your request, and it responds  with text output. Let's consider a couple of examples of computer interaction to highlight the distinction between a GUI and CLI:

1. **Opening an application:**
   * **GUI**: You might simply double-click on the application's icon.
   * **CLI**: You would issue a command like `open -a "application_name"`.
2. **Moving a file:**
   * **GUI**: This could involve using the drag-and-drop paradigm.
   * **CLI**: You'd invoke a command like `mv file.txt ~`.

{% hint style="info" %}
Given the much steeper learning curve of the CLI compared to the GUI, you might wonder why anyone uses the CLI over a GUI. Here's a few reasons:

* **Speed:** Once you're familiar with commands, the CLI can be much faster than using a mouse.
* **Automation:** The CLI makes it easy to automate repetitive tasks.
* **Remote Access:** Remote computer interaction is much more efficient in a CLI environment.&#x20;
* **Necessity:** Some CLI commands have no GUI equivalent.
{% endhint %}

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
