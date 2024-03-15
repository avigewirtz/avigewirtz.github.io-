# Makefiles

To use Make to build a program, you need to create a file called a _makefile_, which is essentially a textual representation of your program's dependency graph. It provides make with all the information it needs to build your program. You can name your makefile 'makefile' or 'Makefile' (or even 'GNUmakefile', if you're using GNU Make). GNU recommends 'Makefile'.&#x20;

When you invoke `make` on the command line, Make searches for a file named makefile. You can name it 'makefile' or 'Makefile' (or even 'GNUmakefile', if you're using GNU Make). GNU recommends calling it 'Makefile'.&#x20;

### Dependency Rules

A makefile primarily consists of _dependency_ _rules_, each of which tells make whether or not a file has to be built, and if so, how to build it. Dependency rules have the following syntax:&#x20;

```
target: dependencies
<tab> command
```

* **Target**: The file you want to build (e.g., `intmath.o`).&#x20;
* **Command**: The command to build the target (e.g., `gcc217 -c intmath.c`). The command must be preceded by a tab character.
* **Dependencies**: The files that need to be up to date before the target can be correctly built. Make builds the target if it's older than any of its dependencies or if the target does not exist.

{% hint style="danger" %}
Note that the command must be preceded by a tab (ASCII character 9) _not_ spaces (ASCII character 32).  Using spaces will cause the following error:

&#x20;  `*** missing separator.  Stop.`
{% endhint %}

## Makefile for testintmath

The transition from a dependency graph to a Makefile is quite straightforward. Recall testintmath's dependency graph, shown in figure 6.&#x20;



<figure><img src="../../.gitbook/assets/Group 28 (1).png" alt="" width="563"><figcaption></figcaption></figure>

1. First, create a file in your project's directory called Makefile or makefile.
2. In the Makefile, create one rule for the executable and one a rule for each object file:

```
testintmath:


testintmath.o:


intmath.o:

```

3: Fill in the commands used to build that file. (Recall to precede the command with a tab)

```
testintmath: 
    gcc217 -o testintmath.o intmath.o -o testintmath

testintmath.o:
    gcc217 -c testintmath.c

intmath.o:
    gcc217 -c intmath.c
```

4: Fill in each target's dependencies.&#x20;

```
testintmath: testintmath.o intmath.o
    gcc217 -o testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc217 -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc217 -c intmath.c
```

## Invoking Make

To invoke make, simple type `make` on the command line. Make will print out all the commands that it executes:

```
make
```











## How make works

