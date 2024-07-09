# Incremental Builds

Recall the underlying process by which gcc builds testintmath.&#x20;









by default, gcc doesn't save the intermediate object files. However, we can instruct it to do so&#x20;

What does it mean to build testintmath incrementally, and how do we do so? When we build it, we save intermediate results (object files) and reuse them when their sources haven't changed.&#x20;

Recall that gcc is a compiler driver. It parses the command line and calls the preprocessor, compiler, assembler, and linker on our behalf to build the program. If we run gcc without anyb arguments to control the build process, it'll perform all four stages. However, it won't save object files. This default behaviopr--where objhect file are deleted--works well if we intend to perform a full rebuold each time.&#x20;

* run the preprocessor, compiler, and assembler on intmath.c, generating object file intmath.o
* run the preprocessor, compiler, and assembler on testintmath.c, generating object file testintmath.o
* run the linker on intmath.o and testintmath.o, generating executable file testintmath

We can perform all these four stages via a single invocation of gcc (i.e.,`gcc217 intmath.c testintmath.c -o testintmath`), Recall the process by which multi-file programs are built. Each `.c` file is _independently_ preprocessed, compiled, and assembled into an object file. For simplicity, we'll refer to this process as compilation, but keep in mind that we actually mean preprocessing, compilation, and assembly. Of note is that in the preprocessing stage, headers specified via the `#include` directive are inserted. Then, to produce an executable, the object files are linked--along with necessary object files from the C standard library. This process is shown in Figure 12 using a dummy `foobar` program.

The key to incremental builds is caching object files and reusing them when the source files they depend on haven't changed. How do we save object files? The gcc driver doesn't offer any option to build the program in one command and retain object files, but it does offer a two command appraoch. First, you run gcc with the -c option, which tells gcc to run the preprocessor, compiler, and assembler on each source file and output the object files.

```
ls
intmath.c testintmath.c intmath.o testintmath.o
```

then, run gcc again, this time to link the object files and produce an executable:

```
gcc intmath.o testintmath.o -o testintmath
```

Now that we have the object files saved, we can perform an incremental build. How it works is quite simple. Suppose we modify intmath.c. First, we rebuild only intmath.o--the object file that depends on intmath.c:

```
gcc -c intmath.c
```

Then, we link the newly generated obnect file--intmath.o--with the "old" object file--testintmath.o--to produce an updated testintmath:

```
gcc intmath.o testintmath.o -o testintmath
```

In other words, by caching the object files, we were able to avoid preprocessing, compiling, and assembling testintmath.c, whose object file was not affected by the changes.&#x20;

Suppose, however, that we were to modify intmath.h. This affects intmath.o and testintmath.o, since both intmath.c and testintmath.c inckude intmath.h.&#x20;



We run this command whether we're building testintmath for the first time, tenth time, or hundredth time. In other words, we don't take into account which source files were actually modified since the last build. We just build the whole thing.&#x20;

This approach is extremely convenient, since it requires no brainpower. We don't need to have any familiarity with the underlying build process or have to track source files and their dependencies.&#x20;

The obvious drawback, however, is that this approach is wasteful. Recall what happens each time we run the command `gcc217 intmath.c testintmath.c -o testintmath`. Intmath.c and testinamth.c are independenctly preprocessed, compiled, and assembnled into object files intmath.o and tetsintmath.o. Then, the object files are linked--along with necessary object files from the C Standard Library--to poduce the executable testintmath.&#x20;



We're rebuilding parts of the program that haven't changed since the last build.&#x20;

The second appraoch is the incremental build appraoch. Here, we cache object files and rebuild only the object files whose source have changed since the last build. It is tempting to&#x20;





Suppose we have the equation $$z = \sin(x) + \sin(y)$$, where $$x = 37^\circ$$ and $$y = 73^\circ$$. To compute $$z$$, we first calculate $$\sin(37^\circ)$$, which is approximately $$0.6018$$. Next, we calculate $$\sin(73^\circ)$$, which is approximately $$0.9563$$. Adding these together, we get $$z = 0.6018 + 0.9563 = 1.5581$$.

Now, suppose 𝑦 changes from $$y = 73^\circ$$ to $$y = 83^\circ$$. To recompute 𝑧, we don’t need to recompute $$\sin(37^\circ)$$. We can reuse the $$0.6018$$ value we obtained in our previous computation--provided we saved it, that is! The only new nontrivial computation needed is $$\sin(83^\circ)$$, which is approximately $$0.9925$$. So now we have $$z = 0.6018 + 0.9925 = 1.5943$$.

