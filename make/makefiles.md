# Automating Incremental Builds With make

As we have seen, implementing incremental builds manually is possible but it requires some work. In particular, you need to:

1. Keep track of which `.c` and `.h` files were modified since the last build.
2. Keep track of which `.o` files are affected by the changes to the `.c` and `.h` files.
3. Run the commands to rebuild the program, in the correct order.&#x20;

Even for a small program like `testintmath`, this task isn’t particularly fun, though it is admittedly manageable. As programs grow larger, however, and the web of dependencies grows increasingly complex, this task becomes incredibly tedious and error-prone.

Consider a scenario where you modify header file `A`, which is `#included` in, say, 20 `.c` files. To rebuild your program, you'd have to track down each of these `.c` files and recompile them. Worse yet, imagine header file `A` is also `#included` in header file `B`. You'd then have to also track down each of the `.c` files that `#include` `B` and recompile them as well. 

To make life easier (no pun intended), the `make` tool was developed, which automates the process of incremental builds. To incrementally build a program, `make` requires two pieces of information:

1. Dependency graph. Specifies dependencies between program's files and commands to build each file from its dependencies.
2. The latest modification timestamps of the files.

make can obtain the timestamps on it's own from the filesystem. The dependency graph we describe via a user-written file known as a makefile. We'll decribe how to set one up below. Once an appropriate makefile is set up, the command:

make

is all it takes to incrementally build the program. 


#### Makefiles

- Continuing with our testintmath example, we'll show how to write makefile 
- the first step is to create a file named Makefile or makefile in the testintmath directory. (In practice, it's possible to name the makefile something other than Makefile or makefile, but then you'd need to specidy its name on the command line when you run make.) 
- next, we populate the Makefile with a dependency graph for testintmath. the dependency graph describes the dependencies among the source and binary files in testintmath and contains the commands to build each binary. before we show how to write the dependency graph in make syntax, let's first go over it graphically. 
- figure 13 shows a graphical representation of testintmath dependency graph. 

In the Makefile, we describe the 


The core of a makefile is a dependency graph. Identical to graph shown in Figure 12, but with arrows flipped.

<figure><img src="../.gitbook/assets/Group 125 (1).png" alt="" width="563"><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>

Describing this dependency graph in `make` syntax is extremely straightforward. We create what is known as a _dependency rule_ for each target in the dependency graph--`testintmath.o`, `intmath.o`, and `testintmath`. Dependency rules have the following syntax:

```
target: dependencies
<tab> command
```

* **Dependencies**. The files that the target _directly_ depends on (e.g., `testintmath` directly depends on `testintmath.o` and `intmath.o`).
* **Command**. The command to build the target (e.g., the command to build `testintmath` is `gcc217 intmath.o testintmath.o -o testintmath`). Note that the command _must_ be preceded by a Tab character. Failure to do so will result in an error.

This results in the following makefile:

```makefile
testintmath: testintmath.o intmath.o
    gcc217 testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc217 -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc217 -c intmath.c
```

#### Running Our Makefile

The general syntax to run a makefile is:

```bash
make target
```

where `target` is the name of the file you want `make` to build. In our case, the target can be `testintmath.o`, `intmath.o`, or `testintmath`. If you omit a target, `make` defaults to the first target in the makefile. In our case, that's `testintmath`. Thus, the command:

```bash
make
```

Is equivalent to:

```bash
make testintmath
```

`make` prints each of the commands it executes to build the target. Thus, say we're building our program for the first time. `make` will execute and print all three commands:

```bash
$ make
gcc -c testintmath.c
gcc -c intmath.c
gcc testintmath.o intmath.o -o testintmath
$
```

If we run `make` again immediately afterward, make will report that the target is up to date and not execute any commands:

```bash
$ make
make: `testintmath' is up to date.
$
```

An important thing to recognize is that `make` does not read a makefile from top to bottom, processing all rules within it. It starts with the first rule in the makefile or the rule specified on the command line and then processes only the rules that are reachable from it. So, for example, if we invoke:

```bash
make intmath.o
```

make will process the rule for `intmath.o` only. It will not process the rules for `testintmath.o` or `testintmath`.
