# Dependency Graphs

A program's dependencies can be formally described with what is known as a _dependency graph,_ such as the one shown in Figure 12.

<figure><img src="../.gitbook/assets/Group 138 (2).png" alt=""><figcaption></figcaption></figure>

In this graph, nodes represent files and directed edges (arrows) indicate dependencies. If A -> B, then A directly depends on B, meaning that a modification to B requires A to be rebuilt. If A -> B and B -> C, then A is indirectly (or transitively) dependent on C. A modification to C requires B to be rebuilt, which in turn requires A to be rebuilt. Non-leaf nodes are labeled with commands to build them. A node without any dependencies is known as a _leaf_. Non-leaf nodes are labeled with commands to build them. Leafs are typically `.c` and `.h` files, which are not  "built". A dependency graph for our `testintmath` program is shown in Figure 12.3.&#x20;

A few observations about our dependency graph that are typical of C programs:

* 2 levels of dependencies. Execuitable depends on object files, and object files depend on .c and .h filesrelationship

#### Constructing a dependency graph

Constructing a dependency graph is quite simple. Let's now create one for our testintmath program.  This can be done by following a few simple steps:

1. Create a node for each of the program files (i.e., the `.c`, `.h`, `.o` files and the executable).
2. Draw an arrow from:
   * The executable to each of the `.o` files
   * Each `.o` file to its corresponding `.c` file
   * Each `.o` file to each `.h` file that is `#included` in the `.o` file's corresponding `.c` file
3. Annotate the executable and each object file with the command to build it

This results in the following dependency graph:

<figure><img src="../.gitbook/assets/Group 125 (1).png" alt="" width="563"><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>
