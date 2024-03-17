# Makefile

make gets the information to build your program by reading a user-created makefile, which is essentially a textual representation of your program's dependency graph. It describes the relationships among files in your program and provides make with the commands to build them. In this section, we will construct a makefile for our testintmath program.&#x20;

You can name your makefile 'makefile' or 'Makefile' (or even 'GNUmakefile', if you're using GNU Make). GNU recommends 'Makefile'.&#x20;

When you invoke `make` on the command line, Make searches for a file named makefile.&#x20;

## Components of a makefile

A makefile is composed of three things: rules, comments, and macros. We will cover macros in section.&#x20;

### Rules

A makefile primarily consists of _rules_, which have the following syntax:&#x20;

```makefile
target: dependencies
<tab> command
```

* **Target**: The file you want to build.
* **Dependencies**: Files that are used as input to build the target.
* **Command**: Command to build the target. Note that the command must be indented by a tab (ASCII character 9), _not_ spaces (ASCII character 32). &#x20;

make executes the command if one of the dependencies is 'newer' than the target, or if the target does not exist.

### Comments

In a Makefile, everything following the `#` symbol on a line is treated as a comment:

```makefile
# This is a comment
```
