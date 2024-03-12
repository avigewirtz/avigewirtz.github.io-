# Example

Now that we understand the four stages involved in building a C program, let's see them in action with a practical example.&#x20;

{% tabs %}
{% tab title="testcircle.c" %}
{% code lineNumbers="true" %}
```c
/*-----------------------------------------------------*/
/* testcircle.c                                        */
/*                                                     */
/* Calculates the area of a circle given its radius.   */
/*-----------------------------------------------------*/
 
#include <stdio.h>
#include <stdlib.h> 
#include "circle.h" 

/* Prompts user for radius of circle. Returns 
   EXIT_FAILURE if input is invalid. Otherwise, prints 
   circle's area to stdout and returns 0. */  
   
int main(void) {

  double radius, area; 

  printf("Enter radius of circle: ");
  if (scanf("%lf", &radius) != 1 || radius <= 0) {
    printf("Invalid input. Must be a positive number.\n");
    exit(EXIT_FAILURE);
  }

  area = calculateArea(radius);

  printf("The area of the circle is: %.2f\n", area);

  return 0;
}

```
{% endcode %}
{% endtab %}

{% tab title="circle.c" %}
{% code lineNumbers="true" %}
```c
/*-----------------------------------------------------*/
/* circle.c                                            */
/*-----------------------------------------------------*/

#include "circle.h"
#define PI 3.14159

/* calculates the area of a circle given its radius */
double calculateArea(double radius) {
    return PI * radius * radius;
}
```
{% endcode %}
{% endtab %}

{% tab title="circle.h" %}
{% code lineNumbers="true" %}
```c
#ifndef CIRCLE_H
#define CIRCLE_H

double area(double radius);

#endif
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Preprocessing Stage

We can invoke the preprocessor alone by using the -E option:

```bash
gcc217 -E testcircle.c -o testcirle.i
gcc217 -E circle.c -o circle.i
```

The sequence of operations performed are summarized in Figure 4.2. Let's analytze each one-by-one, comparing the original code (testcircle.c and circle.c) with the preprocessed code (testcircle.i and circle.i).&#x20;

<figure><img src="../.gitbook/assets/Frame 1.png" alt=""><figcaption><p>Figure 4.2: Preprocessing Stage. (Click to enlarge)</p></figcaption></figure>

Frst, we see that the preprocessor removed all comments from testcircle.c and circle.c. Second, we see that each #include directive was replaced with the contents of its specified header. Namely, circle.h for circle.c and testcircle.c, and stdio.h and stdlib.h for testcircle.h. stdio.h and stdlib.h are system header files, containing declarations of library functions and definitions of macros. stdio.h contains the declaration of printf and scanf, and stdlib contains the declaration of exit and the the definition of the EXIT\_FAILURE macro. Finally, we see that all macros were expanded. PI in circle.,c was replaced with 3.14159, and EXIT\_FAILURE was replaced with 1.&#x20;

## Compilation Stage

The second stage involves compilation itself. Here, testcircle.i and circle.i are sent to the compiler, which translate their C code into assembly-language.&#x20;

Compilation is the most complex stage of the build process. It involves translating C source code into a completely different language. This is where the code is checked for errors. Figure 4.3 shows what the arm64 assembly looks like.&#x20;

<div align="center">

<figure><img src="../.gitbook/assets/Group 30 (1).png" alt="" width="563"><figcaption></figcaption></figure>

</div>

* Assembly language&#x20;
* testcircle.s missing definitions of printf, scanf, exit, and area

#### Characteristics of Assembly Language

A detailed explanation of assembly language is beyond the scope of this chapter. You can find a high level-overview in appendix 8. Arm64 assemvly will be covered in detail in the second hald of the course. For now, we will simply provide a few general points about assembly: &#x20;

* Extremely low-level language. Essentially human readable verson of target processor's machine language. Typically a one-to-one mapping between assembly language instruction and machine language instruction.&#x20;
* Specific to target architecture. each architecture has it's own assembly language.
* Not portable. In simple terms, this means that if I gave you assembly language program written for an architecture like x86 and told you to run it on an architecture like ARM, you'd have a very hard time doing so.&#x20;
* architecture Because assembly is esssentially a human readable version of the target processors machine code, just like machine language isn't portable (i.e., machine language program written for for an X86 will not run on an ARM), assembly language isn't either portable. Meaning, assembly language written for x86 cannot be translated into machine languag einstruciton for arm. compiler knows which assembly language to compile to



## Assembly Stage

The assembler translates the assembly-language in testcircle.s and circle.s into machine language, storing the results in testcircle.o and circle.o. This process is shown in Figure 4.3. Machine language is a binary language, consisting of only two symbols--0 and 1.

<figure><img src="../.gitbook/assets/Group 31.png" alt="" width="563"><figcaption></figcaption></figure>

* machine language&#x20;
* testcircle.o missing definitions of printf, scanf, exit, and area

## Linking Stage

To produce an executable file, the linker combines all these files--testcircle.o, circle.o, and C library--together, resolving all external references in our program. The output is a single file--the executable testcircle. This process is shown in Figure 6.&#x20;

<figure><img src="../.gitbook/assets/Group 49 (2).png" alt="" width="563"><figcaption></figcaption></figure>

