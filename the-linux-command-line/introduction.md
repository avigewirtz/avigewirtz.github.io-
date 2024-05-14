# Introduction

When Linus Torvalds introduced Linux and for a long time thereafter, Linux did not have a graphical user interface (GUI). It ran on character-based terminals only, using a command-line interface (CLI), also referred to as a textual interface. All the tools ran from a command line. Today the Linux GUI is important, but many people— especially system administrators—run many command-line utilities. Command-line utilities are often faster,! \more powerful, or more complete than their GUI counterparts. Sometimes there is no GUI counterpart to a textual utility; some people just prefer the hands-on feeling of the command line.

When you work with a command-line interface, you are working with a shell. Before you start working with a shell, it is important that you understand a basic understanding of the componentds of a Linux system and how they interact with each other.&#x20;



Some tools and technologies lend themselves to a “black-box” approach, in which new users don’t pay too much attention to how a tool works under the hood. You concentrate first on learn‐ ing to manipulate the tool; the “why” and “how” can come later. Git’s particular design, however, is better served by the opposite approach, in that a number of fundamental internal design de‐ cisions are reflected directly in how you use it. By understanding up front and in reasonable detail several key points about its op‐ eration, you will be able to come up to speed with Git more quickly and confidently, and be better prepared to continue learning on your own.

Thus, I encourage you to take the time to read this chapter first, rather than just jump over it to the more tutorial, hands-on chap‐ ters that follow (most of which assume a basic grasp of the ma‐ terial presented here, in any case). You will probably find that your understanding and command of Git will grow more easily if you do.



#### Outline of this chapter

The command-line interface (CLI) is a text-based method of interacting with your computer. Unlike the graphical user interfaces (GUIs) that allow you to issue commands by clicking buttons and icons, a CLI requires you to issue commands by typing typing sequences of text in a [terminal](broken-reference).&#x20;

Imagine using a CLI as if you're texting with your computer: you type in your request, and it responds  with text output. Let's consider a couple of examples of computer interaction to highlight the distinction between a GUI and CLI.&#x20;

## Terminal

CLI commands are issued via a _terminal_. In the nascent days of interactive computing, terminals were hardware devices, consisting of a keyboard and a display unit. The first terminals were teleprinter machines, such as the Teletype Model 33 ASR shown in Figure 1, whose display unit was a paper-roll printer.

Teletypes fell out of use in the 1970s with the advent of video display terminals, such as the DEC VT100 shown in Figure 2, which provided instant user-feedback and editing capabilities.&#x20;

Today, hardware terminals are largely obsolete. The predominant method for accessing the CLI is through a _terminal emulator_, which is a GUI program that simulates the functionality of a hardware terminal. An example of a terminal emulator is macOS's Terminal, shown in Figure 3.&#x20;

<figure><img src="../.gitbook/assets/Frame 1 (4).png" alt=""><figcaption></figcaption></figure>
