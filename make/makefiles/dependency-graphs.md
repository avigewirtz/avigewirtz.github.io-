# Dependency graphs

A program's dependencies can be formally described via a what is known in mathematics as a dependency graph. A dependency graph for our `foobarbaz` program is shown in Figure 2.3.

<figure><img src="../../.gitbook/assets/Group 132.png" alt=""><figcaption></figcaption></figure>

In this graph, the nodes represent files, which (when applicable) are annotated with the commands to build them. The arrows represent dependencies. If file A points to file B, then A directly depends on B, meaning changes to B require A to be rebuilt. If A points to B and B points to C, then A is indirectly (or transitively) dependent on C. A change to C requires B to be rebuilt, which in turn requires A to be rebuilt. The practical distinction between direct and indirect dependencies will become more apparent when we discuss Makefiles.

Notice the relationship between object files and header files in our dependency graph. Multiple object files can depend on a single header file (e.g., `a.o, b.o` and c`.o` all depend on y`.h`), and an object file can depend on multiple header files (e.g., `b.o` depends on both `x.h` and `y.h`). While such relationships are possible for C files, in practice they're rare. Typically, there is a one-to-one relationship between object files and C files, as is the case in our graph.





Let's construct a dependency graph for our program. This can be done by following a few simple steps:

1. Create a node for each of the program files (i.e., the `.c`, `.h`, `.o` files and the executable).
2. Draw an arrow from:
   * The executable to each of the `.o` files
   * Each `.o` file to its corresponding `.c` file
   * Each `.o` file to each `.h` file that is `#included` in the `.o` file's corresponding `.c` file
3. Annotate the executable and each object file with the command to build it

This results in the following dependency graph:

<figure><img src="../../.gitbook/assets/Group 125 (1).png" alt=""><figcaption></figcaption></figure>

A modification to a file requires all the files pointing to it--directly or indirectly--to be rebuilt. For example, a modification to `testintmath.c` requires `testintmath.o` (which is directly dependent on `testintmath.c`) and `testintmath` (which is indirectly dependent on `testintmath.c`) to be rebuilt, but it does not require `intmath.o` to be rebuilt. The same idea applies to `intmath.c`. A modification to `intmath.h`, however, is more drastic. It requires `intmath.o`, `testintmath.o`, and `testintmath` to be rebuilt.&#x20;
