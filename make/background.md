# Introduction

In a nutshell, `make` is a software tool that automates the process of incremental builds. Incremental builds optimize the build process by recompiling only the code modules that have changed since the last build, rather than recompiling the entire project. This significantly reduces build times, especially in larger projects. The key to understanding `make` is understanding what incremental builds are and how to implement them manually. Once you understand this, the mechanics and role of `make` become apparent.&#x20;

As a running example throughout this chapter, we'll use the testintmath program from precept 4, comprised of three files: testintmath.c, intmath.c, and intmath.h. For reference, the source code is provided below.

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

#### Review: GCC Build Process

Recall that the GCC build process involves four sequential stages: preprocessing, compilation, assembly, and linking. This process for our `testintmath` program is shown in Figure 4. For the purposes of incremental builds, recall the following:

* First three stages are performed on each file independently.&#x20;
* In the first stage, the preprocessor inserts the contents of #included files into each file. The result is that our program, initially distributed across two .c files and _n_ .h files, is now consolidated into two .i files—testintmath.i and intmath.i. These files are known as translation units.
* In the second and third stages, each file is compiled and assembled, resulting in relocatable object files testintmath.o and intmath.o.
* In the final stage, the linker combines testintmath.o and intmath.o, along with relavant relocateble object files from C library, producing as output executable object file testintmath.
* By default, object fils not retained. Can retain them via the -c option.&#x20;

#### How Incremental Builds Work

As is aparent from Figure 14, each relocatebale object file is derived from, or _depends_ on, its corresponding C file, as well as any header files #included in the correspinding C file. It is _not_ derived from any other C file. For example, intmath.o depends on intmath.c and intmath.h. It does not depend on testintmath.c or stdio.h. Thus, so long as we retained object files, a change to testintmath.c does not require intmath.o to be rebuilt. Only testintmath.o and testintmath must be rebuilt (testintmath.o by compiling testintmath.c, and testintmath by linking intmath.o and testintmath.o). Similarly, a change to intmath.c does not require testintmath.o to be rebuilt--only intmath.o and testintmath must be rebuilt. Consider the effect of modifying intmath.h. Because both .c files #include it, intmath.o, testintmath.o, and testintmath must be rebuilt. Figure 15 summarizes use of incremental builds with testintmath.&#x20;

<figure><img src="../.gitbook/assets/Frame 28 (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Fundamentally, the underlying GCC build process is the same irrespective of whether we build our program via two commands:

```bash
gcc217 -c intmath.c testintmath.c
gcc217 intmath.o testintmath.o -o testintmath
```

Or via single command:

```bash
gcc217 intmath.c testintmath.c -o testintmath
```

The only difference between the two-command and single-command approaches is that the former retains the intermediate object files while the latter does not.
{% endhint %}
