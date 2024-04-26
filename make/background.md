# Introduction

In a nutshell, make is a software tool that automates the process of incremental builds. The key to understanding make is understanding what incremental builds are and how to implement it manually. Once you understand this, the mechanics and role of make become apparent.

{% hint style="warning" %}
Before reading this chapter, ensure you're familiar with the GCC build process. An overview is provided in [GCC Build Process](broken-reference).
{% endhint %}

## Incremental builds

Incremental builds is an approach where each build builds off the previous one. The first time you build a program, you compile all of its source files, but in subsequent builds, you compile only the source files that have changed or were affected by changes.

They key to implementing incremental builds is to always build a program in two steps. In the first step, you compile the source files into object files. This is done by invoking `gcc217` with the `-c` option, which instructs GCC to halt the build process after assembly. Importantly, you compile only the source files that would produce object files different from the ones you already have from the previous build. In the second step, you link all the object files (the "new "and "old") together to produce the executable.&#x20;

For example, suppose we have a C program comprised of two `.c` files: `foo.c` and `bar.c`. We build our program in two steps. First, we invoke `gcc217 -c` on `foo.c` and `bar.c`:

```
gcc217 -c foo.c bar.c
```

Then, we link `foo.o` and `bar.o`, producing the executable:

```bash
gcc217 foo.o bar.o -o foobar
```

Note that `-o foobar` instructs GCC to name the executable `foobar`, rather than `a.out`.&#x20;

{% hint style="info" %}
As we saw in [GCC Build Process](broken-reference), GCC builds C programs in four sequential stages: preprocessing, compilation, assembly, and linking. This is the case whether we build our program via a single command:

```bash
gcc217 foo.c bar.c -o foobar
```

Or via two commands:

```bash
gcc217 -c foo.c bar.c
gcc217 foo.o bar.o -o foobar
```

Fundamentally, the only difference between these two approaches is that the two-command approach retains the intermediate object files while the single-command approach does not.
{% endhint %}

## Dependency graphs

To know which files need to be rebuilt after changes are made to one or more source files, you need to have a good grasp of the dependencies among the program's files. An efficient method of doing so is by constructing a dependency graph, as example of which is shown Figure 2.3.&#x20;

<figure><img src="../.gitbook/assets/Group 132.png" alt=""><figcaption></figcaption></figure>

In this graph, the nodes represent files, which (when applicable) are annotated with the commands to build them. The arrows represent dependencies. If file A points to file B, then A directly depends on B, meaning changes to B require A to be rebuilt. If A points to B and B points to C, then A is indirectly (or transitively) dependent on C. The distinction will become clear when we discuss makefiles.

Notice the relationship between object files and header files. Multiple object files can depend on a single header file (e.g., `a.o` and `b.o` both depend on `x.h`), and an object file can depend on multiple header files (e.g., `b.o` depends on both `x.h` and `y.h`). While such relationships are possible for C files, in practice they're rare. Typically, there is a one-to-one relationship between object files and C files, as is the case in our graph.

## Example

To demonstrate incremental builds, we'll use the `testintmath` program from precept 4, whose source code is shown below.&#x20;

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

To build `testintmath`, we invoke `gcc217` with the `-c` option on `intmath.c` and `testintmath.c`:&#x20;

```
gcc217 -c intmath.c testintmath.c 
```

This translates `intmath.c` and `testintmath.c` into object files `intmath.o` and `testintmath.o`. We then we invoke `gcc217` on `intmath.o` and `testintmath.o`:

```
gcc217 intmath.o testintmath.o -o testintmath
```

This links the object files together, generating the executable `testintmath`.&#x20;

Going forward, if we modify a source file, we need to only rebuild the affected `.o` files. To see how changes affect the .o files, let's construct a dependency graph.  This can be done by following these simple steps:

1. Create a node for each of the program files (i.e., the `.c`, `.h`, `.o` files and the executable).&#x20;
2. Draw an arrow from:
   * The executable to each of the `.o` files
   * Each `.o` file to its corresponding `.c` file
   * Each `.o` file to each `.h` file that is `#included` in the `.o` file's corresponding `.c` file
3. Annotate the executable and each object file with the command to build it

This results in the following dependency graph:

<figure><img src="../.gitbook/assets/Group 125 (1).png" alt=""><figcaption></figcaption></figure>

A modification to a file requires all the files pointing to it--directly or indirectly--to be rebuilt. A modification to `testintmath.c` requires `testintmath.o` (which is directly dependency on `testintmath.c`) and `testintmath` (which is indirectly dependent on `testintmath.c`) to be rebuilt, but it does not require `intmath.o` to be rebuilt. Similarly, a modification to `intmath.c` requires `intmath.o` and `testintmath` to be rebuilt, but it does not require `testintmath.o` to be rebuilt. A modification to `intmath.h` is more drastic, however. It requires `intmath.o`, `testintmath.o`, and `testintmath` to be rebuilt.&#x20;
