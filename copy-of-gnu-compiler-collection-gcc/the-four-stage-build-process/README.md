# The Four Stage Build Process

The purpose of compilation is to transform C source code—an English-resembling language suitable for human understanding—into executable machine code—a binary language suitable for computer processing.

GCC performs compilation in four sequential stages: preprocessing, compilation proper, assembly, and linking. The purpose of this chapter is to provide a detailed overview of each of these stages. We will illustrate these four stages by following the journey of a C program from source code to executable. The program we will use is a simple program that calculates the area of a circle given its circumference. It consists of three files: main.c, circle.c, and circle.h. Their source code is written below.&#x20;

{% code title="main.c" lineNumbers="true" %}
```c
#include <stdio.h>
#include <stdlib.h>
#include "circle.h"

int main() {
    double circumference, area;

    printf("Enter the circumference of the circle (positive number): ");
    if (scanf("%lf", &circumference) != 1 || circumference <= 0) {
        printf("Invalid input. Circumference must be a positive number.\n");
        exit(EXIT_FAILURE);
    }

    area = calculateArea(circumference);

    printf("The area of the circle is: %.2f\n", area);

    return 0;
}
```
{% endcode %}

{% code title="circle.c" lineNumbers="true" %}
```c
#include "circle.h"
#define PI 3.14159

double calculateArea(double circumference) {
    double radius = circumference / (2 * PI);
    return PI * radius * radius;
}

```
{% endcode %}

{% code title="circle.h" lineNumbers="true" %}
```c
#ifndef CIRCLE_H
#define CIRCLE_H

double calculateArea(double circumference);

#endif
```
{% endcode %}

## Bird’s eye view of the GCC compilation process

Before diving into the complexities of each stage, we'll first give a bird's eye view of the process. Having an overarching view will allow you to grasp the big picture, making it easier to contextualize the more detailed aspects that follow.

Suppose we compile our program with the following command:

```bash
gcc main.c circle.c -o circle
```

GCC will compile the program in the following manner:

* **Preprocessing**: The compilation journey begins with main.c and circle.c being sent to the preprocessor, which is a program that essentially prepares the source files for compilation. It does this by removing comments and responding to preprocessor directives--lines in the code that begin with the # (hash) character. For example, #include \<stdio.h> in main.c tells the preprocessor to insert the contents of stdio.h into the current file. The result of preprocessing is two files: main.i and circle.i. The preprocessor sends main.i and circle.i to the compiler.&#x20;
* **Compilation**: Next, the compiler translates `main.i` and `circle.i` into assembly language, which are stored in main.s and circle.s. Assembly language is essentially a human-readable form of machine language.
* **Assembly**: The assembler converts assembly code in main.s and circle.s to object code, storing the result in main.o and circle.o. These files contain machine code but aren't yet executable due to external references and/or absence of a main function. For example, circle.o lacks a main function, and main.o contains references to calculateArea and library functions (such as printf and scanf), al of which are external to main.o.
* **Linking**: Finally, the linker merges `main.o` and `circle.o`and the relevant library code, resolving external references to functions like calculateArea and printf. The result is is an executable named circle.&#x20;

<figure><img src="../../.gitbook/assets/Group 17.png" alt=""><figcaption><p>Four Stage Compilation Process of main.c and circle.c</p></figcaption></figure>

This process, summarized in Figure 1, resembles an assembly line. Our C program, starting as source code, moves through different 'stations'—the preprocessor, compiler, assembler, and linker—each transforming it closer to a finished product. By the end, our program emerges as an executable, ready to be run on a computer.

### Saving preprocessed, compiled, and assembled versions

By default, GCC stores the preprocessed, compiled, and assembled versions of the program in temporary files, which are discarded. As such, all you'll see is the executable. However, you can instruct GCC to save the preprocessed output by using the -save--temps option. To save the the intermediate outputs for main.c and circle.c, invoke gcc like so:

```bash
gcc main.c circle.c --save-temps -o circle
```

If you examine your directory contents with ls, you'll see the following



### Isolating Each Stage of Compilation









## Separate Compilation

It is important to recognize that main.c and circle.c are preprocessed, compiled, and assembled separately. Only after they are individually translated into machine code are they--along with the necessary library code--merged together to form an executable. This technique is known as _separate compilation_. It is employed by GCC&#x20;







### Motivation

Why are we concerning ourselves with the internals of how GCC performs compilation? After all, we regularly use programs without having any knowledge of their inner workings, focusing only on their output. Take the 'ls' command, for instance; we use it to list directory contents, but we don’t concern ourselves with its internals. So, why do we care when it comes to GCC?

Broadly speaking, there are two reasons. First, understanding these stages aids in debugging. Let’s face it, compilation isn’t always a smooth process. Quite often, something goes wrong along the way, and what you end up with is not an executable but a cryptic error message. Without a basic understanding of how compilation works, the cause of the error is likely to be elusive, making it incredibly difficult to debug your program.

Second, GCC is designed to enable separate compilation. This will be discussed in depth in the chapter on Make. In order to take advantage of separate compilation, however, you have to understand the process, particularly the linking phase.&#x20;

3\. Helps you understand what global variables are. This is mentioned in book when discussing linker

\
