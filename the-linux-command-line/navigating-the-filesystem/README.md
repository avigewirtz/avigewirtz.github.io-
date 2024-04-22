# Navigating the filesystem

To effectively navigate the Linux filesystem, you need to be familiar with three commands: `pwd`, `ls`, and `cd`. These commands are perhaps the most commonly used Bash commands, so it is worth your while to make the extra effort to master them.

## **`pwd` - A sense of Location**

Whenever you're using the command line, bash is always positioned somewhere in the filesystem. This location is known as your (or, more accurately, Bash's) working directory. (See Working Directory.)

You can find out your current working directory by invoking `pwd` (**p**rint **w**orking **d**irectory), which displays the absolute pathname of your working directory on stdout. By default, your working directory will be your home directory, which on armlab is _/u/yourNetID_:

```
~$ pwd
/u/yourNetID
```

As we'll see soon, you can change your working directory with the `cd` command.

{% hint style="success" %}
On Armlab, the working directory is displayed in the [shell prompt](../warm-up-commands.md#shell-prompt), between the colon (:) and dollar ($) sign.&#x20;
{% endhint %}

## **`ls` - A sense of surroundings**

Knowing where you are in the filesystem is important, but in order to navigate, you also need to be familiar with what's around you. The `ls` (**l**i**s**t) command can be used to list the contents of any directory in the filesystem. &#x20;

#### Basic usage

The most basic usage of `ls` is to list the names of the files and directories in the working directory. To do so, simply invoke:

```
ls
```

#### Displaying Hidden Files

By default, `ls` does not display [hidden](../filesystem/notable-directories.md#hidden-files-directories) entries (i.e., files and directories whose names begin with a `.`, such as .bashrc). To include hidden entries in the directory listing, use the `-a` option:

```
ls -a
```

#### Displaying file metadata

Each file and directory has associated metadata, such as access permissions, owner username, and last modification time. You can display the metadata using the `-l` option, which lists the directory's contents in long format:

```bash
ls -l
```

Let's break down the output using the final row as an example:&#x20;

*   **-rw-------.**&#x20;

    The file's access permissions. This will be covered in [file and directory access permissions](../file-and-directory-access-permissions.md).&#x20;
*   **1**

    Number of hard links. You can safely ignore this column.&#x20;
*   **sgewirtz**&#x20;

    Name of the user who owns the file.&#x20;
*   **utemper**&#x20;

    Name of the group that owns the file.&#x20;
*   **686539**

    Size of the file in bytes.&#x20;
*   **Oct 20 22:54**

    Date and time the file was last modified.&#x20;
*   **the\_oddysey.txt**

    &#x20;   name of the file

#### Displaying the Contents of Another Directory

To list the contents of a directory other than the working directory, simply supply it's (absolute or relative) pathname as an argument to ls. For example, to list the contents of `/var`:

```bash
ls /var
```

## **`cd` - Relocating**

You can change your working directory using the `cd` (**c**hange working **d**irectory) command. Its basic syntax is:

```
cd DIRECTORY_PATHNAME
```

Here, `DIRECTORY_PATHNAME` refers to either the absolute or relative pathname of the target directory. (See [pathnames](../filesystem/pathnames.md)).&#x20;

### Example&#x20;

Absolute pathname:

```bash
cd /usr/bin
```

Relative pathname:

```bash
cd ../../usr/bin
```

Recall that `..` represents the parent directory. Figure 3 shows a visualization of both.

{% hint style="warning" %}
**Note:** To navigate to a directory that includes whitespace in its name, you have to ensure that Bash treats the entire directory name as a single argument. This can be done by enclosing the directory name in quotes. For example:

```bash
cd "final draft"
```
{% endhint %}

### **Useful Shortcuts**

* **Going home**: If you invoke `cd` without arguments, it'll take you to your home directory.&#x20;
* **Returning to the last working directory**. `cd -` (hyphen) returns you to your previous working directory.&#x20;
* **Tilde (`~`):** Tilde is a shortcut for your home directory. Thus, to navigate to _/u/yourNetID/A1_, for example, you can invoke`cd ~/A1` instead of `cd /u/yourNetID/A1`.
* **Tab Completion**: If you start typing an directory name and press Tab, Bash will attempt to auto-completes the directory name. This will save you time and reduce typos.

## Exercises

{% hint style="info" %}
Note: For the following questions, assume the working directory is /u/yourNetID, unless otherwise stated,&#x20;
{% endhint %}

1. Which of the following commands lists the metadata of all files in the working directory, including hidden files?
   * A) `ls -a`
   * B) `ls -l`
   * C) `ls -la`
   * D) `ls -lh`
2. What does `cd ..` achieve?
   * A) It moves you up one directory from your current location
   * B) It takes you to your home directory
   * C) It takes you to the root directory
   * D) It does nothing
3. Which of the following is likely to happen if you attempt to change your working directory to another user's home directory, such as `/u/bwk`?
   * A) The command succeeds without issue
   * B) You are prompted for the other user's password
   * C) The command fails with a "Permission denied" error
   * D) You are successfully able to change into the directory, but it contains no files or subdirectories visible to you.
4. Which of the following lists the contents of the root (/) directory? Check all that apply.
   * A) `ls /`
   * B) `cd /` then `ls`
   * C) `pwd /`
   * D) `ls \`
5. Which of the following returns you to your last working directory?
   * A) `cd ..`
   * B) `cd -`
   * C) `cd ~`
   * D) `cd /`
6. If you are in `/usr/bin`, which of the following will take you to your home directory? Mark all that apply.
   * A) `cd`
   * B) `cd ~`
   * C) `cd /u/yourNetID`
   * D) `cd .`
7. How do you change your working directory to `/usr/bin` from anywhere in the filesystem?
   * A) `ls /usr/bin`
   * B) `pwd /usr/bin`
   * C) `cd /usr/bin`
   * D) `dir /usr/bin`
8. What does the `pwd` command output?
   * A) The contents of the current directory
   * B) The contents of the root directory
   * C) Your home directory's pathname
   * D) The working directory's absolute pathname
9. You're in `/home/username` and attempt to `cd` into a file named `notes.txt` in your current directory. What happens?
   * A) The file `notes.txt` opens in the default text editor
   * B) The terminal displays an error message
   * C) The command is successful, and `notes.txt` becomes the current directory
   * D) The command deletes `notes.txt`
10. What is the effect of invoking `cd ././././`?
    * A) It moves you up four levels in the filesystem.&#x20;
    * B) It generates an error message, as the command is invalid.
    * C) It has no effect, as it essentially changes the directory to itself.
    * D) It takes you to the root directory.

<details>

<summary>Answers to exercises</summary>

1. &#x20; C
2. &#x20; A
3. &#x20; C
4. &#x20; A and B
5. &#x20; B
6. &#x20; A, B, and C
7. &#x20; C
8. &#x20; D
9. &#x20; B
10. C

</details>
