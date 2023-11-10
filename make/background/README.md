# Background

The beauty of `make` lies in its ability to combine the efficiency benefits of compiling only what is necessary with the convenience of not having to manually track which parts of the codebase have changed.

## Motivation

As C programs grow larger and evolve into multi-file projects, the compilation process becomes more complex. The traditional method of compiling all source files together in a single step can become impractical due to increased build times and resource consumption. This is where taking advantage of GCC's separate compilation feature comes into play.

Separate compilation refers to the process of compiling each source file (`.c` files) into an object file (`.o` files) independently of others. These object files contain machine code, but they are not yet executable. The final step in building a program is linking these object files together to create an executable.

To make the idea of separate compilation concrete, let's demonstrate with a muti-file program from precept.&#x20;

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

To compile the program, we invoke gcc217 with both intmath.c and testintmath.c as arguments:&#x20;

<pre class="language-bash"><code class="lang-bash"><a data-footnote-ref href="#user-content-fn-1">gcc217 intmath.c testintmath.c -o intmath</a>
</code></pre>

GCC generates an executable named intmath, which we can run by invoking ./intmath. Here is an example:

```bash
~> ./intmath
Enter the first integer:
3
Enter the second integer:
4
Greatest common divisor: 1.
Least common multiple: 12.
~> 
```



Let's walk through what happened during the compilation proccess.&#x20;



<figure><img src="../../.gitbook/assets/Group 65-2.png" alt="" width="563"><figcaption></figcaption></figure>

* Although we passed two source code files to GCC, it did not compile them as a single unit--that is, it did not combine the source code into one unit and then compile that unit.&#x20;
* instead, it compiled each source file independantly into an object file. expand.
* These object files contain the machine code of each of the files, but they are not executable, since intmath.c contains references to external functions--gcd(), lcm(), printf(), and scanf(). An object file contains machine code where any references to the memory addresses of functions (or variables) in other files are left undefined. This allows source files to be compiled without direct reference to each other. The linker fills in these missing addresses when it produces the executable. To make the program executable, the linker will link the two object files, along with the object code of printf() and scanf() from the C Standard Library, and generate an executable named intmath. This proccess is shown in Figure 1.







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









[^1]: Note that the header file ‘intmath.h’ is not specified in the list of files on the command line, since it is automatically included in appropriate points by the #include directives in ‘intmath.c’ and ‘testintmath.c’.&#x20;
