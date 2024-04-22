# Writing a Makefile

The transition from a dependency graph to a Makefile is quite straightforward. Let's demonstrate how to write a makefile for testintmath, whose dependency graph is shown below.&#x20;



<figure><img src="../../.gitbook/assets/Group 28 (1).png" alt="" width="563"><figcaption><p>Figure 6: testintmath dependency graph</p></figcaption></figure>

The first step is creating a makefile in our program's directory. We can name it `Makefile`, `makefile`, or even `GNUmakefile` (assuming we're using GNU Make). GNU recommends `Makefile`.

We then populate the makefile with a textual representation of our program's dependency graph. A textual representation consists of _dependency rules_, which have the following syntax:&#x20;

```
target: dependencies
<tab> command
```

* **Target**: The file of a file you want to build.
* **Dependencies**: The files that the target directly depends on.
* **Command**: The command to build the target. Note that the command must be preceded by a tab.&#x20;

A dependency rule should be created for each object file and for the executable. In our case, that's three dependency rules: one for testintmath, one for intmath.o, and one for testintmath.o. Our dependency graph makes it obvious which files tesintmath, intmath.o, and testintmath.o directly depend on:&#x20;

* testintmath directly depends on intmath.o and testintmath.o
* intmath.o dircetly depends on intmath.c and intmath.h
* testintmath.o directly depends on testintmath.c and intmath.h

This results in the following makefile:

```makefile
testintmath: testintmath.o intmath.o
    gcc217 testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc217 -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc217 -c intmath.c
```

## Running our makefile

To run our makefile, you invoke:&#x20;

```bash
make target
```

`target` is the name of the file you want `make` to build. If you don't specify a target, `make` defaults to the first target listed in the Makefile, which in our case is testintmath. Thus, to build testintmath, we can simply invoke:&#x20;

```
make
```

Notice that make prints each of the commands it executes.&#x20;
