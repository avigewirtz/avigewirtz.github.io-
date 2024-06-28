# Introduction

In a nutshell, `make` is a software tool that automates the process of incremental builds. The premise behind incremental builds is simple: when you rebuild your program after making a change to the source code, you rebuild only the affected files, not the entire program. This is especially important in large projects, where build times can become a bottleneck.

In this chapter, we'll first describe how to implement incremental builds manually. Then, we'll show how to automate the process with make.

#### Running Example

As a running example throughout this chapter on Make, we'll use the `testintmath` program we used in the chapter on GCC to explore the multi-file build process. For reference, the source code is provided below.&#x20;

{% tabs %}
{% tab title="testintmath.c" %}
{% code lineNumbers="true" %}
```c
/*--------------------------------------------------------------------*/
/* testintmath.c                                                      */
/* Author: Bob Dondero                                                */
/*--------------------------------------------------------------------*/

#include "intmath.h"
#include <stdio.h>
#include <stdlib.h>

/*--------------------------------------------------------------------*/

/* Read two positive integers from stdin. Return EXIT_FAILURE if stdin
   contains bad data and an write error message to stderr. Otherwise
   compute the greatest common divisor and least common multiple of
   the two positive integers, write those two values to stdout, and
   return 0. */

int main(void)
{
   int i1;
   int i2;
   int iGcd;
   int iLcm;
   int iScanfReturn;

   printf("Enter the first positive integer:\n");
   iScanfReturn = scanf("%d", &i1);
   if ((iScanfReturn != 1) || (i1 <= 0))
   {
      fprintf(stderr, "Error: Not a positive integer.\n");
      exit(EXIT_FAILURE);
   }

   printf("Enter the second positive integer:\n");
   iScanfReturn = scanf("%d", &i2);
   if ((iScanfReturn != 1) || (i2 <= 0))
   {
      fprintf(stderr, "Error: Not a positive integer.\n");
      exit(EXIT_FAILURE);
   }

   iGcd = gcd(i1, i2);
   iLcm = lcm(i1, i2);

   printf("The greatest common divisor of %d and %d is %d.\n",
      i1, i2, iGcd);
   printf("The least common multiple of %d and %d is %d.\n",
      i1, i2, iLcm);

   return 0;
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Building testintmath: The Incremental Build Appraoch

Recall the process by which multi-file programs such as `testintmath` are built. Each .c file is _independently_ preprocessed, compiled, and assembled into an object file.  Of note is that when the file is preprocessed, all headers specified in #include directives are inserted into the file. Then, the object files are combined--along with along with necessary object files from the C standard library--to produce an executable file. This process for our testintmath program is shown is Figure 12.&#x20;

<figure><img src="../.gitbook/assets/Frame 31 (2).png" alt=""><figcaption></figcaption></figure>

Recall that gcc provides a shortcut command 
The underlying build process we just described holds true regardless of which we build our program. The default behavior of GCC, however, is to We can perform all these steps via a single gcc command--namely:

```
gcc217 intmath.c testintmath.c -o testintmath
```


By default, however, gcc does not retain the object files. To implement incremental builds, however, you need to retain object files. Why? Well notice that each object file is derived only from it's corresponding .c file and #included headers. It does not depend on any other files. Therefore, a change to another file does not require that file to be rebuilt. For example, a change to intmath.o does not require testintmath.o to be rebuilt. Insyead, you'd be able to rebuild only intmath.o, and then link it with the testintmath.o object file from the previous build, generating a new executable.&#x20;

How do we save object files? Simple.&#x20;





To save the object files, we can build our program in two gcc commands. First, we run gcc with the -c option, which tells gcc to preprocess, compile, and assemble the input files, but to not link them:

```
gcc -c intmath.c testintmath.c
```

Next, we run gcc on the object files, which links them and produces an executable:

```
gcc217 intmath.o testintmath.o -o testintmath
```

Why do we want to save the object files?&#x20;

the object files are not retained. In practice, however, we often want to retain object files. Why?&#x20;

{% hint style="info" %}
It's important to understand that, fundamentally, the underlying GCC build process is the same irrespective of whether we build our program via two commands:

```bash
gcc217 -c intmath.c testintmath.c
gcc217 intmath.o testintmath.o -o testintmath
```

Or via a single command:

```bash
gcc217 intmath.c testintmath.c -o testintmath
```

The only difference between these two approaches is that the two-command approach retains the`.o` files while the single-command approach does not.
{% endhint %}

#### Challenges of Manually Implementing Incremental Builds

As this example shows, implementing incremental builds manually is possible but it requires some work. In particular, you have to:

1. Keep track of which `.c` and `.h` files were modified since the last build.
2. Know which `.o` files depend on the modified `.c` and `.o` files.

Even for a small program like `testintmath`, this task isn’t particularly fun, though it is admittedly manageable. As programs grow larger, however, and the web of dependencies grows increasingly complex, this task becomes incredibly tedious and error-prone.

Consider a scenario where you modify header file `A`, which is `#included` in, say, 20 `.c` files. You’d have to track down and recompile all these `.c` file. Worse yet, imagine header file `A` is also `#included` in header file `B`. You'd then have to also track down and recompile all the `.c` files that `#include` `B`.

To make life easier (no pun intended), the `make` tool was developed, which automates the process of incremental builds. In the next section, we describe how to use `make`.
