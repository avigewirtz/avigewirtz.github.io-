# Makefile version 1

Let's now construct a simple but complete makefile that leverages the benefits of partial builds. To effectively draft this makefile, it's helpful to visualize the dependency graph. As a point of reference, the dependency graph for "testintmath" is illustrated in Figure 1.

<figure><img src="../../.gitbook/assets/dependency_graph (1).png" alt=""><figcaption></figcaption></figure>



To craft a proper makefile, we adhere to a few key principles. First, we must create a rule for each object file and the executable. Let's start off by creating three rules and filling in the targets:&#x20;

```
testintmath: dependencies
    command

testintmath.o: dependencies
    command

intmath.o: dependencies
    command
```

For the dependencies, if you follow the following principles, filling them in will be quite easy. Each object file is dependent on its corresponding .c file and any .h files that are included, whether directly or indirectly, in the .c file. It is not dependent on any other .c or .o file. The executable is dependent on only the object files that form it. It is not dependent on any .c or .h file.&#x20;

Looking at the dependency graph, we can easily see that intmath.o depends on intmath.c and intmath.h, and testintmath.o depends on testintmath.c and intmath.h. For the executable testintmath, its dependencies are intmath.o and testintmath.o. Filling in the dependencies, we get:

```makefile
testintmath: testintmath.o intmath.o
     command

testintmath.o: testintmath.c intmath.h
     command

intmath.o: intmath.c intmath.h
     command
```

For the object file commands, recall the -c option, which instructs gcc to stop the build process before the linking stage. For the executabe, the command is the standard gcc comman with the -o option, which enables us to choose the executable filename. Because gcc is being invoked on .o files, it will perform only the linking stage. This leads to the following makefile:



```makefile
testintmath: testintmath.o intmath.o
     gcc testintmath.o intmath.o -o 

testintmath.o: testintmath.c intmath.h
     gcc -c testintmath.c

intmath.o: intmath.c intmath.h
     gcc -c intmath.c
```

### Our makefile in Action

Let's now examine how make processes our makefile at various points of development. We'll consider three cases.

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
