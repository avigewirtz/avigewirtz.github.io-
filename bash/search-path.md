# Search Path

When an executable file (I.e., program) is invoked on the command line, the shell must have some way of locating the file in the directory hierarchy. If it cannot locate it, it will return an error, even if the file in fact exists.&#x20;

How the shell locates the program depends on how it is invoked on the command line. There are three cases:

1. The command name has a / (forward slash) at the start (i.e., /dir1/command\_name).
2. The command name has a / but not at the start (i.e., dir1/command\_name)
3. The command name does not have a / (i.e., coommand\_name)

In cases 1 and 2, the shell will interpret the command as referencing the executable file’s absolute and relative pathname, respectively.&#x20;

In case 1, however—where there is no / in the command name—the shell will search each of the places listed below, in the following order:

1. The shell will search for a shell function with command\_name.&#x20;
2. The shell will search the shell’s builtin list for a builtin with command\_name.
3. The shell will search through the directories listed in $PATH for an executable file with command\_name.&#x20;

### PATH environment variable

The PATH environment variable is a variable that specifies the directories the shell should search to find an executable file when there is no / in the program name. By default, the PATH variable usually contains the following directories.

* /usr/bin
* /usr/sbin
* /usr/local/bin
* /usr/local/sbin
* /bin
* /sbin

Thus, when users invoke programs like logname, hostname, uname, date, and cal, the shell searches for these programs in the directories listed in $PATH. You could also invoke these programs using their absolute or relative pathnames, of course.&#x20;

This shell behavior is often a source of confusion for command-line beginners. Say the executable hello is located in the working directory. Invoking hello will not work, even though it is a valid (relative) pathname–the error “No such file or directory” will be returned.&#x20;

The reason, as we just explained, is that the shell will only search the directories listed in $PATH when a program is invoked without a / in its name. Even if the program is located in the working directory, it still must be invoked using a /. A useful “trick” to invoke hello with a / is to trivially insert a /, as so: ./hello. Because . references the working directory, it essentially has no effect on the command other than inserting a /.&#x20;

To see which directories are currently registered under PATH, open a terminal and run the following command.

Echo $PATH

\
Here, the $ sign is to denote a variable. The echo command prints the value of the PATH variable.