Notice what we did here. We cached the intermediate values generated during the first computation and reused the unaffected values in the next computation. The principle of incremental builds in C work in almost exactly the same way.&#x20;

Recall the process by which multi-file programs are built. Each `.c` file is _independently_ preprocessed, compiled, and assembled into an object file. For simplicity, we'll refer to this process as compilation, but keep in mind that we actually mean preprocessing, compilation, and assembly. Of note is that in the preprocessing stage, headers specified via the `#include` directive are inserted. Then, to produce an executable, the object files are linked--along with necessary object files from the C standard library. This process is shown in Figure 12 using a dummy `foobar` program.

<figure><img src="../.gitbook/assets/Frame 32.png" alt="" width="563"><figcaption></figcaption></figure>

We can model this process using the following equation:

$$foobar = compile(foo.c) + compile(bar.c)$$

(Of course, linking or more complicated than the simple concatenation of object files, but this equation will do.)&#x20;

We apply the same principle we did in our math example. we cache intermediate reuslts--object files. Then, in future builds, we rebuild only the object files that depend on changed source files.&#x20;



Just like in our math example where only sin(y) was recalculated when `y` changed, so too only compile(foo.c) needs to be re-run when bar.c is modified, and vice versa.&#x20;

The caveat is that diving a C program along the lines of `.c` files is an oversimplification, since `.c` files can `#include` header files. To be more precise, we really need to think it terms of translation units. A translation unit is a .c file along with all headers included. Note that translation units can--and often do--overlap.&#x20;

#### Example

Let's demonstrate incremental builds in action. As an example, we'll use the testintmath program from precept four.

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

{% tab title="intmath.c " %}
{% code lineNumbers="true" %}
```c
/*--------------------------------------------------------------------*/
/* intmath.c                                                          */
/* Author: Bob Dondero                                                */
/*--------------------------------------------------------------------*/

#include "intmath.h"

/*--------------------------------------------------------------------*/

int gcd(int iFirst, int iSecond)
{
   int iTemp;

   /* Use Euclid's algorithm. */

   while (iSecond != 0)
   {
      iTemp = iFirst % iSecond;
      iFirst = iSecond;
      iSecond = iTemp;
   }

   return iFirst;
}

/*--------------------------------------------------------------------*/

int lcm(int iFirst, int iSecond)
{
   return (iFirst / gcd(iFirst, iSecond)) * iSecond;
}
```
{% endcode %}
{% endtab %}

{% tab title="intmath.h " %}
```c
/*--------------------------------------------------------------------*/
/* intmath.h                                                          */
/* Author: Bob Dondero                                                */
/*--------------------------------------------------------------------*/

/* Return the greatest common divisor of positive integers iFirst and
   iSecond. */

int gcd(int iFirst, int iSecond);

/*--------------------------------------------------------------------*/

/* Return the least common multiple of positive integers iFirst and
   iSecond. */

int lcm(int iFirst, int iSecond);
```
{% endtab %}
{% endtabs %}

Our program consists of two translation units.

1. intmath.c and intmath.h
2. testintmath.c, intmafh.h, stdio.h, and stdlib.h

Because stdio.h and stdlib.h are system header files that we do not modify, we won't concern ourselves wirh the.

The first time we build testintmath, we compile all source files, but we ensure to save object files. How do we save object files? Recall the -c option, which tells gcc to halt after the assembly stage and output object files. Thus, we build our program with the following two commands:

```
gcc -c intmath.c testintmath.c
gcc intmath.o testintmath.o -o testintmath
```

Now suppose we modify intmath.c. To rebuild testintmath, we run gcc -c on intmath.c only. Then, we link the resulting intmath.o with the testintmath.o form our previous build.

```
gcc -c intmath.c
gcc intmath.o testintmath.o -o testintmath
```

The process would be the same if we were to modify testintmath.c. Notice, however, that if modify intmath.h, we'd have to recompile both intmath.c and testintmath.c, since they both #include it. Ij general, changes to header files tend to be kuch more dramatic than chnagws to .c files, sincs header files are often part of multiple trabslation units.

{% hint style="info" %}
It's important to understand that the underlying GCC build process is the same irrespective of whether we build our program via two commands:

```bash
gcc217 -c intmath.c testintmath.c
gcc217 intmath.o testintmath.o -o testintmath
```

Or via a single command:

```bash
gcc217 intmath.c testintmath.c -o testintmath
```

In other words, in both cases the .c files will be independently preprocessed, conpiled, and assembled into object files, which are then linked. Fundamentally, the only difference between these two approaches is that the two-command approach retains the object files while the single-command approach does not.
{% endhint %}
