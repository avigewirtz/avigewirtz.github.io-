# Example: Multi-file Program

In our previous example, all the source code of our program was contained within a single .c file—charcount.c. However, in real-world scenarios, the source code of a C program is often distributed across multiple files. In such a case, the underlying operations get more interesting, and the true power of the linker is more appreciated.

Let's now walk through the four stage build process again, but this time, let's use a multi-file program as an example. Because we've already gone over the details, we'lol focus on the multi-file aspects of the process. 

For our example, We'll use the `testintmath` program from precept 4, whose source code is distributed across two `.c` files, `testintmath.c` and `intmath.c`, and one (user written) `.h` file, `intmath.h`. `testcircle.c` contains the `main` function, the entry point of our program. It reads two positive integers from stdin and returns their greatest common divisor (gcd) and least common multiple (lcm). `intmath.c` contains the implementation (i.e., definitions) of the `gcd` and `lcm` functions. 

{% tabs %}
{% tab title="testintmath.c (client)" %}
{% code lineNumbers="true" %}
```c
/*--------------------------------------------------------------------*/
/* testintmath.c                                                      */
/* Author: Bob Dondero                                                */
/*--------------------------------------------------------------------*/

#include "intmath.h"
#include <stdio.h>
#include <stdlib.h>

/* Read two positive integers from stdin. Return EXIT_FAILURE if stdin
   contains bad data. Otherwise compute the greatest common divisor
   and least common multiple of the two positive integers, write those
   two values to stdout, and return 0. */

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

   iGcd = IntMath_gcd(i1, i2);
   iLcm = IntMath_lcm(i1, i2);

   printf("The greatest common divisor of %d and %d is %d.\n",
      i1, i2, iGcd);
   printf("The least common multiple of %d and %d is %d.\n",
      i1, i2, iLcm);

   return 0;
}
```
{% endcode %}
{% endtab %}

{% tab title="intmath.c (implementation)" %}
```c
/*--------------------------------------------------------------------*/
/* intmath.c                                                          */
/* Author: Bob Dondero                                                */
/*--------------------------------------------------------------------*/

#include "intmath.h"
#include <assert.h>

int IntMath_gcd(int iFirst, int iSecond)
{
   int iTemp;

   assert(iFirst > 0);
   assert(iSecond > 0);

   /* Use Euclid's algorithm. */

   while (iSecond != 0)
   {
     iTemp = iFirst % iSecond;
     iFirst = iSecond;
     iSecond = iTemp;
   }

   return iFirst;
}

int IntMath_lcm(int iFirst, int iSecond)
{
   assert(iFirst > 0);
   assert(iSecond > 0);

   return (iFirst / IntMath_gcd(iFirst, iSecond)) * iSecond;
}
```
{% endtab %}

{% tab title="intmath.h (interface)" %}
```c
/*--------------------------------------------------------------------*/
/* intmath.h                                                          */
/* Author: Bob Dondero                                                */
/*--------------------------------------------------------------------*/

#ifndef INTMATH_INCLUDED
#define INTMATH_INCLUDED

/* Return the greatest common divisor of positive integers iFirst and
   iSecond. */

int IntMath_gcd(int iFirst, int iSecond);

/* Return the least common multiple of positive integers iFirst and
   iSecond. */

int IntMath_lcm(int iFirst, int iSecond);

#endif
```
{% endtab %}
{% endtabs %}


{% hint style="info" %}
**`#include` Syntax**

Notice that there are two syntaxes for the `#include` directive: with angle brackets (e.g., `#include <stdio.h>`), and with double quotes (e.g., `#include "circle.h"`). The difference between these two syntaxes lies in how the preprocessor searches for the specified file, with the precise details being implementation-defined. In general, files #included with angle brackets are searched for in system directories only, while those #included with double quotes are searched for in the working directory first and then in system directories.
{% endhint %}


### The Starting Point

Program is spread across three files.&#x20;

### Preprocessing Stage

The build process begins with preprocessing. We invoke the preprocessor on `testcircle.c` and `circle.c` with the following commands:

```bash
gcc217 -E tescircle.c > testcircle.i
gcc217 -E circle.c > circle.i
```



