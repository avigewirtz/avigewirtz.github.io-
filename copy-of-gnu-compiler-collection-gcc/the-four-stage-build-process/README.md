# The Four Stage Build Process

The aim of this chapter is to describe in detail how GCC transforms source files to an executable file. Compilation is a four-stage process involving involving preprocessing, compilation proper, assembly, and linking. From a bird’s-eye view, these steps can be summarized as follows:&#x20;

* Preprocessing: prepares the source code for compilation.&#x20;
* Compilation proper: converts the preprocessed source code to the assembly language of the target machine.
* Assembly: converts the assembly language to machine language.
* Linking: resolves external dependencies, producing an executable.

This four-step process is performed by GCC whenever a C source file (i.e., a file with a .c extension) is compiled. is peformed by GCC whenever a C source file is&#x20;

To illustrate the build process in practice, we will examine each stage using`charcount.c`, a simple program that prints the number of characters input by the user in stdin. &#x20;

{% code lineNumbers="true" %}
```c
/*--------------------------------------------------------------------*/
/* charcount.c                                                        */
/*--------------------------------------------------------------------*/

#include <stdio.h>

/* Write to stdout the number of characters in stdin. Return 0. */
int main(void) {
    int c;
    int characterCount = 0;

    while ((c = getchar()) != EOF) {
        characterCount++;
    }   

    printf("%d\n", characterCount);

    return 0;
}

```
{% endcode %}

###



When we compile `charcount.c` with the command `gcc217 charcount.c -o charcount`, GCC automatically performs all four stages--preprocessing, compiling, assembly, and linking. However, the intermediate outputs of these stages (i.e., the preprocessed, compiled, and assembled versions of the code) are by default discarded, leaving only the executable.&#x20;



