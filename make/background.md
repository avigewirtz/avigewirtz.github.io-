# Introduction

In a nutshell, `make` is a software tool that automates the process of incremental builds. Incremental builds optimize the build process by recompiling only the code modules that have changed since the last build, rather than recompiling the entire project. This significantly reduces build times, making it especially important in large projects where build times can become a bottleneck. The key to understanding `make` is understanding how incremental builds work and how to implement them manually. Once you understand this, the mechanics and role of `make` become apparent.&#x20;

#### Running Example

Throughout this chapter, we'll use the multi-file C program as our running example. It consists of five source files: `calc.c`, `add.c`, `mult.c`, `add.h`, and `mult.h`. This simple program is contrived to be easy to follow so you can focus on incremental build concepts without getting bogged down in complex code.

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

## building testintmath: the non-incremental build approach

Comsider the multi-file C program shown below. We'll use it as a running example throughout this chapter. 

The current approach we've been using is to build out program with the following command:

gcc ...

suppose we change add.c. we rebuild
our program by invoking the same command again: 


Incremental builds 

Recall what happens under the hood when we built our program. each file, along with all files included, is independently preprocessoed, compiled, and assembled, producing .o files. then, the .o files are linked, producing the executable. 

in the previous example, we recompiled all source files after only add.c was modified. we were affectivelt treating the entire program as a monolithic unit, wheere all files are always compiled at the same time. notice, however, that the only files affected by the change were add.o and calc. calc.o and mult were not affected. thus, had we have saved the object files from the last build, we could have rebuilt the program by rebuilding add.o alone and then linking it with the "old" object files. 

recall that you can save object files with the -c option. it instructs gcc to halt after assembly and output the .o files. thus, the incremental build approach would have been to invoke gcc on all files with the -c 
- the key is saving object files and tracking dependencies 



{% hint style="success" %}
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

#### Challenges of manually implementing Incremental Builds

As this example shows, implementing incremental builds manually is possible but it requires you to:

1. Keeo track of which source files have been modified since the last build.
2. Understand which object files are affected by these changes.&#x20;

Even for a small program like testintmath, this task isn’t particulurly exciting, though it is reasonably manageable. As programs grow larger, however, and the web of dependencies grows increasingly complex, this task becomes incredibly tedious and error-prone.

Consider a scenario, for example, where you modify a header file `A`, that is `#included` in, say, 20 of your program's `.c` files. You’d have to track down each one of these `.c` files and recompile it. Worse yet, imagine header file `A` is also `#include`d in header file `B`. You'd then have to also track down all `.c` files that `#include` `B` and recompile them.

For this reason, the `make` tool was developed, which automates the process of incremental builds. The section that follows describes how to use make.
