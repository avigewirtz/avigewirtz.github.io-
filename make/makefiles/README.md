# Makefiles

To use Make, you need to create a file in your project directory called a makefile, which tells make how to build your program. You can think of it like a textual representation of a dependency graph. You can name it _makefile_ or _Makefile_ (or even _GNUMakefile_, if you're using GNU Make). GNU recommends naming it Makefile.&#x20;

A makefile primarily consists of _rules_, which typically have the following syntax:&#x20;

```
target: dependencies
<tab> command
```

Let's break this down:

* **target**: the name of the file you want to build.&#x20;
* **dependencies**: the files that are needed to build the executable.
* **command**: the command to build the executable. Note that the command must be preceded by a tab character.&#x20;

The point of a rule is to tell make whether or not a file has to be built, and if so, how. Let's demonstrate how it works with a simple example:&#x20;

```
intmath.o: intmath.c intmath.h
  gcc -c intmath.c
```

In this rule, the target file is intmath.o, the dependencies are intmath.c and intmath.h, and the command is `gcc -c intmath.c`. First, make has to determine whether intmath.o has to be built. If one of the following two conditions is true, then the answer is yes:

1. intmath.o does not exist
2. intmath.o does exist, but intmath.c or intmath.h are "newer" than intmath.o (i.e., have a newer modification timestamp than intmath.o).&#x20;

If intmath.o needs to be built, make executes the gcc -c intmath.c, which builds intmath.o.

{% hint style="danger" %}
One of the most common errors in writing Makefiles is using spaces (ASCII character 32) before the command instead of a tab (ASCII character 9). This can also happen when editing a Makefile in a text editor that automatically converts tabs to spaces. This will lead to the following error:

```
   *** missing separator.  Stop.
```
{% endhint %}

#### Makefile for testintmath

Let's jump right in and create a simple but complete makefile for our program testintmath:

{% code title="makefile " lineNumbers="true" %}
```makefile
testintmath: testintmath.o intmath.o
  gcc testintmath.o intmath.o –o testintmath
  
testintmath.o: testintmath.c intmath.h
  gcc -c testintmath.c
  
intmath.o: intmath.c intmath.h
  gcc -c intmath.c
```
{% endcode %}

* our makefile has three rules

## Running a makefile







### Our makefile in Action

Let's examines what happens the first time we invoke the makefilefirst time



Invoking make again:

modifying intmath.c and invoking make:



## other points i want to make:

* comments&#x20;
* rule can have multiple commands and can have more than one target. won't cover that here

