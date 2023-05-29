# Assembly

To make programming easier, programmers long ago developed assembly, which is basically replaces&#x20;

For example, let's consider the TOY Opcodes.&#x20;

| Instruction        | Opcode (Machine code) | Mnemonic (Assembly) |
| ------------------ | --------------------- | ------------------- |
| halt               | 0000                  | hlt                 |
| add                | 0001                  | add                 |
| subtract           | 0010                  | sub                 |
| and                | 0011                  | and                 |
| xor (exclusive OR) | 0100                  | xor                 |
| left shift         | 0101                  | lsh                 |
| right shift        | 0110                  | rsh                 |
| load address       | 0111                  | lad                 |
| load               | 1000                  | load                |
| store              | 1001                  | str                 |
| load indirect      | 1010                  | ldi                 |
| store indirect     | 1011                  | sti                 |
| branch zero        | 1100                  | brz                 |
| branch positive    | 1101                  | brp                 |
| jump register      | 1110                  | jmpr                |
| jump and link      | 1111                  | jal                 |



Registers:

* Instead of referring to the binary representations of registers (0000 to 1111), we can use the notation r0 to r15.&#x20;

Memory:

* Similar to the registers, instead of referring to memory addresses with binary representations (00000000 to 11111111), we can use the notation m0 to m255.&#x20;
* stdin: read
* stdout: write

Here's how the earlier program would look using this notation:



Labels are another useful feature of assembly language, providing a more human-readable way of referring to memory addresses and simplifying the process of writing and maintaining assembly code. Labels are especially helpful for branching, looping, or other control structures that require jumps to different code parts.



Assembly languages offer many other features, such assembler directives, which are commands or instructions that guide the assembler during the assembly process. Assembler directives perform various tasks, such as defining constants, reserving memory space, specifying memory address origins, defining data elements, and controlling the assembly process.



## Drawbacks of Assembly

* Platform-dependant: Assembly language is specific to a computer's Instruction Set Architecture (ISA)
* Longer to write: more time-consuming and labor-intensive than using high-level languages, which offer more abstract and simplified syntax, built-in functions, libraries, and data structures

















To address the challenges associated with machine code, a layer of abstraction was introduced in the form of assembly language. Assembly language serves as a bridge between high-level programming languages and machine code, offering a more human-readable way to write low-level code while still providing close control over the hardware.

1. **Human Readability:** Unlike machine code, which consists purely of binary or hexadecimal numbers, assembly language uses mnemonic codes to represent instructions. These mnemonics are text-based abbreviations of the instruction's function, such as 'ADD' for addition or 'MOV' for moving data. This makes it much easier to understand what each instruction is doing, improving readability.
2. **Named Variables:** Assembly language also allows the use of symbolic names for memory locations, which can be used like variables in high-level languages. This eliminates the need to manually track and manage specific memory addresses, reducing the cognitive load on the programmer.
3. **Structural Constructs:** While still not as high-level as languages like C or Python, assembly languages typically offer simple structural constructs like labels for branching and looping, providing some degree of the control flow that programmers are accustomed to.
4. **Portability:** Assembly is a low-level language and thus not inherently portable between different processor architectures. However, the process of translating assembly to machine code is handled by an assembler, which could potentially be designed to output machine code for different architectures from the same assembly source code, improving portability.

In essence, assembly language allows programmers to write code that closely resembles machine code in terms of performance and control over the hardware, but with the benefits of increased readability and manageability. It also lays the groundwork for higher-level languages, which further improve on these aspects.









Beyond the features already discussed, assembly languages provide a range of additional features to aid in program development:

1. **Assembler Directives:** Assembler directives (also known as pseudo-operations or pseudo-ops) are instructions that control the operation of the assembler itself. They aren't translated into machine code, but instead, they instruct the assembler to perform a specific action. Examples include defining constants or reserved memory spaces, including other source files, or specifying the starting address for the program.
2. **Macros:** Some assembly languages support macros, which are essentially reusable pieces of code. They allow you to define a sequence of instructions that you can call multiple times throughout your program, like a function in a higher-level language. This can significantly reduce code duplication and make your assembly programs easier to write and maintain.
3. **Conditional Assembly:** This feature allows certain parts of the source code to be assembled based on certain conditions. This can be useful for creating different versions of a program, for example, for debugging or for different hardware configurations.
4. **Comments:** Assembly languages allow programmers to add comments to their code. Comments are ignored by the assembler and do not result in any machine code. However, they are invaluable for explaining the purpose and functionality of the code to others reading it, or to the programmers themselves at a later date.
5. **Symbolic References:** As previously mentioned, assembly language allows programmers to use symbolic references in place of hard-coded memory addresses. This applies not only to variables but also to labels for instructions, such as the target of a jump or branch instruction.
6. **Data Directives:** Assembly language also allows for the declaration of static data regions in the program. This could be for simple values or complex structures, like arrays and records. By using data directives, assembly programmers can allocate and initialize memory at compile-time.
7. **Linking and Libraries:** Assembly languages support the use of external libraries and the linking of multiple source files. This means you can write a piece of code once, compile it, and then reuse that code in multiple programs without having to rewrite or recompile it.

While assembly language does not have the high-level constructs and abstractions found in languages like C++ or Python, these features make assembly programming more manageable, while still offering the hardware control and efficiency of machine code.
