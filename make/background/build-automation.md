# Build Automation

n large software projects, recompiling all source files every time a single file is changed is not efficient, especially when compilation can take a long time. Instead, we only need to recompile the files that are dependent on the changed file.

This process is facilitated by creating object files (`.o` files) for each source file (`.c` files in C). An object file is a file containing object code, including instructions that the processor can understand but that are not executable as is.

Here's an example to illustrate this: if you make a change to `intmath.h`, only `intmath.c` (which directly includes `intmath.h`) needs to be recompiled. Then the object file `intmath.o` (created from `intmath.c`) will be updated. But if you change `intmath.c` without changing the header file `intmath.h`, then only `intmath.c` needs to be recompiled.

#### Keeping Track of Dependencies

However, in a large project, it can be difficult to manually track which source files depend on which headers, making it hard to determine what needs to be recompiled when something changes. This is where a utility like `make` becomes invaluable.

`make` automates this process. It reads a file, usually named `Makefile`, that resides in the same directory as the source files. This file describes the relationships between the source files, object files, and executable files, essentially outlining the dependencies of each file.

#### Using `make` to Build a Project

When we want to build our project, we simply invoke `make` in the command line. `make` then reads the Makefile and determines which files have been modified since the last build. It will then recompile only those source files that either have been modified or are dependent on modified files.

If no files have been changed since the last build, `make` will typically print a message like "make: Nothing to be done for 'all'."

The `make` utility simplifies the process of managing dependencies and compiling large software projects, making software development much more manageable. By only recompiling the files that need to be updated, it saves developers significant time and effort, especially in large projects.





































However, this object file may not be a complete program yet because it can contain unresolved symbols - references to functions or variables that are declared in the source file but defined somewhere else. This is where dependencies come into play.

1. **Object Files (.o)**: Object files depend on each other when they reference functions or variables defined in each other. For example, if file1.c calls a function that's defined in file2.c, then file1.o (the object file resulting from compiling file1.c) is dependent on file2.o. If file2.o changes (because file2.c was modified and recompiled), file1.o doesn't necessarily need to be recompiled (since the function declaration hasn't changed), but the final program needs to be relinked to incorporate the new version of file2.o.
2. **Header Files (.h files)**: These files typically contain function prototypes, type definitions, constants, and so forth, which are used in .c files. If a header file is included in a .c file and the header file changes, then the .c file needs to be recompiled, producing a new .o file. For instance, if file1.c includes header1.h and header1.h is modified, file1.c needs to be recompiled into file1.o, even if file1.c itself hasn't changed.
3. **Library Files (.a or .so files for static and dynamic libraries respectively)**: If an object file uses functions or variables from a library, then it depends on that library. In the case of static libraries, if the library changes (because new versions of the .o files it contains were compiled), the final program needs to be relinked. For dynamic libraries, as the linking happens at runtime, the new library will be used next time the program runs without need for recompilation or relinking.
