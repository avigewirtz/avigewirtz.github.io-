# Writing a Simple Makefile

Continuing with our `testintmath` example, let's explore how to use `make` to build our program.

Assume the working directory contains `testintmath`'s source files (i.e., `testintmath.c`, `intmath.c`, and `intmath.h`). The first step is to create a Makefile in the working directory. We can name the Makefile whatever we'd like, but `make` automatically searches for a file named `makefile` or `Makefile` (capital M), making these names more convenient.

The next step is to populate the Makefile `testintmath`'s dependency graph. Before we show how to write this dependency graph in `make` syntax, let's go over it graphically. Figure 12.3 shows a graphical representation of `testintmath`'s dependency graph.

<figure><img src="../../.gitbook/assets/Group 125 (1).png" alt="" width="563"><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>

In this graph, files are represented by nodes, and dependencies are represented by directed edges (->) . Each file with dependencies—known as a _target_—is labeled with the command to build it. Our program has three targets: the executable `testintmath`, and the object files `testintmath.o` and `intmath.o`. For convenience, these targets are circled in red. We see the following dependencies:

* `testintmath` depends on `testintmath.o` and `intmath.o`
* `tetsintmath.o` depends on `tetsintmath.c` and `intmath.h`
* `intmath.o` depends on `intmath.c` and `intmath.c`

Translating this dependency graph into a Makefile is remarkably straightforward. We create what is known as a _dependency rule_ for each target in the dependency graph. Dependency rules have the following syntax:

```
target: dependencies
<tab> command
```

* **Dependencies**. The files that the target depends on.
* **Command**. The command to build the target. Note that the command _must_ be preceded by a Tab character. Failure to do so will result in an error.

This results in the following makefile:

```makefile
testintmath: testintmath.o intmath.o
    gcc217 testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc217 -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc217 -c intmath.c
```