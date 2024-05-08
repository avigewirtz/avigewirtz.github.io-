# Introduction

In a nutshell, make is a software tool that automates the process of incremental builds. The key to understanding make is understanding what incremental builds are and how to implement them manually. Once you grasp this, the mechanics and role of make become clear.

{% hint style="warning" %}
Before reading this chapter, ensure you're familiar with the GCC build process. An overview is provided in [GCC Build Process](broken-reference/).
{% endhint %}

### **Incremental Builds**

Incremental builds optimize the build process by recompiling only the code modules that have changed since the last build, instead of the entire project. This significantly reduces build times, especially in larger projects.

Implementing incremental builds requires a change in how we approach the build process. Instead of treating the source files of a program as a monolithic unit that are always built together, we instead think of the source files as a collection of independent modules, each of which can be compiled independently. We break down the build process into two phases:

1. **Separate Compilation:** Source files are individually translated into object files. This is done by invoking `gcc217` with the `-c` option.
2. **Linking:** The resulting object files are linked together to create the final executable.

This approach allows for targeted builds: when the program is modified, only the affected source files are recompiled. The updated object files are then linked with the unaffected object files from previous builds, generating a new executable.

{% hint style="info" %}
As we saw in [GCC Build Process](broken-reference/), GCC always builds C programs in four sequential stages: preprocessing, compilation, assembly, and linking. When I distinguish between "single-step" and "two-step" approaches, I'm referring to how we might conceptualize the build process, not the underlying GCC operations.&#x20;
{% endhint %}

### Example

As an example, consider the `testintmath` program from precept 4, whose source code is shown below.

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

The key to incremental builds is we build `testintmath` in two steps, rather than in a single step (i.e, by invoking `gcc217 intmath.c testintmath.c -o testintmath`).&#x20;

First, we translate `intmath.c` and `testintmath.c` into object files `intmath.o` and `testintmath.o`:

```bash
gcc217 -c intmath.c testintmath.c 
```

Then, we link `intmath.o` and `testintmath.o`, producing the executable `testintmath`:

```bash
gcc217 intmath.o testintmath.o -o testintmath
```

This process is is summarized in Figure 1.

<figure><img src="../.gitbook/assets/Group 147 (4).png" alt="" width="563"><figcaption></figcaption></figure>

Going forward, if we modify one of the `.c` files, we don't need to recompile everything—just the file that changed. For instance, if we modify `intmath.c`, we'd invoke `gcc217 -c` on `intmath.c` alone:

```bash
gcc217 -c intmath.c
```

We'd then link the "new" and "old" object files--`intmath.o` and `testinamth.o` respectively--to generate the updated executable:&#x20;

```bash
gcc217 -c intmath.c
gcc217 intmath.o testintmath.o -o testintmath
```

#### Modifying a header file

In general, modifying a header is more dramatic than modifying a `.c` file, since you have to recompile all `.c` files that #include it--whether directly or indirectly. In our case, if we modify `intmath.h`, we'd have to recompile both `intmath.c` and `testintmath.c`, since it's #included in both of them. For this reason, great care should be taken before modifying a header file.&#x20;
