# Introduction

In a nutshell, make is a software tool that automates the process of incremental builds. The key to understanding make is understanding what incremental builds are and how to implement it manually. Once you understand this, the mechanics and role of make become apparent.

{% hint style="warning" %}
Before reading this chapter, ensure you're familiar with the GCC build process. An overview is provided in [GCC Build Process](broken-reference).
{% endhint %}

### Incremental builds <a href="#incremental-builds" id="incremental-builds"></a>

Incremental builds is an approach where each build builds off the previous one. The first time you build a program, you compile all of its source files, but in subsequent builds, you compile only the source files that have changed or were affected by changes.

The key to implementing incremental builds is to always build a program in two steps. First, you compile the source files into object files. This is done by invoking `gcc217` with the `-c` option. Importantly, you compile only the source files that would produce object files different from the ones you already have from the previous build. Second, you link all the object files (the "new "and "old") together to produce the executable.

{% hint style="info" %}
As we saw in GCC Build Process, GCC
{% endhint %}

### Dependency graphs <a href="#dependency-graphs" id="dependency-graphs"></a>

To know which files need to be rebuilt after changes are made to the source code, you need to have a good grasp of the dependencies among the program's files. An efficient method of doing so is by constructing a dependency graph, as example of which is shown Figure 2.3.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fo07Od3DcI8FNUHkrHKNH%2Fuploads%2FsGcSONmRx6U9wybclUgf%2FGroup%20132.png?alt=media&#x26;token=5d3a2178-5136-4154-a67a-04f78958625c" alt=""><figcaption></figcaption></figure>

In this graph, the nodes represent files, which (when applicable) are annotated with the commands to build them. The arrows represent dependencies. If file A points to file B, then A directly depends on B, meaning changes to B require A to be rebuilt. If A points to B and B points to C, then A is indirectly (or transitively) dependent on C. The distinction will become clear when we discuss makefiles.Notice the relationship between object files and header files. Multiple object files can depend on a single header file (e.g., `a.o` and `b.o` both depend on `x.h`), and an object file can depend on multiple header files (e.g., `b.o` depends on both `x.h` and `y.h`). While such relationships are possible for C files, in practice they're rare. Typically, there is a one-to-one relationship between object files and C files, as is the case in our graph.

### Example <a href="#example" id="example"></a>

To demonstrate incremental builds, we'll use the `testintmath` program from precept 4, whose source code is shown below.testintmath.c (client)intmath.c (implementation)intmath.h (interface)1#include "intmath.h"2​3int gcd(int i, int j) {4int temp;5while (j != 0) {6temp = i % j;7i = j;8j = temp;9}10return i;11}12​13int lcm(int i, int j) {14return (i / gcd(i, j)) \* j;15}To build `testintmath`, we invoke `gcc217` with the `-c` option on `intmath.c` and `testintmath.c`:gcc217 -c intmath.c testintmath.cThis translates `intmath.c` and `testintmath.c` into object files `intmath.o` and `testintmath.o`. We then we invoke `gcc217` on `intmath.o` and `testintmath.o`:
