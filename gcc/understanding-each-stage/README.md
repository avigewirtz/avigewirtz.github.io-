# Understanding each stage

## How Information is Represented in Computers

At its core, all information in computers is stored as a sequence of bits, each of which can be in one of two states of the underlying electrical or magnetic states of the computer's memory components. For instance, a memory cell may consist of a tiny capacitor and transistor. A charged capacitor represents a 1, while a discharged capacitor signifies a 0. Alternatively, magnetic polarities of magnetic material may denote binary digits, with one polarity corresponding to a 1 and the opposite polarity to a 0.

All information, such as numbers, images, audio, videos, and executable programs are stored as sequences of 1s and 0s. You might be wondering how a sequence of 1s and 0s can represent such complex information. The answer is we use encoding schemes.&#x20;



### Representing Integers

\<FILL IN>



### Representing Floating-Point Numbers

Floating-point numbers are represented using a standard called the IEEE 754 floating-point standard. This representation uses three components: sign, exponent, and mantissa (or significand). The sign bit indicates the number's sign, the exponent determines the position of the decimal point, and the mantissa represents the actual numerical value. This format allows for a wide range of numbers and precise calculations.

\
\




### Representing text

1. ASCII (American Standard Code for Information Interchange):

ASCII is a character encoding scheme that was created in the 1960s. It represents text using a 7-bit binary code, which allows for 128 different characters (2^7). The first 32 characters (0-31) are control characters, like line feed and carriage return, and the next 96 characters (32-127) are printable characters, including English letters (both uppercase and lowercase), digits, punctuation marks, and some special symbols.

Each character in ASCII has a unique binary representation. For example, the letter 'A' is represented as 65 in decimal or 1000001 in binary.&#x20;



H: 01001000 e: 01100101 l: 01101100 l: 01101100 o: 01101111

2. Extended ASCII

Extended ASCII is a collection of character encoding schemes that build upon the original 7-bit ASCII encoding to accommodate additional characters. Extended ASCII schemes use 8 bits to represent a total of 256 characters (2^8).

In extended ASCII encoding schemes, the first 128 characters (0-127) are the same as in the original ASCII encoding, while the additional 128 characters (128-255) vary depending on the specific extended ASCII set used. To represent text using extended ASCII, each character is converted to its corresponding 8-bit binary code and stored in the computer's memory.

However, extended ASCII character sets have limitations in supporting the wide variety of languages and scripts used worldwide. This led to the development of Unicode, a more comprehensive character encoding standard that can represent a vast array of characters from different writing systems.&#x20;

3. Unicode

UTF-8, a popular method for storing and transmitting Unicode characters, has largely replaced extended ASCII in modern computing systems due to its broader language support and efficient encoding of character data.



<details>

<summary>A brief overview of how computers represent images, audio, and video</summary>

* Images: Images are represented as a matrix of pixels, where each pixel corresponds to a specific color. The color information is represented using various color models, such as RGB (Red, Green, Blue) or CMYK (Cyan, Magenta, Yellow, Key/Black). Each color channel is represented by a specific number of bits, which determines the range of color values that can be represented.

<!---->

* Audio: Audio data is typically represented as a continuous waveform, which is then sampled at regular intervals to create a digital representation. Each sample represents the amplitude of the waveform at a specific point in time, and the samples are stored using various audio formats and encoding techniques.

<!---->

* Video: Video data is essentially a sequence of images (frames) displayed over time. Each frame is represented using image data formats, and the sequence of frames is stored using various video encoding and compression techniques to reduce the file size while maintaining an acceptable level of quality.

</details>



### Representing Executable Programs&#x20;

Executable programs consist of machine code instructions, which are sequences of binary numbers that correspond to specific operations for the computer's processor. These instructions include operations like loading data from memory, performing arithmetic or logical operations, and controlling program flow. The specific binary representation of these instructions depends on the processor's instruction set architecture (ISA). Executable program files also contain metadata, such as memory addresses and linking information, to ensure proper execution.

