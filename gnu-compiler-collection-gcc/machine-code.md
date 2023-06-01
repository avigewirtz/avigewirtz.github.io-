# Machine Code

Consider a simple instruction, directing the computer to add the integers 5 and 10 and store the result in a variable named 'num'.&#x20;

```c
int num = 5 + 10;    
```

How can we write this in binary, so it can be stored in computer memory?&#x20;

| ASCII Character | Binary Equivalent |
| --------------- | ----------------- |
| i               | 01101001          |
| n               | 01101110          |
| t               | 01110100          |
| space           | 00100000          |
| n               | 01101110          |
| u               | 01110101          |
| m               | 01101101          |
| space           | 00100000          |
| =               | 01111101          |
| space           | 00100000          |
| 5               | 00110101          |
| space           | 00100000          |
| +               | 00101011          |
| space           | 00100000          |
| 1               | 00110001          |
| 0               | 00110000          |
| ;               | 00111011          |



So, putting it all together, "int num = 5 + 10;" in binary is

{% code overflow="wrap" %}
```
1101001 1101110 1110100 100000 1101110 1110101 1101101 100000 111101 100000 110101 100000 101011 100000 110001 111000 111011
```
{% endcode %}



Is this a valid instruction?&#x20;

No. An instruction refers to a specific kind of binary code that can be understood by the Central Processing Unit (CPU).&#x20;

A binary representation of an ASCII string, like "int num = 5 + 10;", doesn't form valid machine instructions. It's merely a binary representation of text. The binary code for the ASCII character 'i', for example, doesn't correspond to any kind of CPU operation. It's just the way that character is represented in memory.

High-level programming languages like C++, Python, or JavaScript are designed to be easily readable and writeable by humans, but CPUs can't execute them directly. Before a high-level program can be executed, it must be converted into machine code by a compiler or interpreter.

So while you can convert any data, including ASCII text, into binary, not all binary is executable as machine code. Only binary code that corresponds to valid CPU instructions (and is correctly structured into a valid program) can be executed.



However, these ASCII values are not instructions for the computer's CPU. They don't tell the computer to do anything like perform calculations, move data, or make decisions. That's the role of machine code, which consists of binary-encoded instructions that the CPU can directly execute.

High-level programming languages let humans write instructions in a more readable and abstract way, but these instructions have to be translated into machine code (via a process called compiling or interpreting) before the CPU can execute them. The ASCII representation of a string of high-level code is not the same as the machine code that the CPU needs to execute that code.



n theory, it is possible to design a computer or system that interprets high-level programming languages like C directly, but in practice, it would be incredibly complex and inefficient for several reasons.&#x20;



Instead, most systems use a layered approach, where high-level languages are translated into machine code that the CPU can execute directly. This approach gives a good balance between readability and expressiveness for programmers, and efficiency and performance for execution.



To directly understand and execute C code, the hardware would have to include logic to handle all constructs of the C language, like loops, function calls, pointer arithmetic, and more. This would make the hardware far more complex than current CPUs, which only need to handle a small set of simple instructions.&#x20;















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
