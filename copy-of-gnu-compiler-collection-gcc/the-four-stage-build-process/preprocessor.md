# Preprocessor

The compilation journey begins with preprocessing. The preprocessor is integrated into the GCC compiler and is not a separate program like the assembler or linker. The preprocessor's role is to prepare the source code for compilation. It does this by carrying out two tasks:

1. **Removing Comments**: Comments serve to make the code easier for humans to understand but are not necessary for the program's functionality. Including them in the compilation process would add unnecessary overhead for the compiler. Therefore, they are stripped away before the actual compilation begins. In `intmath.c`, this means that the comments on lines 1-4, 8, and 19 are removed.
2. **Handling Preprocessor Directives**: The other task involves handling preprocessor directives. These directives are special instructions in the source code that guide the preprocessor on how to prepare the code for compilation. Preprocessor directives begin with a # symbol and perform a variety of tasks, such as including other files or defining conditional compilation options. Among these, the `#include` directive is particularly significant and widely used. It tells the preprocessor to include the contents of another file into the current file. This is essential for bringing in external functionalities and libraries that the code may depend on.

In the specific case of `intmath.c`, the preprocessor handles the `#include <stdio.h>` directive on line 6. This includes the contents of the stdio.h file in the place where the include directive appeared. stdio.h contains all function prototypes for C's standard input and output library. If you ever use a standard onput or output call in your code, you likely have to include stdio.h. This is easy to remeber if you recognize that stdio stands for "standard input/output."&#x20;

The preproccessed version of intmath.c looks like the following:

Note that while preprocessing always takes place, GCC by default discards the preprocessed output.&#x20;

It's important to note that preprocessing is essentially just a prelude to the main compilation process. The output of the GCC preprocessor is still C source code, albeit modified and prepared for the next stages of compilation. This modified code is devoid of comments and has integrated all the necessary instructions from the preprocessor directives, ready for the compiler to take over.

### **Compilation Proper**

The next stage involves translating the preprocessed C source code into assembly language. Assembly language is essentially a human-readable version of machisp\[]\\;bm ,./oyg

There are many different assembly languages out there today.&#x20;

Note that the this stage is by far the most resource intensive of all four stages in the build process, since C (or any high level lanuage) and assembly are two completely different types of programming languages This stage is the most resource intensive of all four stages and constitutes the bulk of the work of GCC.&#x20;



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
