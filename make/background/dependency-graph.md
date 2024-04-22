# Dependency graph

To know which files have to be rebuilt after a change, you need to have a good understanding of the dependencies in a C program. Easiest way to understand dependencies is by visualizing it with a dependency graph. Constructing a dependency graph is quite straightforward. An algorithm is provided below.&#x20;

1. We create a node for each `.c` and `.h` file in our program, and we label each node with the name of the file it represents. For example, if our programs consists of the files `a.c`, `b.c`, `c.c`, `d.c`, `x.h`, and `y.h`, we'd create the following nodes:

<figure><img src="../../.gitbook/assets/Group 92.png" alt=""><figcaption></figcaption></figure>

2. For each `.c` file, we create a node for it's corresponding `.o` file, and draw an arrow from the `.c` node to its corresponding `.o` node.

<figure><img src="../../.gitbook/assets/Group 102 (2).png" alt=""><figcaption></figcaption></figure>

&#x20;       An arrow from A to B indicates that B depends on A. If A is modified, B has to be rebuilt.

3. For each .h file, if it's #included in a .c file, draw an arrow from the .h file to the same .o file that the .c file points to. For example, if x.h is #included in a.c and b.c, and y.h is included in b.o, c.o, and d.o, we'd draw the following:

<figure><img src="../../.gitbook/assets/Group 99.png" alt=""><figcaption></figcaption></figure>

4. Create a node for the executable, and draw an arrow from each .o node to the executable:&#x20;

<figure><img src="../../.gitbook/assets/Group 100.png" alt=""><figcaption></figcaption></figure>

5. For extra clarity, it helps to write the commands necessary to build each object file and the executable:&#x20;

<figure><img src="../../.gitbook/assets/Group 111 (1).png" alt=""><figcaption></figcaption></figure>

this graph makes it obvious which files have to be rebuiltn after one of the source files is modified. For example, if we modify a.c, we have to rebuild a.o and a.out. This is done by invoking:

```
gcc217 -c a.c
gcc217 a.o b.o c.o d.o
```

If we modify y.h, we have to rebuild b.o, c.o, d.o, and a.out:

```
gcc217 -c b.c c.c d.c
gcc217 a.o b.o c.o d.o
```