## Machine Code

Computers today do not inherently understand high-level programming languages such as C, Java, or any others. While these languages are more convenient for human comprehension, they are not directly executable by computers. Computer hardware is designed to implement a simple set of instructions, such as loading a value from memory into a register or adding two numbers and storing the result.

The specific set of instructions a computer can support is defined by its Instruction Set Architecture (ISA). An ISA is a specification that outlines the supported instructions, registers, memory organization, and addressing modes that a computer's processor can execute. The ISA serves as the lowest-level software interface to the computer. All instructions must ultimately be translated into this form, as the computer cannot understand anything else.

An instruction is a command that directs the processor to perform a specific operation. Each instruction typically consists of an operation code (opcode) and operands. The opcode identifies the operation to be performed, while the operands provide the necessary data or memory addresses involved in the operation. Some ISAs use fixed-length instructions, with each instruction having the same number of bits, while others use variable-length instructions, where the number of bits can vary between instructions.

### Programming in Machine Code: An Example

To demonstrate what programming in machine code is like, we will write a simple machine code program using the fictional TOY ISA from COS126. Although TOY is not a real computer, it serves as a legitimate example for understanding machine code.

In TOY, each instruction is 16 bits long, with the first four bits representing the opcode and the remaining 12 representing the operands. A simple TOY program in binary looks like this:

```java
1000 1010 1111 1111 // Read a byte from memory address 0xFF (stdin) and store it in register R[A]
1000 1011 1111 1111 // Read a byte from memory address 0xFF (stdin) and store it in register R[B]
0111 1100 0000 0000 // Set register R[C] to 0
0111 0001 0000 0001 // Decrement the value in register R[A] by 1
1100 1010 0001 1000 // Check if R[A] is equal to 0, if not, jump to the instruction at address 0x18
0001 1100 1100 1011 // Add the value of R[B] to the value in R[C] and store the result in R[C]
0010 1010 1010 0001 // Jump back to the instruction at address 0x04 (decrement R[A] and continue the loop)
1100 0001 0000 0100 // If R[A] reaches 0, jump to the instruction at address 0x04 (store result in R[C] and output to stdout)
1001 1100 1111 1111 // Write the value in register R[C] to memory address 0xFF (stdout)
0000 0000 0000 0000 // Halt the program
```

This TOY program reads two numbers from stdin (M\[FF]), stores them in registers R\[A] and R\[B], and initializes register R\[C] to 0. Then, it enters a loop that adds R\[B] to R\[C] and decrements R\[A] until R\[A] reaches 0. Finally, it stores the result in R\[C] and outputs it to stdout (M\[FF]) before halting the program. In other words, the program calculates the product of the two input numbers by iteratively adding the second number (R\[B]) to the sum (R\[C]) the number of times specified by the first number (R\[A]).



Typing 1s and 0s is undoubtedly cumbersome, but the primary issue lies not in the binary representation but in the lack of structure and human readability. The 1s and 0s can be converted to hexadecimal or ASCII, which makes the code more accessible, but it still lacks the structure and readability offered by high-level programming languages.

Typing 1s and 0s is undoubtedly cumbersome, but the primary issue lies not in the binary representation but in the lack of structure and human readability. The 1s and 0s can be converted to hexadecimal or ASCII, which makes the code more accessible, but it still lacks the structure and readability offered by high-level programming languages.

```
1000 1010 1111 1111 => 8AFF
1000 1011 1111 1111 => 47FF
0111 1100 0000 0000 => 7C00
0111 0001 0000 0001 => 7101
1100 1010 0001 1000 => CA18
0001 1100 1100 1011 => 1CCB
0010 1010 1010 0001 => 2AA1
1100 0001 0000 0100 => C104
1001 1100 1111 1111 => 9CFF
0000 0000 0000 0000 => 0000
```





## Assembly
