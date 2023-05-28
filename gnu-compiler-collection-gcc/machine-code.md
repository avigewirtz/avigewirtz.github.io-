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





<figure><img src="../.gitbook/assets/Screenshot 2023-05-28 at 12.35.09 PM.png" alt=""><figcaption></figcaption></figure>



suppose you have some way of feeding these intruction in one-by-one. we will not concern ourselves with how this is done.

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

## Observations

* It's not human readable, meaning that it's not descriptive
* Many lines of code to perform a simple task
* Code is tedious to write&#x20;
* very few instrcutions
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

Even though hexadecimal might be slightly more digestible and easier to code than binary, the underlying challenge remains: it's a flat sequence of numbers without any meaningful structure or descriptive identifiers, making it hard to understand what each part of the code is doing.

Another significant issue with machine code is its lack of portability. Portability, in this context, refers to the ability of a program to be executed on different types of systems without requiring modification.

Machine code lacks portability. Machine code is designed for a specific processor architecture, and it directly uses the instructions defined by that processor's ISA. For example, machine code written for a TOY machine would be different from that written for an ARM processor or an x86 processor, even if they were intended to perform the same task.&#x20;

If you write a program in machine code for one type of processor, it won't run on a different type of processor. You would have to rewrite the program using the different processor's machine language, which is a labor-intensive and error-prone process.

<details>

<summary>Aside: RISC vs. CISC</summary>

Instruction set architectures fall into one of two main categories: Reduced Instruction Set Computing (RISC) and Complex Instruction Set Computing (CISC).

RISC architectures, such as ARM, aim to simplify the set of possible instructions, enabling faster execution and reducing the complexity of the CPU. They rely on a philosophy of executing a single operation on each clock cycle, which makes them efficient and power-saving.

On the other hand, CISC architectures, like x86, contain a large number of complex instructions. This complexity can lead to increased functionality per instruction at the expense of slower clock speeds and higher power consumption

</details>
