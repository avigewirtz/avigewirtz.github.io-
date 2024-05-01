# Introduction

In a nutshell, make is a software tool that automates the process of incremental builds. The key to understanding make is understanding what incremental builds are and how to implement it manually. Once you understand this, the mechanics and role of make become apparent.

{% hint style="warning" %}
Before reading this chapter, ensure you're familiar with the GCC build process. An overview is provided in [GCC Build Process](broken-reference/).
{% endhint %}





## Incremental builds



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

##



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

Going forward, if we modify one of the source files, we rebuild only the files affected by the change (i.e., the files dependent—directly or indirectly—on the modified file).

A modification to a file requires all the files pointing to it--directly or indirectly--to be rebuilt. For example, a modification to `testintmath.c` requires `testintmath.o` (which is directly dependent on `testintmath.c`) and `testintmath` (which is indirectly dependent on `testintmath.c`) to be rebuilt, but it does not require `intmath.o` to be rebuilt. The same idea applies to `intmath.c`. A modification to `intmath.h`, however, is more drastic. It requires `intmath.o`, `testintmath.o`, and `testintmath` to be rebuilt.&#x20;
