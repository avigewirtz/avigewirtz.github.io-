# Deep Dive into Each Stage

Now that we've given a high-level overview of the build process, let's take a deeper five into precisely what happens at each stage.&#x20;

## Preprocessing Stage

In the first stage of the build process, testcircle.c and circle.c are sent to the preprocessor, which outputs testcircle.i and circle.i. The modifications are shown in Figure 2.&#x20;

<div data-full-width="true">

<figure><img src="../.gitbook/assets/Group 19 (4).png" alt=""><figcaption></figcaption></figure>

</div>

Let's now examine the precise modifications the preprocessor makes by comparing testcircle.i and circle.i with testcircle.c and circle.c.&#x20;

* **Comments Removal.** First, we see that testcircle.i and circle.i do not contain comments. All comments in circle.c and testcircle.c were removed.
* **File Inclusion**. Second, we see that the preprocessor fetched the header files specified via #include directives in testcircle.c and circle.c and added their contents in the place where their their include directives appeared. In testcircle.i, we see the contents of the stdio.h, stdlib.h, and circle.h in the place where their directives appeared. Note that stdio and stdlib.h are large files, so we only show the relevant parts. For circle.c, the preprocessor inserted the contents of circle.h.&#x20;
* **Macro expansion**. Finally, we see that all macros have been expanded. PI in circle.c was replaced with 3.14159, and EXIT\_FAILURE in testcircle.c was replaced with 1. EXIT\_FAILURE is a macro defined in stdlib.h.

## Compilation Stage

The second stage involves compilation itself. Here, the compiler translates testcircle.i and circle.i into assembly-language, stored in testcircle.s and circle.s. Compilation is the most complex stage of the build process. It involves translating C source code into a completely different language. This is where the code is checked for errors. Figure 4.3 shows what the arm64 assembly looks like.&#x20;

<figure><img src="../.gitbook/assets/Group 20 (5).png" alt=""><figcaption></figcaption></figure>

## Characteristics of Assembly Language

A detailed explanation of assembly language is beyond the scope of this chapter. You can find a high level-overview in appendix 8. Arm64 assemvly will be covered in detail in the second hald of the course. For now, we will simply provide a few general points about assembly: &#x20;

* Extremely low-level language. Essentially human readable verson of target processor's machine language. Typically a one-to-one mapping between assembly language instruction and machine language instruction.&#x20;
* Specific to target architecture. each architecture has it's own assembly language.
* Not portable. In simple terms, this means that if I gave you assembly language program written for an architecture like x86 and told you to run it on an architecture like ARM, you'd have a very hard time doing so.&#x20;
* architecture Because assembly is esssentially a human readable version of the target processors machine code, just like machine language isn't portable (i.e., machine language program written for for an X86 will not run on an ARM), assembly language isn't either portable. Meaning, assembly language written for x86 cannot be translated into machine languag einstruciton for arm. compiler knows which assembly language to compile to



## Assembly Stage

The assembler translates the assembly-language in testcircle.s and circle.s into machine language, storing the results in testcircle.o and circle.o. This process is shown in Figure 4.3. Machine language is a binary language, consisting of only two symbols--0 and 1.

<figure><img src="../.gitbook/assets/Group 26 (1).png" alt=""><figcaption><p>Figure 4.3: Assembly Stage</p></figcaption></figure>



## Linking Stage

Our program is currently distributed across two files: testcircle.o and circle.o. While both of these files contain machine code, neither of them is executable on its own. For one, `circle.o` lacks a `main` function, which serves as the entry point for the program, and `testcircle.o` contains references to four external functions: `calculateArea`  (defined in circle.o), and `printf`, `scanf`, and `exit` (defined in C Standard Library).

To produce an executable file, the linker combines all these files--testcircle.o, circle.o, and C library--together, resolving all external references in our program. The output is a single file--the executable testcircle. This process is shown in Figure 6.&#x20;

<figure><img src="../.gitbook/assets/Group 28 (3).png" alt=""><figcaption></figcaption></figure>

