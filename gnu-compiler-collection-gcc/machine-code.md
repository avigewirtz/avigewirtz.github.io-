# Machine Code

When it comes to programs, binary encoding takes on a new role. Unlike data, which is passively stored and interpreted, programs are active, providing a series of instructions that a computer follows to perform tasks.

**What is a Program?**

A program is a sequence of instructions that directs the computer to perform specific operations. Like all other types of data in a computer, these instructions are represented in binary.

**Instruction Format and Types:**

Each instruction in a program has a specific format that is determined by the processor's design. For instance, one instruction may tell the processor to add two numbers, while another might tell it to move data from one place to another.

**Instruction Set Architecture (ISA):**

The collection of all possible instructions a given processor can execute is defined by the Instruction Set Architecture (ISA). The ISA serves as a manual for the processor, outlining how instructions are encoded in binary, how they are executed, and what effects they have on the processor's state.

An ISA includes specifications for:

* The format of individual instructions
* The processor's memory model
* The processor's register set
* The addressing modes
* The data types supported
* The instruction set itself (the set of all operations that the processor can perform)

<details>

<summary>Aside: RISC vs. CISC</summary>

Instruction set architectures fall into one of two main categories: Reduced Instruction Set Computing (RISC) and Complex Instruction Set Computing (CISC).

RISC architectures, such as ARM, aim to simplify the set of possible instructions, enabling faster execution and reducing the complexity of the CPU. They rely on a philosophy of executing a single operation on each clock cycle, which makes them efficient and power-saving.

On the other hand, CISC architectures, like x86, contain a large number of complex instructions. This complexity can lead to increased functionality per instruction at the expense of slower clock speeds and higher power consumption

</details>







**Family and Behavior:**

ARM is indeed a family of architectures, with each member defining a set of behaviors but not their implementation. This means that the ARM architecture lays out what instructions should be available and how they should work, but it does not dictate how these instructions are to be implemented in a physical processor.

This separation allows different manufacturers to produce CPUs that are compatible with the ARM architecture, but which may have completely different internal designs. For instance, two CPUs might both implement the ARMv8 architecture, but one might be designed for high performance while the other might be designed for low power consumption. This diversity is one of the strengths of the ARM architecture.









Writing programs directly in machine code in today's world would be incredibly inefficient and time-consuming. However, to demonstrate why this is so, we will code a simple program using the TOY ISA, introduced in the COS126 course.





###

### Programming in Machine Code: An Example





| Format 1 | . . . . | . . . . | . . . . |
| -------- | ------- | ------- | ------- |
| opcode   | d       | s       | t       |



<table data-full-width="false"><thead><tr><th>Format 2</th><th>. . . .</th><th>. . . .</th></tr></thead><tbody><tr><td>opcode</td><td>d</td><td>addr</td></tr></tbody></table>





| OPCODE (Binary) | DESCRIPTION     | FORMAT |
| --------------- | --------------- | ------ |
| 0000            | halt            | -      |
| 0001            | add             | 1      |
| 0010            | subtract        | 1      |
| 0011            | and             | 1      |
| 0100            | xor             | 1      |
| 0101            | left shift      | 1      |
| 0110            | right shift     | 1      |
| 0111            | load address    | 2      |
| 1000            | load            | 2      |
| 1001            | store           | 2      |
| 1010            | load indirect   | 1      |
| 1011            | store indirect  | 1      |
| 1100            | branch zero     | 2      |
| 1101            | branch positive | 2      |
| 1110            | jump register   | -      |
| 1111            | jump and link   | 2      |





To demonstrate what programming in machine code is like, we will write a simple machine code program using the fictional TOY ISA from COS126. Although TOY is not a real computer, it serves as a legitimate example for understanding machine code.

1. TOY has 16 registers&#x20;
2. TOY has 256 memory locations
3. TOY has 16 opcodes

```
Register 0 always reads 0.
Loads from mem[FF] come from stdin.
Stores to mem[FF] go to stdout.
```

In TOY, each instruction is 16 bits long, with the first four bits representing the opcode and the remaining 12 representing the operands. A simple TOY program in binary looks like this:

This program takes two integer inputs from stdin, calculates their sum, and writes the result to stdout.

```java
1000 1010 1111 1111 // Read a byte from memory address 255 (stdin) and store it in register 10
1000 1011 1111 1111 // Read a byte from memory address 255 (stdin) and store it in register 11
0111 1100 0000 0000 // Set register 12 to 0
0111 0001 0000 0001 // Set register 1 to 1
1100 1010 0001 1000 // If the value in register 10 equals 0, jump to address 24
0001 1100 1100 1011 // Add the values in registers 11 and 12 and store the result in register 12
0010 1010 1010 0001 // Decrement register 10 by 1 (the value in register 1)
1100 0000 0001 0100 // Jump back to address 14 
1001 1100 1111 1111 // Write the value in register 12 to memory address 255 (stdout)
0000 0000 0000 0000 // Halt the program
```



## Drawbacks of Machine Code



Coding directly in a machine language like TOY is difficult for several reasons, most importantly because it lacks the qualities that make code human-readable.

\


Machine language, including TOY, doesn't have any of these features. There are no named variables or functions; instead, you have to manually manage registers and memory locations.

```
1000 1010 1111 1111 => 8AFF
1000 1011 1111 1111 => 8BFF
0111 1100 0000 0000 => 7C00
0111 0001 0000 0001 => 7101
1100 1010 0001 1000 => CA18
0001 1100 1100 1011 => 1CCB
0010 1010 1010 0001 => 2AA1
1100 0000 0001 0100 => C014
1001 1100 1111 1111 => 9CFF
0000 0000 0000 0000 => 0000
```

\
\
\


Even though machine code could be written in other numeral systems such as hexadecimal to make it slightly more digestible than binary, the underlying challenge remains: it's a flat sequence of numbers without any meaningful structure or descriptive identifiers. The instructions, addresses, and data are all represented as numbers, making it hard to understand what each part of the code is doing.

\
\
\


PORTABILITY

\


Another significant issue with machine code is its lack of portability. Portability, in this context, refers to the ability of a program to be executed on different types of systems without requiring modification.

\


Machine code is designed for a specific processor architecture, and it directly uses the instructions defined by that architecture's Instruction Set Architecture (ISA). For example, machine code written for a TOY machine would be different from that written for an ARM processor or an x86 processor, even if they were intended to perform the same task. This is because each architecture has its unique set of instructions, and instructions can even vary within families of the same architecture, such as different generations of ARM or x86 processors.

\
\


This means that machine code lacks portability. If you write a program in machine code for one type of processor, it won't run on a different type of processor. You would have to rewrite the program using the different processor's machine language, which is a labor-intensive and error-prone process.

\
\


* Not human readable:
* Not portable:
* Time-consuming development:
* Lack of abstraction:

Typing 1s and 0s is undoubtedly cumbersome, but the primary issue lies not in the binary representation but in the lack of structure and human readability. The 1s and 0s can be converted to hexadecimal, as shown below and as is done in COS126, which makes the code more accessible, but it still lacks the structure and readability offered by high-level programming&#x20;
