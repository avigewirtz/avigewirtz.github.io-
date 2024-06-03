# Deep Dive

Let's now analyze each of the build stages in practice. As an example, we'll use the multi-file C program shown below. The program consists of three files: `testcircle.c`, `circle.c`, and `circle.h`. `testcircle.c` contains the `main` function, the entry point of our program. It prompts the user for the radius of a circle, computes its area using the `calculateArea` function, and prints the result on stdout. `circle.c` and `circle.h` contain the definition (i.e., implementation) and declaration of `calculateArea`, respectively.

{% tabs %}
{% tab title="testcircle.c (client)" %}
{% code lineNumbers="true" %}
```c
/*--------------------------------------------------------------------*/
/* testcircle.c                                                       */
/*                                                                    */
/* Calculates the area of a circle given its radius.                  */
/*--------------------------------------------------------------------*/
 
#include <stdio.h>
#include <stdlib.h>
#include "circle.h"

/* Prompts user for the radius of a circle. Returns
   EXIT_FAILURE if input is invalid. Otherwise, prints
   circle's area to stdout and returns 0. */
   
int main(void) {

  double radius, area;

  printf("Enter radius of circle: ");
  if (scanf("%lf", &radius) != 1 || radius <= 0) {
    printf("Invalid input. Must be a positive number.\n");
    exit(EXIT_FAILURE);
  }

  area = calculateArea(radius);

  printf("The area of the circle is: %.2f\n", area);

  return 0;
}
```
{% endcode %}
{% endtab %}

{% tab title="circle.c (implementation)" %}
{% code lineNumbers="true" %}
```c
/*--------------------------------------------------------------------*/
/* circle.c                                                           */
/*--------------------------------------------------------------------*/

#include "circle.h"
#define PI 3.14159

double calculateArea(double radius) {
    return PI * radius * radius;
}
```
{% endcode %}
{% endtab %}

{% tab title="circle.h (interface)" %}
{% code lineNumbers="true" %}
```c
#ifndef CIRCLE_H
#define CIRCLE_H

double calculateArea(double radius);

#endif
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Preprocessing Stage

The build process begins with preprocessing. We invoke the preprocessor on `testcircle.c` and `circle.c` with the following commands:

```bash
gcc217 -E tescircle.c > testcircle.i
gcc217 -E circle.c > circle.i
```

The result is two preprocessed files: `testcircle.i`, and `circle.i`. As mentioned earlier, the preprocessor performs two main tasks: It removes comments, which are of no use to the compiler, and handles preprocessor directives (lines in the code that begin with a `#`). Our program makes use of three types of preprocessor directives: `#include` (`testintmath.c` and `intmath.c`), `#define` (`intmath.c`), and `#ifndef` / `#else` (`intmath.h`). These directives control file inclusion, macro definition, and conditional compilation, respectively.

#### File Inclusion

Recall that definitions of externally defined functions are resolved at link time. Thus, when the compiler processes a file, it has no knowledge of these function definitions, even if they're defined in another file passed to the compiler simultaneously. This is because the compiler processes only one file at a time.

Consider `testcircle.c`. It uses four externally defined functions: `printf`, `scanf`, `exit`, and `calculateArea`. The first three are defined in the C standard library, while `calculateArea` is defined in `circle.c`

This presents a challenge. One of the roles of the compiler is to check for semantics errors in the code. The compiler needs to know, at a minimum, the return type of each function being called so it can properly handle the returned value. Ideally, it should also know the number and types of arguments the function takes so it can verify correct usage and perform type checking. How can the compiler obtain this information if it doesn't have access to the full function definitions?

The solution is to insert declarations of each externally defined function into every file where the function is called. A declaration specifies the function's name, return type, and the number and types of its arguments. It's a way of informing the compiler, "A function with this signature exists." This enables the compiler to generate correct code for function calls and detect potential errors.

When C first came out, it had no preprocessor, and thus no file inclusion mechanism. Programmers had to manually insert the declaration of all externally defined function into the files in which they were called. As you can imagine, this proved tedious and error prone. The solution was to adopt a file-inclusion mechanism. In this scheme, related declarations are bundled into a header file. For example, all standard I/O functions are bundled into the header file stdio.h. Now, to use I/O library functions, all you have to do is `#include <stdio.h>` into your file, rather than manually adding all relevant declarations.

