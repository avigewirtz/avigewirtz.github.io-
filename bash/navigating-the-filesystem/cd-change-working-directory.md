# cd  (Change Working Directory)

### Syntax: <mark style="color:red;">`cd`</mark><mark style="color:blue;">`DIRECTORY`</mark>&#x20;

<mark style="color:blue;">**DIRECTORY**</mark> is the target directory you want to navigate to, and it can be specified using either an absolute or relative pathname. If the <mark style="color:blue;">**DIRECTORY**</mark> argument is not supplied, `cd` defaults to your home directory.&#x20;

Before we begin with examples, let's review some important notation:

* **`..`** (dot dot) refers to the parent of the working directory. You'll need this to travel "up" when using relative pathnames.
* **`~`** (tilde) refers to the home directory. Knowing this will save you a lot of time when typing absolute pathnames.

{% hint style="info" %}
In the following examples, the absolute pathname of the working directory is highlighted in the [shell prompt](../warm-up-commands.md#shell-prompt). This is to enable you to determine the location of the working directory at all times and to compare the location before and after each command is executed.
{% endhint %}

### Examples

1. Make `/usr/bin` your working directory; use its absolute pathname:&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.09.04 PM.png" alt=""><figcaption></figcaption></figure>

The working directory is now `/usr/bin`, as the shell prompt confirms.

2. Make your home directory your working directory:

The simplest way to change to your home directory is to invoke `cd` without arguments:&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.09.21 PM.png" alt=""><figcaption></figcaption></figure>

However, you can also invoke it with `~` as the argument:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 11.26.15 PM.png" alt=""><figcaption></figcaption></figure>

3. Make `/usr/bin` your working directory again; this time use the relative pathname:&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.09.32 PM.png" alt=""><figcaption></figcaption></figure>

Comparing examples 1 and 3, which are functionally identical, you’ll notice that the absolute pathname (`/usr/bin`) is shorter than the relative pathname (`../../usr/bin`). A simple trick is that if a relative pathname contains the root directory, the absolute pathname counterpart is certainly shorter.&#x20;

4. Make `.git` your working directory, using whichever pathname is shorter:

The absolute pathname (`~/bash_practice/.git`) is clearly shorter than the relative pathname (`../../u/yourNetID/bash_practice/.git`).

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.09.41 PM.png" alt=""><figcaption></figcaption></figure>

5. Change your working directory back to your last working directory:

Neat shortcut: `-` (hyphen) refers to the last working directory. Thus, you can invoke the command like so:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.09.52 PM.png" alt=""><figcaption></figcaption></figure>

6. Once again, make your home directory your working directory:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.09.21 PM.png" alt=""><figcaption></figcaption></figure>

7. Change your working directory to `the_odyssey.txt`:

That was intended to fool you. You cannot make `the_odyssey.txt` your working directory since it is a file.&#x20;

8. Change your working directory to `bwk`:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.10.15 PM.png" alt=""><figcaption></figcaption></figure>

Our request to access `bwk` was denied, since `bwk` is another user's home directory--Professor Brian Kernighan, to be specific. We will discuss file and directory access permissions in more detail in a later section.&#x20;

9. Change your working directory to `/lost+found`:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.10.26 PM.png" alt=""><figcaption></figcaption></figure>

Our request was denied here as well, since `lost+found` is an important directory that only the system administrator is authorized to access. \
