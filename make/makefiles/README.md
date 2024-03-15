# Makefile

To use Make to build a program, you need to create a file called a _Makefile_, which is essentially a textual representation of your program's dependency graph. It provides make with all the information it needs to efficiently build your program. In this section, we will construct a makefile for our testintmath program. We'll start out by constructing a minimal version, and build two new versions as we introduce concepts. &#x20;

### Naming Your makefile

You can name your makefile 'makefile' or 'Makefile' (or even 'GNUmakefile', if you're using GNU Make). GNU recommends 'Makefile'.&#x20;

When you invoke `make` on the command line, Make searches for a file named makefile.&#x20;

### Dependency Rules

A makefile primarily consists of _rules_, which have the following syntax:&#x20;

```
target: dependencies
<tab> command
```

* **Target**: The file you want to build.
* **Dependencies**: Files that are used as input to build the target.
* **Command**: Command to build the target. Note that the command must be indented by a tab (ASCII character 9), _not_ spaces (ASCII character 32). &#x20;

make executes the command if one of the dependencies is 'newer' than the target, or if the target does not exist.

### Comments

In Makefiles, you use the `#` symbol for comments. Everything following the `#` on a line is treated as a comment:

```makefile
# This is a comment
```
