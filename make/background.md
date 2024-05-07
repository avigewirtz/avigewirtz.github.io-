# Introduction

In a nutshell, make is a software tool that automates the process of incremental builds. The key to understanding make is understanding what incremental builds are and how to implement it manually. Once you understand this, the mechanics and role of make become apparent.

{% hint style="warning" %}
Before reading this chapter, ensure you're familiar with the GCC build process. An overview is provided in [GCC Build Process](broken-reference/).
{% endhint %}

### **Incremental Builds**

Incremental builds optimize the build process by recompiling only the code modules that have changed since the last build, instead of the entire project. This significantly reduces build times, especially in larger projects.

Implementing incremental builds requires a change in how we approach the build process. Instead of a monolithic "all-at-once" build, we break it down into two stages:

1. **Separate Compilation:** Source files are individually translated into object files.&#x20;
2. **Linking:** The resulting object files are linked together to create the final executable.&#x20;

This approach allows for targeted builds: when the program modified, only the affected source files need to be recompiled. The updated object files are then linked with the unaffected object files from previous builds, generating a new executable. &#x20;

#### Example

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

### Building testintmath

We build `testintmath` in two steps. First, we translate `intmath.c` and `testintmath.c` into object files `intmath.o` and `testintmath.o`. This is done by invoking `gcc217` with the `-c` option:&#x20;

```
gcc217 -c intmath.c testintmath.c 
```

Then, we link `intmath.o` and `testintmath.o`, producing the executable `testintmath`:

```
gcc217 intmath.o testintmath.o -o testintmath
```

This process is is summarized in Figure 1.

<figure><img src="../.gitbook/assets/Group 147 (3).png" alt="" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
As we saw in [GCC Build Process](broken-reference/), GCC always builds C programs in four sequential stages: preprocessing, compilation, assembly, and linking. This is the case whether we build `testintmath` via a single command:

```bash
gcc217 intmath.c testintmath.c -o testintmath
```

Or via two commands:

```bash
gcc217 -c intmath.c testintmath.c 
gcc217 intmath.o testintmath.o -o testintmath
```

Fundamentally, the only difference between these two build approaches is that the two-command approach retains the intermediate object files while the single-command approach does not.

When I distinguish between "monolithic" and "two-step" approaches, I'm referring to how we might conceptualize the build process, not the underlying GCC mechanisms.
{% endhint %}

### &#x20;Rebuilding `testintmath`

Whenever a change is made to the source code, we&#x20;

Now suppose we modify intmath.c. To rebuild testintmath, we recompile intmath.c only, and then link the intmath.o

A modification to a file requires all the files pointing to it--directly or indirectly--to be rebuilt. For example, a modification to `testintmath.c` requires `testintmath.o` (which is directly dependent on `testintmath.c`) and `testintmath` (which is indirectly dependent on `testintmath.c`) to be rebuilt, but it does not require `intmath.o` to be rebuilt. The same idea applies to `intmath.c`. A modification to `intmath.h`, however, is more drastic. It requires `intmath.o`, `testintmath.o`, and `testintmath` to be rebuilt.&#x20;
