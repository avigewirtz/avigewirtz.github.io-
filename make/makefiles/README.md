# Makefiles

## 1. INTRODUCTION

To use Make to build a program, you need to create a file in your project directory called a makefile, which is essentially a textual representation of your program's dependency graph that tells make how and when to compile and link your program. A makefile can be named 'makefile' or 'Makefile' (or even 'GNUMakefile', if you're using GNU Make). GNU recommends 'Makefile'.&#x20;

A makefile primarily consists of _rules_, each of which tells make whether or not a file has to be built, and if so, how to build it. A rule typically has the following syntax:&#x20;

```
target: dependencies
<tab> command
```

Let's break this down:

* **target**: This is usually the file that the rule will build, such as an object file (`.o`) or an executable.
* **dependencies**: These are the files needed to build the target. If the target is an executable, then the dependencies are typically object files. If the target is an object file, then the dependencies are typically C source (.c) and header (.h) files. &#x20;
* **command**: the command that actually builds the target file. If the target is an executable, then the command typically links the object files necessary to build the executable. If the target is an object file, then the command typically compiles the corresponding C file. &#x20;

{% hint style="danger" %}
One of the most common errors in writing Makefiles is preceding the using spaces (ASCII character 32) instead of a tab (ASCII character 9). This will lead to the following error:

&#x20;  \*\*\* missing separator.  Stop.
{% endhint %}

## Running a makefile

To run our makefile, we use the `make` command in the terminal, followed by the name of the target we want to build. To build `testintmath`, we invoke:

```
make testintmath
```

Alternatively, to build testintmath we can invoke `make` without specifying a target:

```
make
```

Since if no target is specified, make will default to the first target in the makefile, which in our case is testintmath.&#x20;

## Creating a makefile for testintmath

Let's jump right in and consider how to create a makefile for our testintmath program. We will create four versions. &#x20;

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

#### Makefile version 1

Let's now design a properly structured makefile, that takes advantage of partial builds. To do so, we need to create three targets: one for intmath.o, one for testintmath.o, and one for testintmath. To write out the makefile, it is helpful to have a visualization of the dependency graph. Recall our dependency graph for testintmath. For reference, it is provided in Figure 1. &#x20;

<figure><img src="../../.gitbook/assets/dependency_graph (1).png" alt=""><figcaption></figcaption></figure>

In a properly structured makefile follows certain principles:

* Each object file:
  * Depends upon its .c file
    * Does **not** depend upon any other .c file&#x20;
    * Does **not** depend upon any .o file
  * Depends upon any .h files that are #included directly or indirectly
* Each executable:
  * Depends upon the .o files that comprise it&#x20;
  * Does **not** depend upon any .c files&#x20;
  * Does **not** depend upon any .h files

{% code title="makefile version 1" %}
```
testintmath: testintmath.o intmath.o
  gcc testintmath.o intmath.o -o testintmath
  
testintmath.o: testintmath.c intmath.h
  gcc -c testintmath.c
  
intmath.o: intmath.c intmath.h
  gcc -c intmath.c
```
{% endcode %}

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
