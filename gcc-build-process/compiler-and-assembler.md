# Compiler and Assembler

### 1. Introduction

Often, the easiest way to understand the role of software is to explore what development was like before it existed. Back in the day, there was no preprocessor, compiler, assembler, or linker. All coding was done in machine code--a binary language comprised of 0s and 1s. We'll build our way up.&#x20;

### 2. Machine Language

Each CPU has a unique set of instructions it can execute, known as machine code. There's no universal standard for machine code, as each manufacturer designs its own for their specific device. However, two fundamental characteristics of machine code are consistent across all modern computers:

1. Machine code is a binary language, consisting entirely of 1s and 0s. While there's no inherent requirement for machine code to use a binary system (historically, some computers used decimal systems), binary has proven to be the most efficient, leading to its adoption in all modern computers.
2. &#x20;Instructions in machine code are very basic, rarely exceeding the complexity of adding two numbers or transferring data between memory locations.

A processor's control unit expects each instruction in a specific format, typically a fixed length (e.g., 16, 32, or 64 bits). The first few bits, known as the opcode (operation code), specify the general task to be performed (e.g., "store a number" or "add two numbers"). The remaining bits contain operands, providing the necessary information to interpret the instruction (e.g., where to store the number or which numbers to add).

#### Machine Code Program Example

Imagine a hypothetical computer with 256 memory addresses and 16 general-purpose registers. Each memory address is 1 byte (8 bits), and each register is 2 bytes. Instruction are 2 bytes long, wit the first four bits indicating the opcode.&#x20;



&#x20;each holding 16 bits. Each instruction is 16 bits long, with the first four bits indicating the opcode. Upon power-on, the computer begins execution at memory address 0.

* suppose we want to write sum of the first $$𝑛$$ natural numbers

```asm6502
Address |  Instruction/data 
----------------------------
0:      |  10000000
1:      |  00001000  ; load the value at memory address 8 into register 0.
2:      |  01110001
3:      |  00000000  ; initialize register 1 to 0. This will hold the cumulative sum.
2:      |  01110010
5:      |  00000001  ; initialize register 2 to 1. This is used as a decrement value.
3:      |  00010001
7:      |  00010000  ; add the value of R0 to R1 and store the result back in R1.
4:      |  00100000
9:      |  00000010  ; subtract the value of R2 (which is 1) from R0.
5:      |  11010000
11:     |  00000011  ; branch to the memory address 3 if the result of the previous subtraction (R0) is positive. This means the loop continues as long as R0 is greater than 0.
6:      |  10010001
13:     |  00001111  ; store the value of R1 into the memory address 255 (stdout).
7:      |  00000000
15:     |  00000000  ; halt execution.
8:      |  00000000
17:     |  00001100  ; integer value 12
9:      |  00000000
19      |  00000000  ; result will be stored here
----------------------------
```

### 3. Assembly Language&#x20;

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
6:      |  1001000100001111  ; store the value of R1 into the memory address 255 (stdout).
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
        STR R1 STDOUT
        Halt      
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

While assembly language is leaps above machine language, it's still quite inconvenient to code in.&#x20;

* Requires intimate knowledge of processor architecture.&#x20;
* Very simple instructions. Takes many lines to perform simple task.&#x20;
* Not portable.&#x20;

C equivalent:

```c
int printf(const char *format, ...);

int main() {
    int N = 8; // Initialize N with the value 8
    int sum = 0; // Variable to store the sum

    // Calculate the sum of natural numbers from 1 to N
    for (int i = 1; i <= N; i++) {
        sum += i;
    }

    // Print the result
    printf("The sum of natural numbers from 1 to %d is %d\n", N, sum);

    return 0;
}

```
