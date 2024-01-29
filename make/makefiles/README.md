# Makefiles

To use Make to build a program, you need to create a file in your project directory called a makefile, which is essentially a textual representation of your program's dependency graph that tells make how to compile and link your program. You can name your makefile _makefile_ or _Makefile_ (or even _GNUMakefile_, if you're using GNU Make). GNU recommends Makefile.&#x20;

A makefile primarily consists of _rules_, which typically have the following syntax:&#x20;

```
target: dependencies
<tab> command
```

Let's break this down:

* **target**: the name of a file you want to build. Typically an object file (.o) or an executable.&#x20;
* **dependencies**: the files that are needed to build the target. Typically object files or source files (.c or .h).&#x20;
* **command**: the command make executes to build the target file. Note that the command must be preceded by a tab character.&#x20;

{% hint style="danger" %}
One of the most common errors in writing Makefiles is using spaces (ASCII character 32) before the command instead of a tab (ASCII character 9). This will lead to the following error:

&#x20;  \*\*\* missing separator.  Stop.
{% endhint %}

The purpose of a rule is to tell make whether or not a file has to be built, and if so, how to build it. A makefile typically has a rule for each object file and a rule for the final executable file. Let's demonstrate how makefiles work by jumping right in and creating a simple but complete makefile for our testintmath program:&#x20;

```
testintmath: testintmath.o intmath.o
  gcc testintmath.o intmath.o –o testintmath
  
testintmath.o: testintmath.c intmath.h
  gcc -c testintmath.c
  
intmath.o: intmath.c intmath.h
  gcc -c intmath.c
```

Our makefile consists of three rules: one for building the executable testintmath, one for building the object file testintmath.o, and one for building the object file intmath.o. testintmath depends on two object files, each of which in turn depends on two source files.

#### Running our makefile

To run our makefile, we use the `make` command in the terminal, followed by the name of the target we want to build. To build `testintmath`, we invoke:

```
make testintmath
```

Alternatively, we can just invoke `make` without specifying a target:

```
make
```

Since if no target is specified, make will default to the first target in the makefile, which in our case is testintmath.&#x20;















### Our makefile in Action

<figure><img src="../../.gitbook/assets/Group 19 (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Group 20.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Group 22.png" alt=""><figcaption></figcaption></figure>

## other points i want to make:

* comments&#x20;
* rule can have multiple commands and can have more than one target. won't cover that here
* order isn't important, besides for first
* doesn't process all rules. only ones&#x20;

