# Machine Code

We just discussed how computers interpret various data like integers and text. However, the power of a computer lies primarily not in its ability to interpret data but to execute programs.&#x20;

A program is a sequence of instructions that directs the computer to perform specific operations. Like all other types of data in a computer, these instructions are represented in binary. Unlike data, which is passively stored and interpreted, instructions are active, instructing a computer to complete a task. For instance, one instruction may tell the processor to add two numbers, while another might tell it to move data from one place to another.

### Machine Code Instruction

Each machine code instruction consists of two main parts: an opcode and operand(s).

* The opcode, or operation code, is the portion of the instruction that specifies the operation to be performed. This could be any basic operation that the CPU is capable of performing, such as addition, subtraction, multiplication, loading data from memory, storing data into memory, and so on.
* The operand(s) are the data or parameters the operation should act upon. These could represent specific values, or they could represent addresses in memory where values are stored.

To provide an example, consider a fictional machine code instruction like `1010 0110 1111`. Here, `1010` is the opcode, signifying an operation like "ADD". The remaining part `0110 1111` could be the operand(s), which in this case might represent two memory addresses where the numbers to be added are stored. The exact interpretation of opcodes and operands will depend on the specific instruction set architecture (ISA) of the CPU.

**Instruction Set Architecture (ISA):**

The collection of all possible instructions a given processor can execute is defined by the Instruction Set Architecture (ISA). The ISA serves as a manual for the processor, outlining how instructions are encoded in binary, how they are executed, and what effects they have on the processor's state.

An ISA includes specifications for:

* The size and format of individual instructions
* The size of main memory
* The number of registers
* The data types supported
* The instruction set itself (the set of all operations that the processor can perform)

While the ISA lays out what instructions should be available and how they should work, it does not dictate how these instructions are to be implemented in a physical processor. This separation allows different manufacturers to produce CPUs that are compatible with an ISA architecture, but which may have completely different internal designs

### Example of ISA: TOY

The _instruction set architecture_ (ISA) is the interface between the TOY programming language and the physical hardware that executes the program. The ISA specifies the size of main memory, number of registers, and number of bits per instruction. It also specifies exactly which instructions the machine is capable of performing and how each of the instruction bits is interpreted.



