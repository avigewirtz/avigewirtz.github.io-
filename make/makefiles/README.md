# Makefiles

To use Make to build a program, you need to create a file in your project directory called a _makefile_, which is essentially a textual representation of your program's dependency graph that tells make how and when to compile and link your program. A makefile can be named 'makefile' or 'Makefile' (or even 'GNUmakefile', if you're using GNU Make). GNU recommends 'Makefile'.&#x20;

A makefile primarily consists of _rules_, each of which tells make whether or not a file has to be built, and if so, how to build it. A rule typically has the following syntax:&#x20;

```
target: dependencies
<tab> command
```

Let's break this down:

* **Target**: This is usually a file that the rule will build--typically an object file (`.o`) or an executable.
* **Dependencies**: These are the files needed to build the target. If the target is an executable, then the dependencies are typically object files. If the target is an object file, then the dependencies are typically C source (.c) and header (.h) files. &#x20;
* **Command**: the command that builds the target file. Note that the command must be preceded by a tab.&#x20;

{% hint style="danger" %}
One of the most common errors in writing Makefiles is preceding the command with spaces (ASCII character 32) instead of a tab (ASCII character 9). This can also happen if your text editor represents a tab as spaces. This will lead to the following error:

&#x20;  \*\*\* missing separator.  Stop.
{% endhint %}