Although not strictly necessary, `circle.c` also includes `circle.h`. This ensures that the declaration of `calculateArea` in `circle.h` matches its declaration (in its definition) in `circle.c`. If there's a discrepancy between the two, the compiler will report an error.


#### Macro Definition

The `#define` directive creates a preprocessor macro, which is essentially an alias for a specific value or code snippet. In `circle.c`, `#define PI 3.14159` creates the macro `PI` and assigns it the value `3.14159`. Whenever `PI` is subsequently used in `circle.c`, the preprocessor replaces it with `3.14159`.

`testcirle.c` uses the macro `EXIT_FAILURE`, which is defined in `stdlib.h`. The exact value of `EXIT_FAILURE` can vary between different systems, but it is commonly set to 1, as it is in our case.

#### Conditional Compilation

The `#ifndef` / `#else` directives, which we use in `intmath.h`, are part of a set of directives known as _conditional_ directives. These are used to control which parts of the source code are sent to the compiler. One of their most common use cases is to prevent the contents of a header file from being included twice in the same compilation unit (i.e., `.i` file). This technique is known as an _#include guard_. Here's how it works in `intmath.h`:

* `#ifndef CIRCLE_H`: This checks if `CIRCLE_H` is defined as a macro. If this evaluates to TRUE (1) (i.e., `CIRCLE_H` is not defined), the preprocessor will continue to process the code between `#ifndef` and `#endif`. If it evaluates to FALSE (0), the preprocessor will skip the entire block within `#ifndef` ... `#endif`.
* `#define CIRCLE_H`: This defines `CIRCLE_H`. Notice that it doesn't give `CIRCLE_H` any specific value. This is perfectly valid. The preprocessor will simply note that `CIRCLE_H` is defined. Going forward, `#ifndef CIRCLE_H` will evaluate to FALSE, and the preprocessor will skip the block.
* `#endif`: This ends the conditional block started by `#ifndef`. Every conditional directive must have a corresponding `#endif`.

<figure><img src="../.gitbook/assets/Group 20 (9).png" alt=""><figcaption></figcaption></figure>

First, we see that the preprocessor removed all comments from `testcircle.c` and `circle.c`. Second, it replaced each `#include` directive with the contents of its specified header: `circle.h` for both `circle.c` and `testcircle.c`, and `stdio.h` and `stdlib.h` for `testcircle.c`. Finally, all macros were expanded: `PI` in `circle.c` was replaced with `3.14159`, and `EXIT_FAILURE` was replaced with `1`.

### Compilation Stage

We compile `testcircle.i` and `circle.i` by invoking `gcc217` with the `-S` option:

```bash
gcc217 -S testcircle.i circle.i
```



<figure><img src="../.gitbook/assets/Frame 63.png" alt="" width="563"><figcaption></figcaption></figure>


### Assembly Stage


We invoke the assembler on `testcircle.s` and `circle.s` with the following command:

```
gcc217 -c testcircle.s circle.s
```

The result is two relocatable object files, `testcircle.o` and `circle.o`.

<figure><img src="../.gitbook/assets/Frame 62.png" alt="" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
relocatable object files are binary files divided into sections.
{% endhint %}

### Linking Stage

Linking marks the final stage of the build process. The linker takes as input a collection of relocatable object files and combines them into a single file known as an _executable object file_. As its name suggests, an executable object file contains machine code in a form that can be loaded into memory and executed. In our example, the linker's inputs are `testcircle.o`, `circle.o`, and the C standard library, which on Linux is stored in `libc.a`. We invoke the linker using the following command:

```
gcc217 testcircle.o circle.o -o testcircle
```

Note that we don't need to explicitly pass `libc.a` to the linker, as `gcc` automatically includes it. The output is the executable object file `testcircle`.

<figure><img src="../.gitbook/assets/Frame 60 (1).png" alt="" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**libc.a**

`libc.a` is an archive file. An archive file is a single file that contains within it a collection of relocatable object files, along with metadata describing the location of each file. The linker extracts only the relocatable object files of the functions referenced by our program.
{% endhint %}

{% hint style="info" %}
Besides inserting definitions of functions like `printf`, `scanf`, and `exit` from the C standard library, the linker also inserts some runtime starter code. This includes the startup routine responsible for setting up the program's environment and ultimately calling the `main` function.
{% endhint %}
