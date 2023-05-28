# The Four Stage Build Process

## Preprocessing

```bash
gcc217 -E hello.c > hello.i
```

This command preprocesses the C source file "hello.c" and creates an intermediate preprocessed file "hello.i". Preprocessing involves handling directives such as #include, #define, and #ifdef, expanding macros, and performing other tasks before actual compilation.

## Compiling

```bash
gcc217 -S hello.i
```

This command compiles the preprocessed file "hello.i" into an assembly code file "hello.s". The compilation step translates the C code into a low-level assembly language specific to the target architecture.

## Assembling

```bash
gcc217 -c hello.s
```

This command assembles the assembly code file "hello.s" into an object file "hello.o". The assembler converts the assembly language instructions into machine code (binary format) and generates an object file, which contains the machine code representation of the program.

## Linking

```bash
gcc217 hello.o -o hello
```

This command links the object file "hello.o" and creates the final executable named "hello". The linker combines the object files and resolves any external references to libraries or other object files, generating a single executable file that can be run on the target system.

\
