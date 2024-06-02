# Automating Builds With make

`make` is a standard utility on all unix-like systems. It automates the incremental build process we discussed in the last section. Instead of having to keep track of which files have changed and which files are affected by the changes and then invoking a sequence of commands to rebuild the executable, `make` can do all this work for you. All you have to do is invoke:

```bash
make
```

and make will figure out and perform all the necessary recompilations.&#x20;

#### makefiles

if the scheme we just described sounds too goo to be true, it is. There is some initial setup work. to use make to build your project, you have to first set up a file known as a makefile. in this makefile, you describe the dependencies among the files in your program and provide make with the command to build each file from its dependencies. when you invoke make, it looks for a file in the current working directory named makefile or Makefile, reads the dependency rules, and determines the minimum neccessary recompilations. it's algorithm works something like this: If file A depends on B, and B was modified more recently that A, rebuild B by recompiling A.&#x20;

{% hint style="info" %}
#### Assumptions made in this chapter

In this chapter, we assume the following:

* name of your makefile is makefile or Makefile. In practice you can name it something else, but then you'd have to specify the name on the command-line when you invoke make.&#x20;
* makefile and all project files are in the working directory. make looks for the makefile in the working directory.&#x20;

These assumptions are summarized in Figure 2. Of course, none of these assumptions need actually be true in practice. However,&#x20;
{% endhint %}

### Dependency Graphs

the heart of a makefile is a dependency graph. make processes a dependency graph. Before we describe how to create a dependency graph for testintmath in make syntax, let's first go over a visual representation of testintmath's dependency graph. We describe dependency graph in make syntax.&#x20;

<figure><img src="../.gitbook/assets/Group 125 (1).png" alt="" width="563"><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>

Notice a few characteristics of our dependency graph. These are common among C programs.

* 2 levels of dependencies. Execuitable object file depends on relocateable object files, and relocateable object files depend on .c and .h files. `.c` and `.h` files do not have any dependencies. (note, however, that it's not impossible for .c files to have dependencies.)&#x20;
* each .o file depends on a single .c file, but it can depend on an arbitrary number of .h files.&#x20;

#### Dependency Graph in `make` Syntax

We create what is known as a _dependency rule_ for each target in the dependency graph. In our case, that corresponds to testintmath.o, intmath.o, and testintmath. Dependency rules have the following syntax:

```
target: dependencies
<tab> command
```

* **Dependencies** . These are the files that the target depends on (e.g., `testintmath` depends on `testintmath.o` and `intmath.o`).
* **Command**. This is the command to build the target. In our graph, each target is labeled with the command to build it. Note that the command must be preceded by a Tab character.

This results in three dependency rules: one for testintmath, one for intmath.o, and one for testintmath.o, leading to the following makefile:

```makefile
testintmath: testintmath.o intmath.o
    gcc217 testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc217 -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc217 -c intmath.c
```

### Running make

Make normally prints,then executes, the necessary commands a line at a time.

The general syntax to run a Makefile is:

```bash
make target
```

Where `target` is the name of the file you want `make` to build. For example, to build `intmath.o`, you'd invoke:

```bash
make intmath.o
```

If you omit a target, `make` defaults to the first target in the Makefile. In our Makefile, `testintmath` is the first target. Thus, the command:

```bash
make
```

Is equivalent to:

```bash
make testintmath
```

{% hint style="info" %}
`make` does not read a makefile from top to bottom, processing all rules within it. It starts with the first rule or the rule specified on the command line, and then processes only the rules that are reachable from it.
{% endhint %}
