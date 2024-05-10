# Creating Files and Directories

## Creating Directories

Creating directories is done with the mkdir command. This commandThe command to create a new directory is `mkdir. This command is as straighforward as it gets` command followed by the names one of or more directories you want to create. For example, to create `dir1`:&#x20;

```bash
mkdir dir1
```

To create `dir2`, `dir3`, and `dir4`:

```bash
mkdir dir2 dir3 dir4
```

{% hint style="warning" %}
#### Creating a directory with whitespace in its name

Suppose we want to create a directory named `assignment 1`. As you can probably guess, invoking:

```bash
mkdir assignment 1
```

will not work; it'll create two directories--`assignment`, and `1`. A simple solution is to enclose the directory name in quotation marks:

```bash
mkdir "assignment 1"
```

This will create a single directory named `assignment 1`.
{% endhint %}





{% hint style="info" %}
**Special Characters**

Whitespace

Quoting special characters

Backslash

Single quotation marks

Special characters, which have a special meaning to the shell, are discussed in “Filename Generation/Pathname Expansion” on page 152. These characters are mentioned here so you can avoid accidentally using them as regular characters until you understand how the shell interprets them. Avoid using any of the following characters in a filename (even though emacs and some other programs do) because they make the file harder to refer- ence on the command line:

&;|\*?'"‘\[]\()$<>{}#/\\!\~

Although not considered special characters, RETURN, SPACE, and TAB have special meanings to the shell. RETURN usually ends a command line and initiates execution of a command. The SPACE and TAB characters separate tokens (elements) on the command line and are collectively known as whitespace or blanks.

If you need to use a character that has a special meaning to the shell as a regular char- acter, you can quote (or escape) it. When you quote a special character, you prevent the shell from giving it special meaning. The shell treats a quoted special character as a regular character. However, a slash (/) is always a separator in a pathname, even when you quote it.

To quote a character, precede it with a backslash ( \\). When two or more special char- acters appear together, you must precede each with a backslash (for example, you would enter \*\* as \\\*\\\*). You can quote a backslash just as you would quote any other special character—by preceding it with a backslash (\\\\).

Another way of quoting special characters is to enclose them between single quota- tion marks: '\*\*'. You can quote many special and regular characters between a pair

of single quotation marks: 'This is a special character: >'. The regular characters are interpreted as usual, and the shell also interprets the special characters as regular characters.

The only way to quote the erase character (CONTROL-H), the line kill character (CONTROL-U), and other control characters (try CONTROL-M) is by preceding each with a CONTROL-V. Single quotation marks and backslashes do not work. Try the following:

$ echo 'xxxxxxCONTROL-U'\
$ echo xxxxxxCONTROL-VCONTROL-U
{% endhint %}

## Creating Files

There are numerous commands you can use to create files. We'll cover two: `touch`, and `emacs`.&#x20;

### touch

The simplest way to create a file is via the `touch` command. Simply invoke `touch` followed by the names of one or more files you want to create. For example:

```bash
touch file1 file2 file3
```

Note that if one of the files supplied as an argument to `touch` already exists, `touch` will update its last modification timestamp to the current time.&#x20;

The limitation with `touch` is that it cannot be used to view or edit files. It is strictly for creating new, empty files or for updating the timestamps of existing files.

### **emacs**

If your goal is to create a file and immediately begin working in it, your best bet is to do so via a text editor like Emacs. Invoke `emacs` followed by the name of the file you want to create, and the file will be created and opened in Emacs:

```bash
emacs file1
```

{% hint style="warning" %}
Technically, the file is not actually created when you invoke Emacs. Emacs creates a temporary buffer in memory. The physical file is only created on disk when you save your changes within Emacs. This is done by pressing `Ctrl + x` followed by `Ctrl + s`.
{% endhint %}
