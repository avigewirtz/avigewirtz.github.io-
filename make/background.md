# Introduction

In a nutshell, `make` is a software tool that automates the process of incremental builds. Incremental builds optimize the build process by recompiling only the code modules that have changed since the last build, rather than recompiling the entire project. his significantly reduces build times, making it especially important in large projects where build times can become a bottleneck. The key to understanding `make` is understanding how incremental builds work and how to implement them manually. Once you understand this, the mechanics and role of `make` become apparent.&#x20;

#### Running Example

Throughout this chapter, we'll use a multi-file C program as our running example. It consists of five source files: `calc.c`, `add.c`, `mult.c`, `add.h`, and `mult.h`. This simple program is contrived to be easy to follow so you can focus on incremental build concepts without getting bogged down in complex code.

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

Recall how gcc builds multi-file C programs. Each .c file is preprocessed, compiled, and assembled independently into relocatable object files. These relocatable object files are then linked, producing an executable object file. Of note is that in the preprocessing stage, the preprocessor inserts into each file the files specified via #include directives. -c option. This process is shown in Figure 2.&#x20;

<figure><img src="../.gitbook/assets/Frame 30 (2).png" alt=""><figcaption></figcaption></figure>

#### How Incremental Builds Work

The idea behind incremental builds is straightforward. the first time we build a program, we build the entire thing. The key, however, is we ensure to save the object files. in subsequent builds, we rebuols only the affected object files. we then link the updated object file with the old ones to produce an updated executable. notice in figure 14 that each .o file is derived from it's coresponding .c file and any files included. thus, only if one of those files are modified to we rebuld the .o file. Formally, if a modification to source file A requires object file B to be rebuilt, we say that B depends on A.&#x20;

#### Incremental Builds In Action

show examples here using actaul commands

scenario 1: modfying a .c file

scenario 2: modifying a .h file

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
