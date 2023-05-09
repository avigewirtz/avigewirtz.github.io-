# ls (List Directory Contents)

The `ls` command is used to list the contents (files and subdirectories) of directories. Its syntax is as follows: <mark style="color:red;">**`ls`**</mark><mark style="color:green;">**`OPTION(S)`**</mark><mark style="color:blue;">**`DIRECTORY(IES)`**</mark>

The contents of the specified <mark style="color:blue;">**`DIRECTORY(IES)`**</mark> will be listed. If <mark style="color:blue;">**`DIRECTORY(IES)`**</mark>argument is not specified, `ls` defaults to the working directory. By default, `ls` does not display hidden files/directories. &#x20;

### Common options:

* **`-a`**:  Includes [hidden](broken-reference) files/directories in the listing.&#x20;
* &#x20;**`-l`**: Display the long listing for each entry, in the following format: file type, permissions, number of hard links, owner, group, size, last modification date, and name. &#x20;

### Exercises:

{% hint style="warning" %}
These exercises assume that the working directory is _\~/bash\_practice_.
{% endhint %}

1. List the contents of the working directory:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.10.51 PM.png" alt=""><figcaption></figcaption></figure>

If you examine the output of this listing, you'll notice that the hidden files/directories (_**.**_, _**..**_, and _.git_) _are_ displayed, even though the `-a` option was not used. This is because the command was executed on armlab, where `ls` is [aliased](../useful-command-line-features.md#aliases) to `ls -a`.

If you want to avoid alias expansion, you can prefix the command with a \ (backward slash):&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.50.55 PM.png" alt=""><figcaption></figcaption></figure>

Notice that hidden entries are not displayed this time.&#x20;

2. List the contents of your working directory in long format:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.11.18 PM.png" alt=""><figcaption></figcaption></figure>

3. List the contents of `/var`:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.11.29 PM.png" alt=""><figcaption></figcaption></figure>

4. List the contents of _/u_: &#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.11.40 PM.png" alt=""><figcaption></figcaption></figure>

Notice that the _/u_ directory contains the home directories of all regular armlab users.&#x20;

5. List the contents of the root directory: &#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.11.54 PM.png" alt=""><figcaption></figcaption></figure>

These are important directories that are rarely accessed by anyone other than the system administrator.\
