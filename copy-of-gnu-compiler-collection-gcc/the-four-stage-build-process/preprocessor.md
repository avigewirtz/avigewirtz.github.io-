# Preprocessor

The preprocessor is a program that reads the source code and responds to directives embedded in it to produce a modified version of the source, which is fed to the compiler.



### Preprocessor Directives

Preprocessor directives are instructions in the source code The instructions to the preprocessor appear in the source as directives and can be easily spotted in the source code because they all begin with a hash (#) character, appearing as the first nonblank character on a line. The hash character usually appears on column 1 and is immediately followed by the directive keyword. All the directives are listed in Table 3-1 and described in the paragraphs that follow the table. It is possible for the preprocessor to modify source lines other than the ones with directives, but only if there is a directive instructing it to do so.

\#include

The include directive searches for the named file and inserts its contents into the text just as if it had been inserted there by a text editor. A file that is included this way is generally referred to as a header file and carries a .h suffix, but it can be any text file with any name.

The include directive has two forms. The one most used for system header files surrounds the name with a pair of angle brackets, with the form for user header files being surrounded by quotes, as follows:

```
       #include <syshead.h>
       #include "userhead.h"
```

The following is a list of characteristics and rules that apply to the #include directive:

* The angle brackets surrounding the file name cause the search to begin in any directories that were specified by using a -I option and then continue by looking through the standard set of system directories.
* A pair of quotes surrounding the file name causes the search to begin in the current working directory (the one containing the source file being processed) and then continue with the directories that would normally be searched by\
  a directive with the angle brackets.
* It is an error to have anything other than a comment on the same line as the #include directive.

\#define Defines a name as a macro that the preprocessor will expand in the code every place the name is used.



### Predefined Macros

The GCC compiler predefines a large number of macros.

inserted by a text editor.

1. **Removing Comments**: Comments serve to make the code easier for humans to understand but are not necessary for the program's functionality. Including them in the compilation process would add unnecessary overhead for the compiler. Therefore, they are stripped away before the actual compilation begins. In `intmath.c`, this means that the comments on lines 1-4, 8, and 19 are removed.
2. **Handling Preprocessor Directives**: The other task involves handling preprocessor directives. These directives are special instructions in the source code that guide the preprocessor on how to prepare the code for compilation. Preprocessor directives begin with a # symbol and perform a variety of tasks, such as including other files or defining conditional compilation options. Among these, the `#include` directive is particularly significant and widely used. It tells the preprocessor to include the contents of another file into the current file. This is essential for bringing in external functionalities and libraries that the code may depend on.

In the specific case of `intmath.c`, the preprocessor handles the `#include <stdio.h>` directive on line 6. This includes the contents of the stdio.h file in the place where the include directive appeared. stdio.h contains all function prototypes for C's standard input and output library. If you ever use a standard onput or output call in your code, you likely have to include stdio.h. This is easy to remeber if you recognize that stdio stands for "standard input/output."&#x20;

The preproccessed version of intmath.c looks like the following:

Note that while preprocessing always takes place, GCC by default discards the preprocessed output.&#x20;

It's important to note that preprocessing is essentially just a prelude to the main compilation process. The output of the GCC preprocessor is still C source code, albeit modified and prepared for the next stages of compilation. This modified code is devoid of comments and has integrated all the necessary instructions from the preprocessor directives, ready for the compiler to take over.

###
