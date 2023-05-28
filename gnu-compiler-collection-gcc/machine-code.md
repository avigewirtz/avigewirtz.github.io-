# Machine Code

A program is a sequence of instructions that directs the computer to perform specific operations. Like all other types of data in a computer, these instructions are represented in binary. Unlike data, which is passively stored and interpreted, instructions are active, instructing a computer to complete a task. For instance, one instruction may tell the processor to add two numbers, while another might tell it to move data from one place to another.

### Instructions

Each machine code instruction consists of two main parts: an opcode and operand(s).

* The opcode, or operation code, is the portion of the instruction that specifies the operation to be performed. This could be any basic operation that the CPU is capable of performing, such as addition, subtraction, multiplication, loading data from memory, storing data into memory, and so on.
* The operand(s) are the data or parameters the operation should act upon. These could represent specific values, or they could represent addresses in memory where values are stored.

To provide an example, consider a simplified machine code instruction like `1010 0110 1111`. Here, `1010` could be the opcode, signifying an operation like "ADD". The remaining part `0110 1111` could be the operand(s), which in this case might represent two memory addresses where the numbers to be added are stored. The exact interpretation of opcodes and operands will depend on the specific instruction set architecture (ISA) of the CPU.

**Instruction Set Architecture (ISA):**

The collection of all possible instructions a given processor can execute is defined by the Instruction Set Architecture (ISA). The ISA serves as a manual for the processor, outlining how instructions are encoded in binary, how they are executed, and what effects they have on the processor's state.

An ISA includes specifications for:

* The format of individual instructions
* The processor's memory model
* The processor's register set
* The addressing modes
* The data types supported
* The instruction set itself (the set of all operations that the processor can perform)

While the ISA lays out what instructions should be available and how they should work, it does not dictate how these instructions are to be implemented in a physical processor. This separation allows different manufacturers to produce CPUs that are compatible with an ISA architecture, but which may have completely different internal designs

<details>

<summary>Aside: RISC vs. CISC</summary>

Instruction set architectures fall into one of two main categories: Reduced Instruction Set Computing (RISC) and Complex Instruction Set Computing (CISC).

RISC architectures, such as ARM, aim to simplify the set of possible instructions, enabling faster execution and reducing the complexity of the CPU. They rely on a philosophy of executing a single operation on each clock cycle, which makes them efficient and power-saving.

On the other hand, CISC architectures, like x86, contain a large number of complex instructions. This complexity can lead to increased functionality per instruction at the expense of slower clock speeds and higher power consumption

</details>

### Programming in Machine Code: An Example

As you can imagine, writing programs directly in machine code is incredibly difficult. To demonstrate why this is so, we will write a simple machine code program using the fictional TOY ISA, introduced in COS126.&#x20;

Recall that TOY:

1. TOY has 16 registers&#x20;
2. TOY has 256 memory locations
3. TOY has 16 opcodes

```
Register 0 always reads 0.
Loads from mem[FF] come from stdin.
Stores to mem[FF] go to stdout.
```

In TOY, each instruction is 16 bits long, with the first four bits representing the opcode and the remaining 12 representing the operands.&#x20;



| Format 1 | . . . . | . . . . | . . . . |
| -------- | ------- | ------- | ------- |
| opcode   | d       | s       | t       |



<table data-full-width="false"><thead><tr><th>Format 2</th><th>. . . .</th><th>. . . .</th></tr></thead><tbody><tr><td>opcode</td><td>d</td><td>addr</td></tr></tbody></table>





<table><thead><tr><th>OPCODE (Binary)</th><th width="236">DESCRIPTION</th><th>FORMAT</th></tr></thead><tbody><tr><td>0000</td><td>halt</td><td>-</td></tr><tr><td>0001</td><td>add</td><td>1</td></tr><tr><td>0010</td><td>subtract</td><td>1</td></tr><tr><td>0011</td><td>and</td><td>1</td></tr><tr><td>0100</td><td>xor</td><td>1</td></tr><tr><td>0101</td><td>left shift</td><td>1</td></tr><tr><td>0110</td><td>right shift</td><td>1</td></tr><tr><td>0111</td><td>load address</td><td>2</td></tr><tr><td>1000</td><td>load</td><td>2</td></tr><tr><td>1001</td><td>store</td><td>2</td></tr><tr><td>1010</td><td>load indirect</td><td>1</td></tr><tr><td>1011</td><td>store indirect</td><td>1</td></tr><tr><td>1100</td><td>branch zero</td><td>2</td></tr><tr><td>1101</td><td>branch positive</td><td>2</td></tr><tr><td>1110</td><td>jump register</td><td>-</td></tr><tr><td>1111</td><td>jump and link</td><td>2</td></tr></tbody></table>







Let's consider a toy program that takes two integer inputs from stdin, calculates their sum, and writes the result on stdout.

{% code overflow="wrap" %}
```java



1000 1010 1111 1111 // Read byte from memory address 255 (stdin) and store it in register 10
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
{% endcode %}



Typing 1s and 0s is undoubtedly cumbersome, so an improvement we can do is to instead code in hexadecimal:

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

and the hex will undoubtedly exist in binary.

Even though machine code written in hexadecimal is slightly more digestible than binary, the underlying challenge remains: it's a flat sequence of numbers without any meaningful structure or descriptive identifiers. The instructions, addresses, and data are all represented as numbers, making it hard to understand what each part of the code is doing.

Machine language, including TOY, doesn't have any of these features. There are no named variables or functions; instead, you have to manually manage registers and memory locations.



## Drawbacks of Machine Code







#### PORTABILITY







Another significant issue with machine code is its lack of portability. Portability, in this context, refers to the ability of a program to be executed on different types of systems without requiring modification.



Machine code lacks portability. Machine code is designed for a specific processor architecture, and it directly uses the instructions defined by that processor's ISA. For example, machine code written for a TOY machine would be different from that written for an ARM processor or an x86 processor, even if they were intended to perform the same task.&#x20;

If you write a program in machine code for one type of processor, it won't run on a different type of processor. You would have to rewrite the program using the different processor's machine language, which is a labor-intensive and error-prone process.

\
