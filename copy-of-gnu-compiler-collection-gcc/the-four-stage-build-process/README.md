# The Four Stage Build Process

This chapter aims to describe in detail how GCC transforms source files into an executable file. Compilation is a four-stage process involving preprocessing, compilation proper, assembly, and linking. From a bird’s-eye view, these steps can be summarized as follows:&#x20;

1. Preprocessing: This is the first stage, where GCC processes the source code before actual compilation. It involves handling directives such as #include (which includes other files), #define (which defines macros), and conditional compilation directives like #if. This stage essentially prepares the source code by expanding macros, processing includes, and applying conditional compilation.
2. Compilation proper: During this stage, the preprocessed source code is converted into assembly language specific to the target processor. The compiler analyzes the code (syntax and semantics) and translates it into a lower-level, more detailed representation. This is where the high-level constructs (like loops, conditionals, etc.) are translated into a series of instructions that the processor can understand.
3. Assembly: The assembly language code generated in the previous step is then converted into machine code by an assembler. The machine code is essentially a set of binary instructions understandable by the processor. Each line of assembly language corresponds to a machine language instruction.
4. Linking: The final stage involves the linker. If your program consists of multiple source files or uses external libraries, these need to be combined into a single executable. The linker resolves references to undefined symbols, like functions or global variables defined in other files or libraries, and combines the object files (the compiled files) into a single executable program.

Explain how GCC abstracts this away

This four-step build process is performed by GCC whenever a C source file (i.e., a file with a .c extension) is built. By default, GCC discards the intermediate outputs, leaving only the resulting executable.  You can instruct GCC to save the intermediate outputs using the --savetemps command. For example, to save the intermediate outputs of hello.c:&#x20;

```
gcc --savetemps hello.c -o hello
```

the preprocessed, compiled, and assembled outputs will be saved in hello.i, hello.s, and hello.o respectively. You can confirm this by invoking ls.



Why it matters:

Let's be real: programming isn't just about getting your code to work. It's also about understanding why and how it works. This is especially true when you're dealing with something as fundamental as the GCC compilation process. For instance, have you thought about why you don't have to recompile your entire project every time you make a small change? That's thanks to GCC's ability to compile files separately – a real time-saver, especially when you're working on larger projects, which you'll often encounter here at Princeton.

And then there's debugging – every programmer's favorite pastime, right? Knowing what happens at each stage of the GCC compilation can be a game-changer when you're trying to figure out why something's not working. Say you're stuck with a linking error. With a solid understanding of the compilation process, you'll know that it's probably not about your code's syntax but more about how different parts of your program are being stitched together.







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





