# Preprocessor

Before a C program is compiled, it is first edited by a preprocessor. The result of preprocessing is a single file, which is then fed into the actual compiler.&#x20;















is replaced by the contents of the file _filename_. If the _filename_ is quoted, searching for the file

typically begins where the source program was found; if it is not found there, or if the name is

enclosed in < and >, searching follows an implementation-defined rule to find the file. An

included file may itself contain #include lines.









The majority of its job consists of making textual substitutions in the source code. A couple of the types of substitutions are triggered automatically, while others are trigged by intructions in the code known as preprocessor directives. &#x20;

Most of the textual substitutions performed by the preprocessor are triggered by preprocessor, but while others are dictated by the user via specific instructions in the code known as preprocessor directives. Preprocessor directives are easy to spot, since they all begin with a # (hash) character.  Let's first go over this textual substitution that happen by default and then go over the substitutions dictated by preprocessor directives. We will then examine a specific example with charcount.c.&#x20;

###

### Default substitutions&#x20;

* removing comments
* predefined macros

### Preprocessor Directives

There are numerous preprocessor directives. In cos217, you will encounter three types: #include, #define, and #ifdef. For now, we will describe only #include and #define, leaving the discussion of ifdef another chapter.&#x20;







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





###
