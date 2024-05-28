# Introduction

In a nutshell, `make` is a software tool that automates the process of incremental builds. Incremental builds optimize the build process by recompiling only the code modules that have changed since the last build, rather than recompiling the entire project. This significantly reduces build times, especially in larger projects. The key to understanding `make` is understanding what incremental builds are and how to implement them manually. Once you understand this, the mechanics and role of `make` become apparent. 
As a running example throughout this chapter, we'll use the testintmath program from precept 4, comprised of three files: testintmath.c, intmath.c, and intmath.h. For reference, the source code is provided below. 

### Review: GCC Build Process&#x20;

Recall that GCC builds C programs in four sequential stages: preprocessing, compilation, assembly, and linking. In the first stage, each .c file is sent to the preprocessor, which, among other things, inserts into each file all files specified with the #include directive. Each preprocessed file is a translation unit. In the next two stages, each translation unit is compiled and then asssmbled, resulting in a relocateable object file. Finally, the relocatable object files, including reocateblae object files from C standard library, are sent to the linker, which produces as output an executable object file--i.e., a single file that can be loaded into memory and executed.&#x20;

<figure><img src="../.gitbook/assets/Frame 27 (3).png" alt=""><figcaption></figcaption></figure>

### **How Incremental Builds Work**

Recall that by default, GCC does not retain intermediate files. For the purposes of incremental builds, .i and .s files are of no use (since we're not programming in them directly) , so we can leave those discraded. The key to incremental builds, however, is caching object files. This way, we can reuse them in later builds. When source code is modified, only affected object files are rebuilt, and then the new and old object files are linked, producing an updated executable. The general strategy for building a program with incremental builds is as follows:

* Think of building as a two step process. First step you build all object files that need to be built. Second step you build executable by linking all object files. In the first step, you build only the object files depend on the modified source files. Put another way, you invoke gcc -c on a .c file only if the resulting object file will be different from the one you already have from a previous build. Note that in the linking step, you always link all object files. Thus, incremental builds do not lower link times. However, linking is only a minor part of build process.&#x20;

<figure><img src="../.gitbook/assets/Frame 28 (1).png" alt=""><figcaption></figcaption></figure>

### Dependency graph

We mentioned that object file has to be rebuilt if&#x20;

A program's dependencies can be formally described with what is known as a _dependency graph,_ such as the one shown in Figure 12.

<figure><img src="../.gitbook/assets/Group 138 (2).png" alt=""><figcaption></figcaption></figure>

In this graph, nodes represent files and directed edges (arrows) indicate dependencies. If A -> B, then A directly depends on B, meaning that a modification to B requires A to be rebuilt. If A -> B and B -> C, then A is indirectly (or transitively) dependent on C. A modification to C requires B to be rebuilt, which in turn requires A to be rebuilt. Non-leaf nodes are labeled with commands to build them. A node without any dependencies is known as a _leaf_. Non-leaf nodes are labeled with commands to build them. Leafs are typically `.c` and `.h` files, which are not  "built". A dependency graph for our `testintmath` program is shown in Figure 12.3.&#x20;

A few observations about our dependency graph that are typical of C programs:

* 2 levels of dependencies. Execuitable depends on object files, and object files depend on .c and .h filesrelationship



#### Example

Let's demonstrate how this works in practice using the `testintmath` program from precept 4, whose source code is shown below.

{% tabs %}
{% tab title="testintmath.c (client)" %}
{% code lineNumbers="true" %}
```c
#include "intmath.h"
#include <stdio.h>

int main() {
  int i, j;
  printf("Enter the first integer:\n");
  scanf("%d", &i);
  printf("Enter the second integer:\n");
  scanf("%d", &j);
  printf("Greatest common divisor: %d.\n", gcd(i, j));
  printf("Least common multiple: %d.\n", lcm(i, j));
  return 0;
}
```
{% endcode %}
{% endtab %}

{% tab title="intmath.c (implementation)" %}
{% code lineNumbers="true" %}
```c
#include "intmath.h"

int gcd(int i, int j) {
  int temp;
  while (j != 0) {
      temp = i % j;
      i = j;
      j = temp;
  }
  return i;
}

int lcm(int i, int j) {
  return (i / gcd(i, j)) * j;
}
```
{% endcode %}
{% endtab %}

{% tab title="intmath.h (interface)" %}
{% code lineNumbers="true" %}
```c
#ifndef INTMATH_INCLUDED
#define INTMATH_INCLUDED

int gcd(int i, int j);
int lcm(int i, int j);

#endif
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Building testintmath for the first time

The first time we build `testintmath`, we build as usual. However, we ensure to cache the object files.&#x20;



compile all source files. The key, however, is that we cache the object files, so we can reuse them in later builds. This can be done by building `testintmath` in two steps. First, we translate `intmath.c` and `testintmath.c` into object files `intmath.o` and `testintmath.o`:

```bash
gcc217 -c intmath.c testintmath.c 
```

Then, we link `intmath.o` and `testintmath.o`, producing the executable `testintmath`:

```bash
gcc217 intmath.o testintmath.o -o testintmath
```

This process is is summarized in Figure 1.

{% hint style="info" %}
Fundamentally, the underlying build process is the same irrespective of whether we build our program via two commands:

```bash
gcc217 -c intmath.c testintmath.c
gcc217 intmath.o testintmath.o -o testintmath
```

Or via single command:

```bash
gcc217 intmath.c testintmath.c -o testintmath
```

The only difference between the two-command and single-command approaches is that the former retains the intermediate object files while the latter does not.&#x20;
{% endhint %}

#### Rebuilding testintmath

When we rebuild `testintmath`, we only recompile the source file's that will produce an object file different from the one we already have from the last build.&#x20;

**Scenario 1: Modifying a .c File**

When a `.c` file is modified, the effect is typically localized, since `.c` files aren't normally `#included` in other files. Thus, only the modified `.c` file has to be recompiled. In our case, if we modify `intmath.c`, for example, we recompile it alone. The steps are straightforward:

1. Recompile only `intmath.c`:

```
gcc217 -c intmath.c
```

2. Link the newly created `intmath.o` with the unchanged `testintmath.o` to produce the updated executable:&#x20;

```
gcc217 intmath.o testintmath.o -o testintmath
```

**Scenario 2: Modifying a .h File**

When a header file is modified, the effects can be quite dramatic, since all `.c` files that `#include` it have to be recompiled. In our case, if we modify `intmath.h`, we'd have to recompile both `intmath.c` and `testintmath.c`, since they both `#include` it.&#x20;

```bash
gcc217 -c intmath.c testintmath.c -o testintmath
gcc217 intmath.o testintmath.o -o testintmath
```
