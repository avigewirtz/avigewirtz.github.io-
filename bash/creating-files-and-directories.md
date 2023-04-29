# Creating Files and Directories

As stated [earlier](../linux/filesystem/filenames.md), Linux filesystems impose very few restrictions on file and directory names. That said, not all legal filenames are equal. Some are poorly suited for the shell environment and are best avoided. The following naming suggestions will make your life on the command line easier:&#x20;

1. Avoid using whitespace or special characters in filenames, since such files are harder to reference on the command line. The following characters are special:&#x20;
   * &   ;   |   \*   ?   '   "   ‘   \[   ]   (   )   $   <   >   {   }   #   /   \   !   \~
2. Avoid beginning a file or directory name with a `-` (hyphen) or `.` (period). This is because a leading hyphen can cause the shell to confuse the file/directory for a command line option, and a leading period will make the file/directory hidden.&#x20;

It is often desirable for filenames to be portable, since you might want to transfer files from one computer to another––for example, you might want to transfer files between armlab (Linux) and your PC (Windows or Mac). To ensure portability, follow these rules:&#x20;

* Use case-insensitivity when naming files–-that is, treat `Hello.c` and `hello.c` as equivalent filenames (and therefore disallowed in the same directory). Windows and macOS are both case-insensitive, so this is particularly important. &#x20;
* Avoid using extremely long filenames (i.e., close to 255 bytes), since some file systems impose shorter length limits.&#x20;
* Only use characters from the POSIX Portable Filename Character Set:&#x20;

A B C D E F G H I J K L M N O P Q R S T U V W X Y Z

a b c d e f g h i j k l m n o p q r s t u v w x y z

0 1 2 3 4 5 6 7 8 9 . \_ -



## Creating directories

### Syntax: <mark style="color:red;">`mkdir`</mark><mark style="color:green;">`OPTION(S)`</mark><mark style="color:blue;">`DIRECTORY(IES)`</mark> &#x20;



Creates directory(ies).

mkdir (make directory(ies))

\
Examples

1. Create `dir1`:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 3.28.15 PM.png" alt=""><figcaption></figcaption></figure>

2. Create `dir2`, `dir3`, and `dir4`:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 3.28.24 PM.png" alt=""><figcaption></figcaption></figure>

3. Create a directory named `bad name`:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 3.28.36 PM.png" alt=""><figcaption></figcaption></figure>

As you can see, instead of creating one directory called `bad name`, Bash created two directories: `bad` and `name`. This is because `mkdir` interprets each of these strings as a separate argument. If you want to use whitespace in a directory name, you must enclose the name in double or single quotes or escape the whitespace:\


<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 3.28.49 PM.png" alt=""><figcaption></figcaption></figure>

Now `bad name` appears as a single directory.

## Creating files

There are numerous ways you can create files on the command line. The choice between using `touch` and a text editor depends on your needs. If you need to create an empty file quickly or update the timestamp of an existing file, `touch` is a good choice. Whichever option you choose, the syntax for creating the file is the same: Type the editor's name or `touch` followed by the filename you want to create.&#x20;

### Examples

1. Create `file1`:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.07.49 PM.png" alt=""><figcaption></figcaption></figure>

2. Create `file2` in `dir2`:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.08.03 PM.png" alt=""><figcaption></figcaption></figure>

3. Create `file3` and `file4`:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.11.32 PM.png" alt=""><figcaption></figcaption></figure>

