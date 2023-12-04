# Preprocessor

The C preprocessor, often known as _cpp_, is a _macro processor_ that is used automatically by the C compiler to transform your program before compilation. It is called a macro processor because it allows you to define _macros_, which are brief abbreviations for longer constructs.

The preprocessor's role is to prepare the source code for compilation. It does this by carrying out two tasks:

1. **Removing Comments**: Comments serve to make the code easier for humans to understand but are not necessary for the program's functionality. Including them in the compilation process would add unnecessary overhead for the compiler. Therefore, they are stripped away before the actual compilation begins. In `intmath.c`, this means that the comments on lines 1-4, 8, and 19 are removed.
2. **Handling Preprocessor Directives**: The other task involves handling preprocessor directives. These directives are special instructions in the source code that guide the preprocessor on how to prepare the code for compilation. Preprocessor directives begin with a # symbol and perform a variety of tasks, such as including other files or defining conditional compilation options. Among these, the `#include` directive is particularly significant and widely used. It tells the preprocessor to include the contents of another file into the current file. This is essential for bringing in external functionalities and libraries that the code may depend on.

In the specific case of `intmath.c`, the preprocessor handles the `#include <stdio.h>` directive on line 6. This includes the contents of the stdio.h file in the place where the include directive appeared. stdio.h contains all function prototypes for C's standard input and output library. If you ever use a standard onput or output call in your code, you likely have to include stdio.h. This is easy to remeber if you recognize that stdio stands for "standard input/output."&#x20;

The preproccessed version of intmath.c looks like the following:

Note that while preprocessing always takes place, GCC by default discards the preprocessed output.&#x20;

It's important to note that preprocessing is essentially just a prelude to the main compilation process. The output of the GCC preprocessor is still C source code, albeit modified and prepared for the next stages of compilation. This modified code is devoid of comments and has integrated all the necessary instructions from the preprocessor directives, ready for the compiler to take over.

###
