# Automating Builds With make

As we saw in the previous section, managing incremental builds manually is possible but tends to be tedious and error prone. It requires you to:

* Keep track of which files have been modified.
* Understand the dependencies among the files in your program. This is the hardest part. Problem is header files.&#x20;

Admittedly, for a small program like `testintmath`, this is manageable, but as programs grow larger and the web of dependencies grows increasingly complex, this task becomes incredibly painful to do manually.&#x20;

A much better approach is to automate the process with `make`. To do so, you create a file named `Makefile` or `makefile` in your program's directory, which you populate with a textual representation of your program's [dependency graph](broken-reference). This graph describes the relationships between your program's files and provide make with the necessary build commands. Once you have a suitable Makefile, you can build your program by simply invoking:

```bash
make
```

`make` will read the Makefile and (assuming its set up correctly) build the minimum necessary files to produce an updated executable.

### Dependency Graphs

<figure><img src="../.gitbook/assets/Group 138 (2).png" alt=""><figcaption></figcaption></figure>

In this graph, nodes represent files and directed edges (arrows) indicate dependencies. If A -> B, then A directly depends on B, meaning that a modification to B requires A to be rebuilt. If A -> B and B -> C, then A is indirectly (or transitively) dependent on C. A modification to C requires B to be rebuilt, which in turn requires A to be rebuilt. Non-leaf nodes are labeled with commands to build them. A node without any dependencies is known as a _leaf_. Non-leaf nodes are labeled with commands to build them. Leafs are typically `.c` and `.h` files, which are not "built". A dependency graph for our `testintmath` program is shown in Figure 12.3.

A few observations about our dependency graph that are typical of C programs:

* 2 levels of dependencies. Execuitable depends on object files, and object files depend on .c and .h filesrelationship

Let's now create a makefile for our testintmath program. First, we'll draw a dependency graph for our program. Then, we'll explain how to translate it to make syntax.

#### Constructing a dependency graph

Constructing a dependency graph is quite simple. Let's now create one for our testintmath program.  This can be done by following a few simple steps:

1. Create a node for each of the program  `.c`, `.h`, `.o` files and the executable
2. Draw an arrow from:
   * The executable to each of the `.o` files
   * Each `.o` file to its corresponding `.c` file
   * Each `.o` file to each `.h` file that is `#included` in the `.o` file's corresponding `.c` file
3. Annotate the executable and each object file with the command to build it

This results in the following dependency graph:

<figure><img src="../.gitbook/assets/Group 125 (1).png" alt="" width="563"><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>

d

The transition from a dependency graph to a makefile is quite straightforward. Let's

We create what is known as a _dependency rule_ for each file in the dependency graph that is not a leaf. In make terminology, such files are called targets. In our case, we have three targets: `intmath.o`, `testintmath.o`, and `testintmath`. Dependency rules have the following syntax:

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
