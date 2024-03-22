# Machine Code

We know from lecture 3 that when you invoke gcc on a .c file, it undergoes four stages of transformation--preprocessing, compilation proper, assembly, and linking--culminating in an executable file--that is, a file that can be run on the computer. In lecture, a thorough overview of the four stage process was shown four the charcount program, tracing its journey from source code to executable. In this chapter, we aim to supplement the explanation in lecture by going over in from the opposite appraoch. Starting at machine code and buiding up to C. more depth the design decisions behind this process. We will use a different appraoch. We will first explore the journey from the opposite direction--from machine code to C source code. This follows the historical progression. Our goal is that by explaining from this appraoch, it'll offer a better understanding of how each stage builds off the oprevious stage, and why it was offered to begin with.&#x20;

## The Big Picture

A programming language serves as a medium to provide instructions to a computer. Computers only understand one type of language—machine language, which consists of only 1s and 0s. This binary system is used because computers operate using electrical signals that can only be in one of two states: on (1) or off (0). The challenge is that such a language is inconvenient for humans. For instance, "hello" might be expressed in ASCII (a character encoding standard), "5" as 00000101 (correct binary representation of 5), "5.1" in IEEE floating-point representation (a standard for representing real numbers), and an operation like "a = 2 + 3" would be translated into a sequence of binary codes that perform the addition.

The question then arises: How do we bridge the gap between the type of language convenient for humans and the type of language convenient for computers?

The solution involves designing a new set of instructions that are more convenient for people to use than the built-in machine instructions. One method of executing a program written in our language is to first translate each instruction into an equivalent sequence of instructions in machine language. The resulting program consists entirely of machine language instructions. The computer then executes this machine language version instead of our original version. This technique is known as translation.

## Machine code

* Explain where the machine code instructions are defined (ISA) and by whom. Give brief practical modern day example.&#x20;
* Programmer's used to program in machine code, but quickly replaced by assembly. Perhaps the best way to explain the nature of machine code is to use a machine code program. we'll go over a machine code program written in TOY. fictional computer, but very similar to real computers in that day. a full overview is provided in chapter 6 of computer science: an interdisciplinary approach. highly recommend you read it, but you don't have to to understand the program we'll go over. In order to program with TOY, you would consult it's ISA.&#x20;
* review of toy components:&#x20;
  * 16 types of instructions, each 16 bits long
  * 256 memory location, each holds 16 bits
  * 16 general-purpose registers, each holds 16 bits
  * a program counter, which contains the memory address of the current instruction being executed
  * an instruction register, which contains the intsruction currently being executed
  * TOY components summarized in Figure 1.&#x20;













<figure><img src="../.gitbook/assets/Group 29 (2).png" alt=""><figcaption><p>Toy components</p></figcaption></figure>



Suppose we load the following 6 instructions into memory, say at memory addresses 20-25:

```
0111100000000000
1000110011111111
1100110001010101
0001100010001100
1100000001010001
1001100011111111
0000000000000000


LOAD R8 #0
LOAD R0 A255
BRZ R0 A55
ADD R8 R8 R12
BRZ R0 A51
STORE R8 A255
HALT


            LOAD R8 #0
LOOP_START: LOAD R0 STDIO
            BRZ R0 LOOP_END
            ADD R8 R8 R12
            BRZ R0 LOOP_START
LOOP_END:   STORE R8 STDIO
            HALT
```

And we set the program counter to 20.&#x20;

















have some way of storing groups of binary digits and feeding them into the computer. On reading a particular pattern of bits, the computer will react in some way. This is absolutely deterministic; that is, every time the computer sees that pattern its response will be the same. Let's say we have a mythical computer which reads in groups of 16 eight at a time, and according to the pattern of 1s and 0s in the group, performs some task. On reading this pattern, for example





For example, upon reading the pattern:

```
0111001000000001
```

The CPU will react by setting the value of register 2 to 300. Or upon reading the pattern:

```
1001 0010 10101111
```

stores the contents of register 2 into memory location addr = 175





it might switch off that voltage. The two patterns may then be regarded as instructions to the computer, the first meaning 'voltage on', the second 'voltage off'. Every time the instruction 10100111 is read, the voltage will come on, and whenever the pattern 10100110 is encountered, the computer turns the voltage off. Such patterns of bits are called the machine code of a computer; they are the codes which the raw machinery reacts to.











## Assembly language and assemblers

There are 256 combinations of eight 1s and 0s, from 00000000 to 11111111, with 254 others in between. Remembering what each of these means is asking too much of a human: we are only good at remembering groups of at most six or seven items. To make the task of remembering the instructions a little easier, we resort to the next step in the progression towards the high-level instructions found in BASIC. Each machine code instruction is given a name, or mnemonic. Mnemonics often consist of three letters, but this is by no means obligatory. We could make up mnemonics for our two machine codes:

ON means 10100111 OFF means 10100110

So whenever we write ON in a program, we really mean 10100111, but ON is easier to remember. A program written using these textual names for instructions is called an assembly language program, and the set of mnemonics that is used to represent a computer's machine code is called the assembly language of that computer. Assembly language is the lowest level used by humans to program a computer; only an incurable masochist would program using pure machine code.

It is usual for machine codes to come in groups which perform similar functions. For 2 of 20

example, whereas 10100111 might mean switch on the voltage at the signal called 'output 0', the very similar pattern 10101111 could mean switch on the signal called 'output 1'. Both instructions are 'ON' ones, but they affect different signals. Now we could define two mnemonics, say ON0 and ON1, but it is much more usual in assembly language to use the simple mnemonic ON and follow this with extra information saying which signal we want to switch on. For example, the assembly language instruction

ON 1

would be translated into 10101111, whereas: ON 0

