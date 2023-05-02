# How Bash Executes Commands

The job of a shell is to find and run commands. This file explains how the shell identifies commands names and then finds the commands to run, such as the `date` command:

1. Performs expansions (such as alias expansion), assignments, and redirections.&#x20;
2. Assuming there is a resulting command name:
   1. Searches for a function that matches the command name.
   2. Searches the shell built-in list for a built-in matching command name.&#x20;

If these searches are unsuccessful, there are two cases to consider:

1. The command name contains a forward slash (/) (e.g., `/bin/ls` or `../../bin/ls`).
2. The command name does not contain a forward slash (e.g., `ls`).

In case 1, the command name is interpreted as the (absolute or relative) pathname of a program. If no such file exists, an error will be returned.&#x20;

In case 2, the shell searches the directories listed in the PATH environment variable for a filename that matches the command name.&#x20;

### Examples

Assume the working directory is /u/NetID and contains an executable file named hello that prints "Hello, World!" on stdout.&#x20;

* Case 1: Invoking `/bin/ls`
  1. Any expansions, assignments, and redirections? :heavy\_multiplication\_x:
  2. Is `/bin/ls` a shell function? :heavy\_multiplication\_x:
  3. Is `/bin/ls` a shell built-in?  :heavy\_multiplication\_x:
  4. Does `/bin/ls` contain a forward slash? :heavy\_check\_mark:
  5. Is `/bin/ls` an executable file?  :heavy\_check\_mark:
  6. Execute it.
* Case 2: Invoking `../../bin/ls`:&#x20;
  1. Any expansions, assignments, and redirections? :heavy\_multiplication\_x:
  2. Is `../../bin/ls` a shell function? :heavy\_multiplication\_x:
  3. Is `../../bin/ls` a shell built-in?  :heavy\_multiplication\_x:
  4. Does `../../bin/ls` contain a forward slash? :heavy\_check\_mark:
  5. Is `../../bin/ls` an executable file?  :heavy\_check\_mark:
  6. Execute it.
* Case 3: Invoking `ls`:&#x20;
  1. Any expansions, assignments, and redirections? :heavy\_check\_mark:&#x20;
  2. Expand ls to ls -a. Use the _first word_ of `ls -a` (i.e., `ls`) as the command name.
  3. Is `ls` a shell function? :heavy\_multiplication\_x:
  4. Is `ls` a shell built-in?  :heavy\_check\_mark:
  5. Execute it
*   Invoking `hello`:

    1. Any expansions, assignments, and redirections? :heavy\_multiplication\_x:
    2. Is `hello` a shell function? :heavy\_multiplication\_x:
    3. Is `hello` a shell built-in?  :heavy\_multiplication\_x:
    4. Does `hello` contain a forward slash? :heavy\_multiplication\_x:
    5. Is `hello` an entry in one of the PATH directories? :heavy\_multiplication\_x:
    6. Print `-bash: hello: command not found`.



Invoking `./hello`:

* Any expansions, assignments, and redirections? :heavy\_multiplication\_x:
* Is `./hello` a shell function? :heavy\_multiplication\_x:
* Is `./hello` a shell built-in?  :heavy\_multiplication\_x:
* Does `./hello` contain a forward slash? :heavy\_check\_mark:
* Does an executable named `hello` exist in the working directory? :heavy\_check\_mark:
* Execute `hello`.

Invoking `/u/NetID/hello`:

* Any expansions, assignments, and redirections? :heavy\_multiplication\_x:
* Is `/u/NetID/hello` a shell function? :heavy\_multiplication\_x:
* Is `/u/NetID/hello` a shell built-in?  :heavy\_multiplication\_x:
* Does `/u/NetID/hello` contain a forward slash? :heavy\_check\_mark:
* Does an executable named `hello` exist in `/u/NetID`? :heavy\_check\_mark:
* Execute `/u/NetID/hello`.
