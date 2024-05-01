# Bash Execution Environment

The exact behavior of commands issued in Bash depends upon the execution environment provided by Bash.

Bash maintains a set of _environment variables_ that are used to provide information, like the current working directory, and the type of terminal being used, to the programs you run. The environment variables are passed to all programs that are not built into Bash and may be consulted, or modified, by the program. By convention, environment variables are given in upper case letters.

To view all the environment variables, use the command:

```
printenv
```

You can also view a particular environment variable using the echo command:

```
echo $TERM
```

### The creation of the execution environment

When the shell program starts, it reads configuration files called _login scripts_ to configure the execution environment. On HP-UX, the file /etc/profile provides initialization parameters for ksh and sh, while the file /etc/csh.login is used for csh. After the system login scripts are read, the shell looks for user-specified login scripts.

Shell startup: User login scripts After the system login scripts are read, the shell reads user login scripts. User login scripts are kept in one's home directory, and are the means by which one can customize the shell environment. Sh and ksh look for a file called .profile. Ksh also reads a file defined in the environment variable ENV. Csh reads a file called .cshrc, and (if it is the login shell), the file .login.



## Execution environment

When a user logs in or out of a Bash terminal session, various Bash configuration files are automatically executed.&#x20;

## Login configuration files

These files define the user's environment, initializing variables, aliases, and functions. The main login configuration files include`/etc/profile`, `~/.bash_profile` or `~/.profile`.&#x20;

* `/etc/profile`: This is a global configuration file that is executed when a user logs into the system using a Bash shell. It sets up system-wide environment variables, such as the `PATH`, and is generally used for defining global settings that apply to all users.
* `~/.bash_profile` or `~/.profile`: These are user-specific configuration files that are executed when a user logs in with a Bash login shell. They are used to set up user-specific environment variables, aliases, and functions. If both files exist, `~/.bash_profile` takes precedence.

Upon login, these files are executed in the following order:

1. `/etc/profile`
2. `~/.bash_profile` or `~/.profile`

If there is a conflict between any two configuration files, the one executed second will override the previously executed one. So, for example, if there is a conflict between `/etc/profile` and  `~/.bash_profile` or `~/.profile`, the latter will override the former.

## Logout configuration file

When a user logs out of a bash terminal session, the `~/.bash_logout` configuration file is executed. This performs cleanup tasks, such as clearing the terminal and saving command history.

{% hint style="info" %}
You can view the contents of configuration files by using any of the [file viewing commands](basic-file-and-directory-operations/viewing-files.md), such as `cat` or `emacs`. Understanding these configuration files enables you to customize the behavior and appearance of your Bash terminal sessions.
{% endhint %}

## Environment variables

In Linux, environment variables are a type of variable used to store information about the system environment, such as the current user's name, the current system's directory path, or settings for software applications. Standard environment variables on Linux include:

* `PATH`: Stores a list of directories where the shell looks for executable programs when a command is entered that does not contain a slash. Directories in the `PATH` variable are separated by colons (:).
* `HOME`: Specifies the home directory of the current user.  The HOME variable contains the name of your home directory. When you issue the cd command with no directory argument, you will be placed in the directory defined in the HOME environment variable. The HOME variable is also where the shell will look for the user login scripts.
* `USER`: Contains the username of the currently logged-in user. The USER variable contains your username. Any time you access a file or directory, the access permissions are checked against the value of USER.
* `PWD`: Specifies the current working directory. Whenever you change your directory with cd, this value changes.&#x20;
* `LANG`: Specifies the default language and character encoding used by the system.
* `EDITOR`: Defines the default text editor to be used by certain command-line programs. The EDITOR variable is used by programs that must invoke a text editor to provide the ability to edit or compose documents. One example is the elm program, which is used to read and send electronic mail. If you elect to compose a new mail message while in elm, the elm program will check the contents of the EDITOR variable to determine which editor to invoke.
* `SHELL`: Indicates the user's preferred shell program, such as Bash or Zsh.
* HOST The HOST environment variable contains the name of the host machine that is running your shell program. When you connect to a remote host through telnet or ftp, the name of your host is relayed to the remote machine, so the administrators of the remote machine can keep track of who is connecting, and from where.

To print the value of an environment variable, you can use the `echo` command with the variable name prefixed by a dollar sign ($), as so:

```bash
echo $PATH
```
