# Writing a Makefile

The transition from a dependency graph to a Makefile is quite straightforward. Let's demonstrate how to write a makefile for testintmath, whose dependency graph is shown below.&#x20;



<figure><img src="../../.gitbook/assets/Group 28 (1).png" alt="" width="563"><figcaption><p>Figure 6: testintmath dependency graph</p></figcaption></figure>

The first step is creating a makefile in the program directory. You can name it `Makefile`, `makefile`, or even `GNUmakefile` if you're using GNU Make. GNU recommends `Makefile`.

We then populate it with a dependency rule for each object file (intmath.o, testintmath.o) and for the executable (testintmath). A dependency rule has the following syntax:

```
target: dependencies
<tab> command
```

* **Target**: The file you want to build.
* **Dependencies**: The files that the target directly depends on.
* **Command**: The command to build the target. Note that the command must be preceded by a tab.&#x20;

For our program, we need to create three dependency rules: one for testintmath, one for intmath.o, and one for testintmath.o. For each rule, we need to determine which files the target directly depends on. Our dependency graph makes this obvious:&#x20;

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

Where `target` is the name of the file you want `make` to build. If you don't specify a target, `make` defaults to the first target listed in the Makefile, which in our case is testintmath. To build testintmath, we can simply invoke make:&#x20;

```
make
```

Notice that make prints each of the commands it executes.&#x20;
