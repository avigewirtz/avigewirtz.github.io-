# Automating Builds With make

As we saw in the previous section, implementing incremental builds manually requires you to (1) keep track of which source files have been modified since the last build; and (2) understand which object files are affected by these changes. Even for a small program like testintmath, this task isn’t exactly fun, though it is reasonably manageable. As programs grow larger, however, and the web of dependencies grows increasingly complex, this task becomes incredibly tedious and error-prone.

Consider a scenario, for example, where you modify a header file, `A`, that is `#include`d in, say, 20 of your program's `.c` files. You’d have to track down each one of these `.c` files and recompile it. Worse yet, imagine header file `A` is also `#include`d in another header file, `B`. You'd then have to also track down all `.c` files that `#include` `B` and recompile them.

For this reason, the `make` tool was developed, which automates the process of incremental builds. Here's how it works: you create a file named `Makefile` or `makefile` in your program's directory. In this `Makefile`, you describe the dependencies among the files in your program and provide `make` with the necessary commands to build each file from its dependencies. Once you have a suitable Makefile set up, you can build your entire program by simply invoking:&#x20;

```bash
make
```

`make` will read the Makefile, and, assuming it is set up correctly, build the minimum necessary files to produce an updated executable.&#x20;

### Dependency Graphs

The dependencies among files in a program can be formally described via a _dependency graph_. In this graph, nodes represent files and directed edges (arrows) indicate dependencies. If A -> B, then A depends on B, meaning that a modification to B requires A to be rebuilt. If A -> B and B -> C, then A indirectly (or transitively) depends on C. A modification to C requires B to be rebuilt, which in turn requires A to be rebuilt. A node without any dependencies is known as a _leaf_. Non-leaf nodes are labeled with commands to build them. Leafs are typically `.c` and `.h` files, which are not "built". A dependency graph for our `testintmath` program is shown in Figure 12.3.

<figure><img src="../.gitbook/assets/Group 125 (1).png" alt="" width="563"><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>

A few observations about our dependency graph that are typical of C programs:

* .c, and .h files are leaf nodes. They do not have any dependencies.
* Each .o file depends on only one .c file.&#x20;
* 2 levels of dependencies. Execuitable depends on object files, and object files depend on .c and .h filesrelationship

#### Dependency Graph to Makefile

The transition from a dependency graph to a makefile is quite straightforward. We create what is known as a _dependency rule_ for each file in the dependency graph that is not a leaf. In make terminology, such files are called targets. In our case, we have three targets: `intmath.o`, `testintmath.o`, and `testintmath`. Dependency rules have the following syntax:

```
target: dependencies
<tab> command
```

* **Dependencies** . These are the files that the target _directly_ depends on (e.g., `testintmath` directly depends on `testintmath.o` and `intmath.o`). We do not include indirect dependencies.
* **Command**. This is the command make invokes to build the target. Note that it must be preceded by a Tab character.

This results in the following Makefile:

```makefile
testintmath: testintmath.o intmath.o
    gcc217 testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc217 -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc217 -c intmath.c
```

### Running a makefile

The general syntax to run a Makefile is:

```bash
make target
```

If you omit a target, `make` defaults to the first target in the makefile.

To build `testintmath`, we can invoke make without specifying a target and make will default to `testintmath`, since it's the first target in our Makefile:

```bash
make
```

If we wanted to build `intmath.o` alone, we'd invoke:

```bash
make intmath.o
```

{% hint style="info" %}
`make` does not read a makefile from top to bottom, processing all rules within it. It starts with the default rule or the rule specified on the command line, and then processes only the rules that are reachable from it.&#x20;
{% endhint %}
