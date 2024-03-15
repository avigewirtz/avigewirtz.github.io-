# Shell

Just as commands issued in high-level programming languages utilize a specific syntactical structure, commands issued in the CLI also have their own syntax. Similarly, just as commands in programming languages interact with hardware via various intermediary software, CLI commands also interact via intermediary software.

The program that implements the CLI is called the shell, which is both a programming language and a command interpreter. As a programming language, it defines the syntax and semantics of CLI commands, specifying the format that commands must adhere to and the range of possible operations. As a command interpreter, it interprets the commands entered in the terminal.

There are various shell implementations available, each offering its own set of features and functionalities. Some popular shell implementations include Bash, Zsh, PowerShell, and Ksh.

Each operating system typically has a default shell: Bash for Linux, Zsh for macOS, and PowerShell for Windows. In COS217, our focus will be on the Bash shell due to its widespread usage, particularly in Linux.

While Unix shells such as Bash and Zsh have slight differences in their syntax and capabilities, they share many similarities, making transitioning from one to the other (such as from Bash to Zsh or vice versa) relatively seamless.
