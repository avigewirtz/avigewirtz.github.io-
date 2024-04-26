# Dependency graphs

To know which files need to be rebuilt after a change to the source code, you need to have a good grasp of the program's dependencies. For our testintmath program, which consisted of only 3 source files, keeping track of the dependencies was quite straightforward. figuring our the dependencies TA dependency graph clearly shows which object files need to be rebuilt after changes to the source code. , making it easy to see which files depend on which. To know which object files have to be rebuilt, you need to have a good grasp of the project's dependencies. The easiest way to understand dependencies is by visualizing it with a dependency graph. Constructing a dependency graph is quite straightforward. An algorithm is provided below.

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



As we mentioned earlier, we only rebuild an object file if it will produce a version different than the one generated in the previous build. To know when this is the case, you need to have a good understanding of the program's dependencies. Easiest way to understand dependencies is by visualizing it with a dependency graph. Constructing a dependency graph is quite straightforward. An algorithm is provided below.&#x20;

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
