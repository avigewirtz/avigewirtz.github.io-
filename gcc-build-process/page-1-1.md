# Example: testintmath

In our previous example, all the source code of our program was contained within a single `.c` file—`charcount.c`. In real-world scenarios, however, the source code of a C program is often distributed across many `.c` files. What does the underlying build process look like then?

Let's walk through the four-stage build process again, but this time, using a multi-file program as an example. We won't go over every detail since we've covered the basics. Our goal here is to illustrate the multi-file aspects of the process.

For our example, we'll use the `testintmath` program from precept 4. Its source code is distributed across two `.c` files (`testintmath.c` and `intmath.c`) and one user-written `.h` file (`intmath.h`).

* `testintmath.c` (client)**.** Contains the `main` function, the entry point of the program. It reads two integers from standard input (stdin) and returns their greatest common divisor (GCD) and least common multiple (LCM).
* `intmath.c` (implementation)**.** Contains the definitions of the `gcd` and `lcm` functions, which `testintmath.c` calls.
* `intmath.h` (interface)**.** Contains the declarations of the `gcd` and `lcm` functions. Note that intmath.h is #included in both `testintmath.c` and `intmath.c`. We'll see why shortly.

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

{% hint style="info" %}
**`#include` Syntax**

Notice that the include directive for `intmath.h` uses double quotes (`#include "intmath.h"`) rather than angle brackets, as is used for system headers like `stdio.h`. Using double quotes tells the preprocessor to look in the current directory for the file, instead of just the system directories.
{% endhint %}

#### Building testintmath

Like with a single-file program, we can build a multi-file program with a single `gcc` command. We simply list both `.c` files:

```
gcc intmath.c testintmath.c -o testintmath 
```

This command takes `testintmath.c` and `intmath.c` as input and produces the executable `testintmath` as output. We can confirm this with ls:

```
ls
intmath.c testintmath.c testintmath
```

What happens under the hood? There are many ideas we can come up with, but thankfully, we don't have to guess. Thankfully, we don’t have to guess. Gcc tells us the precise operations it performs if we run it with the -v option. Unfortunately, however, the output is extremely long and difficult to read. Thus, we won’t show it here. Instead, we'll just summarize it here. 

- preprocessor on testintmath.c, generating testintmath.i 
- Compiler on testintmath.i, generating testintmath.s
- Assembler on testintmath.s, generating testintmath.o 
- Preprocessor on intmath.c, generating intmath.i
- Compiler on intmath.i, generating intmath.s
- Assembler on intmath.s, generating intmath.o 
- Linker on testintmath.o, intmath.o, and libc.a, generating testintmath. 


A few critical things:

- even though we compiled with a single command, each file is processed independently 
- No knowledge of each other 
- Intermediate files not retained 





Each `.c` file is processed independently by the preprocessor, compiler, and assembler, resulting in separate object files (`.o`). The linker then combines these object files, along with any necessary library code, to produce the final executable `testintmath`.

The important thing to understand is that each stage of the build process (preprocessor, compiler, assembler) works on one unit of input at a time. For the preprocessor, this unit is a `.c` file and its included files. For the compiler and assembler, the units are `.i` and `.s` files, respectively.





Like a singe-file program, the process involves four stages:preprocessing, compilation, assembly, and linking. The important thing to understand is that each stage of the build process (preprocessor, compiler, assembler) works on one unit of input at a time. For the preprocessor, this unit is a `.c` file and its included files. For the compiler and assembler, the units are `.i` and `.s` files, respectively.



a single file as output--the executable testintnmath. The important thing to understand, however, is that the preprocessor, compiler, and assembler process only a single unit of input at a time. In the case of the preprocessor, this unit is the .c file along with all files included in it via the #include directive. In the case of the compiler and assembler, the unit is a .i and .s file, respectively.&#x20;

For our example program, this means that testintmath.c and intmath.c will each be preprocessed, compiled, and assembled separately.&#x20;

#### Preprocessing

The build process begins with preprocessing. We invoke the preprocessor on `testcircle.c` and `circle.c` with the following commands:

```bash
gcc217 -E tescircle.c > testcircle.i
gcc217 -E circle.c > circle.i
```

Although not strictly necessary, `circle.c` also includes `circle.h`. This ensures that the declaration of `calculateArea` in `circle.h` matches its declaration (in its definition) in `circle.c`. If there's a discrepancy between the two, the compiler will report an error.

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