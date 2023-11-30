# The Four Stage Build Process

The aim of this chapter is to describe in detail how GCC transforms source files to an executable file. While this transformation typically occurs through a single invocation of gcc, it is actually multi-stage process involving four distinct tools: the preprocessor, compiler, assembler, and linker. Roughly speaking, the role of each of these tools can be described as follows:&#x20;

1. Preprocessor: prepares the source code for compilation.&#x20;
2. Compiler: converts the preprocessed source code to assembly language.
3. Assembly: converts the assembly language to machine language.
4. Linking: resolves external dependencies, producing an executable.

While GCC performs each of these stages automatically whenever compiling a C source file (i.e., a file with a .c extension), by default it discards the intermediate outputs, leaving only the executable. It is possible to isolate and preserve the output of each stage by using the following options:

```bash
gcc217 -E # preprocess but do not compile 
gcc217 -S # compile but do not assemble
gcc217 -C # assemble but do not link
```

To illustrate the four stage build process in practice, we will examine each of the stages using ‘intmath.c’, a simple program for calculating the greatest common divisor (gcd) and least common multiple (lcm) of two integers.

{% code lineNumbers="true" %}
```c
/*--------------------------------------------------------------------*/
/* intmath.c                                                          */
/* Author: Bob Dondero                                                */
/*--------------------------------------------------------------------*/

#include <stdio.h>

/* Returns the greatest common divisor of integers i and j */
int gcd(int i, int j) {
    int temp;
    while (j != 0) {
        temp = i % j;
        i = j;
        j = temp;
    }
    return i;
}

/* Returns the least common multiple of integers i and j*/
int lcm(int i, int j) {
    return (i / gcd(i, j)) * j;
}

int main(void) {
    int i, j;

    printf("Enter the first integer:\n");
    scanf("%d", &i);

    printf("Enter the second integer:\n");
    scanf("%d", &j);

    printf("Greatest common divisor: %d.\n", gcd(i, j));
    printf("Least common multiple: %d.\n", lcm(i, j));

    return 0;
}

```
{% endcode %}

<figure><img src="../../.gitbook/assets/Group 81.png" alt=""><figcaption></figcaption></figure>
