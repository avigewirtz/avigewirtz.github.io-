# How Bash Processes Commands

In Bash, the first word of a command line is interpreted as the name of the command to be executed. There are three cases to consider:

1. The first word of the command starts with a _/_ (forward slash).

When a command starts with a forward slash, Bash interprets it as an absolute path to the command's executable file. Bash will try to execute the file located at the specified path. If the file is not found or is not executable, an error will be displayed.

Example:

```shell
/bin/ls
```

2. The first word contains a _/_, but not at the start.

When a command contains a forward slash in it but not at the start, Bash interprets it as a relative pathname of an executable file. It will attempt to execute the file located at the specified path. If the file is not found or is not executable, an error will be displayed.

Example:

Assume you're working directory is /u/NetID/, and you invoke:&#x20;

```
../../bin/ls
```

Bash interprets _../../bin ls_ as the relative pathname of the `ls` executable. Because `ls` is in fact located in /bin, the command will succeed.&#x20;

3. The first word does not contain a _/_.

When a first word of a command does not have a _/_ in it, Bash searches for a match in the following order:

1. **Aliases**: Bash checks if an alias matches the command name. An alias is a user-defined shortcut for a longer command or a sequence of commands.
2. **Bash built-ins**: Bash searches for a built-in matching the command name. Built-ins are commands which are built into Bash itself. Examples include `cd`, `echo`, and `type`. These commands are executed directly by the shell without invoking an external program.
3. **Functions**: Bash checks for a user-defined Bash function matching the command name.&#x20;
4. **External programs**: Finally, if none of the above searches yield a match, Bash searches in the directories listed in the `PATH` environment variable for an executable file matching the command name. This is called the _search path_.

Example 1:

```shell
ls
```

1. Bash checks if `ls` is an alias = :heavy\_multiplication\_x:.
2. Bash checks if `ls` is a shell built-in command = :heavy\_multiplication\_x:.
3. Bash checks if `ls` is a function = :heavy\_multiplication\_x:.
4. Bash search is `ls` is an executable file in the search path = :heavy\_check\_mark:

Example 2:

Assume an executable file named _hello_ is in the working directory and you invoke:

```shell
hello
```

Because `hello` does not contain a /, bash will search for a match in the following order:

1. Bash checks if _hello_ is an alias = :heavy\_multiplication\_x:.
2. Bash checks if _hello_ is a shell built-in command = :heavy\_multiplication\_x:.
3. Bash checks if _hello_ is a function = :heavy\_multiplication\_x:.
4. Bash search for an executable file named _hello_ in the directories listed in the `PATH` environment variable = :heavy\_multiplication\_x:.

Because none of the searches yielded a match, Bash will return the following output:

```
-bash: hello: command not found
```

While this behavior may initially seem preprexling given that hello is a valid relative pathname of the hello executable, it makes sense, since the first word does not contain a /.&#x20;

Instead, you must invoke hello as so:

```
./hello
```

Bash will not search for hello in the working directory, and the command will succeed.&#x20;

Hopefully this helps explain why user-created executables in the working directory must be invoked with a `./`. &#x20;
