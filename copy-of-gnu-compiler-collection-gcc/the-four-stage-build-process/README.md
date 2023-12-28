# The Four Stage Build Process

The aim of this chapter is to discuss in detail how GCC. There are four distinct programs involved in transforming C source code into executable machine code with GCC: the preprocessor, compiler, assembler, and linker. From a bird's eye view, the process looks like the following:&#x20;

1. GCC sends the source file to the preprocessor. The preprocessor's job is to essentially prepare the source code for compilation. It does this by scanning through the source code and making a bunch of substitutions. For example, it substitutes comments with whitespace and macros with their actual value.&#x20;
2. Next, GCC takes the preprocessed source code and sends it to the compiler, which translates the C source code into assembly language. Assembly language consists of low-level (but human-readable) instructions, specific to the target processor
3. GCC then feeds the assembly language version of the program into the assembler, which translates each assembly language instruction into its corresponding machine language instructions. Machine language is the binary language (1s and 0s) that the processor understands. At this point, the code is no longer human-readable.&#x20;
4. It might seem like GCC's job should have been finished after assembly. After all, the code is currently in machine language, which the processor understands. The problem, however, is that the assembled version almost certainly contains external references--that is, references to things like variables or functions defined in external files or libraries. To make the program executable, all the relevant code must be combined into a single file. This task is handled by the linker, which resolves all external dependencies, generating an executable.&#x20;

You can think of the process as a production line. The program begins as C source code and goes through a series of tools each progressively transforming it until it becomes an executable.&#x20;



You're probably wondering why you've never noticed that it's a four-stage process. That's because GCC abstracts it all away, enabling you the build a program via only a single command. probably compiled many source files with GCC but have not realized that it's a four-stage process, and for good reason. Having to manually do each step would be cumbersome. GCC abstracts these stages in such a way that a user only needs to execute a single command to perform all these steps. Although you don't see them happening, they're happening behind the scenes.&#x20;

1. By default, GCC discards the intermediate outputs, leaving only the resulting executable.  You can instruct GCC to save the intermediate outputs using the --savetemps command. For example, to save the intermediate outputs of hello.c:&#x20;

```
gcc --savetemps hello.c -o hello
```

the preprocessed, compiled, and assembled outputs will be saved in hello.i, hello.s, and hello.o respectively. You can confirm this by invoking ls.

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





