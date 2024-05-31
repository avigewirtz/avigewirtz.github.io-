# Introduction

In a nutshell, `make` is a software tool that automates the process of incremental builds. Incremental builds optimize the build process by recompiling only the code modules that have changed since the last build, rather than recompiling the entire project. This significantly reduces build times, making it especially important in large projects, where build times are a bottleneck. The key to understanding `make` is understanding how incremental builds work and how to implement them manually. Once you understand this, the mechanics and role of `make` become apparent.&#x20;

As a running example throughout this chapter, we'll use the `testintmath` program from precept 4, comprised of three files: `testintmath.c`, `intmath.c`, and `intmath.h`. For reference, the source code is provided below.



{% tabs %}
{% tab title="main.c" %}
```c
#include <stdio.h>
#include "add.h"
#include "mult.h"

int main() {
    int sum = add(5, 3);
    int product = mult(5, 3);
    printf("The result of adding 5 and 3 is: %d\n", result);
    printf("The The result of multiplying 5 and 3 is: %d\n", multiplied);
    return 0;
}
```
{% endtab %}

{% tab title="add.c" %}
```c
#include "add.h"

int add(int a, int b) {
    return a + b;
}
```
{% endtab %}

{% tab title="multiply.c" %}
```c
#include "mult.h"

int mult(int x, int y) {
    return x * y;
}
```
{% endtab %}

{% tab title="add.h" %}
```c
#ifndef ADD_INCLUDED
#define ADD_INCLUDED

int add(int x, int y);

#endif
```
{% endtab %}

{% tab title="mult.h" %}
```c
#ifndef MULT_INCLUDED
#define MULT_INCLUDED

int mult(int x, int y);

#endif
```
{% endtab %}
{% endtabs %}











#### Review: GCC Build Process



<figure><img src="../.gitbook/assets/Frame 30.png" alt=""><figcaption></figcaption></figure>

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

#### Incremental Builds In Action



#### Challenges of manually implementing Incremental Builds

As this example shows, implementing incremental builds manually is possible but it requires you to:

1. Keeo track of which source files have been modified since the last build.
2. Understand which object files are affected by these changes.&#x20;

Even for a small program like testintmath, this task isn’t particulurly exciting, though it is reasonably manageable. As programs grow larger, however, and the web of dependencies grows increasingly complex, this task becomes incredibly tedious and error-prone.

Consider a scenario, for example, where you modify a header file `A`, that is `#included` in, say, 20 of your program's `.c` files. You’d have to track down each one of these `.c` files and recompile it. Worse yet, imagine header file `A` is also `#include`d in header file `B`. You'd then have to also track down all `.c` files that `#include` `B` and recompile them.

For this reason, the `make` tool was developed, which automates the process of incremental builds. The section that follows describes how to use make.
