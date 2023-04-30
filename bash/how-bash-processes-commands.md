# How Bash Processes Commands

A command name normally represents one of two things:

1. &#x20;A function that is built into Bash. This is called a Bash _built-in._&#x20;
2. An executable file. This represents either an OS utility program or a user-written program.&#x20;

The practical distinction between the two is normally irrelevant, but it does matter in certain contexts, such as when [retrieving documentation](getting-help.md) for a command, which will be covered soon.&#x20;



There are three cases:

1. The command name has a / (forward slash) at the start (i.e., /dir1/command\_name).
2. The command name has a / but not at the start (i.e., dir1/command\_name)
3. The command name does not have a / (i.e., coommand\_name)

In cases 1 and 2, the shell will interpret the command as referencing a file’s absolute and relative pathname, respectively.&#x20;





### Command execution

Once you press ENTER, the command is sent to Bash for interpretation. Bash will first check if a command\_name function exists. If it does, Bash will execute the function. If it does not exist, Bash will check if a command\_name executable file exists. Bash will not check every filename on the computer for a match, however. It will only check for matches in specific directories, known as the "[search path](search-path.md)," which are listed in the PATH environment variable. &#x20;
