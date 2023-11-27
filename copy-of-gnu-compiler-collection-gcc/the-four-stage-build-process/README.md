# The Four Stage Build Process

The aim of this chapter is to describe in detail how GCC transforms source files to an executable file. Compilation involves up to four stages: preprocessing, compilation proper, assembly, and linking.&#x20;





several tools, including the GNU Compiler itself (gcc), the GNU Assembler (as), and the GNU Linker (ld).  Note that it is not necessary to use any of the individual commands described in this section to compile a program. All the commands are exe- cuted automatically and transparently by GCC internally, and can be seen using the ‘-v’ option described earlier. The purpose of this chapter is to provide an understanding of how the GCC compiler works.

As you know, in order to run this program, we first have to compile it. Compilation refers to the process of converting a program from the textual source code into machine code--the sequence of 1’s and 0’s used to control the central processing unit (CPU) of the computer. This machine code is then stored in a file known as an executable file.&#x20;

### Overview of the compilation process

The sequence of stages executed by a single invocation of GCC consists of:

1. Preprocessing
2. Compilation proper
3. Assembly
4. Linking

As an example, we will examine these compilation stages individually using the program ‘intmath.c’, which calculates the greatest common divisor (gcd) and least common multiple (lcm) of two integers:

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

To compile intmath.c with gcc217, we can use the following command:

```
gcc217 intmath.c
```

This command compiles the source code from `intmath.c` into machine code, creating an executable file. By default, this file is named `a.out`. However, if you want to specify a different name for the executable, you can use the `-o` option in your command. We'll do that and name our executable `intmath`:

```
gcc217 intmath.c -o intmath 
```

To run intmath, we invoke its pathname on the command line, like so:&#x20;

```
~> ./intmath
Enter the first integer:
2
Enter the second integer:
3
Greatest common divisor: 1.
Least common multiple: 6.
~> 
```
