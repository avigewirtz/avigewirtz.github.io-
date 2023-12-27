# The Four Stage Build Process

GCC's internal process of transforming C source code into executable machine code consists of four sequential stages: (four programs involved. footnote: technically, three, since preprocessor is currently integrated into compiler). preprocessing, compilation proper, assembly, and linking.  From a bird’s-eye view, the stages can be summarized as follows:&#x20;

1. Preprocessing: GCC prepares the code for compilation by scanning through the code and making a bunch of substitutions. For example, it substitutes comments with whitespace and macros with their actual value.
2. Compilation proper: GCC translates the preprocessed source code into assembly language, specific to the target processor. This is where the high-level constructs (like loops, conditionals, etc.) are translated into a series of low-level (but human-readable) instructions.&#x20;
3. Assembly: GCC then translates the assembly language instructions into their corresponding machine language instructions. Machine language is the set of binary (0s and 1s) instructions the processor understands.&#x20;
4. Linking: If your program consists of multiple source files or uses external libraries, GCC combines all the relevant code into a single file. This file is known as an executable.&#x20;

You've probably compiled many source files with GCC but have not realized that it's a four-stage process, and for good reason. Having to manually do each step would be cumbersome. GCC abstracts these stages in such a way that a user only needs to execute a single command to perform all these steps. Although you don't see them happening, they're happening behind the scenes.&#x20;

1. &#x20;For instance, running gcc -o output source.c will preprocess, compile, assemble, and link the source code, producing an executable named ‘output’.
2. By default, GCC discards the intermediate outputs, leaving only the resulting executable.  You can instruct GCC to save the intermediate outputs using the --savetemps command. For example, to save the intermediate outputs of hello.c:&#x20;

```
gcc --savetemps hello.c -o hello
```

the preprocessed, compiled, and assembled outputs will be saved in hello.i, hello.s, and hello.o respectively. You can confirm this by invoking ls.

8. This chapter aims to describe in detail how GCC transforms source files into an executable file. Compilation is a four-stage process involving preprocessing, compilation proper, assembly, and linking. To illustrate the build process in practice, we will examine each stage using`charcount.c`, a simple program that prints the number of characters input by the user in stdin. &#x20;

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





