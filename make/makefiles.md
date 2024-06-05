# Automating Builds With make

`make` is a standard utility on all unix-like systems. It automates the incremental build process we described in the last section. Instead of having to keep track of which files have changed and which files are affected by the changes and then invoking a sequence of commands to rebuild the executable, `make` can do all this work for you.&#x20;

To use `make` to build a program, you need to create a file known as a _makefile_, which you populate with a textual representation of your program's dependency graph (see below). Once you have a suitable makefile set up, the command:

```
make
```

Is all it takes to build your program. `make` will look for a file in the working directory named makefile or Makefile and analyze its dependency graph. If file A depends on B and B has a more recent modification timestamp, make will rebuild A.&#x20;

{% hint style="info" %}
**Assumptions made in this chapter**

In this chapter, we assume the following:

* The name of the makefile is makefile or Makefile. In practice you can name it something else, but then you'd have to specify the name on the command-line when you invoke make.
* makefile and all project files are in the working directory.&#x20;
{% endhint %}

#### Writing a makefile for testintmath

The core of a makefile is a dependency graph. Identical to graph shown in Figure 12, but with arrows flipped.&#x20;



<figure><img src="../.gitbook/assets/Group 125 (1).png" alt="" width="563"><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>

Describing this dependency graph in `make` syntax is extremely straightforward. We create what is known as a _dependency rule_ for each target in the dependency graph--`testintmath.o`, `intmath.o`, and `testintmath`. Dependency rules have the following syntax:

```
target: dependencies
<tab> command
```

* **Dependencies**. The files that the target _directly_ depends on (e.g., `testintmath` directly depends on `testintmath.o` and `intmath.o`).
* **Command**. The command to build the target (e.g., `gcc217 intmath.o testintmath.o -o testintmath`). Note that the command _must_ be preceded by a Tab character. Failure to do so will result in an error.

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

`make` prints each of the commands it executes to build the target. If the target is already up-to-date, it will respond: `target up to date`. Thus, say we run make when all targets need to be built. make will print all three commands:

```bash
$ make
gcc -c testintmath.c
gcc -c intmath.c
gcc testintmath.o intmath.o -o testintmath
$
```

If we run make again immediately afterward, make will print "target up-to-date" and not execute any commands:

```bash
$ make
make: `testintmath' is up to date.
$
```

Note that `make` does not read a makefile from top to bottom, processing all rules within it. It starts with the first rule or the rule specified on the command line, and then processes only the rules that are reachable from it. So, for example, if we invoke:

```bash
make intmath.o
```

make will process the rule for `intmath.o` only (i.e., it will build intmath.o or tell us it's up to date). It will not process the rules for `testintmath.o` or `testintmath`.
