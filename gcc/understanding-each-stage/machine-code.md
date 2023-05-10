# Machine Code

Computers do not understand high-level programming languages such as C, Java, or any others. While these languages are more convenient for human comprehension, they are not directly executable by computers. Computer hardware is designed to implement a simple set of instructions, such as loading a value from memory into a register or adding two numbers and storing the result.

The specific set of instructions a computer can support is defined by its Instruction Set Architecture (ISA). An ISA is a specification that outlines the supported instructions, registers, memory organization, and addressing modes that a computer's processor can execute. The ISA serves as the lowest-level software interface to the computer. All instructions must ultimately be translated into this form, as the computer cannot understand anything else.

An instruction is a command that directs the processor to perform a specific operation. Each instruction typically consists of an operation code (opcode) and operands. The opcode identifies the operation to be performed, while the operands provide the necessary data or memory addresses involved in the operation. Some ISAs use fixed-length instructions, with each instruction having the same number of bits, while others use variable-length instructions, where the number of bits can vary between instructions.

### Programming in Machine Code: An Example

To demonstrate what programming in machine code is like, we will write a simple machine code program using the fictional TOY ISA from COS126. Although TOY is not a real computer, it serves as a legitimate example for understanding machine code.

1. TOY has 16 registers&#x20;
2. TOY has 256 memory locations
3. TOY has 16 opcodes

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

* Not human readable:
* Not portable:
* Time-consuming development:
* Lack of abstraction:

Typing 1s and 0s is undoubtedly cumbersome, but the primary issue lies not in the binary representation but in the lack of structure and human readability. The 1s and 0s can be converted to hexadecimal, as shown below and as is done in COS126, which makes the code more accessible, but it still lacks the structure and readability offered by high-level programming languages.

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

