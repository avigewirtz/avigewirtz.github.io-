# Machine Code

We began by discussing how computers interpret data, like integers and text. But the power of a computer primarily lies in its ability to execute programs, which are sequences of instructions that direct specific operations. These instructions, represented in binary like all data in a computer, are active; they direct the computer to complete tasks. For instance, one instruction might tell the processor to add two numbers, while another directs it to move data from one place to another.

Each machine code instruction consists of an opcode and operand(s). The opcode, or operation code, specifies the operation to be performed, such as addition, subtraction, or loading data from memory. The operand(s) are the data or parameters the operation should act upon. For example, a fictional machine code instruction like 1010 0110 1111 might have 1010 as the opcode (signifying "ADD") and 0110 1111 as the operands (representing memory addresses where numbers to be added are stored).

The set of all possible instructions a processor can execute is defined by the Instruction Set Architecture (ISA). The ISA outlines how instructions are encoded in binary, executed, and their effects on the processor's state. It also specifies the size and format of instructions, main memory and registers, the supported data types, and the instruction set itself. However, it does not dictate how these instructions are implemented in a physical processor.

Take the TOY Instruction Set Architecture (ISA) as an example. It serves as the interface between the TOY programming language and the hardware that executes the program, specifying details such as the size of main memory (256 words), number of registers (16), and bits per instruction (16). It also lists the 16 unique instruction types, each designated by an opcode from 0 through F.

Each TOY instruction is encoded with 4 hex digits (16 bits): the leftmost hex digit encodes one of the 16 opcodes, the second encodes the destination register (denoted as d), and the interpretation of the two rightmost hex digits depends on the opcode. In Format 1 opcodes, these represent source registers (denoted as s and t). In Format 2 opcodes, they represent an 8-bit memory address.

The TOY machine uses registers as scratch space during computation. Register 0 is special, always outputting a value of 0. Main memory is used to store instructions and data, with each memory location labeled with a unique address. Certain special behaviors apply, like loads from memory address FF coming from stdin, and stores to this address going to stdout.



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
