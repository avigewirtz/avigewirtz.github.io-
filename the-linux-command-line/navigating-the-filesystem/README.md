# Navigating the Filesystem

To effectively navigate the Linux filesystem, you need to be familiar with three commands: `pwd`, `ls`, and `cd`. These commands are perhaps the most commonly used Bash commands, so it is worth your while to make the extra effort to master them.

## **`pwd` - A Sense of Location**

Whenever you're using the command line, bash is always positioned somewhere in the filesystem. This location is known as your (or, more accurately, Bash's) _working directory_.

You can find out your current working directory by invoking `pwd` (**p**rint **w**orking **d**irectory), which displays the absolute pathname of your working directory on stdout. By default, your working directory will be your home directory, which on Armlab is `/u/yourNetID`. When I invoke `pwd` on Armlab, I get the following output:

```bash
$ pwd
/u/sgewirtz
$
```

As we'll soon see, you can change your working directory with the `cd` command.

{% hint style="success" %}
On Armlab, your working directory is displayed in the [shell prompt](../warm-up-commands.md#shell-prompt), between the colon (:) and dollar ($) sign. Thus, you can determine what your working directory is without invoking `pwd`.&#x20;
{% endhint %}

## **`ls` - A Sense of Surroundings**

Knowing where you are in the filesystem is important, but in order to navigate, you also need to be familiar with what's around you. The `ls` (**l**i**s**t) command can be used to list the contents of any directory in the filesystem. &#x20;

#### Basic usage

The most basic usage of `ls` is to list the names of the files and directories in the working directory. To do so, invoke `ls` without arguments:

```bash
~$ ls 
A1	A2	CLI_playground
~$ 
```

#### Displaying Hidden Files

By default, `ls` does not display [hidden](broken-reference) entries (i.e., files and directories whose names begin with a `.`, such as `.bashrc`). To include hidden entries in the directory listing, use the `-a` option:

```bash
~$ ls 
.      .bashrc     A1     CLI_playground
..     .emacs	   A2
~$ 
```

{% hint style="warning" %}
On Armlab, '`ls'` is aliased to `'ls -a --color=always'`(see [Aliases](broken-reference)). Thus, an invocation of `ls` will display hidden entries. You can avoid alias expansion by prefixing the command with a '`\'` (e.g., `\ls`). If you invoke `ls` in this manner, you'll see that hidden entries are not displayed.&#x20;
{% endhint %}

#### Displaying file metadata

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

Let's break down the output using `README.md` as an example:&#x20;

*   **-rw-------.**&#x20;

    &#x20;   The file's access permissions. This will be covered in F[ile and Directory Access Permissions](../file-and-directory-access-permissions.md).&#x20;
*   **1**

    &#x20;   Number of hard links. You can safely ignore this column.&#x20;
*   **sgewirtz**&#x20;

    &#x20;   Name of the user who owns the file.&#x20;
*   **utemper**&#x20;

    &#x20;   Name of the group that owns the file.&#x20;
*   **17**

    &#x20;   Size of the file's contents in bytes.&#x20;
*   **Oct 12 14:35**

    &#x20;   Date and time the file was last modified.&#x20;

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

## **`cd` - Relocating**

You can change your working directory using the `cd` (**c**hange working **d**irectory) command. Its basic syntax is:

```bash
cd DIRECTORY_PATHNAME
```

`DIRECTORY_PATHNAME` refers to either the absolute or relative pathname of the target directory (see [Pathnames](../filesystem.md#pathnames)).

#### Example&#x20;

As we mentioned earlier, the default working directory is your home directory, which on Armlab is `/u/yourNetID`. Suppose we want to change our working directory to `/usr/bin` (Figure 12).&#x20;

<figure><img src="../../.gitbook/assets/filesystem10.17 (7).png" alt=""><figcaption></figcaption></figure>

Using its absolute pathname, we'd invoke:

```bash
cd /usr/bin
```

The "journey" begins at the root directory (Figure 14).&#x20;

<figure><img src="../../.gitbook/assets/Group 43.png" alt=""><figcaption></figcaption></figure>

Using it's relative pathname, the journey begins at the working directory. Hence, we need to navigate up to the root directory and then descend into `usr/bin`. Recall that `..` represents the parent directory. Thus, the command is:

```bash
cd ../../usr/bin
```

<figure><img src="../../.gitbook/assets/filesystem10.17 (6).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
To navigate to a directory, you must have appropriate access permissions. This will be covered in [File and Directory Access Permissions](../file-and-directory-access-permissions.md). If you try to navigate to a directory for which you don't have appropriate access permissions, you'll get a "permission denied" error. This will be the case if, for example, we try to navigate to another user's home directory, such as`/u/bwk`:

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

### **Useful Shortcuts**

* **Going home**: If you invoke `cd` without arguments, it'll take you to your home directory.&#x20;
* **Returning to the last working directory**. `cd -` (hyphen) returns you to your previous working directory.&#x20;
* **Tilde (`~`):** You can use the tilde character as a shortcut for your home directory. For example,  `cd ~/A1` is equivalent to `cd /u/yourNetID/A1`.
* **Tab Completion**: If you start typing an directory name and press Tab, Bash will attempt to auto-completes the directory name. This will save you time and reduce typos.

## Exercises

**Note**: For the following questions, assume the working directory is `/u/yourNetID`, unless otherwise stated.&#x20;

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
