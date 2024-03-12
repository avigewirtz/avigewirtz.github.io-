# Deep Dive into Each Stage

Now that we've given a high-level overview of the build process, let's take a deeper five into precisely what happens at each stage.&#x20;

## Preprocessing Stage

We know that in the first stage of the build process, the testcircle.c and circle.c are sent to the preprocessor, which performs some modifications and outputs testcircle.i and circle.i. Let's figure out what modifications it performs by examining testcircle.i and circle.i: The modifications are summed up in Figure 4.2. Let's go through each one-by-one:&#x20;

The output is testcircle.i and circle.i. This process is illustrated in&#x20;

Let's now examine testcircle.i and circle.i The build process begins with the preprocessor. In this stage, testcircle.c and circle.c are sent to the p, which takes testcircle.c and circle.c as input, and outputs preprocessed files testcircle.i and circle.i. This process is illustrated in Figure 4.2.  &#x20;

1. **Removes comments**. Comments are intended for humans, but are of no use to the compiler. Hence, they can be discarded.&#x20;
2. **Handles **_**preprocessor directives**._ These are lines in the source code that start with a `#` (hash) symbol. Preprocessor macros control things like file inclusion and macro expansion.&#x20;

Let's now examine the the specific modification the preprocessor performs on our program. preprocessing n the first stage of the build process, `testcircle.c` and `circle.c` are sent to the preprocessor, which modifies their source code before actual compilation begins. It does two main things: The preprocessed output is stored in testcircle.i and circle.i. This process is illustrated in Figure 4.2. Let's now examine how these modifications work with our program. Let's now go over each one: &#x20;

<figure><img src="../.gitbook/assets/Frame 5 (3).png" alt="" width="563"><figcaption><p>Figure 4.3: Preprocessing Stage</p></figcaption></figure>

In testcircle.c, for example, the preprocessor inserts the contents of stdio.h in the place where `#include <stdio.h>` appears. _stdio.h_ is a system header file which contains the prototypes of functions like `printf()` and `scanf()`.

The `#define` directive creates a preprocessor macro, which is essentially an alias for a specific value or code snippet. Whenever the macro name is used in the code, the preprocessor replaces it with the macro's value. In circle.c, for example, `#define PI 3.14159` creates the macro `PI` and assigns it the value `3.14159`.  Whenever `PI` is subsequently used in circle.c, the preprocessor replaces it with `3.14159`.&#x20;

* **Comments Removal.** First, we see that testcircle.i and circle.i do not contain comments.&#x20;
* **File Inclusion**. Second, we see that the preprocessor fetched the header files specified via #include directives in testcircle.c and circle.c and added their contents in the place where their their include directives appeared. In testcircle.i, we see the contents of the stdio.h, stdlib.h, and circle.h in the place where their directives appeared. Note that stdio and stdlib.h are large files, so we only show the relevant parts. For circle.c, the preprocessor inserted the contents of circle.h.&#x20;
* **Macro expansion**. Finally, we see that all macros have been expanded. PI in circle.c was replaced with 3.14159, and EXIT\_FAILURE in testcircle.c was replaced with 1. EXIT\_FAILURE is a macro defined in stdlib.h.



After preprocessing, the source code, now free of comments and with all macros expanded and header file contents included, is ready for the next stage: compilation.

## Compilation Stage

The second stage involves compilation itself. Here, testcircle.i and circle.i are sent to the compiler, which translate their C code into assembly-language, stored in testcircle.s and circle.s. Compilation is the most complex stage of the build process. It involves translating C source code into a completely different language. This is where the code is checked for errors. Figure 4.3 shows what the arm64 assembly looks like.&#x20;

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

