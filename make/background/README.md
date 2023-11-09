# Background

* The purpose of Make is to make compiling multi-file programs easier. Understanding the challenges of compiling multi-file programs
* To understand this, we need to back up and review some of the fundamentals of how compiling works in C. Specificaly, it's important that you understand the concept of "seperate compilation" and how it works in C

Suppose we have a program made up of three files: `intmath.c`, `testintmath.c`, and `intmath.h`. `intmath.c` contains the implementation of two functions, `gcd` (greatest common divisor) and `lcm` (least common multiple).`testintmath.c` contains the `main` function, which tests these two functions by prompting the user for two integers, passing them to the gcd and lcm functions in intmath.c, and displaying the results. The `intmath.h` file contains declarations of the `gcd` and `lcm` functions, ensuring that the types of the arguments and return value match up correctly between the function call and the function definition.



```c
/*--------------------------------------------------------------------*/
/* testintmath.c                                                      */
/*--------------------------------------------------------------------*/

#include <stdio.h>
#include "intmath.h"

int main(void)
{
int i, j;
printf("Enter the first integer:\n"); scanf("%d", &i);
printf("Enter the second integer:\n"); scanf("%d", &j);
printf("Greatest common divisor: %d.\n", gcd(i, j));
printf("Least common multiple: %d.\n", lcm(i, j));
return 0; 
}
```

2

```c
/*--------------------------------------------------------------------*/
/* testintmath.c                                                      */
/*--------------------------------------------------------------------*/

#include <stdio.h>
#include "intmath.h"

int main(void)
{
int i, j;
printf("Enter the first integer:\n"); scanf("%d", &i);
printf("Enter the second integer:\n"); scanf("%d", &j);
printf("Greatest common divisor: %d.\n", gcd(i, j));
printf("Least common multiple: %d.\n", lcm(i, j));
return 0; 
}
```

```c
/*--------------------------------------------------------------------*/
/* intmath.h */
/*--------------------------------------------------------------------*/
#ifndef INTMATH_INCLUDED 
#define INTMATH_INCLUDED 
int gcd(int i, int j); 
int lcm(int i, int j); 
#endif
```

To compile the program with gcc217, we can use the following command:&#x20;

```bash
gcc217 intmath.c testintmath.c -o intmath
```

The gcc compiler will then generate an executable named intmath. (Note that there is no need to put the header file ‘intmath.h’ on the command line, since it is automatically included by the #include statements in ‘intmath.c’ and ‘testintmath.c’. ) We can run intmath with by invoking ./intmath.&#x20;

As you're familiar from the beginning of COS217, the process of converting source code to an executable with GCC involves four stages: preprocessing, compiling, assembling, and linking.&#x20;

,,preproccess, compile, assemble, and link intmath.c and testintmath.c seperately, generating the object files intmath.o and testintmath.o. An object file contains machine code where any references to the memory addresses of functions (or variables) in other files are left undefined. This allows source files to be compiled without direct reference to each other. The linker fills in these missing addresses when it produces the executable. These object files contain the machine code of each of the files, but they are not executable, since intmath.c contains references to external functions--gcd(), lcm(), printf(), and scanf(). To make the program executable, the linker will link the two object files, along with the object code of printf() and scanf() from the C Standard Library, and generate an executable named intmath. This proccess is shown in Figure 1.































###

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











































Suppose we want to write a program that calculates the greatest common divisor and least common multiple of two integers. We create a file named intmath.c and write two functions in it--one for gcd, and one for lcd.&#x20;

```c
/*--------------------------------------------------------------------*/
/* intmath.c                                                          */
/*--------------------------------------------------------------------*/

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

To test our implementation, we create another file named testintmath.c that prompts the user for two integerts, calls the gcd and lcm functions, and outputs the answers to the user.

```c
/*--------------------------------------------------------------------*/
/* testintmath.c                                                      */
/*--------------------------------------------------------------------*/

#include <stdio.h>

int main(void)
{
int i, j;
printf("Enter the first integer:\n"); scanf("%d", &i);
printf("Enter the second integer:\n"); scanf("%d", &j);
printf("Greatest common divisor: %d.\n", gcd(i, j));
printf("Least common multiple: %d.\n", lcm(i, j));
return 0; 
}

```

You then try to compile testintmath.c using gcc217, but to your dismay, you get the following errors:

```bash
~> gcc217 testintmath.c -o testintmath
testintmath.c:8:42: error: implicit declaration of function 'gcd' [-Werror,-Wimplicit-function-declaration]
printf("Greatest common divisor: %d.\n", gcd(i, j));
                                         ^
testintmath.c:9:40: error: implicit declaration of function 'lcm' [-Werror,-Wimplicit-function-declaration]
printf("Least common multiple: %d.\n", lcm(i, j));
                                       ^
2 errors generated.
~> 
```

The exact meaning of these error messages is not clear to you, but you know it has something to do with the parts that call the gcd and lcm functions. You then realize, of course the program won't work--gcd and lcm are not defined anywhere in testinmath.c! So when you try to compile it, the compiler doesnt have a clue what gcd and lcm are!

solution 1: bad

Simple add the code for gcd and lcm into the testintmath.c program, above the main function. This is obviouslyt n ot a great solution, as it defeatsa the purpose of creating two seperate files--to make your program more modular!&#x20;



Solution two: better

You include the intmath.c code via a preproccesor directive--namely, by adding #include "intmath.c" at the top of your file. This way, you don;'t have to manulally copy and paste all the code. Instead, whenmeverrt you want to use it, you let the preproccessor do the work.

<pre class="language-c"><code class="lang-c">/*--------------------------------------------------------------------*/
/* testintmath.c                                                      */
/*--------------------------------------------------------------------*/

#include &#x3C;stdio.h>
<strong>#include "intmath.c" /* you add the following line*/
</strong>

int main(void)
{
int i, j;
printf("Enter the first integer:\n"); scanf("%d", &#x26;i);
printf("Enter the second integer:\n"); scanf("%d", &#x26;j);
printf("Greatest common divisor: %d.\n", gcd(i, j));
printf("Least common multiple: %d.\n", lcm(i, j));
return 0; 
}
</code></pre>

Solution 3: You&#x20;
