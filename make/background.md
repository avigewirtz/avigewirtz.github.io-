# Introduction

In a nutshell, make is a software tool that automates the process of incremental builds. The key to understanding make is understanding what incremental builds are and how to implement it manually. Once you understand this, the mechanics and role of make become obvious.

{% hint style="warning" %}
Before reading this chapter, ensure you're familiar with the GCC build process. An overview is provided in [GCC Build Process](broken-reference).
{% endhint %}

## Incremental builds

Incremental builds is an approach where each build builds off the previous one. The first time you build a program, you compile all of its source files. In subsequent builds, however, you compile only the source files that have changed since the last build or were affected by changes.

They key to implementing incremental builds is to always build a program in two steps. In the first step, you compile the source files into object files. This is done by invoking `gcc217` with the `-c` option. The key is that you only compile those source files that would produce object files different from those generated in the previous build. In the second step, you link all the object files (i.e., the "new" and "old" object files) together to produce the executable.

{% hint style="info" %}
**Note**: As we saw in [GCC Build Process](broken-reference), GCC builds C programs in four sequential stages: preprocessing, compilation, assembly, and linking. This is the case even if we invoke GCC without any options to control the build process. For example, if we invoke:

`gcc217 foo.c bar.c -o foobar`

GCC will preprocess, compile, assemble, and link our program, producing the executable `foobar`. By default, however, GCC does not retain the intermediate (i.e., `.i`, `.s`, and `.o`) files generated during the build process. To implement incremental builds, however, we need to retain the `.o` files. To do so, we instead build `foobar` in two steps. First, we preprocess, compile, and assemble `foo.c` and `bar.c`, producing `foo.o` and `bar.o`:

`gcc217 -c foo.c bar.c`

Then, we link `foo.o` and `bar.o`, producing the executable `foobar`:

`gcc217 foo.o bar.o -o foobar`

Fundamentally, the only difference between these two build approaches is that the latter retains the intermediate object files while the former does not. &#x20;
{% endhint %}

## Dependency graphs

To know which files need to be rebuilt after changes to the source code, you need to have a good grasp of the program's dependencies. An efficient method of doing so is by constructing a dependency graph for your program, as example of which is shown Figure 2.3.&#x20;

<figure><img src="../.gitbook/assets/Group 132.png" alt=""><figcaption></figcaption></figure>

In this graph, the nodes represent files, which (when applicable) are annotated with the commands to build them. The arrows represent dependencies. If file A points to file B, then A directly depends on B. In other words, a change to B requires A to be rebuilt. If A points to B, which in turn points to C, then A is indirectly (or transitively) dependent on C. The distinction will become clear when we discuss makefiles.

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
  scanf("%sd", &i);
  printf("Enter the second integer:\n");
  scanf("%sd", &j);
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

The first time we build `testintmath`, we invoke `gcc217` with the `-c` option on `intmath.c` and `testintmath.c`:

```
gcc217 -c intmath.c testintmath.c 
```

This compiles `intmath.c` and `testintmath.c` into object files `intmath.o` and `testintmath.o`. We then we invoke `gcc217` on `intmath.o` and `testintmath.o`:

```
gcc217 intmath.o testintmath.o -o testintmath
```

This links the object files together, generating the executable `testintmath`.&#x20;

Going forward, if we modify a source file, we only need to rebuild the affected `.o` files, and then link all the `.o` files together to produce the updated executable. Let's visualize the dependencies for testintmath with a dependency graph. We can construct one by following these simple steps:

1. Create a node for each of the program files (i.e., the .c, .h, .o files and the executable).&#x20;
2. Draw an arrow from:
   * The executable to each of the .o files
   * Each .o file to its corresponding .c file
   * Each .o file to each .h file that is #included in the .o file's corresponding .c file
3. Annotate the executable and each object file with the command to build it

This results in the following dependency graph:

<figure><img src="../.gitbook/assets/Group 125 (1).png" alt=""><figcaption></figcaption></figure>

As we can see from the dependency graph, a modification to `testintmath.c` requires `testintmath.o` and `testintmath` to be rebuilt, but it does not require `intmath.o` to be rebuilt. Similarly, a modification to `intmath.c` requires `intmath.o` and `testintmath` to be rebuilt, but it does not require `testintmath.o` to be rebuilt. A modification to `intmath.h` is more drastic, however. It requires `intmath.o`, `testintmath.o`, and `testintmath` to be rebuilt.&#x20;
