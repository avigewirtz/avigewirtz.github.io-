# Writing a Simple Makefile

Assume the working directory contains `testintmath`'s source files (i.e., `testintmath.c`, `intmath.c`, and `intmath.h`). To build `testintmath` with `make`, the first step is to create a makefile in the working directory. You can name the makefile whatever you'd like, but `make` automatically searches for a file named `makefile` or `Makefile`, making these names more convenient. To create the makefile, run the following command:

```bash
touch Makefile
```

The next step is to populate the Makefile `testintmath`'s dependency graph. As we mentioned earlier, a dependency graph is a directed graph that contains two pieces of information:

* The dependencies between the source files, object files, and the executable.&#x20;
* The commands to build each each file from its dependencies.&#x20;

Visually, it looks like this:

<figure><img src="../../.gitbook/assets/Frame 33.png" alt="" width="563"><figcaption></figcaption></figure>

The dependencies are indicated by arrows, and the each file with dependencies is labeled with the command to build it from its dependencies. In make temrinology, these files are known as targets.&#x20;

The neat thing about dependency graphs is they make it really easy to see which files are rendered obsolete by changes to one of the source files. Just follow the arrows. Any file which directly or indirectly points to the modified source file is rendered obsolete. So, for example, if intmath.c is modified, intmath.o and testintmath are rendered obsolete.&#x20;

There is a difference, however, between direct and transitive dependencies. For example, intmath.o directly depends on intmath.c, but testintmath transitively depends on intmath.o.

{% hint style="info" %}
NOTE BOX: Note that we're not including stdio.h and stdlib.h, even though testintmath.c #includes them, since we don't modify these files, and as such don't need to be concerned with them in makefiles.&#x20;
{% endhint %}

Translating this dependency graph into a Makefile is remarkably straightforward. We create what is known as a _dependency rule_ for each target in the dependency graph. The target's in our dependency graph correspond to the object files (intmath.o and testintmath.o) and the executable (testintmath). Dependency rules have the following syntax:

```
target: dependencies
<tab> command
```

This syntax should hopefully be pretty self-explanatory, but note a couple of things:

* dependencies refers to direct dependencies, not trastitive ones. So, for example, in the rule for testintmath, we list testintmath.o and intmath.o only. We don't list&#x20;
* the command must be preceded by a tab

Here is the complete makefile for testintmath:

```makefile
testintmath: testintmath.o intmath.o
    gcc217 testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc217 -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc217 -c intmath.c
```

This makefile is extremely simple, but it captures the core of make.&#x20;
