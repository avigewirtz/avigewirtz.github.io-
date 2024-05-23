# Compiler and Assembler

Often, the easiest way to understand the role of software is to explore what development was like before it existed. Back in the day, there was no preprocessor, compiler, assembler, or linker. All coding was done in machine code--a binary language comprised of 0s and 1s. We'll build our way up.&#x20;

### Machine Language

* Each CPU has a set of instructions it supports. These instructions are known as machine code. There is no hard set rule for what machine code is, since each manufacturer designs their own machine code for their device. In general, however, the following two characteristics of machine code are universal to all modern computers:
  * Binary language consisting of 1s and 0s.&#x20;
  * Very primitive instructions, rarely more complex than adding two numbers and transferring data from one memory location to another&#x20;

A processor’s control unit has a format it expects each such instruction to be in: typically a instruction will be a set length, say 16 or 32 or 64 bits and the first few bits will specify what kind of instruction it is. These first few bits, known as the **opcode** (operation code), say what general task is to be done - something like “store a number” or “add two numbers”. The rest of the instruction will contain **operands**, the extra information needed to understand the instruction - things like where to store the number or which two numbers to add.



{% hint style="info" %}
Theres no law that mandates that machine code use a binary system. In fact, computers existed that used a decimal system. In practice, however, binary has proven to be the most efficient system, and thus all modern computers use it.&#x20;
{% endhint %}

{% hint style="info" %}
**Microcode**

Machine code is by definition the lowest level of programming detail visible to the programmer, but internally many processors use [microcode](https://en.wikipedia.org/wiki/Microcode) or optimize and transform machine code instructions into sequences of [micro-ops](https://en.wikipedia.org/wiki/Micro-operation). Microcode and micro-ops are not generally considered to be machine code; except on some machines, the user cannot write microcode or micro-ops, and the operation of microcode and the transformation of machine-code instructions into micro-ops happens transparently to the programmer except for performance related side effects. In some computers, the machine code of the [architecture](https://en.wikipedia.org/wiki/Computer\_architecture) is implemented by an even more fundamental underlying layer called [microcode](https://en.wikipedia.org/wiki/Microcode), providing a common machine language interface across a line or family of different models of computer with widely different underlying [dataflows](https://en.wikipedia.org/wiki/Dataflow).&#x20;
{% endhint %}

hypothetical computer:&#x20;

* 256 memory addresses and 16 general purpose registers. Each holds 16 bits.&#x20;
* Instruction is 16 bits long. First four bits indicate opcode.&#x20;
* suppose our machine is set that whenever it's powered on, it begins execution at address 0.&#x20;
* suppose we want to write sum of the first $$𝑛$$ natural numbers

```asm6502
Address |  Instruction/data 
----------------------------
0:      |  1000000000001000  ; load the value at memory address 8 into register 0.
1:      |  0111000100000000  ; initialize register 1 to 0. This will hold the cumulative sum.
2:      |  0111001000000001  ; initialize register 2 to 1. This is used as a decrement value.
3:      |  0001000100010000  ; add the value of R0 to R1 and store the result back in R1.
4:      |  0010000000000010  ; subtract the value of R2 (which is 1) from R0.
5:      |  1101000000000011  ; branch to the memory address 3 if the result of the previous subtraction (R0) is positive. This means the loop continues as long as R0 is greater than 0.
6:      |  1001000100001001  ; store the value of R1 into the memory address 9.
7:      |  0000000000000000  ; halt execution.
8:      |  0000000000001100  ; integer value 12
9:      |  0000000000000000  ; result will be stored here
----------------------------
```

### Assembly Language&#x20;

While machine language is convenient for computers, it is extremely inconvenient for humans. For one, it's not readable. Opcodes, registers, and memory addresses all written in binary. Second, we reference code by its memory address. Requires a lot of planning to get program to work. And what if you go through all the work and then realize you need to modify your program by adding a few lines, say at memory location 4-6. Now the entire program is broken.&#x20;

```asm6502
Address |  Instruction/data 
----------------------------
0:      |  1000000000001000  ; load the value at memory address 8 into register 0.
1:      |  0111000100000000  ; initialize register 1 to 0. This will hold the cumulative sum.
2:      |  0111001000000001  ; initialize register 2 to 1. This is used as a decrement value.
3:      |  0101010100101011  ; NEW INSTRUCTION
4:      |  1101010101011010  ; NEW INSTRUCTION
5:      |  0010101011100001  ; NEW INSTRUCTION
6:      |  0001000100010000  ; add the value of R0 to R1 and store the result back in R1.
7:      |  0010000000000010  ; subtract the value of R2 (which is 1) from R0.
8:      |  1101000000000011  ; branch to memory address 3 if the result of the previous subtraction (R0) is positive. This means the loop continues as long as R0 is greater than 0.
9:      |  1001000100001001  ; store the value of R1 into the memory address 9.
10:     |  0000000000000000  ; halt execution.
11:     |  0000000000001100  ; integer value 12
12:     |  0000000000000000  ; result 
----------------------------
```

As we can see, machine language programs are incredibly difficult to write and maintain. Assembly is designed to make both of these tasks easier. Instead of writing in binary, we use mnemonics for opcodes. For example, rather than using 1101 to indicate load value from memory into register, we instead use the mnemonic LD. For registers, we refer to them by R1-R16, rather than 0000 to 1111. For memory addresses, we don't refer to them directly at all. Instead, we use labels, which are essentially placeholders for memory addresses that the assembler will fill in.&#x20;

```
        LD R0 N   
        LDB R1 #0      
        LDB R2 #1     
LOOP:   ADD R1 R1 R0   
        SUB R0 R0 R2   
        BRP R0 LOOP
        STR R1 SUM 
        Halt      
N:      12
SUM:
```

To run our program, we write it out like this, then we feed it to the assembler, which converts it into an equivalent machine language version. The precise memory locations wll be filled in my the assembler.&#x20;

This solves the problem of being able to modify a program. Since we're reffering to labels, rather than raw addresses, even if we insert some lines and now LOOP, N, and SUM are all three memory locations further, that does not matter, since the references are to labels, not actual memory locations.&#x20;

```
        LD R0 N   
        LDB R1 #0      
        LDB R2 #1  
        NEW INSTRUCTION
        NEW INSTRUCTION
        NEW INSTRUCTION   
LOOP:   ADD R1 R1 R0   
        SUB R0 R0 R2   
        BRP R0 LOOP
        STR R1 SUM 
        Halt      
N:      12
SUM:
```

### High Level Languages

While assembly language is leaps above machine language, it's still quite inconvinient to code in.&#x20;

* Requires intimate knowledge of processor architecture.&#x20;
* Very simple instructions. Takes many lines to perform simple task.&#x20;
* Not portable.&#x20;
