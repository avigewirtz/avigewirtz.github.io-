# Incremental Builds


- the key idea of incremwntsl builds is to cache intermediate results rhat can potentially be reused in a sunsequent build


- how does rhis work wirh C programs? 

- recall underlying process

- 
- the key idea of incremental builds is for a build to save time by using knowledge obtained in a previous buuod 

- how do we do so 
- current method we've been using is to rebuild entire program every time a chamgw is made

- an incremental build, by contrast, rebuilds only chnaged parts 
- how do we make aomething incremwnral? 

- we dont have to chnage anything about the structure of our program or the underlying build process. we simply avoid redundant work. 
- recall the underlying process 
- 

Recall the process by which multi-file programs are built. The source files are independently translated into object files. Then the resulting object files are linked, generating an executable. This underlying proxess rakes places regardless of which soecific commands ws use to build tje prohram. 

With this knowledge in mind, Consider two approaches to rebuilding a program after changes have been made to the source code:

1. Rebuild all object files, then link them to produce an updated executable.
2. Rebuild only affected object files, then link updated object files with "old" object files to produce an updated executable. Notjing about the structure ofnthe program or build process changes  we simplt avoid doing redundant work&#x20; 

Approach 1 is easy, since we can blindly run the followinfg command each time a change is made:&#x20;

Appraoch 2, however, requires some work. First, we have to cache object files. Second, to know which object files have been rendered obsolete by changes. This requires tracking dependencies.&#x20;







Consider the following approach to building testintmath. Eaach time, we run the The current approach we've been using to build multi-file programs like testintmath is to build the entire thing every time a change is made. We do so via the following command:

```
gcc217 intmath.c testintmath.c -o testintmath
```

This appraoch is wasteful, however. Recall what happens under the hood each time we run this command. The source files are independtly preprocessed, compiled, and assembled into object files, which are then linked. Here, we're rebubuilding ovbject files that were not affected by changes. Instead, we could rebuold only the affected files. In practice, how do we make the build incremental? relies on two key things:

1. caching object files. This may sound trivial, but to reuse object files, you have to actaully have them in the first place.&#x20;
2. dependency tracking. you have to know which source files each object file depends on. only then can you know which cached object files have been rendered obsolete and must be rebuilt.&#x20;





Incremental builds work by caching intermediate results of a build and then reusing them in future builds. To know which cached results can be reused and which were rendered obsolete by changes to the source code, it relies on accurate dependency tracking.&#x20;

To make things concrete, let's first apply the incremental build technique to a simple mathematical system of questions and then tie it in to C programs. Consider the following system of equations:

$$z = x + y\\ x = \sin(a)\\y = \sin(b)$$+ 3.5

where $$a = 37^\circ$$ and $$b = 73^\circ$$.

To compute $$z$$, we first calculate $$x = \sin(37^\circ) = 0.6018$$. Next, we calculate $$y = \sin(73^\circ) = 0.9563$$. To compute z, we add x and y, getting $$z = 0.6018 + 0.9563 = 1.5581$$.

Now, suppose b changes from $$b = 73^\circ$$ to $$b = 83^\circ$$. We now want to recompute z. Two questionsDo we need to recalculate everything? Not necessarily! An incremental build would realize that:

z and y depend on b, but x does not depend on b. therefore, we need only recompute x



To recompute 𝑧, we don’t need to recompute x. We can reuse the $$0.6018$$ value we obtained in our previous computation--provided we saved it, that is! we recompute y, then add the result to the

is $$\sin(83^\circ)$$, which is approximately $$0.9925$$. So now we have $$z = 0.6018 + 0.9925 = 1.5943$$.



More formally, we can capture these dependencies via a directed graph.

As our winded example has hopefille shown,

What does this have to do with C programs? Well, the principle of incremental builds in C work in exactly the same way. Recall the process by which multi-file programs are built. Each `.c` file is _independently_ translated into an object file. For simplicity, we'll refer to this process as compilation, but keep in mind that we actually mean preprocessing, compilation, and assembly. Of note is that in the preprocessing stage, headers specified in `#include` directives are inserted. Then, to produce an executable, the object files are linked--along with necessary object files from the C standard library. This process is shown in Figure 12 using a dummy `foobar` program.

<figure><img src="../.gitbook/assets/Frame 32.png" alt="" width="563"><figcaption></figcaption></figure>

We can model this process using the following equation:

$$foobar = compile(foo.c) + compile(bar.c)$$

(Of course, linking or more complicated than the simple concatenation of object files, but this equation will do.) Just like in our math example where only sin(y) was recalculated when `y` changed, so too only compile(foo.c) needs to be re-run when bar.c is modified, and vice versa.

The caveat is that diving a C program along the lines of `.c` files is an oversimplification, since `.c` files can `#include` header files. To be more precise, we really need to think it terms of translation units. A translation unit is a .c file along with all headers included. Note that translation units can--and often do--overlap.

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