`testintmath.c` `#includes` three header files: `stdio.h`, `stdlib.h`, and `circle.h`. These contain the declarations of the `printf/scanf`, `exit`, and `calculateArea` functions, respectively. Additionally, `stdlib.h` contains the definition of the `EXIT_FAILURE` macro (see below).

Although not strictly necessary, `circle.c` also includes `circle.h`. This ensures that the declaration of `calculateArea` in `circle.h` matches its declaration (in its definition) in `circle.c`. If there's a discrepancy between the two, the compiler will report an error.

{% hint style="info" %}
**`#include` Syntax**

Notice that there are two syntaxes for the `#include` directive: with angle brackets (e.g., `#include <stdio.h>`), and with double quotes (e.g., `#include "circle.h"`). The difference between these two syntaxes lies in how the preprocessor searches for the specified file, with the precise details being implementation-defined. In general, files #included with angle brackets are searched for in system directories only, while those #included with double quotes are searched for in the working directory first and then in system directories.
{% endhint %}

#### Macro Definition

The `#define` directive creates a preprocessor macro, which is essentially an alias for a specific value or code snippet. In `circle.c`, `#define PI 3.14159` creates the macro `PI` and assigns it the value `3.14159`. Whenever `PI` is subsequently used in `circle.c`, the preprocessor replaces it with `3.14159`.

`testcirle.c` uses the macro `EXIT_FAILURE`, which is defined in `stdlib.h`. The exact value of `EXIT_FAILURE` can vary between different systems, but it is commonly set to 1, as it is in our case.

#### Conditional Compilation

The `#ifndef` / `#else` directives, which we use in `intmath.h`, are part of a set of directives known as _conditional_ directives. They define a block of code that is either to be included These are used to control which parts of the source code are sent to the compiler. One of their most common use cases is to prevent the contents of a header file from being included twice in the same compilation unit (i.e., `.i` file). This technique is known as an _#include guard_. Here's how it works in `intmath.h`:

* `#ifndef CIRCLE_H`: This checks if `CIRCLE_H` is defined as a macro. If this evaluates to TRUE (1) (i.e., `CIRCLE_H` is not defined), the preprocessor will continue to process the code between `#ifndef` and `#endif`. If it evaluates to FALSE (0), the preprocessor will skip the entire block within `#ifndef` ... `#endif`.
* `#define CIRCLE_H`: This defines `CIRCLE_H`. Notice that it doesn't give `CIRCLE_H` any specific value. This is perfectly valid. The preprocessor will simply note that `CIRCLE_H` is defined. Going forward, `#ifndef CIRCLE_H` will evaluate to FALSE, and the preprocessor will skip the block.
* `#endif`: This ends the conditional block started by `#ifndef`. Every conditional directive must have a corresponding `#endif`.

#### Examining Preprocessed Output

You can view the preprocessed files with a text editor like emacs. Let’s examine `testcircle.i` and `circle.i` to see what precisely was done by the preprocessor. A side-by-side comparison is shown in Figure 12.

<figure><img src="../.gitbook/assets/Group 20 (9).png" alt=""><figcaption></figcaption></figure>

First, we see that the preprocessor removed all comments from `testcircle.c` and `circle.c`. Second, it replaced each `#include` directive with the contents of its specified header: `circle.h` for both `circle.c` and `testcircle.c`, and `stdio.h` and `stdlib.h` for `testcircle.c`. Finally, all macros were expanded: `PI` in `circle.c` was replaced with `3.14159`, and `EXIT_FAILURE` was replaced with `1`.

{% hint style="success" %}
You can think of the preprocessor as a "search-and-replace" tool:

* It replaces each comment with a whitespace character.
* It replaces each `#include` directive with the contents of the specified file.
* It replaces each macro with its value.
{% endhint %}

### Compilation Stage

