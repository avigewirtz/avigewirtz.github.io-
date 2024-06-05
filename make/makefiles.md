# Automating Builds With make

Automating the incremental build process with `make` is quite straightforward. You create a text file in your program's directory known as a _makefile._ In this makefile, you describe the dependencies among the files in your program and provide `make` with the commands to build them. Once you have a suitable makefile set up, the command:

```bash
make
```

Is all it takes to incrementally build your program. `make` will read your program's makefile and, based on the dependency graph and the latest modification timesstamps of each file,  rebuild the minimum necessary files to produce an updated executable. determine the minimum set of look for a file named `makefile` or `Makefile` in the working directory and analyze its dependency graph. If file A depends on B and B has a more recent modification timestamp, make will rebuild A.

{% hint style="info" %}
**Assumptions**

We made some implicit assumptions, which we'll continue to make.&#x20;

* name of makefile is Makefile or makefile. In practice you can name it anything, but make
*


{% endhint %}

#### Writing a makefile for testintmath

The core of a makefile is a dependency graph. Have to Identical to graph shown in Figure 12, but with arrows flipped.

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

`make` prints each of the commands it executes to build the target. Thus, say we're building our program for the first time. `make` will execute and print all three commands:

```bash
$ make
gcc -c testintmath.c
gcc -c intmath.c
gcc testintmath.o intmath.o -o testintmath
$
```

If we run `make` again immediately afterward, make will respond that the target is up to date, and it will and not execute any commands:

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
