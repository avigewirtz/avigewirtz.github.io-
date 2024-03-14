# Makefiles

To use Make to build a program, you need to create a file called a _makefile_, which is essentially a textual representation of your program's dependency graph. It provides make with all the information it needs to build your program in the most efficient way.&#x20;

When you invoke make on the command line, Make searches for a file named makefileYou can name it 'makefile' or 'Makefile' (or even 'GNUmakefile', if you're using GNU Make). GNU recommends calling it 'Makefile'.&#x20;

### Dependency Rules

A makefile primarily consists of _dependency_ _rules_, each of which tells make whether or not a file has to be built, and if so, how to build it. Dependency rules have the following syntax:&#x20;

```
target: dependencies
<tab> command
```

* **Target**: The file that the rule will build--typically an object (.o) or executable file.
* **Dependencies**: The files that need to be up to date before the target can be correctly built. If the target is an executable, then the dependencies are typically object files. If the target is an object file, then the dependencies are typically source (.c) and header (.h) files.&#x20;
*   **Command**: The command make executes to build the target. Note that the command must be preceded by a tab. One of the most common errors in writing Makefiles is preceding the command with spaces (ASCII character 32) instead of a tab (ASCII character 9). This will lead to the following error:

    &#x20;  `*** missing separator.  Stop.`

Make builds the target file if it's older than any of its dependencies or if it does not exist. A makefile should contain a rule for the executable and for each object file.&#x20;

## Makefile for testintmath

The transition from a dependency graph to a Makefile is intuitive and straightforward. The dependency graph for testintmath is shown in figure 1.&#x20;



<figure><img src="../../.gitbook/assets/Group 28 (1).png" alt="" width="563"><figcaption></figcaption></figure>
