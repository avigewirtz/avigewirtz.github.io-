# Incremental builds and dependency graphs 

Incremental builds is an approach where each build builds off the previous one. The first time you build a program, you compile all of its source files. In subsequent builds, however, you compile only the source files that have changed since the last build or were affected by changes.

They key to implementing incremental builds is to always build a program in two steps. In the first step, you compile the source files into object files. This is done by invoking `gcc217` with the `-c` option. The caveat is that you only compile those source files that would produce object files different from those generated in the previous build. In the second step, you link all the object files (i.e., the "new" and "old" object files) together to produce the executable.&#x20;




Whenever a change is made to one of the source files, the executable has to be rebuilt. This is obvious. The challenge is figuring out which object files have to be rebuilt. This is less obvious. To know which object files have to be rebuilt after changes, you need to have a good understanding of the project's dependencies. The easiest way to understand dependencies is by visualizing it with a dependency graph. Constructing a dependency graph is quite straightforward. An algorithm is provided below.&#x20;

<figure><img src="../../.gitbook/assets/Group 137.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Group 132.png" alt=""><figcaption></figcaption></figure>











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