# Understanding Working Directories

Now that we’ve covered pathnames, the working directory concept should make more sense. In particular, we’ve seen one of its practical functions: to resolve relative pathnames. To make the concept of a working directory even more concrete, here is an example demonstrating a common mistake command-line beginners make. In the screen shown in Figure 5, there are two armlab terminal sessions open simultaneously, labeled 1 and 2.

\
Terminal 1 shows the source code of hello.c, the classic Hello World program. When invoking ./hello on both terminals, we anticipate that “Hello, world” will be displayed on both terminals. As you can see in Figure 5, however, invoking ./hello on both terminals produces surprising results. The command succeeds in terminal 1, displaying “Hello, World” on the terminal. It fails in terminal 2, however, with the message: -bash: ./hello: No such file or directory.

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 3.14.12 PM.png" alt=""><figcaption></figcaption></figure>

\
The issue, as you may have realized, has to do with each terminal’s working directory.

To explain, let’s back up a bit. For the shell to execute a program on the command line, the shell must be aware of the program’s location in the hierarchy structure. This holds true whether the program is an OS utility or a user program. Most programs invoked on the command line are OS utilities. In such a case, you need not explicitly tell the shell where to locate the program (I.e., provide a pathname), since it already knows where to locate it. (See PATH \<section>…) Thus, you can invoke an OS utility by simply using its name. By default, however, the shell does not know where user programs are located. Therefore, when such a program is invoked, the user must supply a pathname—absolute or relative.&#x20;

\
Back to our example. Although it may not be obvious, ./hello is interpreted by the shell as the pathname of hello—relative to each terminal’s working directory, that is. (Recall that “.” represents the working directory.) Thus, when ./hello is invoked in each terminal, the shell looks for hello in each terminal’s working directory. The command succeeds in terminal 1, since hello is in fact located in terminal 1’s working directory (\~/workingDirectoryPractice). It fails in terminal 2, however, since hello is not in its working directories (\~ and \~/Downloads respectively). In the shell’s words: “No such file or directory.” (Admittedly, a message like “you’re telling me to locate hello in the working directory, but it ain’t there” might have been easier to understand.) If correct pathnames are supplied in terminal 2, the command will succeed, as shown in Figure 6.&#x20;

\


<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 3.14.12 PM (1).png" alt=""><figcaption></figcaption></figure>
