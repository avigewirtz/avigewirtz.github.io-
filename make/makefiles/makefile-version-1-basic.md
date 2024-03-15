# Makefile 1: Basic Version



<figure><img src="../../.gitbook/assets/Group 28 (1).png" alt="" width="563"><figcaption></figcaption></figure>



The transition from a dependency graph to a Makefile is intuitive and straightforward.

1. Create a rule for each object file and for the executable. In our dependency graph, they're circled in red.&#x20;

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

Let's now examine how make processes our makefile at various points of development. We'll consider three cases. Show depth first search tree.&#x20;

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

