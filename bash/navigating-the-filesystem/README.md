# Navigating the filesystem

To effectively navigate the Linux filesystem, you need to be familiar with three commands: `pwd`, `ls`, and `cd`. These commands are perhaps the most commonly used Bash commands, so it is worth your while to make the extra effort to master them.

## **`pwd` - A sense of Location**

Whenever you're using the command line, bash is always positioned somewhere in the filesystem. This location is known as your (or, more accurately, Bash's) working directory.&#x20;

You can find out your current location by invoking `pwd`, which displays the absolute pathname of your working directory on stdout. By default, your working directory will be your home directory, which on armlab is /u/yourNetID:

```
~$ pwd
/u/yourNetID
```

{% hint style="success" %}
On Armlab, the working directory is displayed in the [shell prompt](../warm-up-commands.md#shell-prompt), between the colon (:) and dollar ($) sign.
{% endhint %}

## **`ls` - A sense of surroundings**

In order to navigate, you ofd course need to have a sense of your surroundings. That is, what else is in the filesystem. That's where ls (list) comes into play, which can be used to display the contents of any directory in the filesystem.&#x20;

#### Basic usage

The most basic use case of `ls` is to list the names of the files and directories in the working directory. To do so, simply invoke:

```
ls
```

#### Displaying Hidden Files

By default, `ls` does not display [hidden](../filesystem/notable-directories.md#hidden-files-directories) entries (i.e., files and directories that begin with a `.`). To include hidden entries in the directory listing, use the `-a` option:

```
ls -a
```

#### Long Listing Format

You can also use `ls` to display the metadata about the file, such as the file type, owner, and last modification time. To do so, use the `-l` option:

```bash
ls -l
```

Let's go over the columns one by one:

* file type,&#x20;
* Access permissions
* number of hard links
* File owner
* group
* File size
* last modification date
* File name. &#x20;

#### Displaying the Contents of Another Directory

You can use ls to list the contents of a directory other than your working directory by listing the directory's pathname as as argument to ls. For example, to list the contents of /var, invoke:

```
ls /var
```

## **`cd` - Moving to a Different Location**

You can change your working directory via the `cd` command. For example, if your current working directory is _/u/yourNetID_ and you want to change your working directory to _/usr/bin_, you can invoke it's absolute pathname:

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

## Exercises

For the following questions, unless otherwise stated, assume the working directory is /u/yourNetID.

1. Which of the following commands will list the contents of your current working directory in a detailed format, including hidden files?
   * A) `ls -a`
   * B) `ls -l`
   * C) `ls -la`
   * D) `ls -lh`
2. What does `cd ..` achieve?
   * A) It moves you up one directory from your current location
   * B) It takess you to your home directory
   * C) It takes you to the root directory
   * D) It does nothing
3. What happens if you attempt to change your working directory to another user's home directory, such as `/u/bwk`?
   * A) The command succeeds without any issue
   * B) You are prompted for the other user's password
   * C) The command fails due to permissions, unless you have explicit permissions
   * D) Your current directory is unchanged, and an error message is displayed
4. Which of the following lists the contents of the root (/) directory?
   * A) `ls /`
   * B) `cd /` then `ls`
   * C) `pwd /`
   * D) `ls -root`
5. How do you return to the last directory you were in?
   * A) `cd ..`
   * B) `cd -`
   * C) `cd ~`
   * D) `cd /`
6. If you are in `/u/yourNetID`, what command takes you directly to your home directory?
   * A) `cd`
   * B) `cd ~`
   * C) `cd /u/yourNetID`
   * D) Both A and B
7. How do you change your working directory to `/usr/bin` from anywhere in the filesystem?
   * A) `ls /usr/bin`
   * B) `pwd /usr/bin`
   * C) `cd /usr/bin`
   * D) `dir /usr/bin`
8. What does the `pwd` command output?
   * A) List of files in the current directory
   * B) The current working directory's absolute path
   * C) The user's home directory path
   * D) The contents of a specified directory
9. Which of the following commands lists the contents of the working directory in long format?
   * A) `ls -l`
   * B) `pwd -l`
   * C) `cd -l`
   * D) `ls --long`
10. You're in `/home/username` and attempt to `cd` into a file named `notes.txt` in your current directory. What happens?
    * A) The file `notes.txt` opens in the default text editor
    * B) The terminal displays an error message
    * C) The command is successful, and `notes.txt` becomes the current directory
    * D) The command deletes `notes.txt`
11. From `/home/username/documents`, how do you navigate to `/home/username` using `cd`?
    * A) `cd /home/username` using absolute path
    * B) `cd ..` using relative path
    * C) Both A and B are correct
    * D) `cd ~/documents`
12. If your current working directory is `/home/username`, how can you change it to `/usr/bin`?
    * A) `cd /usr/bin`
    * B) `cd ../../usr/bin` assuming `/home/username` is your starting point
    * C) `ls /usr/bin`
    * D) Both A and B are correct
13. What happens when you invoke cd ././././?



<details>

<summary>Exercise answers</summary>



</details>
