# Automating Builds With make

`make` is a standard utility on all unix-like systems. It automates the incremental build process we described in the last section. Instead of having to keep track of which files have changed and which files are affected by the changes and then invoking a sequence of commands to rebuild the executable, `make` can do all this work for you. All you have to do is invoke:

```bash
make
```

and make will figure out and perform all the necessary recompilations.

if the scheme we just described sounds too goo to be true, it is. There is some initial setup work. to use make to build your project, you have to first set up a file known as a makefile. this makefile a dependency graph. this describes the dependencies among files in the program and the commands to build each file from its dependencies. when you invoke make, it looks for a file in the current working directory named makefile or Makefile, reads the dependency graph, and determines the minimum neccessary recompilations. it's algorithm works something like this: If file A depends on B, and B was modified more recently that A, rebuild B by recompiling A.

{% hint style="info" %}
**Assumptions made in this chapter**

In this chapter, we assume the following:

* name of your makefile is makefile or Makefile. In practice you can name it something else, but then you'd have to specify the name on the command-line when you invoke make.
* makefile and all project files are in the working directory. make looks for the makefile in the working directory.

These assumptions are summarized in Figure 2. Of course, none of these assumptions need actually be true in practice. However,
{% endhint %}

#### Writing a Simple makefile



<figure><img src="../.gitbook/assets/Group 125 (1).png" alt="" width="563"><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>

The make syntax for a dependency graph is extremely simple. It consists of a _dependency rule_ for each target in the dependency graph. In our case, that corresponds to testintmath.o, intmath.o, and testintmath. Dependency rules have the following syntax:

```
target: dependencies
<tab> command
```

* **Dependencies**. The files that the target _directly_ depends on (e.g., `testintmath` directly depends on `testintmath.o` and `intmath.o`).
* **Command**. The command to build the target (e.g., `gcc217 intmath.o testintmath.o -o testintmath`). Note that the command must be preceded by a Tab character. Failure to do so will result in an error.

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

We can run our makefile by simply typing make. make will look in the current diectpry for a file named makefile or Makefile. make will look at the first target in the makefile, in our case testintmath, and build it if it does not exist or if it's not up-to-date. Note that before make can build testintmath, it must first ensure that it's dependencies are up to date. It thus processes the rules for its dependencies first. make prints all first process the rulesmake checks to see if the first target has become out of date with its prerequisites. make prints each of the commands it executes to bring the target up-to-date. If the target is already up-to-date, it will print "target up-to-date." Thus, say we run make when all targets need to be built. make will print all three commands:

```bash
$ make
gcc -c testintmath.c
gcc -c intmath.c
gcc testintmath.o intmath.o -o testintmath
$
```

If we run make when testintmath is up to date, it'll print "target up-to-date" and not execute any commands:

```bash
$ make
make: `testintmath' is up to date.
$
```

You can also specify a target to make on the command line. Where `target` is the name of the file you want `make` to build. For example, to build `intmath.o`, you'd invoke:

```bash
make intmath.o
```

`make` does not read a makefile from top to bottom, processing all rules within it. It starts with the first rule or the rule specified on the command line, and then processes only the rules that are reachable from it.
