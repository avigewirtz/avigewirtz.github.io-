# ls (List Directory Contents)

The `ls` command is used to list the contents (files and directories) of a directory. Here we'll cover it's basic usage and and some commonly used options.

* [ ] A
* [ ] B&#x20;
* [ ] C
*

#### Basic usage

The most basic use case is to list the names of the files and directories in the working directory. To do so, simply invoke:

```
ls
```

#### Displaying Hidden Files

By default `ls` does not display [hidden](../../linux-operating-system/filesystem/notable-directories.md#hidden-files-directories) files (i.e., files that begin with a `.`). To include hidden entries in the directory listing, use the -a option:

```
ls -a
```

#### Long Listing Format

You can also use ls to display the metadata about the file, such as the file type, owner, and last modification time. To do so, use the -l option:

```bash
ls -l
```

Let's go over the output one by one:

file type, permissions, number of hard links, owner, group, size, last modification date, and name. &#x20;

#### Displaying the Contents of Another Directory

To list the contents of a directory other than your working directory, simple provide its pathname as an argument to ls. For example, to list the contents of /var, invoke:

```
ls /var
```



### Exercises

<details>

<summary>1. List the contents of the working directory</summary>



</details>

List the contents of the working directory:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.10.51 PM.png" alt=""><figcaption></figcaption></figure>

If you examine the output of this listing, you'll notice that the hidden files/directories (_**.**_, _**..**_, and _.git_) _are_ displayed, even though the `-a` option was not used. This is because on Armlab, `ls` is [aliased](../useful-command-line-features.md#aliases) to `ls -a`.

If you want to avoid alias expansion, you can prefix the command with a \ (backward slash):&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.50.55 PM.png" alt=""><figcaption></figcaption></figure>

Notice that hidden entries are not displayed this time.&#x20;

2. List the contents of the working directory in long format:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.11.18 PM.png" alt=""><figcaption></figcaption></figure>

3. List the contents of `/var`:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.11.29 PM.png" alt=""><figcaption></figcaption></figure>

4. List the contents of _/u_: &#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.11.40 PM.png" alt=""><figcaption></figcaption></figure>

Notice that the _/u_ directory contains the home directories of all regular Armlab users.&#x20;

5. List the contents of the root directory: &#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.11.54 PM.png" alt=""><figcaption></figcaption></figure>

These are important directories that are rarely accessed by anyone other than the system administrator.\
