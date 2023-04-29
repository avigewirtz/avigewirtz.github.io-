# pwd (Print Working Directory)

It is often useful to know your working directory’s location in the hierarchy structure. This knowledge is particularly relevant when using relative pathnames, since relative paths start at the working directory. To determine the location of the working directory, use the `pwd` (**p**rint **w**orking **d**irectory) command, which prints the absolute pathname of the working directory.

### Syntax: <mark style="color:red;">`pwd`</mark>

Pwd is a very simple command. It has no options ordinary users need to be aware of, and it takes no arguments.&#x20;

Upon logging into armlab, your home directory will by default be your working directory. To verify this, log into armlab and execute the pwd command. The output should look like the following:&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.08.38 PM.png" alt=""><figcaption></figcaption></figure>

where `/u/yourNetID` is the absolute pathname of your home directory.&#x20;

A useful feature on armlab is that your working directory is always displayed in the shell prompt, between the colon and dollar sign. In the previous example, we see that the \~ (tilde) character is displayed in the shell prompt. Recall that \~ represents your home directory and, on armlab, is equivalent to `/u/yourNetID`. Using that knowledge, we could have determined that the working directory is `/u/yourNetId` by simply inspecting the shell prompt (instead of invoking pwd).
