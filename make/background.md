# Introduction

In a nutshell, `make` is a software tool that automates the process of incremental builds. Incremental builds optimize the build process by recompiling only the code modules that have changed since the last build, rather than recompiling the entire project. This significantly reduces build times, making it especially important in large projects, where build times are a bottleneck. The key to understanding `make` is understanding how incremental builds work and how to implement them manually. Once you understand this, the mechanics and role of `make` become apparent.&#x20;

As a running example throughout this chapter, we'll use the multi-file C program shown below.  It consists of five source files: calc.c, add.c, mult.c, add.h, and mult.h. This contrived program is designed to be easy to follow so you can focus on incremental build concepts without getting bogged down in complex code.

{% tabs %}
{% tab title="calc.c" %}
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

{% tab title="mult.c" %}
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

Each file in our program, along with header files included, represents a separate module. When we invoke gcc to build our prigram, it builds them each separately and then links them.&#x20;





Recall how multi-file programs are built in C. Each .c file is preprocessed, compiled, and assembled independently into relocatable object files. These relocatable object files are then linked, producing an executable object file. Usually we don't care about any of this. We provide gcc without our input files and get an executable.&#x20;





This process is shown in Figure 2. The following points are of note:

* Of note is that in the preprocessing stage, preprocessor inserts into each file the files specified via include directive.&#x20;
* can build all files in a single command
* can build each file seperately and then link the two

<figure><img src="../.gitbook/assets/Frame 30 (2).png" alt=""><figcaption></figcaption></figure>

#### How Incremental Builds Work

The idea behind incremental builds in quite straightforward. Notice in Figure 14 that each .o file is derived from it's corresponding .c file, as well as any file included in the .c file. However, they are not derived from any other source files. For example, add.o is derived from add.c and add.h. It is not derived from calc.c, mult.c, or any .h files other than add.h.&#x20;

It stands to reason that if we cache object files, we can 'reuse' them in later builds.&#x20;



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