Compilation is where the bulk of the work takes place. The job of the compiler is to translate preprocessed source code into assembly language. If the compiler encounters any syntax or semantic errors in the C code, it will flag them and terminate.

Syntax errors are straightforward grammar related mistakes, such as forgetting a semicolon or a curly brace. Semantic errors, on the other hand, are more complex errors that affect the meaning of the code, such as using variables that have not been initialized, type mismatches, or operations that don’t make sense on the given data types. These are often not as immediately obvious as syntax errors and can result in logic errors if not caught. An example of a semantics error is calling a function with incompatible arguments, or wrong return type. This is precisely why we wrong number of arguments

We compile `testcircle.i` and `circle.i` by invoking `gcc217` with the `-S` option:

```bash
gcc217 -S testcircle.i circle.i
```

This instructs the `gcc` to stop after compilation and output assembly-language files `testcircle.s` and `circle.s`. Assembly language is essentially a human-readable version of the target processor's machine language. As such, the precise assembly language generated by the compiler depends on the architecture of the target processor. Figure 14 shows what the assembly output might look like on an ARM64 machine, such as Armlab.

<figure><img src="../.gitbook/assets/Frame 63.png" alt="" width="563"><figcaption></figcaption></figure>

#### Characteristics of Assembly language

Detailed coverage of assembly language is beyond the scope of this chapter. ARM64 assembly will be covered in detail in the second half of COS217. For now, we will make a few general points about assembly.

*   Each assembly instruction performs a very basic task, such as adding two numbers or moving data from one memory location to another. As such, it has a poor ratio of functionality to code size compared to higher-level languages like C. For example, the C statement `x = y + z` requires four ARM assembly instructions:

    ```armasm
    LDR X0, [y]      ; Load the value of y into register X0 
    LDR X1, [z]      ; Load the value of z into register X1
    ADD X0, X0, X1   ; Add the values in X0 and X1, store result in X0
    STR X0, [x]      ; Store the result from X0 into the variable x
    ```
* Assembly language gives you total control over the CPU. Some operations possible in assembly have no high-level language equivalent. This allows you to optimize performance and resource usage to a degree not possible in higher-level languages.
* One of the main drawbacks of assembly is that it's not portable. Unlike like a high-level language like C, \<fill in>.

### Assembly Stage

The third stage is assembly. Here, the assembler translates the assembly language in `testcircle.s` and `circle.s` into machine language and stores the result in what are known as _relocatable object files_, which by convention have a `.o` extension. Because there's typically a one-to-one mapping between assembly language instructions and machine-language instructions, this translation is much simpler than compilation.

We invoke the assembler on `testcircle.s` and `circle.s` with the following command:

```
gcc217 -c testcircle.s circle.s
```

The result is two relocatable object files, `testcircle.o` and `circle.o`. Because these are binary files, viewing their contents with a text editor will display gibberish.

<figure><img src="../.gitbook/assets/Frame 62.png" alt="" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
relocateable object files are binary files divided into sections.
{% endhint %}

### Linking Stage

Linking marks the final stage of the build process. The linker takes as input a collection of relocatable object files and combines them into a single file known as an _executable object file_. As its name suggests, an executable object file contains machine code in a form that can be loaded into memory and executed. In our example, the linker's inputs are `testcircle.o`, `circle.o`, and the C standard library, which on Linux is stored in `libc.a`. We invoke the linker using the following command:

```
gcc217 testcircle.o circle.o -o testcircle
```

Note that we don't need to explicitly pass `libc.a` to the linker, as `gcc` automatically includes it. The output is the executable object file `testcircle`.

<figure><img src="../.gitbook/assets/Frame 60 (1).png" alt="" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**libc.a**

`libc.a` is an archive file. An archive file is a single file that contains within it a collection of relocatable object files, along with metadata describing the location of each file. The linker extracts only the relocatable object files of the functions referenced by our program.
{% endhint %}

{% hint style="info" %}
Besides inserting definitions of functions like `printf`, `scanf`, and `exit` from the C standard library, the linker also inserts some runtime starter code. This includes the startup routine responsible for setting up the program's environment and ultimately calling the `main` function.
{% endhint %}
