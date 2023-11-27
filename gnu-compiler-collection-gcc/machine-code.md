# Machine Code

We began by exploring how computers interpret data, including integers and text. However, the true power of a computer lies in its ability to execute programs, which are sequences of instructions that direct the computer to perform specific tasks. For instance, one instruction might instruct the processor to add two numbers, while another might instruct it to move data from one memory location to another. All these instructions, like any other type of data within a computer, are represented in binary.

**Format of an Instruction**

Each machine code instruction is composed of an operation code (opcode) and one or more operands. The opcode specifies the operation to be performed, such as addition, subtraction, or loading data from memory. The operands are the data or parameters the operation should act upon.

**Instruction Set Architecture**

The set of all possible instructions a processor can execute is defined by the Instruction Set Architecture (ISA), which is the interface to the computer. The ISA outlines how instructions are encoded in binary and the impact they have on the processor's state. It also specifies the size and format of instructions, main memory and registers, the supported data types, and the instruction set itself. However, it doesn't dictate how these instructions are implemented within a physical processor.

**Machine Code Example:**

Demonstrating what machine code is truly like necessitates an example of a machine code program. However, modern machine code languages, such as ARM and X86, are so complex, that it's unrealistic to write a self-contained machine code program. Therefore, we will demonstrate machine code by using the TOY computer introduced in COS126, which has a much simpler instruction set. Though TOY is a fictional computer, it closely resembles the computers from the era when programmers coded in machine code.

Let's revisit the TOY ISA, which provides all the information a programmer needs to write programs in TOY machine code. The TOY machine comprises:

* 256 addresses, each containing 16 bits
* 16 registers, each 16 bits
* An instruction set comprising of 16 distinct types of 16-bit instructions

TOY instructions can be formatted in two ways, as shown below. In each case, the leftmost 4 bits always represent the opcode.

<figure><img src="../.gitbook/assets/Screenshot 2023-05-28 at 12.35.09 PM.png" alt=""><figcaption></figcaption></figure>

For the following program, we will assume it is already loaded into memory, and the first instruction starts at address 10. &#x20;



```c
Address | instruction 
----------------------------
10:     |  1000101011111111 // read 16 bits from stdin and store in register 10       
11:     |  1000101111111111 // read 16 bits from stdin and store in register 11        
12:     |  0111110000000000 // load value 0 into register 12   
13:     |  0111000100000001 // load value 1 intro register 1  
14:     |  1100101000011000 // if the value in register 10 is 0, jump to memory address 18 
15:     |  0001110011001011 // add the value in register 11 to register 12
16:     |  0010101010000001 // decrement the value in register by the value in register 1 (1) 
17:     |  1100000001010011 // jump back to memory address 14      
18:     |  1001110011111111 // write the value in register 12 on stdout       
19:     |  0000000000000000 // halt the execution of the program    
----------------------------
```

## Observations

* It's not human readable, meaning that it's not descriptive
* Many lines of code to perform a simple task
* Code is tedious to write&#x20;
* very few instructions
* very simple instructions
* no high level constructs such as loops
* have to combine to do anything useful
* have to be hardcode memory and register addresses, requiring us to be intimately familiar with hardware



It should be noted that we can improve machine code writing by for example using hex instead of binary. so, for example, instead of typing out 1000 1010 1111 1111, we type 8AFF. In fact, this is how programming in TOY was in COS126.&#x20;



```
10: 1000101011111111 => 8AFF
11: 1000101111111111 => 8BFF
12: 0111110000000000 => 7C00
13: 0111000100000001 => 7101
14: 1100101000011000 => CA18
15: 0001110011001011 => 1CCB
16: 0010101010100001 => 2AA1
17: 1100000000010100 => C014
18: 1001110011111111 => 9CFF
19: 0000000000000000 => 0000
```

However, while hexadecimal might be slightly more digestible and easier to code than binary, the underlying challenge remains: it's a flat sequence of numbers without any meaningful structure or descriptive identifiers, making it hard to understand what each part of the code is doing.

Another significant issue with machine code is its lack of portability. Portability, in this context, refers to the ability of a program to be executed on different types of systems without requiring modification.

Machine code lacks portability. Machine code is designed for a specific processor architecture, and it directly uses the instructions defined by that processor's ISA. For example, machine code written for a TOY machine would be different from that written for an ARM processor or an x86 processor, even if they were intended to perform the same task.&#x20;

If you write a program in machine code for one type of processor, it won't run on a different type of processor. You would have to rewrite the program using the different processor's machine language, which is a labor-intensive and error-prone process.





The key idea of a programming languege is as follows:&#x20;

what if we enable programs&#x20;

<details>

<summary>Aside: RISC vs. CISC</summary>

Instruction set architectures fall into one of two main categories: Reduced Instruction Set Computing (RISC) and Complex Instruction Set Computing (CISC).

RISC architectures, such as ARM, aim to simplify the set of possible instructions, enabling faster execution and reducing the complexity of the CPU. They rely on a philosophy of executing a single operation on each clock cycle, which makes them efficient and power-saving.

On the other hand, CISC architectures, like x86, contain a large number of complex instructions. This complexity can lead to increased functionality per instruction at the expense of slower clock speeds and higher power consumption

</details>
