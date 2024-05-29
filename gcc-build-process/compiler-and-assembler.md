# Compiler and Assembler

### 1. Introduction

Often, the easiest way to understand the role of software is to explore what development was like before it existed. Back in the day, there was no preprocessor, compiler, assembler, or linker. All coding was done in machine code--a binary language comprised of 0s and 1s. We'll build our way up.&#x20;











### 2. Machine Language

Each CPU has a unique set of instructions it can execute, known as machine code. There's no universal standard for machine code, as each manufacturer designs its own for their specific device. However, two fundamental characteristics of machine code are consistent across all modern computers.

First, machine code is a binary language, consisting entirely of 1s and 0s. While there's no inherent requirement for machine code to use a binary system (historically, some computers used decimal systems), binary has proven to be the most efficient, leading to its adoption in all modern computers. Second, instructions in machine code are very basic, rarely exceeding the complexity of adding two numbers or transferring data between memory locations.

A processor's control unit expects each instruction in a specific format, typically a fixed length (e.g., 16, 32, or 64 bits). The first few bits, known as the opcode (operation code), specify the general task to be performed (e.g., "store a number" or "add two numbers"). The remaining bits contain operands, providing the necessary information to interpret the instruction (e.g., where to store the number or which numbers to add).

#### Machine Code Program Example

Imagine a hypothetical computer with&#x20;

* 256 memory addresses and 16 general-purpose registers, each holding 16 bits.&#x20;
* Each instruction is 16 bits long, with the first four bits indicating the opcode.&#x20;



suppose we want to write sum of the first $$𝑛$$ natural numbers

```asm6502
Address |  Instruction/data 
----------------------------
0:      |  1000000000001000  ; load the value at memory address 8 into register 0.
1:      |  0111000100000000  ; initialize register 1 to 0. This will hold the cumulative sum.
2:      |  0111001000000001  ; initialize register 2 to 1. This is used as a decrement value.
3:      |  0001000100010000  ; add the value of R0 to R1 and store the result back in R1.
4:      |  0010000000000010  ; subtract the value of R2 (which is 1) from R0.
5:      |  1101000000000011  ; branch to the memory address 3 if the result of the previous subtraction (R0) is positive. This means the loop continues as long as R0 is greater than 0.
6:      |  1001000100001111  ; store the value of R1 into the memory address 255 (stdout).
7:      |  0000000000000000  ; halt execution.
8:      |  0000000000001100  ; integer value 12
9:      |  0000000000000000  ; result will be stored here
----------------------------
```

This process seems exceedingly simple, but we still have not described the process of actually getting the program to run. For Java, we were able to describe how you would use an editor to create a file containing the program, then use a compiler and the Java Virtual Machine to execute it and view the results in the terminal window. For TOY, you have to consider that there is no operating system, no applications, certainly no editor, terminal emulator, compiler, or runtime—not even a keyboard or a display.

### 3. Assembly Language&#x20;

While machine language is convenient for computers, it is extremely inconvenient for humans. For one, it's not readable, with opcodes, registers, and memory addresses all written in binary. Second, code is referenced by its memory address, requiring a lot of planning to ensure a program works correctly. Imagine the frustration if you meticulously crafted a program only to realize you need to add a few lines. Inserting those lines would break the entire program because all subsequent instructions would be displaced to different memory addresses.

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
6:      |  1001000100001111  ; store the value of R1 into the memory address 255 (stdout).
10:     |  0000000000000000  ; halt execution.
11:     |  0000000000001100  ; integer value 12
12:     |  0000000000000000  ; result 
----------------------------
```

As we can see, machine language programs are incredibly difficult to write and maintain. Assembly is designed to make both of these tasks easier. Instead of writing raw binary opcodes (e.g., `1000` for "load value"), assembly language uses human-readable mnemonics. For example, the mnemonic `LD` is used for loading values, `ADD` for addition, and `BRP` for branching if a result is positive. This makes the code much easier to understand.

Program known as assembler converts the mnemonic opcodes to binary.&#x20;

Rather than referring to registers by their binary numbers (e.g., `0000` for register 0), assembly language uses names like `R0`, `R1`, up to `R16` (or however many the architecture supports). This is more intuitive for programmers.

Instead of hardcoding specific memory addresses (e.g., `00001000` for address 8), assembly language allows you to use labels. These labels are essentially symbolic names for memory locations. For instance, you might have a label called `START` to indicate where your program begins or a label `DATA` to represent a section of memory where your data is stored. The assembler automatically calculates the actual memory addresses corresponding to these labels, making your code much more flexible.

Here's what our&#x20;

```
        LD R0 N   
        LDB R1 #0      
        LDB R2 #1     
LOOP:   ADD R1 R1 R0   
        SUB R0 R0 R2   
        BRP R0 LOOP
        STR R1 STDOUT
        HALT     
N:      12
```

To run our program, we write it out like this, then we feed it to the assembler, which converts it into an equivalent machine language version. The precise memory locations wll be filled in my the assembler.&#x20;

<figure><img src="../.gitbook/assets/Frame 65 (2).png" alt="" width="375"><figcaption></figcaption></figure>

This solves the problem of being able to modify a program. Since we're reffering to labels, rather than raw addresses, even if we insert some lines and LOOP and N no point to a few memory locations later, that does not matter, since the references are to labels, not actual memory locations.&#x20;

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
        STR R1 STDOUT 
        Halt      
N:      12
```

### 4. High Level Languages

While assembly language represents a significant improvement over machine language, it is still cumbersome for many reasons.&#x20;

First, to write efficient assembly code, you need to be intimately familiar with the specific processor you're targeting. This means knowing the number and types of registers, the available instruction set, and the nuances of how those instructions interact with memory. This makes assembly programming a specialized skill.

Second, extremely tedious because assembly instructions are very low-level. As we saw, each instruction performs a very basic task, like loading a value into a register, adding two numbers, or jumping to a different part of the program. Building complex functionality, such as calculating an average, sorting data, or displaying graphics, requires many lines of assembly code. This can lead to long, intricate programs that are difficult to write, understand, and maintain.

Perhaps the most significant limitation of assembly language is its lack of portability. Assembly code is tightly coupled to a specific processor architecture. Imagine you've written a fantastic game in assembly language for the TOY architecture. If you want to make that game available for other computers, you'd essentially need to rewrite the entire game for each different processor architecture—an impractical and costly endeavor. There's no straightforward way to automatically translate assembly code from one architecture to another because the instructions and underlying hardware are fundamentally different.

\<explain how high level languages address these challenges>

```c
< write pseudocode in high-level language of assembly program showing how it's easier>

    int N = 8, sum = 0;
    for (int i = 1; i <= N; i++) {
        sum += i;
    }
    print(sum);


```
