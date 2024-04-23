# Writing a Makefile

The transition from a dependency graph to a Makefile is quite straightforward. Let's demonstrate how to write a makefile for testintmath, whose dependency graph is shown below.&#x20;



<figure><img src="../../.gitbook/assets/Group 28 (1).png" alt="" width="563"><figcaption><p>Figure 6: testintmath dependency graph</p></figcaption></figure>

The first step is to create a makefile in our program's directory. We can name it `Makefile`, `makefile`, or even `GNUmakefile` (assuming we're using GNU Make). GNU recommends `Makefile`.

Next, we populate the makefile with a textual representation of our program's dependency graph. A textual representation consists of _dependency rules_, which have the following syntax:&#x20;

```
target: dependencies
<tab> command
```

* **Target**: The file of a file you want to build.
* **Dependencies**: The files that the target directly depends on.&#x20;
* **Command**: The command to build the target. Note that the command must be preceded by a tab.&#x20;

We need to create a dependency rule for the executable and for each object file. This results in three dependency rules: one for the target testintmath, one for the target intmath.o, and one for the target testintmath.o. Determining which files each of these targets directly depend on is straightforward. If file A points to file B, then file B directly depends on file A. In our case:&#x20;

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

An important thing to notice is that a dependency can have its own rule. In other words, a file can be both a dependency and a target. In our case, testintmath.o and intmath.o, the dependencies of testintmath, each have their own rule.  As we'll soon see, make processes rules recursively. If a dependency has a rule, make processes the dependency's rule before completing to process the current rule.&#x20;

## Running our makefile

To run a makefile, you invoke:&#x20;

```bash
make target
```

`target` is the name of the file you want `make` to build. If you don't specify a target, `make` defaults to the first target listed in the Makefile. In our case, since testintmath is the default target, we can build it by simply invoking:&#x20;

```
make
```

make will process all theee rules, since...

If we were fo invoke:

Notice that make prints each of the commands it executes.&#x20;

If we were ro invoke:

```
make intmath.o
```

make would process the rule for intmath.o alone. It would not process the rules for testintmath or testintmath.o, since they aren't reachable from intmath.o. This highlights an important point: make does not read a makefile from top to bottom. it starts from the default rule or the rule specified on the commanf line, and processes rules reachable from it it. and the third rule alone will be processed. Thus, you should recogniuze that make does not read the makefile from top to bottom, processing all rules. It starts from the default rule, and only processes other rules that are reacheable from it.&#x20;
