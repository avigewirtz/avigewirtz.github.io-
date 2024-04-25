# Dependency graph

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
