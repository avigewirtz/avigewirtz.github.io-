# Introduction

In a nutshell, make is a software tool that automates the process of incremental builds. The key to understanding make is understanding what incremental builds are and how to implement it manually. Once you understand this, the mechanics and role of make become apparent.

{% hint style="warning" %}
Before reading this chapter, ensure you're familiar with the GCC build process. An overview is provided in [GCC Build Process](broken-reference/).
{% endhint %}

## Incremental builds

Incremental builds are a technique where you compile only the parts of a program that have changed since the last build, rather than recompiling the entire program. Implementing incremental builds requirs a shift in our way of thinking about builds. We typically think of builds as a single-step process, where the executable is built from the source files. For example, suppose we have a program with three source files: foo.c, bar.c, and baz.c. For simplicity, we'll assume neither of these files #include any other files. To build the executable, we might invoke:

```
gcc217 foo.c bar.c baz.c -o foobarbaz
```

<figure><img src="../.gitbook/assets/Group 175 (2).png" alt="" width="375"><figcaption></figcaption></figure>

We build foobarbaz from foo.c, bar.c and baz.c. While this build appraoch is simple, the downside is that if any of the source files are changed, all of them them have to be recompiled in order to generate a new executable.&#x20;

The key to incremental builds is we instead think of building as a two-step process. In the first step, we build object files from the source files. This is done by compiling the source files with the -c option:

```
gcc217 -c foo.c bar.c baz.c
```

In the second step, we build the executable by linking the object files:

```
gcc217 foo.o bar.o baz.o -o foobarbaz
```

The benefit to this approach is if a change is made to one of the source files, such as baz.c for example, only bar.c needs to be recompiled. We then link the newly generated bar.o with the foo.o and baz.o, producing an updated executable (Figure 12).&#x20;

<figure><img src="../.gitbook/assets/Frame 7 (1).png" alt="" width="563"><figcaption></figcaption></figure>

## Dependencies

The key to effective incremental builds is accurate dependency tracking. We must precisely know which files depend on which, so we can determine exactly what needs to be recompiled when a file changes.

In the previous example, we used an extremely simple model, where each object file depended on a single file. In this case, dependency tracking is extremely easy. executable depends on .o files. Each .o file depends on .c file.&#x20;

In practice, trasnslation units typically comprise multiple files. A translation unit is not only the .c file being invoked with gcc, but all files included directly or indirectly. Let's make our example more realiztic:

<figure><img src="../.gitbook/assets/Group 184.png" alt="" width="375"><figcaption></figcaption></figure>



## Dependency graph

A program's dependencies can be formally described via a dependency graph, such as the one shown in Figure 2.3.

<figure><img src="../.gitbook/assets/Group 132.png" alt=""><figcaption></figcaption></figure>

In this graph, the nodes represent files, which (when applicable) are annotated with the commands to build them. The arrows represent dependencies. If file A points to file B, then A directly depends on B, meaning changes to B require A to be rebuilt. If A points to B and B points to C, then A is indirectly (or transitively) dependent on C. A change to C requires B to be rebuilt, which in turn requires A to be rebuilt. The practical distinction between direct and indirect dependencies will become more apparent when we discuss Makefiles.

Notice the relationship between object files and header files in our dependency graph. Multiple object files can depend on a single header file (e.g., `a.o, b.o` and c`.o` all depend on y`.h`), and an object file can depend on multiple header files (e.g., `b.o` depends on both `x.h` and `y.h`). While such relationships are possible for C files, in practice they're rare. Typically, there is a one-to-one relationship between object files and C files, as is the case in our graph.

## Example

To demonstrate incremental builds, we'll use the `testintmath` program from precept 4, whose source code is shown below.

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

To build `testintmath`, we invoke `gcc217` with the `-c` option on `intmath.c` and `testintmath.c`:

```
gcc217 -c intmath.c testintmath.c 
```

This translates `intmath.c` and `testintmath.c` into object files `intmath.o` and `testintmath.o`. We then link `intmath.o` and `testintmath.o` together, producing the executable `testintmath`:

```
gcc217 intmath.o testintmath.o -o testintmath
```

Going forward, if we modify one of the source files, we rebuild only the files affected by the change (i.e., the files dependent—directly or indirectly—on the modified file). Let's construct a dependency graph for our program. This can be done by following a few simple steps:

1. Create a node for each of the program files (i.e., the `.c`, `.h`, `.o` files and the executable).
2. Draw an arrow from:
   * The executable to each of the `.o` files
   * Each `.o` file to its corresponding `.c` file
   * Each `.o` file to each `.h` file that is `#included` in the `.o` file's corresponding `.c` file
3. Annotate the executable and each object file with the command to build it

This results in the following dependency graph:

<figure><img src="../.gitbook/assets/Group 125 (1).png" alt=""><figcaption></figcaption></figure>

A modification to a file requires all the files pointing to it--directly or indirectly--to be rebuilt. For example, a modification to `testintmath.c` requires `testintmath.o` (which is directly dependent on `testintmath.c`) and `testintmath` (which is indirectly dependent on `testintmath.c`) to be rebuilt, but it does not require `intmath.o` to be rebuilt. The same idea applies to `intmath.c`. A modification to `intmath.h`, however, is more drastic. It requires `intmath.o`, `testintmath.o`, and `testintmath` to be rebuilt.&#x20;

{% hint style="info" %}
As we saw in [GCC Build Process](broken-reference/), GCC builds C programs in four sequential stages: preprocessing, compilation, assembly, and linking. This is the case whether we build our program via a single command:

```bash
gcc217 foo.c bar.c baz.c -o foobarbaz
```

Or via two commands:

```bash
gcc217 -c foo.c bar.c baz.c 
gcc217 foo.o bar.o baz.o -o foobarbaz 
```

Fundamentally, the only difference between these two build approaches is that the two-command approach retains the intermediate object files while the single-command approach does not.
{% endhint %}