is 10100111 in machine code. The items of information which come after the mnemonic (there might be more than one) are called the operands of the instruction.

How does an assembly program, which is made up of textual information, get converted into the machine code for the computer? We write a program to do it, of course! Well, we don't write it. Whoever supplies the computer writes it for us. The program is called an assembler. The process of using an assembler to convert from mnemonics to machine code is called assembling. We shall have more to say about one particular assembler - which converts from ARM assembly language into ARM machine code - in Chapter Four.





## Compilers and interpreters

As the subject of this book is ARM assembly language programming, we could halt the discussion of the various levels of instructing the computer here. However, for completeness we will briefly discuss the missing link between assembly language and, say, Pascal. The Pascal assignment

a := a+12

looks like a simple operation to us, and so it should. However, the computer knows nothing of variables called a or decimal numbers such as 12. Before the computer can do what we've asked, the assignment must be translated into a suitable sequence of instructions. Such a sequence (for some mythical computer) might be:

```
LOAD a
ADD 12
STORE a
```

Here we see three mnemonics, LOAD, ADD and STORE. LOAD obtains the value from the place we've called a, ADD adds 12 to this loaded value, and STORE saves it away again. Of course, this assembly language sequence must be converted into machine code before it can be obeyed. The three mnemonics above might convert into these instructions:

3 of 20

ARM Assembly Language Programming - Chapter 1 - First Concepts

00010011\
00111100\
00100011\
Once this machine code has been programmed into the computer, it may be obeyed, and the initial assignment carried out.

To get from Pascal to the machine code, we use another program. This is called a compiler. It is similar to an assembler in that it converts from a human-readable program into something a computer can understand. There is one important difference though: whereas there is a one-to-one relationship between an assembly language instruction and the machine code it represents, there is no such relationship between a high-level language instruction such as

PRINT "HELLO"

and the machine code a compiler produces which has the same effect. Therein lies one of the advantages of programming in assembler: you know at all times exactly what the computer is up to and have very intimate control over it. Additionally, because a compiler is only a program, the machine code it produces can rarely be as 'good' as that which a human could write.

A compiler has to produce working machine code for the infinite number of programs that can be written in the language it compiles. It is impossible to ensure that all possible high- level instructions are translated in the optimum way; faster and smaller human-written assembly language programs will always be possible. Against these advantages of using assembler must be weighed the fact that high-level languages are, by definition, easier for humans to write, read and debug (remove the errors).

The process of writing a program in a high-level language, running the compiler on it, correcting the mistakes, re-compiling it and so on is often time consuming, especially for large programs which may take several minutes (or even hours) to compile. An alternative approach is provided by another technique used to make the transition from high-level language to machine code. This technique is know as interpreting. The most popular interpreted language is BASIC.

An interpreted program is not converted from, say, BASIC text into machine code. Instead, a program (the interpreter) examines the BASIC program and decides which operations to perform to produce the desired effect. For example, to interpret the assignment

LET a=a+12

in BASIC, the interpreter would do something like the following:

4 of 20

ARM Assembly Language Programming - Chapter 1 - First Concepts

1. Look at the command LET
2. This means assignment, so look for the variable to be assigned
3. Check there's an equals sign after the a
4. If not, give a Missing = error
5. Find out where the value for a is stored
6. Evaluate the expression after the =
7. Store that value in the right place for a

Notice at step 6 we simplify things by not mentioning exactly how the expression after the = is evaluated. In reality, this step, called 'expression evaluation' can be quite a complex operation.

The advantage of operating directly on the BASIC text like this is that an interpreted language can be made interactive. This means that program lines can be changed and the effect seen immediately, without time-consuming recompilation; and the values of variables may be inspected and changed 'on the fly'. The drawback is that the interpreted program will run slower than an equivalent compiled one because of all the checking (for equals signs etc.) that has to occur every time a statement is executed. Interpreters are usually written in assembler for speed, but it is also possible to write one in a high-level language.

Summary

We can summarise what we have learnt in this section as follows. Computers understand (respond to) the presence or absence of voltages. We can represent these voltages on paper by sequences of 1s and 0s (bits). The set of bit sequences which cause the computer to respond in some well-defined way is called its machine code. Humans can't tell 10110111 from 10010111 very well, so we give short names, or mnemonics, to instructions. The set of mnemonics is the assembly language of the computer, and an assembler is a program to convert from this representation to the computer-readable machine code. A compiler does a similar job for high-level languages.





We began by exploring how computers interpret data, including integers and text. However, the true power of a computer lies in its ability to execute programs, which are sequences of instructions that direct the computer to perform specific tasks. For instance, one instruction might instruct the processor to add two numbers, while another might instruct it to move data from one memory location to another. All these instructions, like any other type of data within a computer, are represented in binary.

**Format of an Instruction**

Each machine code instruction is composed of an operation code (opcode) and one or more operands. The opcode specifies the operation to be performed, such as addition, subtraction, or loading data from memory. The operands are the data or parameters the operation should act upon.

**Instruction Set Architecture**

The set of all possible instructions a processor can execute is defined by the Instruction Set Architecture (ISA), which is the interface to the computer. The ISA outlines how instructions are encoded in binary and the impact they have on the processor's state. It also specifies the size and format of instructions, main memory and registers, the supported data types, and the instruction set itself. However, it doesn't dictate how these instructions are implemented within a physical processor.

**Machine Code Example:**

Demonstrating what machine code is truly like necessitates an example of a machine code program. However, modern machine code languages, such as ARM and X86, are so complex, that it's unrealistic to write a self-contained machine code program. Therefore, we will demonstrate machine code by using the TOY computer introduced in COS126, which has a much simpler instruction set. Though TOY is a fictional computer, it closely resembles the computers from the era when programmers coded in machine code.

"?

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
