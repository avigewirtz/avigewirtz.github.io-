# Makefile Version 1: Basic

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

## Running a makefile

To run a makefile, we use the `make` command in the terminal, followed by the name of the target we want to build. To build `testintmath`, we invoke:

```
make testintmath
```

Alternatively, to build testintmath we can invoke `make` without specifying a target:

```
make
```

Since if no target is specified, make will default to the first target in the makefile, which in our case is testintmath.&#x20;

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



{% hint style="info" %}
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
{% endhint %}
