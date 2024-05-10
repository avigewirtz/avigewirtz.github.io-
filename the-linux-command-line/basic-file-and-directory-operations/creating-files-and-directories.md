# Creating Files and Directories

### Creating Directories

To create a directory, type `mkdir` (**m**a**k**`e` **dir**ectory/ies) followed by the name of the directory you want to create. For example:

```bash
mkdir dir1
```

This creates `dir1` in the working directory. To create multiple directories, supply the name of each directory you want to create as an argument to `mkdir`. For example:&#x20;

```bash
mkdir dir2 dir3 dir4
```

This creates  `dir2`, `dir3`, and `dir4` in the working directory.

{% hint style="warning" %}
**Creating a Directory With Whitespace in Its Name**

Suppose we want to create a directory named `assignment 1`. As you can probably guess, invoking:

```bash
mkdir assignment 1
```

will not work; it'll create two directories--`assignment`, and `1`. A simple solution is to enclose the directory name in quotation marks:

```bash
mkdir "assignment 1"
```

This will create a single directory named `assignment 1`.&#x20;
{% endhint %}

### Creating Files

There are numerous commands for creating files. We'll cover two: `touch`, and `emacs`.&#x20;

### touch

The simplest way to create a file is via the `touch` command. Simply type touch followed by the name of the file you want to create. For example:

```bash
touch file1
```

This creates file1 in the working directory. To create multiple files, supply the name of each file you want to create as an argument to `touch`. For example:&#x20;

```bash
touch file2 file3 file4
```

{% hint style="info" %}
If one of the files supplied as an argument to `touch` already exists, `touch` will update its access and modification times. Please refer to the `touch` manpage for more details.&#x20;
{% endhint %}

### **emacs**

The limitation of `touch` is that it cannot be used to view or edit files. It is strictly for creating new, empty files or for updating the timestamps of existing files. If your goal is to create a file and immediately begin working in it, your best bet is to do so via a text editor like Emacs. Invoke `emacs` followed by the name of the file you want to create. For example:

```bash
emacs file1
```

{% hint style="info" %}
Technically, the file is not actually created. Emacs creates a temporary buffer in memory. The physical file is only created on disk when you save your work within Emacs. This is done by pressing `Ctrl + x` followed by `Ctrl + s`.
{% endhint %}
