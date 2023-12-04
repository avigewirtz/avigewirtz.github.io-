# The Four Stage Build Process

The aim of this chapter is to describe in detail how GCC transforms source files to an executable file. While this transformation typically occurs through a single invocation of gcc, it is actually multi-stage process involving four tools: the preprocessor, compiler, assembler, and linker. Roughly speaking, the role of each tool can be summarized as follows:&#x20;

1. Preprocessor: prepares the source code for compilation.&#x20;
2. Compiler: converts the preprocessed source code to assembly language.
3. Assembly: converts the assembly language to machine language.
4. Linking: resolves external dependencies, producing an executable.

To illustrate the four-stage build process in practice, we will examine each of the stages using `charcount.c`, a simple program that counts the number of characters input in stdin by the user.

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

When we compile `charcount.c` with the command `gcc217 charcount.c -o charcount`, GCC automatically performs all four stages--preprocessing, compiling, assembly, and linking--producing the charcount executable.   However, the intermediate outputs of these stages (i.e., the preprocessed, compiled, and assembled versions of the code) are by default discarded. You can preserve these intermediate outputs by using specific GCC command-line options. The relevant options which we will explore in this chapter are -E, -S, and -c, which instruct GCC to stop after the preprocessing, compilation, and assembly stages respectively.&#x20;

Preserving intermediate output can be beneficial for several reasons. For example, you might want to save the compiled version so you can make low-level assembly optimizations, or you might want to save the assembled version to avoid having to later recompile it , as will be explained in the chapter on Make.&#x20;
