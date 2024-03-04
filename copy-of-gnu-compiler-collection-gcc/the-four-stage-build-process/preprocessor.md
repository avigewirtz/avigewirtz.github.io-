# Preprocessing Stage

The preprocessor is a program that processes the source files before the bulk of processing (i.e., compilation) takes place--hence the name preprocessor. Input is .c files, and output is .i files.&#x20;

* removing comments&#x20;
* Handling preprocessor directives
* Can think of preprocessor as a "search and replace" tool. &#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2024-03-04 at 11.43.20 AM.png" alt=""><figcaption></figcaption></figure>

preprocessor adds the following capabilities:&#x20;

* Inclusion of header files. These are files of declarations that can be substituted into your program.&#x20;
* Macro expansion. You can define macros, which are abbreviations for arbitrary fragments of C code. The preprocessor will replace the macros with their definitions throughout the program. Some macros are automatically defined for you.&#x20;
* Conditional compilation. You can include or exclude parts of the program according to various conditions

{% hint style="info" %}
* The preprocessor was not originally part of C language. Added in 1973&#x20;
{% endhint %}



### Preprocessor Directives

Preprocessor directives are lines in our program that start with the hash symbol #. Unlike traditional C code, they’re meant to be interpreted by the preprocessor, not the compiler. Our program makes use of preprocessor directives for three types of tasks: file inclusion, macro definition, and conditional compilation. While there are more types of preprocessor directives in C, these three are the most common, and the only ones you will encounter in cos217.

#### Macro&#x20;

The #define directive defines a macro, which is a fragment of code that has been given a name. In circle.c, #define PI 3.14159 defines the macro PI to represent the constant 3.14159.&#x20;

Whenever PI is used in circle.c, the preprocessor will replace it with 3.14159. This means that `return circumference / (2 *`` `<mark style="color:red;">`PI`</mark>`);` will be replaced by the preprocessor with `return circumference / (2 *`` `<mark style="color:red;">`3.14159`</mark>`);`

Macros offer several advantages:

* &#x20;It makes programs easier to read. The name of the macro—if well-chosen— helps the reader understand the meaning of the constant. The alternative is a program full of “magic numbers” that can easily mystify the reader.
* It makes programs easier to modify. We can change the value of a constant throughout a program by modifying a single macro definition. “Hard-coded” constants are more difficult to change, especially since they sometimes appear in a slightly altered form. (For example, a program with an array of length 100 may have a loop that goes from 0 to 99. If we merely try to locate occurrences of 100 in the program, we’ll miss the 99.)
* &#x20;It helps avoid inconsistencies and typographical errors. If a numerical constant like 3.14159 appears many times in a program, chances are it will occasionally be written 3.1416 or 3.14195 by accident.

#### Predefined macros

Some macros are already defined for us by the C preprocessor. One such macro is EXIT\_FAILURE, which we use in main.c.&#x20;

### File inclusion

By far the most popular preprocessor directive in C is the #include directive. Our program contains the following three:

* `#include <stdio.h>` (main.c)
* `#include <stdlib.g>` (main.c)
* `#include “circle.h”` (main.c and circle.c)

The `#include` directive instructs the preprocessor to include the contents of the specified file in the place where the include directive appears. In main.c, for example, the preprocessor replaces `#include <stdio.h>` with the contents of _stdio.h_. stdio.h is a system header file which contains, among other things, the prototypes of the printf() and scanf() functions.&#x20;

Notice that the syntax for the #include directive differs slightly depending on whether the specified file is a system header file or our header file. For system files, we enclose the filename in <>, such as with #include \<stdio.h> and #include \<stdlib.h> in main.c In contrast, when we include circle.h, which is our own header file we enclose the filename in quotes: #include “circle.h”.&#x20;

{% hint style="info" %}
The `#include`directive is typically used to include header files, but it can be used to include any file, regardless of its content or file extension. For example, #include "myprog.c" can be used to insert the contents of myprog.c in place where the directive appears.&#x20;
{% endhint %}

### Conditional compilation

Conditional compilation is a technique whereby you can omit entire segments of code from the translation unit sent by the preprocessor to the compiler. Preprocessor directives that control conditional compilation are known as conditional directives. Conditional directives all begin with #if, and they must be terminated by an #endif. This segment of text enclosed within the conditional directives is called controlled text.&#x20;

In circle.h, we wrap all the contents in conditional directives to prevent it from being included twice in the same translation unit. For reference, here is the relevant code, with the controlled text highlighted in red:

\#ifndef CIRCLE\_H

\#define CIRCLE\_H

double calculateRadius(double circumference);&#x20;

\


\#endif

\


Let’s break it down:

\


* \#ifndef CIRCLE\_H: This stands for "if not defined CIRCLE\_H". It checks if CIRCLE\_H has already been defined in the translation unit.&#x20;
*
  * If CIRCLE\_H is defined, that means that the circle.h header was already included in the translation unit, and the preprocessor will skip to the #endif directive. This will result in no
  * If CIRCLE\_H is not defined, that means that the circle.h header was not previously included in the translation unit, and the preprocessor will continue to the next line.&#x20;
  *
    * \#define CIRCLE\_H.&#x20;

\
\








### #include

The include directive searches for the named file and inserts its contents into the text just as if it had been inserted there by a text editor. A file that is included this way is generally referred to as a header file and carries a .h suffix, but it can be any text file with any name.

There are two ways to include files with the `#include` directive: using angle brackets (`#include <filename>`) and using double quotes (`#include "filename"`). The difference between these two has to do with how the compiler searches for the referenced file, with the precise details being implementation-defined. As a general rule, use angle brackets for library headers and double quotes for all other headers.&#x20;

The include directive has two forms. The one most used for system header files surrounds the name with a pair of angle brackets, with the form for user header files being surrounded by quotes, as follows:

The following is a list of characteristics and rules that apply to the #include directive:

* The angle brackets surrounding the file name cause the search to begin in any directories that were specified by using a -I option and then continue by looking through the standard set of system directories.
* A pair of quotes surrounding the file name causes the search to begin in the current working directory (the one containing the source file being processed) and then continue with the directories that would normally be searched by\
  a directive with the angle brackets.

### #define&#x20;

Defines a name as a macro that the preprocessor will expand in the code every place the name is used.



### Predefined Macros

The GCC compiler predefines a large number of macros.



1. **Removing Comments**: Comments serve to make the code easier for humans to understand but are not necessary for the program's functionality. As such, they are removed before actual compilation begins. In `intmath.c`, this means that the comments on lines 1-4, 8, and 19 are removed.
2. **Handling Preprocessor Directives**: The other task involves handling preprocessor directives. These directives are special instructions in the source code that guide the preprocessor on how to prepare the code for compilation. Preprocessor directives begin with a # symbol and perform a variety of tasks, such as including other files or defining conditional compilation options. Among these, the `#include` directive is particularly significant and widely used. It tells the preprocessor to include the contents of another file into the current file. This is essential for bringing in external functionalities and libraries that the code may depend on.

In the specific case of `intmath.c`, the preprocessor handles the `#include <stdio.h>` directive on line 6. This includes the contents of the stdio.h file in the place where the include directive appeared. stdio.h contains all function prototypes for C's standard input and output library. If you ever use a standard onput or output call in your code, you likely have to include stdio.h. This is easy to remeber if you recognize that stdio stands for "standard input/output."&#x20;



Difference between include syntax

###
