# Pathnames

The location of a file in the directory hierarchy can be expressed by specifying its path from the root directory. Such paths are built by listing all directory names starting from the root, separated by slashes, followed by the file's name. This is called an _absolute pathname_. For example:`/u/sgewirtz/CLI_playground/the_odyssey.txt` means start at root directory, go to u, then sgewirtz, then CLI\_playground, and there you'll find the\_odyssey.txt. Since no two files in the same directory may have the same name, the absolute pathname uniquely identifies its location in the directory hierarchy. Figure 3 shows several examples of absolute pathnames.

## Working Directory

Listing full pathnames can become cumbersome. For that reason, we have the concept of a working directory, which can be thought of as the directory you're currently "in." When you specify a path that does not begin with `/`, it is interpreted as starting from the working directory. This is known as a _relative pathname_. By default, your working directory will be your home directory, but you can change it using the `cd` command, which we'll cover in [Navigating the Filesystem](../../navigating-the-filesystem/#cd-relocating). &#x20;

Suppose our working directory is `/u/sgewirtz` and we invoke `emacs .bashrc`. The system will look for `.bashrc` in `/u/sgewirtz`.



{% hint style="info" %}
**Tilde notation**

**Home directories often occur in pathnames.Can abbrevieate with tilde. Will be expanded by shell.** Note that pathname beggining with tilde is absolute pathname.&#x20;

* \~/ your home directory
* \~

Tilde is a shell concept, not an OS concept.&#x20;
{% endhint %}
