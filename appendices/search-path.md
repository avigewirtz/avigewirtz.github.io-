# Search Path

When an executable file (I.e., program) is invoked on the command line, the shell must have some way of locating the file in the directory hierarchy. If it cannot locate it, it will return an error, even if the file in fact exists.&#x20;

How the shell locates the program depends on how it is invoked on the command line. There are three cases:

1. The command name has a / (forward slash) at the start (i.e., /dir1/command\_name).
2. The command name has a / but not at the start (i.e., dir1/command\_name)
3. The command name does not have a / (i.e., coommand\_name)

In cases 1 and 2, the shell will interpret the command as referencing the executable file’s absolute and relative pathname, respectively.&#x20;

In case 3, however—where there is no / in the command name—the shell will search for the command in the following order:

1. The shell searches for an alias with the command\_name.&#x20;
2. The shell searches for a shell function with the command\_name.&#x20;
3. The shell searches the shell's built-in list for a built-in with the command\_name.&#x20;
4. The shell searches through the directories listed in the $PATH environment variable for an executable file with the command\_name.

\
\




each of the places listed below, in the following order:

The shell searches for an alias with the command\_name. b. The shell searches for a shell function with the command\_name. c. The shell searches the shell's built-in list for a built-in with the command\_name. d. The shell searches through the directories listed in the $PATH environment variable for an executable file with the command\_name.

1. The shell will search for a shell function with command\_name.&#x20;
2. The shell will search the shell’s builtin list for a builtin with command\_name.
3. The shell will search through the directories listed in $PATH for an executable file with command\_name.&#x20;

###
