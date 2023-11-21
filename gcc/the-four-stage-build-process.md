# The Four Stage Build Process

Suppose we have the following C program stored in intmath.c:

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

It prompts the user for two inetegrs and then prints their greatest common divisor and least common multiple on the screen.

As you know, in order to run this program, we first have to compile it. Compilation refers to the process of converting a program from the textual source code into machine code--the sequence of 1’s and 0’s used to control the central processing unit (CPU) of the computer. This machine code is then stored in a file known as an executable file.&#x20;

To compile intmath.c with gcc217, we can use the following command:

```
gcc217 intmath.c
```

This command compiles the source code from `intmath.c` into machine code, creating an executable file. By default, this file is named `a.out`. However, if you want to specify a different name for the executable, you can use the `-o` option in your command. For example, to name your executable `intmath`:

```
gcc217 intmath.c -o intmath 
```

And the executable will be saved in a file named intmath instead of a.out.&#x20;

To run intmath, simple invoke its pathname on the command line, like so:&#x20;

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

**Build process**

The compilation of a C program actually involves four distinct stages: preprocessing, compilation proper, assembly, and linking. Show diagram of files. explain that while each of these are generated, they are by default discarded by GCC. Let's elaborate these four stages and examine them in relation to intmath.c.&#x20;

### Preprocessing&#x20;

The compilation journey begins with preprocessing. In this stage, the preprocessor prepares the source code for compilation by carrying out two main tasks:

1. **Removing the Comments**: The preprocessor starts by removing comments from the source code. Comments, which are used to make the code easier to understand for humans, are not necessary for the program's functionality. Including them in the compilation process would add unnecessary overhead for the compiler. Therefore, they are stripped away before the actual compilation begins. In `intmath.c`, this means that the comments on lines 1-4, 8, and 19 are removed.
2. **Handling Preprocessor Directives**: The other task involves handling preprocessor directives. These directives are special instructions in the source code that guide the preprocessor on how to prepare the code for compilation. Preprocessor directives begin with a # symbol and perform a variety of tasks, such as including other files or defining conditional compilation options. Among these, the `#include` directive is particularly significant and widely used. It tells the preprocessor to include the contents of another file into the current file. This is essential for bringing in external functionalities and libraries that the code may depend on.

In the specific case of `intmath.c`, the preprocessor handles the `#include <stdio.h>` directive on line 6. This directive includes the standard input and output header file (stdio.h), which provides necessary functions like printfandscanf\` used in the program.

By default, GCC will discard the preproccessed version of the The preprocessed version of intmath.c looks like the following:

It's important to note that preprocessing is essentially just a prelude to the main compilation process. The output of the GCC preprocessor is still C source code, albeit modified and prepared for the next stages of compilation. This modified code is devoid of comments and has integrated all the necessary instructions from the preprocessor directives, ready for the compiler to take over.

\


**2. Compilation**

The next stage is the compilation of the preprocessed code. Here, the source code of `intmath.c` is translated from C into assembly language. This transformation is significant as it turns high-level constructs like loops and function calls into a set of instructions understandable at a lower level, bridging the gap between abstract programming concepts and the more concrete instructions needed by the machine.

**3. Assembly**

Following compilation, the assembly process commences. The assembly language code, derived from `intmath.c`, is converted into machine code, also known as object code. This code is a binary representation tailored to the processor type that will execute the program, comprising the instructions that the computer will directly execute.

**4. Linking**

The final stage is linking. The object code from `intmath.c` is not yet a complete executable program. It requires linking with other object files and libraries. For example, the standard I/O functions utilized in `intmath.c` are part of external libraries that need to be connected with our program. The linking stage amalgamates the object code with these necessary libraries to create the final executable.

We will assume that the source code is stored in a file called ‘intmath.c’.&#x20;

In order to make intmath.c executabe, we need to convert it to machine code, which is the only language the computer understands. To do this, we can invoke gcc217 like so:&#x20;

```bash
gcc217 intmath.c -o intmath
```

This compiles the source code in ‘intmath.c’ to machine code and stores it in an executable file ‘intmath’. The output file for the machine code is specified using the ‘-o’ option. This option is usually given as the last argument on the command line. If it is omitted, the output is written to a default file called ‘a.out’.&#x20;

Note that if a file with the same name as the executable file already exists in the current directory it will be overwritten.&#x20;

### Compiling multiple source files&#x20;

Suppose in the interest of modularity, we want to split our program into two files. This makes it easier to understand and maintain, especially as our program grows larger.&#x20;

Suppose we try to split it up as follows: we keep the gcd and lcm functions in intmath.c, but we move the main method into a new file named testintmath.c. The idea is for intmath.c to contain the implementation of the gcd and lcm functions, while testintmain.c serves as a client of intmath.c. However, splitting the program requires us to add prototypes for the gcd and lcm functions to testintmath.c. Now, our program looks like the following:&#x20;

intmath.c:

```c
int gcd(int i, int j) {
    int temp;
    while (j != 0) {
        temp = i % j;
        i = j;
        j = temp;
    } 
    return i;
} 

int lcm(int i, int j) {
    return (i / gcd(i, j)) * j;
}
```

testintmath.c:

```c
int gcd(int i, int j);
int lcm(int i, int j);

int main(void) {
    int greatest_common_divisor = gcd(2, 3);
    int least_common_multiple = lcm(2, 3);
    return 0; 
}
```



To compile out program, we invoke gcc217 with intmath.c and testintmath.c, like so:

```
gcc217 intmath.c testintmath.c -o intmath
```

Which will generate an executable named intmath. In order to understand why we had to add the function prototypes, we need to understand how the compilation process works in C.&#x20;

### Seperate Compilation

When multiple source files are passed to GCC to be compiled, GCC does not compile the source files as a single unit. That is, it does not combine the source code of all files into one file and then compile that file into an executable. Instead, it compiles each source file _seperately_ into and stores each files corresponding machine code in an _object file_ with the same name as the source file but with a .o extension_._ Object files contain machine code, but they are not executable, since (1) they need not contain a main method; and (2) they may contain references to external functions or variables.  is essentially a machine code version of the corresponding source file, but its not execcutable, since (1) it contains references to functions or variables defined in other object files and need not contain a main method.  It then merges, or links, all the object files together to create an executable. This idea is demonstrating in Figure X using intmath.c and testintmath.c.&#x20;

<figure><img src="../.gitbook/assets/Group 82.png" alt=""><figcaption></figcaption></figure>





<figure><img src="../.gitbook/assets/Group 81.png" alt=""><figcaption></figcaption></figure>
