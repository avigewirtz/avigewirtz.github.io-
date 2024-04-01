# Navigating the filesystem

To effectively navigate the Linux filesystem, you need to be familiar with three commands: `pwd`, `ls`, and `cd`. These commands are perhaps the most commonly used Bash commands, so it is worth your while to make the extra effort to master them.

## **`pwd` - A sense of Location**

Whenever you're using the command line, bash is always positioned somewhere in the filesystem. This location is known as your (or, more accurately, Bash's) working directory. (See Working Directory.)

You can find out your current location by invoking `pwd`, which displays the absolute pathname of your working directory on stdout. By default, your working directory will be your home directory, which on armlab is /u/yourNetID:

```
~$ pwd
/u/yourNetID
```

As we'll see soon, you can change your working directory with the `cd` command.

{% hint style="success" %}
On Armlab, the working directory is displayed in the [shell prompt](../warm-up-commands.md#shell-prompt), between the colon (:) and dollar ($) sign.
{% endhint %}

## **`ls` - A sense of surroundings**

Knowing where you are is important, but in order to navigate, you also need to know what's around you. The `ls` (list) command can be used to list the contents of any directory in the filesystem. &#x20;

#### Basic usage

The most basic usage of `ls` is to list the names of the files and directories in the working directory. To do so, simply invoke:

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

For now, you can safely ignore most of the information output by `ls -l`, but note that the long form lists a date and time indicating the last time the file was modified. The number before the date is the _size_ of the file, in bytes.[3](https://www.learnenough.com/command-line-tutorial/manipulating\_files#cha-2\_footnote-3)



#### Displaying the Contents of Another Directory

You can use ls to list the contents of a directory other than your working directory by providing the directory's pathname as as argument to ls. For example, to list the contents of `/var,`:

```
ls /var
```

LS \*.TXT

Here `*.txt` (read “star dot tee-ex-tee”) automatically expands to all the filenames that match the pattern “any string followed by .txt”.

## **`cd` - Moving to a Different Location**

You can change your working directory via the `cd` (change directory) command. The basic syntax is&#x20;

```
cd DIRECTORY_PATHNAME
```

where DIRECTORY\_PATHNAME is the absolute or relative pathname of the target directory. For example, suppose you're in your home directory, and you want to navigate to the decomment directory, which contains the files for assignment 1. To do so,&#x20;

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

#### Question with filename that has spaces

{% hint style="info" %}
**Tab completion**

Bash support _tab completion_, which involves automatically completing a word if there’s only one valid match on the system. For example, if the only file starting with the letters “tes” is `test_file`, we could create the command to remove it as follows:

```
 $ rm tes⇥
```

where ⇥ is the tab key ([Table 1.1](https://www.learnenough.com/command-line-tutorial#table-keyboard\_symbols)). The shell would then complete the filename, yielding `rm test_file`. Especially with longer filenames (or directories), tab completion can save a huge amount of typing. It also lowers the [_cognitive load_](https://en.wikipedia.org/wiki/Cognitive\_load), since it means you don’t have to remember the full name of the file—only its first few letters.

If the match is ambiguous, as would happen if we had files called `foobarquux` and `foobazquux`, the word will be completed only as far as possible, so

```
 $ ls foo⇥
```

would be completed to

```
 $ ls fooba
```

If we then hit tab _again_, we would see a list of matches:

```
 $ ls fooba⇥
 foobarquux foobazquux
```

We could then type more letters to resolve the ambiguity, so typing the `r` after `fooba` and hitting `⇥` would yield

```
 $ ls foobar⇥
```

which would be completed to `foobarquux`. This situation is common enough that experienced command-line users will often just hit something like `f⇥⇥` to get the shell to show all the possibilities:

```
 $ ls f⇥⇥
 figure_1.png foobarquux  foobazquux
```

Additional letters would then be typed as usual to resolve the ambiguity.
{% endhint %}

####

#### Tips for Using `cd`

* **Tab Completion**: Start typing the directory name and press Tab; the system auto-completes the directory name, saving time and reducing typos.
* **Using Quotes**: If a directory name contains spaces, enclose the name in quotes (e.g., `cd "My Documents"`).

## Exercises

For the following questions, unless otherwise stated, assume the working directory is /u/yourNetID.

For the following questions, assume no aliases are being used.&#x20;

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
