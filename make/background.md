# Introduction

In a nutshell, `make` is a software tool that automates the process of incremental builds. The key to understanding `make` is understanding what incremental builds are and how to implement them manually. Once you understand this, the mechanics and role of `make` become apparent

{% hint style="warning" %}
Before reading this chapter, ensure you're familiar with the GCC build process. An overview is provided in [GCC Build Process](broken-reference/).
{% endhint %}

### **Incremental Builds**

Incremental builds optimize the build process by recompiling only the code modules that have changed since the last build, instead of the entire project. This significantly reduces build times, especially in larger projects.

Implementing incremental builds requires a change in how we approach the build process. Instead of treating the source files of a program as a monolithic unit that are always built together, we instead think of the source files as a collection of independent modules that can be compiled independently. We break down the build process into two steps:

1. **Translation:** Source files are individually translated into object files. This is done by invoking `gcc217` with the `-c` option.&#x20;
2. **Linking:** The resulting object files are linked together to create the final executable.

This approach allows for targeted builds: when the program is modified, only the affected source files are recompiled. The updated object files are then linked with the unaffected object files from previous builds, generating a new executable.

{% hint style="info" %}
**Note**: Under the hood, "translation" is technically a three step process, involving preprocessing, compilation proper, and assembly. For the purposes of incremental builds, however, we can conceptualize translation as a single step, in which the source files are converted to object files.&#x20;
{% endhint %}

### Example

We'll demonstrate incremental builds using the `testintmath` program from precept 4, whose source code is shown below.

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

### Building testintmath for the first time

The first time we build `testintmath`, we compile all source files. The key, however, is that we cache the object files, so we can reuse them in later builds. This can be done by building `testintmath` in two steps. First, we translate `intmath.c` and `testintmath.c` into object files `intmath.o` and `testintmath.o`:

```bash
gcc217 -c intmath.c testintmath.c 
```

Then, we link `intmath.o` and `testintmath.o`, producing the executable `testintmath`:

```bash
gcc217 intmath.o testintmath.o -o testintmath
```

This process is is summarized in Figure 1.

<figure><img src="../.gitbook/assets/Group 147 (4).png" alt="" width="563"><figcaption></figcaption></figure>

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

### Rebuilding testintmath

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
