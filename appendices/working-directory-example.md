# Understanding Working Directories

To better understand the concept of a working directory, it's helpful to start with a common error that new command-line users often encounter. Consider Figure 5, which shows two Armlab terminal sessions (labeled 1 and 2). Terminal 1's working directory is _\~/bash\_practice/workingDirEx_, and Terminal 2's working directory is _\~/bash\_practice_. As you can see in both terminals, the command ./hello was invoked, yet it was only successful in terminal 1.

<figure><img src="../.gitbook/assets/Screenshot 2023-05-25 at 12.02.37 AM.png" alt="" width="563"><figcaption><p>Figure 5</p></figcaption></figure>

\
Running the command './hello' in both terminals might be expected to display 'Hello, World' in each. However, Figure 5 shows that it only succeeds in Terminal 1. Terminal 2 produces an error: '-bash: ./hello: No such file or directory'. The './hello' command is telling the shell to run a program named 'hello' located in the current working directory (indicated by the '.'), but in Terminal 2, no such file exists in the current directory.

This stems from how the shell locates programs. For system utilities, their locations are pre-known to the shell via a list of directories stored in the PATH variable, allowing you to invoke these utilities by simply typing their names. However, for user-created programs like 'hello', their locations are not automatically known to the shell. Hence, when invoking these programs, you must provide a pathname pointing to the program's location, which can be either absolute (from the root directory) or relative (from the current working directory).

In our example, the shell interprets './hello' as a relative pathname to the 'hello' program. It succeeds in Terminal 1, as the 'hello' program is indeed in its working directory. However, it fails in Terminal 2, as there is no 'hello' in its current working directory, resulting in the error 'No such file or directory'. If the correct pathname to 'hello' is provided in Terminal 2, the command will run successfully as shown in Figure 6.

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 3.14.12 PM.png" alt="" width="563"><figcaption><p>Figure 6</p></figcaption></figure>
