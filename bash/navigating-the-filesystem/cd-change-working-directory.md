# cd (Change Working Directory)

The `cd` command is used to change the working directory. Its syntax is as follows: &#x20;

```bash
cd DIRECTORY_PATHNAME
```

`DIRECTORY_PATHNAME` represents the absolute or relative pathname of the directory you want to make your working directory. For example, if your current working directory is \~ (i.e., _/u/yourNetID_) and you want to change your working directory to _/usr/bin_, you can invoke it's absolute pathname:

```bash
cd /usr/bin
```

Or you can specify it's relative pathname:

```bash
cd ../../usr/bin
```

Recall that `..` represents the parent directory.&#x20;

If you invoke `cd` without arguments, it'll default to your home directory:&#x20;

```
cd
```

{% hint style="info" %}
In the following examples, the absolute pathname of the working directory is highlighted in the shell prompt, enabling you to contrast the value of the working directory before and after each command is executed.
{% endhint %}

### Exercises

1. Make _/usr/bin_ your working directory; use its absolute pathname:&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.09.04 PM.png" alt=""><figcaption></figcaption></figure>

2. Make your home directory your working directory:

The simplest method is to invoke `cd` without arguments:&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.09.21 PM.png" alt=""><figcaption></figcaption></figure>

3. Make _/usr/bin_ your working directory again, this time using the relative pathname:&#x20;

To navigate to /usr/bin using the relative pathname, you need to travel "up" the hierarchy. To do this, recall that [**`..`**](../../linux-operating-system/filesystem/notable-directories.md#the-.-dot-and-..-dot-dot-directories) (dot dot) refers to the parent directory.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.09.32 PM.png" alt=""><figcaption></figcaption></figure>

4. Make _.git_ your working directory, using whichever pathname is shorter:

The absolute pathname (`~/bash_practice/.git`) is clearly shorter than the relative pathname (`../../u/yourNetID/bash_practice/.git`).

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.09.41 PM.png" alt=""><figcaption></figcaption></figure>

5. Change your working directory back to your last working directory:

Neat shortcut: - (hyphen) refers to the last working directory. Thus, you can invoke the command like so:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.09.52 PM.png" alt=""><figcaption></figcaption></figure>

6. Once again, make your home directory your working directory:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.09.21 PM.png" alt=""><figcaption></figcaption></figure>

7. Change your working directory to _the\_odyssey.txt_:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-09 at 5.12.33 PM.png" alt=""><figcaption></figcaption></figure>

This example was intended to fool you. You cannot make the\_odyssey.txt your working directory since it is a file.&#x20;

8. Change your working directory to /u/_bwk_:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.10.15 PM.png" alt=""><figcaption></figcaption></figure>

Our request to access _/u/bwk_ was denied since it is another user's home directory--Professor Brian Kernighan, to be specific. We will discuss file and directory access permissions in more detail in a later section.&#x20;

9. Change your working directory to _/lost+found_:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.10.26 PM.png" alt=""><figcaption></figcaption></figure>

Our request was denied here as well, since _/lost+found_ is an important directory that only the system administrator has access to. \
