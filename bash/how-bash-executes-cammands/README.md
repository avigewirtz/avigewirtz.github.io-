# How Bash Executes Cammands

The job of a shell is to find and run commands. Whenever a command is invoked, Bash goes through the following steps to execute the command:

1. Performs expansions (such as alias expansion), assignments, and redirections. Assuming after these actions there is a resulting command name, Bash will search for the command in the following order:
   1. Search for a function that matches the command name.
   2. Searches for a shell built-in matching command name.&#x20;

If both these searches are unsuccessful, there are two cases to consider:

* The command name contains a forward slash (/) (e.g., `/bin/ls` or `../../bin/ls`).
* The command name does not contain a forward slash (e.g., `ls`).

In case 1, the command name is interpreted as the (absolute or relative) pathname, and Bash will look for an executable file in the specified pathname. If such a file exists, Bash will execute it. If not, Bash will return an error.

In case 2, Bash searches the directories listed in the PATH environment variable for a filename that matches the command name. If it finds a file with the specified name, Bash will execute it. If not, Bash will return an error.

## Examples

To illustrate this idea concretely, here are some examples showing the steps Bash takes when commands are invoked. In the following examples, assume the working directory is _/u/yourNetID._

* **Case 1**: Sat you invoke `/bin/ls`. Bash will perform the  following checks:
  1. Are there any expansions, assignments, and redirections in _/bin/ls_? :heavy\_multiplication\_x:
  2. Is `/bin/ls` a shell function? :heavy\_multiplication\_x:
  3. Is `/bin/ls` a shell built-in?  :heavy\_multiplication\_x:
  4. Does `/bin/ls` contain a forward slash? :heavy\_check\_mark:
  5. Is `/bin/ls` an executable file?  :heavy\_check\_mark:
  6. Execute it.
* **Case 2:** Invoking `../../bin/ls`:&#x20;
  1. Any expansions, assignments, and redirections? :heavy\_multiplication\_x:
  2. Is `../../bin/ls` a shell function? :heavy\_multiplication\_x:
  3. Is `../../bin/ls` a shell built-in?  :heavy\_multiplication\_x:
  4. Does `../../bin/ls` contain a forward slash? :heavy\_check\_mark:
  5. Is `../../bin/ls` an executable file?  :heavy\_check\_mark:
  6. Execute it.
* **Case 3**: Invoking `ls`:&#x20;
  1. Any expansions, assignments, and redirections? :heavy\_check\_mark:&#x20;
  2. Expand ls to ls -a. Use the _first word_ of `ls -a` (i.e., `ls`) as the command name.
  3. Is `ls` a shell function? :heavy\_multiplication\_x:
  4. Is `ls` a shell built-in?  :heavy\_check\_mark:
  5. Execute it
*   **Case 4**: Invoking `hello`:

    1. Any expansions, assignments, and redirections? :heavy\_multiplication\_x:
    2. Is `hello` a shell function? :heavy\_multiplication\_x:
    3. Is `hello` a shell built-in?  :heavy\_multiplication\_x:
    4. Does `hello` contain a forward slash? :heavy\_multiplication\_x:
    5. Is `hello` an entry in one of the PATH directories? :heavy\_multiplication\_x:
    6. Print `-bash: hello: command not found`.


* Case 5: Invoking `./hello`:
  * Any expansions, assignments, and redirections? :heavy\_multiplication\_x:
  * Is `./hello` a shell function? :heavy\_multiplication\_x:
  * Is `./hello` a shell built-in?  :heavy\_multiplication\_x:
  * Does `./hello` contain a forward slash? :heavy\_check\_mark:
  * Does an executable named `hello` exist in the working directory? :heavy\_check\_mark:
  * Execute `hello`.
* Case 6: Invoking `/u/NetID/hello`:
  * Any expansions, assignments, and redirections? :heavy\_multiplication\_x:
  * Is `/u/NetID/hello` a shell function? :heavy\_multiplication\_x:
  * Is `/u/NetID/hello` a shell built-in?  :heavy\_multiplication\_x:
  * Does `/u/NetID/hello` contain a forward slash? :heavy\_check\_mark:
  * Does an executable named `hello` exist in `/u/NetID`? :heavy\_check\_mark:
  * Execute `/u/NetID/hello`.

