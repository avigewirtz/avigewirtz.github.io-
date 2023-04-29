# ls (List Directory Contents)

### Syntax:  <mark style="color:red;">**`ls`**</mark><mark style="color:green;">**`OPTION(S)`**</mark><mark style="color:blue;">**`DIRECTORY(IES)`**</mark>

The <mark style="color:red;">**`ls`**</mark> command lists the contents (files and subdirectories) of the specified <mark style="color:blue;">**`DIRECTORY(IES`**</mark>. By default, hidden files/directories are not displayed. If the <mark style="color:blue;">**`DIRECTORY(IES)`**</mark>argument is not supplied, <mark style="color:red;">**`ls`**</mark> defaults to the working directory.&#x20;

### Common options:

* **`-a`**:  Includes [hidden](broken-reference) files/directories in the listing.&#x20;
* &#x20;**`-l`**: Display the long listing for each entry, in the following format: file type, permissions, number of hard links, owner, group, size, last modification date, and name. &#x20;

### Examples:

1. List the contents of the working directory:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.10.51 PM.png" alt=""><figcaption></figcaption></figure>

If you examine the output of this listing, you'll notice that the hidden files/directories (`.`, `..`, and `.git`) _are_ displayed, even though the `-a` option was not used. This is because the command was executed on armlab, where `ls` is aliased to `ls -a`.

An alias is simply a substitute for a command. It can be thought of as a shortcut, normally used for abbreviating long commands or for adding default arguments to commands. Thus, when you invoke `ls` on armlab, you’re really invoking `ls -a`. We will discuss aliases in more detail in a later section.&#x20;

If you don't want to avoid alias expansion, you can prefix the command with a \ (backward slash). This will ensure ls is executed by itself, and not ls-l.&#x20;

2. List the contents of your working directory; avoid alias expansion:&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.50.55 PM.png" alt=""><figcaption></figcaption></figure>

Notice that hidden entries are not displayed this time.&#x20;

3. List the contents of your working directory in long format:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.11.18 PM.png" alt=""><figcaption></figcaption></figure>

4. List the contents of `/var`:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.11.29 PM.png" alt=""><figcaption></figcaption></figure>

5. List the contents of `/u`: &#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.11.40 PM.png" alt=""><figcaption></figcaption></figure>

Notice that the `/u` directory contains the home directories of all regular armlab users.&#x20;

6. List the contents of the root directory: &#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.11.54 PM.png" alt=""><figcaption></figcaption></figure>

These are important directories that are rarely accessed by anyone other than the system administrator.

\
\


\
\
