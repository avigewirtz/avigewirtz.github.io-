# Makefile

To use Make to build a program, you need to create a file called a _Makefile_, which is essentially a textual representation of your program's dependency graph. It provides make with all the information it needs to efficiently build your program. In this section, we will construct a makefile for our testintmath program. We'll start out by constructing a minimal version, and build two new versions as we introduce concepts. &#x20;

### Naming Your makefile

You can name your makefile 'makefile' or 'Makefile' (or even 'GNUmakefile', if you're using GNU Make). GNU recommends 'Makefile'.&#x20;

When you invoke `make` on the command line, Make searches for a file named makefile.&#x20;

### Dependency Rules

A makefile primarily consists of _rules_, which have the following syntax:&#x20;

```
target: dependencies
<tab> command
```

* **Target**: File you want to build.
* **Dependencies**: Files used as input to build the target.
* **Command**: Command to build the target. Note that the command must be indented by a tab (ASCII character 9), _not_ spaces (ASCII character 32). &#x20;

make executes the command if one of the dependencies is 'newer' than the target, or if the target does not exist.

## Writing a Makefile

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

## Invoking Make

To invoke make, simple type `make` on the command line. Make will print out all the commands that it executes:

```
make
```











## How make works

