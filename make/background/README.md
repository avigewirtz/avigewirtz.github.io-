# Background

### Compiling a C program

Consider the following program that prompts the user for two integers and calculates the greatest common divisor and the least common multiple.&#x20;

```c
/*--------------------------------------------------------------------*/
/* intmath.c                                                          */
/*--------------------------------------------------------------------*/

#include <stdio.h>

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

We will assume that the source code is stored in a file called ‘intmath.c’. To compile the file ‘intmath.c’ with gcc217, use the following command:

```
gcc217 intmath.c -o intmath
```

This compiles the source code in ‘intmath.c’ to machine code and stores it in an executable file ‘intmath’. To run intmath, you can type the path name of the executable like this: `./intmath`

### Compiling multiple source files

A program can be split up into multiple files. This makes it easier to understand and maintain, especially in the case of large programs. More importantly, it allows the individual parts to be compiled independently.

In the following example we will split up intmath.c into three files: ‘intmath.c’, ‘testintmath.c’ and the header file ‘intmath.h’. Here are the three files:

```c
/*--------------------------------------------------------------------*/
/* intmath.c                                                          */
/*--------------------------------------------------------------------*/

#include "intmath.h"

int gcd(int i, int j)
{
   int temp;
   while (j != 0) {
     temp = i % j;
     i = j;
     j = temp;
}
return i; }

int lcm(int i, int j)
{
   return (i / gcd(i, j)) * j;
}
```

```c
/*--------------------------------------------------------------------*/
/* testintmath.c                                                      */
/*--------------------------------------------------------------------*/

#include "intmath.h"
#include <stdio.h>

int main(void)
{
int i, j;
printf("Enter the first integer:\n"); scanf("%d", &i);
printf("Enter the second integer:\n"); scanf("%d", &j);
printf("Greatest common divisor: %d.\n", gcd(i, j));
printf("Least common multiple: %d.\n", lcm(i, j);
return 0; 
}
```

```c
/*--------------------------------------------------------------------*/
/* intmath.h                                                          */
/*--------------------------------------------------------------------*/

#ifndef INTMATH_INCLUDED 
#define INTMATH_INCLUDED 
int gcd(int i, int j); 
int lcm(int i, int j); 
#endif
```



The main program also includes the header file ‘hello.h’ which will contain the declaration of the function hello. The declaration is used to ensure that the types of the arguments and return value match up correctly between the function call and the function definition.

We no longer need to include the system header file ‘stdio.h’ in ‘main.c’ to declare the function printf, since the file ‘main.c’ does not call printf directly.

To compile these source files with gcc217, use the following command:&#x20;

```bash
gcc intmath.c testintmath.c -o intmath
```

Note that the header file ‘intmath.h’ is not specified in the list of files on the command line. The directive #include "intmath.h" in the source files instructs the compiler to include it automatically at the appropriate points.

All the parts of the program have been combined into a single executable file, intmath, which produces the same result as the executable created from the single source file used earlier.

### Compiling files independently

If a program is stored in a single file then any change to an individual function requires the whole program to be recompiled to produce a new executable. The recompilation of large source files can be very time- consuming.

When programs are stored in independent source files, only the files which have changed need to be recompiled after the source code has been modified. In this approach, the source files are compiled separately and then linked together—a two stage process. In the first stage, a file is compiled without creating an executable. The result is referred to as an object file, and has the extension ‘.o’ when using GCC.

In the second stage, the object files are merged together by a separate program called the linker. The linker combines all the object files together to create a single executable.

An object file contains machine code where any references to the memory addresses of functions (or variables) in other files are left undefined. This allows source files to be compiled without direct reference to each other. The linker fills in these missing addresses when it produces the executable.

### Creating object files from source files

The command-line option ‘-c’ is used to compile a source file to an object file. For example, the following command will compile the source file ‘intmath.c’ to an object file:

```
gcc217 -c intmath.c
```

This produces an object file ‘intmath.o’ containing the machine code for the main function. It contains a reference to the external function hello, but the corresponding memory address is left undefined in the object file at this stage (it will be filled in later by linking).

The corresponding command for compiling the hello function in the source file ‘testintmath.c’ is:

```
gcc217 -c testintmath.c
```

This produces the object file ‘testintmath.o’.

Note that there is no need to use the option ‘-o’ to specify the name of the output file in this case. When compiling with ‘-c’ the compiler automatically creates an object file whose name is the same as the source file, with ‘.o’ instead of the original extension.

There is no need to put the header file ‘intmath.h’ on the command line, since it is automatically included by the #include statements in ‘intmath.c’ and ‘testintmath.c’.

### Creating executables from object files

The final step in creating an executable file is to use gcc to link the object files together and fill in the missing addresses of external functions. To link object files together, they are simply listed on the command line:

```
    $ gcc main.o hello_fn.o -o hello
```

This is one of the few occasions where there is no need to use the ‘-Wall’ warning option, since the individual source files have already been success- fully compiled to object code. Once the source files have been compiled, linking is an unambiguous process which either succeeds or fails (it fails only if there are references which cannot be resolved).

To perform the linking step gcc uses the linker ld, which is a separate program. On GNU systems the GNU linker, GNU ld, is used. Other systems may use the GNU linker with GCC, or may have their own linkers. The linker itself will be discussed later (see Chapter 11 \[How the compiler works], page 81). By running the linker, gcc creates an executable file from the object files.

The resulting executable file can now be run:

```
    $ ./hello
    Hello, world!
```

It produces the same output as the version of the program using a single source file in the previous section.

### Recompiling and relinking

To show how source files can be compiled independently we will edit the main program ‘main.c’ and modify it to print a greeting to everyoneinstead of world:

```
      #include "hello.h"
```

```
      int
      main (void)
      {
```

```
        hello ("everyone");  /* changed from "world" */
```

return 0; }

The updated file ‘main.c’ can now be recompiled with the following com- mand:

```
    $ gcc -Wall -c main.c
```

This produces a new object file ‘main.o’. There is no need to create a new object file for ‘hello\_fn.c’, since that file and the related files that it depends on, such as header files, have not changed.

The new object file can be relinked with the hello function to create a new executable file:

$ gcc main.o hello\_fn.o -o hello\
The resulting executable ‘hello’ now uses the new main function to pro-

duce the following output:

```
    $ ./hello
    Hello, everyone!
```

Note that only the file ‘main.c’ has been recompiled, and then relinked with the existing object file for the hello function. If the file ‘hello\_fn.c’ had been modified instead, we could have recompiled ‘hello\_fn.c’ to create a new object file ‘hello\_fn.o’ and relinked this with the existing file ‘main.o’.(1)

In general, linking is faster than compilation—in a large project with many source files, recompiling only those that have been modified can make a significant saving. The process of recompiling only the modified

(1) If the prototype of a function has changed, it is necessary to modify and recompile all of the other source files which use it.

files in a project can be automated using GNU Make&#x20;
