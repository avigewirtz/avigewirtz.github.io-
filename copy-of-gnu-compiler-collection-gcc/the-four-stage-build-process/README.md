# The Four Stage Build Process

We know from lecture 3 that when you invoke gcc on a .c file, it undergoes four stages of transformation--preprocessing, compilation proper, assembly, and linking--culminating in an executable file--that is, a file that can be run on the computer. In lecture, a thorough overview of the four stage process was shown four the charcount program, tracing its journey from source code to executable. In this chapter, we aim to supplement the explanation in lecture by going over in from the opposite appraoch. Starting at machine code and buiding up to C. more depth the design decisions behind this process. We will use a different appraoch. We will first explore the journey from the opposite direction--from machine code to C source code. This follows the historical progression. Our goal is that by explaining from this appraoch, it'll offer a better understanding of how each stage builds off the oprevious stage, and why it was offered to begin with.&#x20;

## The Big Picture

* Imagine trying to send a message to someone who speaks a completely different language than you do. You could invest the time and effort to learn their language, but this is&#x20;
* Computers operate using a primitive language known as machine language, which consists entirely of binary code—strings of 1s and 0s. This language is perfectly suited to the binary nature of computer processing, as it directly represents the on and off states of a computer's electronic components. However, for humans, trying to write complex programs or algorithms in machine language is exceedingly difficult and error-prone. It requires a deep understanding of the computer's architecture and leaves a lot of room for mistakes.
* On the flip side, we have languages like Java, C, and Python, which are designed to be more intuitive for humans. These high-level programming languages incorporate elements that resemble English, such as descriptive variable names, and familiar structures like loops and conditional statements, making them far more accessible for programmers. The challenge, however, is that computers cannot directly understand these high-level languages as they are fundamentally different from the computer's native machine language.
* These tools take the high-level programming language code written by developers and translate it into the machine language that the computer can understand and execute.





## Machine code

* First go over simple instruction or two. show equivelant in assembly. Then go over full program.&#x20;





* Perhaps the best way to explain the nature of machine code is to use a machine code program.&#x20;
* we'll go over a machine code program written in TOY. fictional computer, but very similar to real computers in that day
* a full overview is provided in chapter 6 of computer science: an interdisciplinary approach. highly recommend you read it, but you don't have to to understand the program we'll go over.&#x20;
* review of toy components:&#x20;
  * 16 types of instructions, each 16 bits long
  * 256 memory location, each holds 16 bits
  * 16 general-purpose registers, each holds 16 bits
  * a program counter, which contains the memory address of the current instruction being executed
  * an instruction register, which contains the intsruction currently being executed
  * TOY components summarized in Figure 1.&#x20;

<figure><img src="../../.gitbook/assets/Group 29 (2).png" alt=""><figcaption><p>Toy components</p></figcaption></figure>



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







































The purpose of compilation is to transform C source code—an English-resembling language suitable for human understanding—into executable machine code—a binary language suitable for computer processing.

GCC performs compilation in four sequential stages: preprocessing, compilation proper, assembly, and linking. The purpose of this chapter is to provide a detailed overview of each of these stages. We will illustrate these four stages by following the journey of a C program from source code to executable. The program we will use is a simple program that calculates the area of a circle given its circumference. It consists of three files: main.c, circle.c, and circle.h. Their source code is written below.&#x20;

{% code title="main.c" lineNumbers="true" %}
```c
#include <stdio.h>
#include <stdlib.h>
#include "circle.h"

int main() {
    double circumference, area;

    printf("Enter the circumference of the circle (positive number): ");
    if (scanf("%lf", &circumference) != 1 || circumference <= 0) {
        printf("Invalid input. Circumference must be a positive number.\n");
        exit(EXIT_FAILURE);
    }

    area = calculateArea(circumference);

    printf("The area of the circle is: %.2f\n", area);

    return 0;
}
```
{% endcode %}

