# High Level Programming Language









{% code lineNumbers="true" %}
```c
 int num1 = 8;
 int num2 = 5;
 int result = num1 + num2;
```
{% endcode %}







Executable files, which contain the binary code for a program, have a specific format that distinguishes them from other types of files. The precise format can depend on the operating system and the architecture of the machine, but most executable file formats include a header section that provides metadata about the file.

This header contains information such as:

* The type of the file (confirming that it is an executable)
* The machine architecture for which the code was compiled (such as x86 or ARM)
* The entry point of the program (where execution should begin)
* The size and location of the code and data sections

The operating system uses this metadata to correctly interpret the binary data in the file. When the OS loads an executable file into memory to run it, it will interpret the binary data in the 'text' or 'code' section of the file as machine instructions according to the instruction set architecture specified in the header. Other sections of the file will be interpreted as data or resources used by the program.

In summary, the operating system knows that the binary data in an executable file represents instructions because the file follows a specific format that tells the OS how to interpret the data. The OS uses this information to load and execute the program correctly.









The portability of a language like C is one of its key features. When we say a language is "portable", we're referring to the ability of programs written in that language to run on different types of computer systems with little or no modification. Here's why C is portable and assembly language like ARMv8 isn't:

**C (High-Level Language)**:

1. **Machine Independence:** C, being a high-level language, is designed to be independent of any particular type of machine or processor architecture. A program written in C can theoretically be run on any machine, provided there is a compiler available for that machine. The compiler is responsible for translating the high-level C code into machine code that is specific to the target hardware.
2. **Standardization:** C has a standard (the ISO C standard), which sets out the rules for how C programs should behave. Any compliant C compiler should produce executable code that behaves as defined by this standard, regardless of the specific hardware.

**ARMv8 Assembly (Low-Level Language)**:

1. **Machine Dependence:** Assembly languages are low-level and are designed for a specific type of processor or family of processors. ARMv8 assembly, for example, is specific to the ARMv8 family of processors. If you have a program written in ARMv8 assembly, it can only be directly run on ARMv8 processors.
2. **No Standardization:** Each type of processor has its own assembly language, with its own set of instructions. The same program will need to be rewritten in different assembly languages to run on different types of processors.

So, the main reason C is portable and ARMv8 assembly isn't is that C abstracts away the details of the machine, while assembly languages expose them. This abstraction is a double-edged sword, though: while it makes C more portable, it also means that C programs may not be able to take full advantage of all features of a particular machine, or to optimize performance as finely as an assembly program might. But in most cases, the portability and productivity gains of using a high-level language like C outweigh these disadvantages.
