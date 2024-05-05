# Creating Files/Directories

## Creating Directories

To create a new directory, use the `mkdir` command followed by the name of the directory you want to create. For example, to create `dir1`:&#x20;

```bash
mkdir dir1
```

#### Creating multiple directories

Multiple directories can be created via a single invocation of `mkdir` by supplying multiple directory names as arguments. For example:

```bash
mkdir dir1 dir2 dir3
```

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

{% hint style="info" %}
**Good naming practice**\
When you consider both case sensitivity and escaping, a good rule of thumb is to keep your file names all lower case, with only letters, numbers, underscores and hyphens. For files there’s usually also a dot and a few characters on the end to indicate the type of file it is (referred to as the “file extension”). This guideline may seem restrictive, but if you end up using the command line with any frequency you’ll be glad you stuck to this pattern.
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