The TOY ISA. The TOY machine has 256 words of main memory, 16 registers, and 16-bit instructions. There are 16 different instruction types; each one is designated by one of the _opcodes_ 0 through F. Each instruction manipulates the contents of memory, registers, or the program counter in a completely specified manner. The 16 TOY instructions are organized into three categories: arithmetic-logic, transfer between memory and registers, and flow control. The table below gives a brief summary. (Here is a text version of the [TOY cheatsheet](https://introcs.cs.princeton.edu/java/62toy/cheatsheet.txt).) We describe them in more detail later.



Each TOY instruction consists of 4 hex digits (16 bits). The leading (left-most) hex digit encodes one of the 16 opcodes. The second (from the left) hex digit refers to one of the 16 registers, which we call the _destination register_ and denote by d. The interpretation of the two rightmost hex digits depends on the opcode. With _Format 1_ opcodes, the third and fourth hex digits are each interpreted as the index of a register, which we call the two _source registers_ and denote by s and t. For example, the instruction 1462 adds the contents of registers s = 6 and t = 2 and puts the result into register d = 4. With _Format 2_ opcodes, the third and fourth hex digits (the rightmost 8 bits) are interpreted as a memory address, which we denote by addr. For example, the instruction 9462 stores the contents of register d = 4 into memory location addr = 62. Note that there is no ambiguity between Format 1 and Format 2 instruction since each opcode has a unique format.



1. TOY has 16 registers, each 16 bits. Registers. The TOY machine has 16 _registers_, indexed from 0 through F. Registers are much like main memory: each register stores one 16-bit word. However, registers provide a faster form of storage than main memory. Registers are used as scratch space during computation and play the role of variables in the TOY language. Register 0 is a special register whose output value is always 0.
2. Main memory. The TOY machine has 256 words of _main memory_. Each memory location is labeled with a unique _memory address_. By convention, we use the 256 hexadecimal integers in the range 00 through FF. Think of a memory location as a mailbox, and a memory address as a postal address. Main memory is used to store instructions and data. TOY has 256 memory locations, each 16-bit
3. TOY has 16 opcodes, each 4 bits
4. TOY has two types of instruction formats&#x20;
5.

```
Register 0 always reads 0.
Loads from mem[FF] come from stdin.
Stores to mem[FF] go to stdout.
```

In TOY, each instruction is 16 bits long, with the first four bits representing the opcode and the remaining 12 representing the operands.&#x20;





Each instruction consists of 16 bits.&#x20;

&#x20;Bits 12-15 encode one of 16 instruction types or opcodes.&#x20;

&#x20;Bits 8-11 encode destination register d. &#x20;

Bits 0-7 encode: \[Format 1] source registers s and t&#x20;

\[Format 2] 8-bit memory address or constant



<figure><img src="../.gitbook/assets/Screenshot 2023-05-28 at 12.35.09 PM.png" alt=""><figcaption></figcaption></figure>





<table><thead><tr><th>OPCODE (Binary)</th><th width="236">DESCRIPTION</th><th>FORMAT</th></tr></thead><tbody><tr><td>0000</td><td>halt</td><td>-</td></tr><tr><td>0001</td><td>add</td><td>1</td></tr><tr><td>0010</td><td>subtract</td><td>1</td></tr><tr><td>0011</td><td>and</td><td>1</td></tr><tr><td>0100</td><td>xor</td><td>1</td></tr><tr><td>0101</td><td>left shift</td><td>1</td></tr><tr><td>0110</td><td>right shift</td><td>1</td></tr><tr><td>0111</td><td>load address</td><td>2</td></tr><tr><td>1000</td><td>load</td><td>2</td></tr><tr><td>1001</td><td>store</td><td>2</td></tr><tr><td>1010</td><td>load indirect</td><td>1</td></tr><tr><td>1011</td><td>store indirect</td><td>1</td></tr><tr><td>1100</td><td>branch zero</td><td>2</td></tr><tr><td>1101</td><td>branch positive</td><td>2</td></tr><tr><td>1110</td><td>jump register</td><td>-</td></tr><tr><td>1111</td><td>jump and link</td><td>2</td></tr></tbody></table>





### Programming in Machine Code: An Example

\
As you can imagine, writing programs directly in machine code is incredibly difficult. To demonstrate why this is so, we will write a simple machine code program using the fictional TOY ISA, introduced in COS126.&#x20;

Let's consider a toy program that takes two integer inputs from stdin, calculates their sum, and writes the result on stdout.

{% code overflow="wrap" %}
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

Even though writing machine code in hexadecimal is slightly more digestible than binary, the underlying challenge remains: it's a flat sequence of numbers without any meaningful structure or descriptive identifiers, making it hard to understand what each part of the code is doing.





## Drawbacks of Machine Code

#### PORTABILITY

Another significant issue with machine code is its lack of portability. Portability, in this context, refers to the ability of a program to be executed on different types of systems without requiring modification.

Machine code lacks portability. Machine code is designed for a specific processor architecture, and it directly uses the instructions defined by that processor's ISA. For example, machine code written for a TOY machine would be different from that written for an ARM processor or an x86 processor, even if they were intended to perform the same task.&#x20;

If you write a program in machine code for one type of processor, it won't run on a different type of processor. You would have to rewrite the program using the different processor's machine language, which is a labor-intensive and error-prone process.

<details>

<summary>Aside: RISC vs. CISC</summary>

Instruction set architectures fall into one of two main categories: Reduced Instruction Set Computing (RISC) and Complex Instruction Set Computing (CISC).

RISC architectures, such as ARM, aim to simplify the set of possible instructions, enabling faster execution and reducing the complexity of the CPU. They rely on a philosophy of executing a single operation on each clock cycle, which makes them efficient and power-saving.

On the other hand, CISC architectures, like x86, contain a large number of complex instructions. This complexity can lead to increased functionality per instruction at the expense of slower clock speeds and higher power consumption

</details>