{% code title="circle.c" lineNumbers="true" %}
```c
#include "circle.h"
#define PI 3.14159

double calculateArea(double circumference) {
    double radius = circumference / (2 * PI);
    return PI * radius * radius;
}

```
{% endcode %}

{% code title="circle.h" lineNumbers="true" %}
```c
#ifndef CIRCLE_H
#define CIRCLE_H

double calculateArea(double circumference);

#endif
```
{% endcode %}

## Bird’s eye view of the GCC compilation process

Before diving into the complexities of each stage, we'll first give a bird's eye view of the process. Having an overarching view will allow you to grasp the big picture, making it easier to contextualize the more detailed aspects that follow.

Suppose we compile our program with the following command:

```bash
gcc main.c circle.c -o circle
```

GCC will compile the program in the following manner:

* **Preprocessing**: The compilation journey begins with main.c and circle.c being sent to the preprocessor, which is a program that essentially prepares the source files for compilation. It does this by removing comments and responding to preprocessor directives--lines in the code that begin with the # (hash) character. For example, #include \<stdio.h> in main.c tells the preprocessor to insert the contents of stdio.h into the current file. The result of preprocessing is two files: main.i and circle.i. The preprocessor sends main.i and circle.i to the compiler.&#x20;
* **Compilation**: Next, the compiler translates `main.i` and `circle.i` into assembly language, which are stored in main.s and circle.s. Assembly language is essentially a human-readable form of machine language.
* **Assembly**: The assembler converts assembly code in main.s and circle.s to object code, storing the result in main.o and circle.o. These files contain machine code but aren't yet executable due to external references and/or absence of a main function. For example, circle.o lacks a main function, and main.o contains references to calculateArea and library functions (such as printf and scanf), al of which are external to main.o.
* **Linking**: Finally, the linker merges `main.o` and `circle.o`and the relevant library code, resolving external references to functions like calculateArea and printf. The result is is an executable named circle.&#x20;

<figure><img src="../../.gitbook/assets/Group 17.png" alt=""><figcaption><p>Four Stage Compilation Process of main.c and circle.c</p></figcaption></figure>

This process, summarized in Figure 1, resembles an assembly line. Our C program, starting as source code, moves through different 'stations'—the preprocessor, compiler, assembler, and linker—each transforming it closer to a finished product. By the end, our program emerges as an executable, ready to be run on a computer.

### Saving preprocessed, compiled, and assembled versions

By default, GCC stores the preprocessed, compiled, and assembled versions of the program in temporary files, which are discarded. As such, all you'll see is the executable. However, you can instruct GCC to save the preprocessed output by using the -save--temps option. To save the the intermediate outputs for main.c and circle.c, invoke gcc like so:

```bash
gcc main.c circle.c --save-temps -o circle
```

If you examine your directory contents with ls, you'll see the following



### Isolating Each Stage of Compilation









## Separate Compilation

It is important to recognize that main.c and circle.c are preprocessed, compiled, and assembled separately. Only after they are individually translated into machine code are they--along with the necessary library code--merged together to form an executable. This technique is known as _separate compilation_. It is employed by GCC&#x20;







### Motivation

Why are we concerning ourselves with the internals of how GCC performs compilation? After all, we regularly use programs without having any knowledge of their inner workings, focusing only on their output. Take the 'ls' command, for instance; we use it to list directory contents, but we don’t concern ourselves with its internals. So, why do we care when it comes to GCC?

Broadly speaking, there are two reasons. First, understanding these stages aids in debugging. Let’s face it, compilation isn’t always a smooth process. Quite often, something goes wrong along the way, and what you end up with is not an executable but a cryptic error message. Without a basic understanding of how compilation works, the cause of the error is likely to be elusive, making it incredibly difficult to debug your program.

Second, GCC is designed to enable separate compilation. This will be discussed in depth in the chapter on Make. In order to take advantage of separate compilation, however, you have to understand the process, particularly the linking phase.&#x20;

3\. Helps you understand what global variables are. This is mentioned in book when discussing linker

\
