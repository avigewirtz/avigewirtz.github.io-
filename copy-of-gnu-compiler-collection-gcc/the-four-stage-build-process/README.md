# The Four Stage Build Process



In reality, as you're aware, the process involves multiple stages, each handled by different programs or components within the GCC toolchain. The stages — preprocessing, compiling, assembling, and linking — are distinct, each performing a specific task in transforming source code into an executable.

1. It works kind of like a production line, where the program begins as source code and then gets transformed from one version to another by each tool—preprocessor, compiler, assembler, and linker, in that order—to create a final product--the executable.&#x20;
2. From a bird’s-eye view, these steps can be summarized as follows:&#x20;
   * Preprocessing: This is the first stage, where GCC processes the source code before actual compilation. It involves handling directives such as #include (which includes other files), #define (which defines macros), and conditional compilation directives like #if. This stage essentially prepares the source code by expanding macros, processing includes, and applying conditional compilation.
   * Compilation proper: During this stage, the preprocessed source code is converted into assembly language specific to the target processor. The compiler analyzes the code (syntax and semantics) and translates it into a lower-level, more detailed representation. This is where the high-level constructs (like loops, conditionals, etc.) are translated into a series of instructions that the processor can understand.
   * Assembly: The assembly language code generated in the previous step is then converted into machine code by an assembler. The machine code is essentially a set of binary instructions understandable by the processor. Each line of assembly language corresponds to a machine language instruction.
   * Linking: The final stage involves the linker. If your program consists of multiple source files or uses external libraries, these need to be combined into a single executable. The linker resolves references to undefined symbols, like functions or global variables defined in other files or libraries, and combines the object files (the compiled files) into a single executable program.
3. Thankfully, GCC abstracts these stages in such a way that a user typically only needs to execute a single command to perform all these steps. For instance, running gcc -o output source.c will preprocess, compile, assemble, and link the source code, producing an executable named ‘output’.
4. By default, GCC discards the intermediate outputs, leaving only the resulting executable.  You can instruct GCC to save the intermediate outputs using the --savetemps command. For example, to save the intermediate outputs of hello.c:&#x20;

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





