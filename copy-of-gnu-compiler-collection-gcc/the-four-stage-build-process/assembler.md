# Assembler

**3. Assembly**

Following compilation, the assembly process commences. The assembly language code, derived from `intmath.c`, is converted into machine code, also known as object code. This code is a binary representation tailored to the processor type that will execute the program, comprising the instructions that the computer will directly execute.



* The assembler is invoked to translate the assembly language into an object file. This file is not in an executable format—it contains executable object code, but not in a form that it can actually be run. Besides, it more than likely contains unresolved references to routines and data in other modules.
* The linker combines object files from the assembler (some of which may be stored in libraries filled with object files) into an executable program.
