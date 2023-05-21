# Appendix B: Detailed Explanation of I/O and Redirection & Piping

## **Shell**

Sitting above utilities and user programs is the shell. The shell provides a language in which commands are issued. It handles tasks like locating programs, handling input and output calls, and starting a new process. The shell essentially provides a cleaner interface and makes it more efficient for users to interact with the system. This is done via the shell's language, which allows programs to be run with simple commands and implements the command-line interface (CLI).

A shell is a command interpreter that provides a text-based interface for users to interact with the OS. Shells allow users to launch programs, manage files, and perform other tasks by typing commands. The shell interprets these commands and uses system calls to execute them. Examples of shells include bash, zsh, and PowerShell. The shell interacts with the system call interface, executing system calls based on user input. When you type a command into the shell, like `ls` or `cat`, the shell locates the appropriate utility program, starts a new process, and makes system calls to execute the command.

## **Terminal**

At the top of this abstraction pyramid is the terminal or terminal emulator. This is the interface that users interact with directly. It captures input from the user and passes it to the shell for interpretation and execution.

So, to summarize, the flow of command execution starts from the terminal, where you type a command. This command is interpreted by the shell, which may use core utilities and libraries to execute the command. The libraries interface with the OS, making system calls as necessary. The OS interprets these calls and communicates with the hardware using the language specified by the ISA. Finally, the hardware executes the low-level instructions, thus completing the flow from terminal to hardware and back.
