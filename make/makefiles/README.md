# Makefiles

To use Make to build a program, you need to create a file in your project directory called a makefile, which is essentially a textual representation of your program's dependency graph that tells make how and when to compile and link your program. A makefile can be named 'makefile' or 'Makefile' (or even 'GNUmakefile', if you're using GNU Make). GNU recommends 'Makefile'.&#x20;

A makefile primarily consists of _rules_, each of which tells make whether or not a file has to be built, and if so, how to build it. A rule typically has the following syntax:&#x20;

```
target: dependencies
<tab> command
```

Let's break this down:

* **target**: This is usually a file that the rule will build--typically an object file (`.o`) or an executable.
* **dependencies**: These are the files needed to build the target. If the target is an executable, then the dependencies are typically object files. If the target is an object file, then the dependencies are typically C source (.c) and header (.h) files. &#x20;
* **command**: the command that builds the target file. Note that the command must be preceded by a tab.&#x20;

{% hint style="danger" %}
One of the most common errors in writing Makefiles is preceding the command with spaces (ASCII character 32) instead of a tab (ASCII character 9). This will lead to the following error:

&#x20;  \*\*\* missing separator.  Stop.
{% endhint %}

## Creating a makefile for testintmath

Let's jump right in and consider how to create a makefile for our testintmath program.&#x20;

#### Makefile version 0

First up is what we're calling Version 0. It's a bit unconventional – it does the job, but it's not the model of a well-crafted makefile. Think of it as our "what not to do" guide. By seeing the flaws and missteps in Version 0, you'll get a clearer picture of what makes a makefile effective and well-structured. Here's how it looks:

{% code title="Makefile version 0" %}
```
testintmath: testintmath.c intmath.c intmath.h
    gcc intmath.c testintmath.c -o testintmath
```
{% endcode %}

The first line declares a target `testintmath`, which depends on `testintmath.c`, `intmath.c`, and `intmath.h`. This means that if any of these files change, `make` will rebuild `testintmath`. The second line is the command that `make` will execute to build testintmath.&#x20;

Despite being functional, Version 0 is structurally flawed, since it re-compiles the entire program whenever a change is introduced to any one of the dependencies--intmath.c, testintmath.c, or intmath.h. However, as we know from...

####
