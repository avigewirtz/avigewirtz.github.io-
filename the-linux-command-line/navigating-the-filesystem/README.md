# Navigating the Filesystem

To effectively navigate the Linux filesystem, you need to be familiar with three commands: `pwd`, `ls`, and `cd`. These commands are perhaps the most commonly used Bash commands, so it is worth your while to make the extra effort to master them.

### **`pwd` - A Sense of Location**

Recall that whenever you're using the command line, `bash` is always positioned somewhere in the filesystem. This location is known as your (or, more accurately, Bash's) _working directory_.

You can find out your current working directory by invoking `pwd` (**p**rint **w**orking **d**irectory), which displays the absolute pathname of your working directory on stdout. By default, your working directory will be your home directory, which on Armlab is `/u/yourNetID`. When I invoke `pwd` on Armlab, I get the following output:

```bash
$ pwd
/u/sgewirtz
$
```

As we'll soon see, you can change your working directory with the `cd` command.

{% hint style="success" %}
On Armlab, your working directory is displayed in the [shell prompt](../warm-up-commands.md#shell-prompt), between the colon (:) and dollar ($) sign. Thus, you can determine what your working directory is without invoking `pwd`.
{% endhint %}

### **`ls` - A Sense of Surroundings**

Knowing where you are in the filesystem is important, but in order to navigate, you also need to be familiar with your surroundings. The `ls` (**l**i**s**t) command can be used to list the contents of any directory in the filesystem.

#### Basic usage

The most basic usage of `ls` is to list the files and directories in the working directory. To do so, just type `ls`:

```bash
~$ ls
.      .bashrc     A1     CLI_playground
..     .emacs	   A2     hello
~$ 
```

We see seven entries in the working directory. Recall that `.` is a reference to the directory itself, and `..` is a reference to the parent directory.

{% hint style="info" %}
By default, `ls` does not display [hidden](../a-tour-of-linux/filesystem.md#hidden-files) entries (i.e., those whose names begin with a `.`, such as `.bashrc`). To include hidden entries, you need to use the`-a` option (i.e., `ls -a`). The reason hidden entries were displayed in our listing is because on Armlab, '`ls`' is [aliased](../useful-command-line-features.md#aliases) to '`ls -a --color=always`'. (Note that `--color=always` causes regular files appear in black, directories in blue, and executable files in green).
{% endhint %}

**Displaying File Types**

In the previous listing, there was no indication what type of file each entry is. `ls` does not indicate what type of file each entry is. So, for example, In the previous listing, there's no indication of whether A1 is a file or a directory. To know what type of file each entry is, you can use the **`-F`** option, which shows regular files as usual, but directories with a / appended to them and executable files with a \*.

```bash
ls -F
```

Alternatively, you can use the `--color=always` option, which colors the output. Typically, regular files appear in black, directories in blue, and executable files in green or red:

```bash
ls --color=always
```

{% hint style="warning" %}
On Armlab, '`ls`' is [aliased](../useful-command-line-features.md#aliases) to '`ls -a --color=always`'. Thus, hidden entries and colored output is the default. Note: You can avoid alias expansion by prefixing the command with a `\` (e.g., `\ls`).
{% endhint %}

#### Displaying File Metadata

Each file and directory has associated metadata, such as access permissions, owner username, and last modification time. You can display the metadata using the `-l` option, which lists the directory's contents in long format:

```bash
~$ ls -l
total 14
drwx------  2 sgewirtz  utemper  218 Oct  16 14:28 A1
drwx------  2 sgewirtz  utemper  364 Oct  16 14:28 A2
drwx------  6 sgewirtz  utemper  192 Oct  12 14:36 CLI_playground
-rw-------  1 sgewirtz  utemper   17 Oct  12 14:35 README.md
~$
```

Let's break down the output using `README.md` as an example:

*   **-rw-------.**

    The file's access permissions. This will be covered in F[ile and Directory Access Permissions](../file-and-directory-access-permissions.md).
*   **1**

    Number of hard links. You can safely ignore this column.
*   **sgewirtz**

    Name of the user who owns the file.
*   **utemper**

    Name of the group that owns the file.
*   **17**

    Size of the file's contents in bytes.
*   **Oct 12 14:35**

    Date and time the file was last modified.

#### Displaying the Contents of Another Directory

To list the contents of a directory that is not your working directory, simply supply the target directory's pathname (absolute or relative) as an argument to `ls`. For example, to list the contents of `/var`:

```bash
$ ls /var
agentx    db        gopher      lock          net-snmp    run            tmp
cache     empty     kerberos    log           nis         singularity    yp
crash     ftp       lib         lost+found    opt         spool
adm       cvs       games       local         mail        preserve       srvmagt
$
```

### **`cd` - Relocating**

You can change your working directory using the `cd` (**c**hange working **d**irectory) command. Its basic syntax is:

```bash
cd DIRECTORY_PATHNAME
```

`DIRECTORY_PATHNAME` is either the absolute or relative pathname of the target directory (see [Pathnames](../a-tour-of-linux/filesystem.md#pathnames)).

#### Example

As we mentioned earlier, the default working directory is your home directory, which on Armlab is `/u/yourNetID`. Suppose we want to change our working directory to `/usr/bin` (Figure 12).

<figure><img src="../../.gitbook/assets/filesystem10.17 (7).png" alt=""><figcaption></figcaption></figure>

Using its absolute pathname, we'd invoke:

```bash
cd /usr/bin
```

The "journey" begins at the root directory (Figure 14).

<figure><img src="../../.gitbook/assets/Group 43.png" alt=""><figcaption></figcaption></figure>

Using it's relative pathname, the journey begins at the working directory. Hence, we need to navigate up to the root directory and then descend into `usr/bin`. Recall that `..` represents the parent directory. Thus, the command is:

```bash
cd ../../usr/bin
```

<figure><img src="../../.gitbook/assets/filesystem10.17 (6).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
To navigate to a directory, you must have appropriate access permissions. We'll cover this in [File and Directory Access Permissions](../file-and-directory-access-permissions.md). If you try to navigate to a directory for which you don't have appropriate access permissions, you'll get a "permission denied" error. This will be the case if, for example, you try to navigate to another user's home directory, such as`/u/bwk`:

```bash
~$ cd /u/bwk
-bash: cd: /u/bwk: Permission denied
~$
```
{% endhint %}

{% hint style="warning" %}
To navigate to a directory that includes whitespace in its name, you have to ensure that Bash treats the entire directory name as a single argument. This can be done by enclosing the directory name in quotes. For example:

```bash
cd "assignment 1"
```
{% endhint %}

#### **Useful Shortcuts**

* **Going home**: If you invoke `cd` without arguments, it'll take you to your home directory.
* **Returning to the last working directory**. `cd -` (hyphen) returns you to your previous working directory.
* **Tilde (`~`):** You can use the tilde character as a shortcut for your home directory. For example, `cd ~/A1` is equivalent to `cd /u/yourNetID/A1`.
* **Tab Completion**: If you start typing an directory name and press Tab, Bash will attempt to auto-completes the directory name. This will save you time and reduce typos.

### Exercises

**Note**: For the following questions, assume the working directory is `/u/yourNetID`, unless otherwise stated.

1. Which of the following commands lists the metadata of all files in the working directory, including hidden files?
   * A) `ls -a`
   * B) `ls -l`
   * C) `ls -la`
   * D) `ls -lh`
2. What does `cd ..` achieve?
   * A) It takes you to the parent of the working directory
   * B) It takes you to your home directory
   * C) It takes you to the root directory
   * D) It does nothing
3. Which of the following will happen if on Armlab you attempt to change your working directory to another user's home directory?
   * A) The command succeeds without issue
   * B) You are prompted for the other user's password
   * C) The command fails with a "Permission denied" error
   * D) You are successfully able to change into the directory, but it contains no files or subdirectories visible to you.
4. Which of the following lists the contents of the root directory? Mark all that apply.
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
9. `.bashrc` is a file in your current directory. You invoke `cd .bashrc`. What happens?
   * A) `.bashrc` opens in the default text editor
   * B) An error is returned, since `.bashrc` is not a directory
   * C) The command is successful
   * D) `.bashrc`
10. What is the effect of invoking `cd ././././`?
    * A) It moves you up four levels in the filesystem.
    * B) It generates an error message, as the command is invalid.
    * C) It has no effect, as it essentially changes the directory to itself.
    * D) It takes you to the root directory.

<details>

<summary>Answers to exercises</summary>

1. C
2. A
3. C
4. A and B
5. B
6. A, B, and C
7. C
8. D
9. B
10. C

</details>
