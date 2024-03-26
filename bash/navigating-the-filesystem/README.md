# Navigating the filesystem

Whenever you're using the command line, bash is always positioned somewhere in the filesystem. This location is known as your (or, more accurately, Bash's) working directory.

When you begin a Bash session, you start in your home directory.&#x20;



Thus, to effectively navigate the Linux filesystem, you need to be familiar with three commands: `pwd`, `ls`, and `cd`. These commands are perhaps the most commonly used Bash commands, so it is worth your while to make the extra effort to master them.

## <mark style="color:red;">pwd</mark> (<mark style="color:red;">p</mark>rint <mark style="color:red;">w</mark>orking <mark style="color:red;">d</mark>irectory)

The first step to navigating the filesystem is knowing where you currently Changing directories is easy as long as you know where you are (your current directory) and how that relates to where you want to go.

`pwd` displays the absolute pathname of the working directory on stdout. In simple terms, it tells you which directory you're currently "in." When you open a terminal session, you start in your home directory. As you navigate through the filesystem, you can use `pwd` to check your current location. &#x20;

Suppose you log into armlab and invoke `pwd`. It should display /u/yourNetID on stdout:

{% hint style="success" %}
On Armlab, the working directory is displayed in the [shell prompt](../warm-up-commands.md#shell-prompt), between the colon (:) and dollar ($) sign. Hence, you can determine your working directory without invoking `pwd`.&#x20;
{% endhint %}

## <mark style="color:red;">ls</mark> (<mark style="color:red;">l</mark>i<mark style="color:red;">s</mark>t directory contents)

TKnowing where you are is important, but to navigate, you also need to know what's around you. The `ls` command lists the contents of directories, showing you the files and other directories within your current location.

#### Basic usage

The most basic use case is to list the names of the files and directories in the working directory. To do so, simply invoke:

```
ls
```

#### Displaying Hidden Files

By default `ls` does not display [hidden](../filesystem/notable-directories.md#hidden-files-directories) files (i.e., files that begin with a `.`). To include hidden entries in the directory listing, use the -a option:

```
ls -a
```

#### Long Listing Format

You can also use ls to display the metadata about the file, such as the file type, owner, and last modification time. To do so, use the -l option:

```bash
ls -l
```

Let's go over the output one by one:

file type, permissions, number of hard links, owner, group, size, last modification date, and name. &#x20;

#### Displaying the Contents of Another Directory

To list the contents of a directory other than your working directory, simple provide its pathname as an argument to ls. For example, to list the contents of /var, invoke:

```
ls /var
```

## <mark style="color:red;">cd</mark> (<mark style="color:red;">c</mark>hange working <mark style="color:red;">d</mark>irectory)

You can change your working directory via the `cd` command. You must have execute (search) permission in the specified directory. It's syntax

#### Basic usage

For example, if your current working directory is _/u/yourNetID_ and you want to change your working directory to _/usr/bin_, you can invoke it's absolute pathname:

```bash
cd /usr/bin
```

Or you can specify it's relative pathname:

```bash
cd ../../usr/bin
```

Recall that `..` represents the parent directory.&#x20;

#### Going home

If you invoke `cd` without arguments, it'll take you to your home directory:&#x20;

```
cd
```

#### Tips for Using `cd`

* **Tab Completion**: Start typing the directory name and press Tab; the system auto-completes the directory name, saving time and reducing typos.
* **Using Quotes**: If a directory name contains spaces, enclose the name in quotes (e.g., `cd "My Documents"`).

##
