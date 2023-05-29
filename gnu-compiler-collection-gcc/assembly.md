# Assembly

To make programming easier, programmers long ago developed assembly. \<explain how assembly makes coding easier by using mnemonics instead of numbers, etc. demonstrate this with a couple simple examples. Then explain how we might design an assembly language for TOY. For example, we could use the following mnemonics instead of the opcodes.&#x20;

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





Here's how the earlier program would look using this notation. in our assembly language, you replace the TOY binary opcodes with: 0000 -> hlt 0001 -> add 0010 -> sub 0011 -> and 0100 -> xor 0101 -> lsh 0110 -> rsh 0111 -> lad 1000 -> lod 1001 -> str 1010 -> ldi 1011 -> sti 1100 -> brz 1101 -> brp 1110 -> jmpr 1111 -> jal













recall in our last program how we reffered to registers using 8 bits and memory addresseses using 16 bits. we could instead use the following:

Registers:

* Instead of referring to the binary representations of registers (0000 to 1111), we can use the notation r0 to r15.&#x20;

Memory:

* Similar to the registers, instead of referring to memory addresses with binary representations (00000000 to 11111111), we can use the notation m0 to m255.&#x20;

Here's how the earlier program would look using this notation:

```
Address | instruction 
-----------------------------
10:     |  lod r10 m255   
11:     |  lod r11 m255        
12:     |  lad r12, 0     
13:     |  lad r1, 1   
14:     |  brz r10, m18   
15:     |  add r12, r12, r11
16:     |  sub r10, r10, r1 
17:     |  jmpr m14       
18:     |  str r12 m255   
19:     |  hlt     
-----------------------------
```



This program is clearly much easier to read and write. \<ELABORATE>. Of course, it must ultimately be translated into machine code. That is done via a program known as an assembler. So called because it takes assembly and translates it into machine code.&#x20;





In fact, we can do even better. We can use&#x20;

* rd for all stdin&#x20;
* wrt for stdout

Additionally, we can add labels instead of hardcoding memory addresses. \<EXPLAIN LABELS>

Now, we don't have to worry about memory addresses

of course, the program will ultimately have to be in binary to be executed. For that, we design a program known as an assembler.&#x20;



```
START: rd r10        
rd r11        
lad r12, 0     
lad r1, 1   
LOOP: brz r10, END  
add r12, r12, r11
sub r10, r10, r1 
jmpr LOOP       
END: wrt r12       
hlt     

```





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
