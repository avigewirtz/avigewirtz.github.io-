# Makefiles

To use Make to build a program, you need to create a file in your project directory called a makefile, which is essentially a textual representation of your program's dependency graph that tells make how and when to compile and link your program. You can name your makefile _makefile_ or _Makefile_ (or even _GNUMakefile_, if you're using GNU Make). GNU recommends Makefile.&#x20;

A makefile primarily consists of _rules_, each of which tell make whether or not a file has to be built, and if so, how to build it. A rule typically have the following syntax:&#x20;

```
target: dependencies
<tab> command
```

Let's break this down:

* **target**: the name of a file you want to build. Typically an object file (.o) or an executable.&#x20;
* **dependencies**: the files that are needed to build the target. Typically object files, source files (.c), or header files (.h).&#x20;
* **command**: the command that builds the target file. Note that the command must be preceded by a tab character.&#x20;

{% hint style="danger" %}
One of the most common errors in writing Makefiles is using spaces (ASCII character 32) before the command instead of a tab (ASCII character 9). This will lead to the following error:

&#x20;  \*\*\* missing separator.  Stop.
{% endhint %}

## Creating a makefile for testintmath

Recall our dependency graph for testintmath. For reference, it is provided in Figure 1. To create a makefile for testintmath, we need to create a rule for each file we want to build. In our case, that's the three files circled in red: intmath.o, testintmath.o, and testintmath.&#x20;

<figure><img src="../../.gitbook/assets/dependency_graph (1).png" alt=""><figcaption></figcaption></figure>

Let's create a simple but complete makefile for testintmath. makefile with three rules and add the target files. &#x20;

```
testintmath: dependencies
  command
  
testintmath.o: dependencies
  command
  
intmath.o: dependencies
  command
```

For their dependencies,&#x20;

* `testintmath.o` depends on `testintmath.c` and  `intmath.h`. This is because changes in `testintmath.c` or `intmath.h` require recompilation of `testintmath.o`.
* Similarly, `intmath.o` depends on `intmath.c` and  `intmath.h`, since changes to either of these files require recompilation of `intmath.o`.
* `testintmath` (the final executable) depends on `testintmath.o` and `intmath.o`, not directly on the source files (`intmath.c` or `testintmath.c`). This is because the executable is created from the object files, not directly from the source files.

```
testintmath: testintmath.o intmath.o
  command
  
testintmath.o: testintmath.c intmath.h
  command
  
intmath.o: intmath.c intmath.h
  command
```

For the commands:

```
testintmath: testintmath.o intmath.o
  gcc testintmath.o intmath.o -o testintmath
  
testintmath.o: testintmath.c intmath.h
  gcc -c testintmath.c
  
intmath.o: intmath.c intmath.h
  gcc -c intmath.c
```

#### Running our makefile

To run our makefile, we use the `make` command in the terminal, followed by the name of the target we want to build. To build `testintmath`, we invoke:

```
make testintmath
```

Alternatively, to build testintmath we can invoke `make` without specifying a target:

```
make
```

Since if no target is specified, make will default to the first target in the makefile, which in our case is testintmath.&#x20;

### Our makefile in Action

Let's now examine how make processes our makefile. We'll consider three cases.

<figure><img src="../../.gitbook/assets/Group 19 (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Group 20.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Group 22.png" alt=""><figcaption></figcaption></figure>

## other points i want to make:

* You can add comments in a makefile by beginning the line with a # symbol. For example:

```
# this is a comment
```

* A rule can have multiple commands and targets. We won't cover such rules here.&#x20;
* The order in which rules appear in the makefile isn't signifigant, except for the first rule, which&#x20;
* doesn't process all rules. only ones&#x20;
* In a proper Makefile, each object file:
  * Depends upon its .c file
    * Does not depend upon any other .c file&#x20;
    * Does not depend upon any .o file
  * Depends upon any .h files that are #included directly or indirectly
* In a proper Makefile, each executable:
  * Depends upon the .o files that comprise it&#x20;
  * Does not depend upon any .c files&#x20;
  * Does not depend upon any .h files
