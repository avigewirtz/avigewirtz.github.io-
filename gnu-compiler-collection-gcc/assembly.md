# Assembly

To make programming easier, programmers long ago developed assembly. In assembly language, we replace numerical opcodes with mnemonics, which are descriptive and human-readable. For example, we if we want to use the "add" opcode in TOY, rather that typing 0001 (or 1 in hex), we might type 'add', which will later be converted to '0001' by a program called an assembler. Similarly, rather than typing '1100' when we want to store the content of a register in memory, we type the a mnemonic like ' str'.  &#x20;

In a similar vein, assembly languages use symbols to refer to reguster and memory addresses. For example, when referencing a register or memory address in an instruction, we might refer to the registers as r0 to r15 and we might refer to memory addresses as m0 to m255.&#x20;

Putting this all together, if we want to, for example, write an instruction telling the computer to store the value of register 10 in memory address 255, our instruction would look like the following:&#x20;

```
str r10 m255
```

rather than

```
1100111011111111
```

**Designing an Assembly Language for TOY**

Consider how we might design an assembly language for TOY. Let's discuss how we might design an assembly language for our TOY computer.&#x20;

* For Registers: We can replace binary representations of registers (0000 to 1111) with the notation r0 to r15.
* For Memory: Instead of binary representations for memory addresses (00000000 to 11111111), we can use the notation m0 to m255.
* When referring to literals, such as integers, we can use notation like the following: #0, #1, #2
* For opcodes, we could use the following mnemonics:

```c
0000 -> hlt (HALT)
0001 -> add (ADD)
0010 -> sub (SUBTRACT)
0011 -> and (AND)
0100 -> xor (EXCLUSIVE OR)
0101 -> lsh (LEFT SHIFT)
0110 -> rsh (RIGHT SHIFT)
0111 -> lda (LOAD ADDRESS)
1000 -> ld (LOAD)
1001 -> str (STORE)
1010 -> ldi (LOAD INDIRECT)
1011 -> stri (STORE INDIRECT)
1100 -> brz (BRANCH ZERO)
1101 -> brp (BRANCH POSITIVE)
1110 -> jmpr (JUMP REGISTER)
1111 -> jal (JUMP AND LINK)
```

Using this assembly notation, this is how our previous program would look:&#x20;

```
Address | instruction 
-----------------------------
10:     |  ld r10 m255   
11:     |  ld r11 m255        
12:     |  lda r12, #0     
13:     |  lda r1, #1   
14:     |  brz r10, m18   
15:     |  add r12, r12, r11
16:     |  sub r10, r10, r1 
17:     |  jmpr m14       
18:     |  str r12 m255   
19:     |  hlt     
-----------------------------
```



This program is clearly much easier to read and write. \<ELABORATE>. Of course, it must ultimately be translated into machine code. That is done via a program known as an assembler. So-called because it takes an assembly program and translates it into machine code.&#x20;

However, note we still need to be intimately familiar with the hardware, including memory locations of instructions, as well as register and memory layout. For example, observe in the previous program that we still had to know:

* memory address 255 represents stdin and stdout
* the brz r10 m18 instruction was in  memory address 14
* the str r12 instruction was in memory address 18

To make programming in assembly even easier, we can abstract things further by:

* using the mnemonic 'rd' whenever you want to 'read' from stdin and using the mnemonic 'wrt' whenever you want to write to stdout. This way, you need not now that memory address 255 represents stdin and stdout.&#x20;
* We can use labels to represent memory addresses instead of hardcoding them. For example,  we can denote a labels as so:

```armasm
START: 
    rd r10        
    rd r11        
    ld r12, #0     
    ld r1, #1   
LOOP: 
    brz r10, END  
    add r12, r12, r11
    sub r10, r10, r1 
    jmpr LOOP       
END: 
    wrt r12       
    hlt     
```

where 'START', 'LOOP' and 'END'--all suffixed with a colon--are all labels.&#x20;

Observe the benefits of this approach:

* We read from stdin with 'rd' and we write to stdout with 'wrt', rather than having to know that memory address 255 represents stdin and stdout.&#x20;
* Rather than having to be be familiar with the memory addresses of the program--particularly where the loop and end of the program are--we can label them with 'LOOP' and 'END' respectively, and use those terms to refer to it. This eliminates the need to manually track and manage specific memory addresses, reducing the cognitive load on the programmer.

As you can see, labels provide a more human-readable way of referring to memory addresses and simplifying the process of writing and maintaining assembly code. Labels are especially helpful for branching, looping, or other control structures that require jumps to different code parts.

{% hint style="info" %}
Assembly languages offer many other features, such assembler directives, which are commands or instructions that guide the assembler during the assembly process. Assembler directives perform various tasks, such as defining constants, reserving memory space, specifying memory address origins, defining data elements, and controlling the assembly process.
{% endhint %}

## Drawbacks of Assembly

* Platform-dependent: Assembly language is specific to a computer's Instruction Set Architecture (ISA)
* Still primitive and few instructions, so many instructions are required to perform a simple task&#x20;
* Although less knowledge of hardware is required compared to machine code, a lot of knowledge is still required. For example, for many programs, we'd need to be familiar with memory and registers. Even in our previous program, we had to be familiar with registers.

In essence, assembly language allows programmers to write code that closely resembles machine code in terms of performance and control over the hardware, but with the benefits of increased readability and manageability.&#x20;



Variables in assembly?&#x20;
