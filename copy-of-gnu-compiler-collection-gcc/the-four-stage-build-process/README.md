# The Four Stage Build Process

The aim of this chapter is to provide a high-level overview of the GCC compilation process. While from the user's point of view compiling a C program is as simple as executing a single gcc command, behind the scenes. From GCC’s point of view, however, compilation is a multi-stage process, involving a suite of programs. By the end of this chapter, you should have a clearer understanding and appreciation of each stage involved in the GCC compilation process.&#x20;

## Motivation

You might be wondering why we are concerning ourselves with the internals of how GCC performs compilation. After all, we regularly use programs without having any knowledge of their inner workings, focusing only on their output. Take the 'ls' command, for instance; we use it to list directory contents, but we don’t concern ourselves with its internals. So, why do we care when it comes to GCC?

Broadly speaking, there are two reasons. First, understanding these stages aids in debugging. Let’s face it, compilation isn’t always a smooth process. Quite often, something goes wrong along the way, and what you end up with is not an executable but a cryptic error message. Without a basic understanding of how compilation works, the cause of the error is likely to be elusive, making it incredibly difficult to debug your program.

Second, GCC is designed to enable separate compilation. This will be discussed in depth in the chapter on Make. In order to take advantage of separate compilation, however, you have to understand the process, particularly the linking phase.&#x20;

3\. Helps you understand what global variables are. This is mentioned in book when discussing linker\


{% hint style="info" %}
Note on terminology

* terminology caan be confusing
*
{% endhint %}

## Bird’s eye view of the GCC compilation process

The GCC compilation process can be likened to an assembly line in a factory. The product is a C program, which begins its life as a source file. As it progresses through the production line, it is worked upon by different programs, each of which transforms the program one step closer to a finished product. By the end, the program emerges as an executable file.&#x20;

This ‘assembly line’ comprises four programs:

* Preprocessor (cpp)
* Compiler (cc1)
* Assembler (as)
* Linker (ld)

The source code is worked on by the preprocessor, whose output is fed to the compiler, whose output is fed to the assembler,&#x20;

The role of each of these programs can be summarized as follows:

1. The C preprocessor is a program that processes your source code before actual compilation. main compilation step in programming. Think of it as a preparatory stage where the code is pre-processed (processed beforehand). This involves handling specific instructions, known as preprocessor directives, which are not traditional C code but commands for the preprocessor. These directives can modify the code by including other files, defining constants, or even conditioning which parts of the code to compile. The preprocessor essentially sets up your code, making it ready for the compiler to take over and convert it into an executable program.
2. The program is first given to a preprocessor, which obeys commands that begin with # (known as directives). A preprocessor is a bit like an editor; it can add things to the program and make modifications.
3. The modified program now goes to a compiler, which translates it into assembly language instructions.&#x20;
4. Assembly to machine language. Object code.\

5. In the final step, a linker combines the object code produced by the compiler with any additional code needed to yield a complete executable program. This additional code includes library functions (like printf) that are used in the program.

\


Thankfully, the process is automated by the gcc compiler driver.&#x20;

\
\


### Saving preprocessed, compiled, and assembled versions

gcc -o hello hello.c --save-temps

This command will generate the following files in addition to the executable hello:

* hello.i: The result of the preprocessing stage.
* hello.s: The assembly code generated from the C source.
* hello.o: The object file generated from the assembly code.

### Isolating Each Stage of Compilation



\
