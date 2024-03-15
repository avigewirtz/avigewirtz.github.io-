# Writing a Makefile

As we mentioned earlier, a makefile is essentially a textual representation of a program's dependency graph. The transition from a dependency graph to a Makefile is quite straightforward. Let's demonstrate how to write a makefile for testintmath, whose dependency graph is shown below.&#x20;



<figure><img src="../../.gitbook/assets/Group 28 (1).png" alt="" width="563"><figcaption><p>Figure 6: testintmath dependency graph</p></figcaption></figure>

**Step 1**: Create a makefile in the testintmath directory (e.g., invoke `emacs Makefile`).

**Step 2**: Create a rule for:

* The executable (i.e., testintmath)
* Each object file (i.e., testintmath.o and intmath.o)

```
testintmath:


testintmath.o:


intmath.o:

```

**Step 3**: Fill in the dependencies for each target. In the dependency graph, an arrow (i.e., directed edge) from file A to B indicates that B depends on A.  In our case:

* testintmath depends on testintmath.o and intmath.o
* testintmath.o depends on testintmath.c and intmath.h&#x20;
* intmath.o depends on intmath.c and intmath.h&#x20;

```
testintmath: testintmath.o intmath.o
 
 
testintmath.o: testintmath.c intmath.h
  

intmath.o: intmath.c intmath.h
  
```

**Step 4**: Fill in the command for each target. The commands for our program are specified in the dependency graph. As a general rule, the command for each object file is a compilation command, and the command for the executable is a linking command.&#x20;

```makefile
testintmath: testintmath.o intmath.o
    gcc217 -o testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc217 -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc217 -c intmath.c
```

## Running makefile

To invoke make, simple type `make` on the command line. Make will print out all the commands that it executes:

```
make
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

### testintmath makefile in Action

Let's now examine how make processes our makefile. We'll examine this at various points of development. We'll consider three cases. Show depth first search tree.&#x20;

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

