# Creating Directories

The _mkdir_ command is used to create directories (also known as folders). Its syntax is as follows: <mark style="color:red;">**`mkdir`**</mark><mark style="color:blue;">**`DIRECTORY(IES)`**</mark>.

The <mark style="color:blue;">**`DIRECTORY(IES)`**</mark> parameter represents the name(s) of the directories you want to create. You can specify multiple directory names, each separated by spaces. Before creating directories, let's review filenames.&#x20;

As stated [earlier](../linux/filesystem/filenames.md), Linux filesystems impose very few restrictions on file and directory names. That said, not all valid filenames are equal. Some are poorly suited for the shell environment and are best avoided. The following naming suggestions will make your life on the command line easier:&#x20;

1. Avoid using whitespace or special characters in filenames, since such files are harder to reference on the command line. The following characters are special:&#x20;

{% code overflow="wrap" %}
```
&   ;   |   *   ?   '   "   ‘   [   ]   (   )   $   <   >   {   }   #   /   \   !   ~
```
{% endcode %}

2. Avoid beginning a file or directory name with a **-** (hyphen) or a **.** (period). This is because a leading hyphen might cause the shell to confuse the file/directory for a command line option, and a leading period will make the file/directory hidden.&#x20;

### Exercises

1. Create _dir1_:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 3.28.15 PM.png" alt=""><figcaption></figcaption></figure>

2. Create _dir2_, _dir3_, and _dir4_:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 3.28.24 PM.png" alt=""><figcaption></figcaption></figure>

3. Create a directory named _bad name_:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 3.28.36 PM.png" alt=""><figcaption></figcaption></figure>

As you can see, instead of creating one directory named "_bad name_", Bash created two directories: "_bad_" and "_name_". This is because Bash interprets each string as a distinct argument. If you want to use whitespace in a directory name escape the whitespace. There are various methods to achieve this. One is by enclosing the argument in quotes: \


<figure><img src="../.gitbook/assets/Screenshot 2023-05-09 at 5.46.36 PM.png" alt=""><figcaption></figcaption></figure>

Now _bad name_ appears as a single directory.

