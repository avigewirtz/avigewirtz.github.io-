# Machine Code

We began by discussing how computers interpret data, like integers and text. But the power of a computer primarily lies in its ability to execute programs, which are sequences of instructions that direct the computer to perform specific operations. For instance, one instruction might tell the processor to add two numbers, while another directs it to move data from one place to another. These instructions, like all other types of data in a computer, are represented in binary.

#### Format of an instruction

Each machine code instruction consists of an operation code (opcode) and operand(s). The opcode specifies the operation to be performed, such as addition, subtraction, or loading data from memory. The operand(s) are the data or parameters the operation should act upon.&#x20;

For example, a machine code instruction might look like this:

1010 0110 1111&#x20;

Where 1010 is the opcode (signifying "ADD") and 0110 1111 is the operands (representing memory addresses where numbers to be added are stored).

## Instruction Set Architecture

The set of all possible instructions a processor can execute is defined by the Instruction Set Architecture (ISA). It serves as the interface between the TOY programming language and the hardware that executes the program. The ISA outlines how instructions are encoded in binary, executed, and their effects on the processor's state. It also specifies the size and format of instructions, main memory and registers, the supported data types, and the instruction set itself. However, it does not dictate how these instructions are implemented in a physical processor.

## Machine Code example:

It's difficult to demonstrate what machine code is truly like without an example of a machine code program. However, modern machine code languages, such as ARM and X86, are so complex, that it would be unrealistic to write a self-contained program. As such, we will demonstrate machine code by using the TOY computer introduced in COS126. While TOY is a fictional computer, it is very similar to computers that existed when programmers programmed in machine code.&#x20;

Let's review the TOY ISA. It specifies all the details a programmer would need to know to write programs in TOY machine code.&#x20;

The TOY machine consists of:

* 256 addresses, each containing 16 bits
* 16 registers, each 16 bits
* 16 instructions, each 16 bits&#x20;
* Instructions can be in 2 formats, as shown below. The leftmost 4 bits always represent the opcode.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-05-28 at 12.35.09 PM.png" alt=""><figcaption></figcaption></figure>



For the following program, we will assume it is already loaded into memory, and the first instruction starts at address 10. &#x20;



<table><thead><tr><th width="183">Memory Address</th><th width="223">Instruction/Data (Binary)</th><th>Description</th></tr></thead><tbody><tr><td>10</td><td>1000101000010101</td><td>Load the value from memory address 15 into register 10.</td></tr><tr><td>11</td><td>1000101100010110</td><td>Load the value from memory address 16 into register 11.</td></tr><tr><td>12</td><td>0001110010101011</td><td>Add the contents of registers 10 and 11, storing the result in register 12.</td></tr><tr><td>13</td><td>1001110000010111</td><td>Store the result from register 12 into memory address 17.</td></tr><tr><td>14</td><td>0000000000000000</td><td>This is a halt instruction. It stops the execution of the program.</td></tr><tr><td>15</td><td>0000000000001000</td><td>Memory address 15 contains the value 0008.</td></tr><tr><td>16</td><td>0000000000000110</td><td>Memory address 16 contains the value 0005.</td></tr><tr><td>17</td><td>0000000000000000</td><td>Memory address 17 initially contains the value 0000 and will be used to store the result.</td></tr></tbody></table>



So, this program loads the values from memory addresses 15 and 16 into registers 10 and 11, adds these values together, stores the result in memory address 17, and then halts. Given the provided memory values, this program will effectively add 8 and 5, storing the result (13) in memory address 17.

## Observations

* It's not human readable, meaning that it's not descriptive
* Many lines of code to perform a simple task
* Code is tedious to write&#x20;
* very few instructions
* very simple instructions
* no high level constructs such as loops
* have to combine to do anything useful
* have to be hardcode memory and register addresses, requiring us to be intimately familiar with hardware
*



It should be noted that we can improve machine code wiritng by for example using hex instead of binary. so, for example, instead of typing out 1000 1010 1111 1111, we type 8AFF. In fact, this is how programming in TOY was in COS126.&#x20;

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

However, while hexadecimal might be slightly more digestible and easier to code than binary, the underlying challenge remains: it's a flat sequence of numbers without any meaningful structure or descriptive identifiers, making it hard to understand what each part of the code is doing.

Another significant issue with machine code is its lack of portability. Portability, in this context, refers to the ability of a program to be executed on different types of systems without requiring modification.

Machine code lacks portability. Machine code is designed for a specific processor architecture, and it directly uses the instructions defined by that processor's ISA. For example, machine code written for a TOY machine would be different from that written for an ARM processor or an x86 processor, even if they were intended to perform the same task.&#x20;

If you write a program in machine code for one type of processor, it won't run on a different type of processor. You would have to rewrite the program using the different processor's machine language, which is a labor-intensive and error-prone process.

<details>

<summary>Aside: RISC vs. CISC</summary>

Instruction set architectures fall into one of two main categories: Reduced Instruction Set Computing (RISC) and Complex Instruction Set Computing (CISC).

RISC architectures, such as ARM, aim to simplify the set of possible instructions, enabling faster execution and reducing the complexity of the CPU. They rely on a philosophy of executing a single operation on each clock cycle, which makes them efficient and power-saving.

On the other hand, CISC architectures, like x86, contain a large number of complex instructions. This complexity can lead to increased functionality per instruction at the expense of slower clock speeds and higher power consumption

</details>
