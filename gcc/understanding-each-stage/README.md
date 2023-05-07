# Understanding each stage

## How Computers Store Data

Computers store data utilizing the binary system, a base-2 numeral system comprising only two digits: 0 and 1. All types of data, including numerical, text, image, audio, and video, are encoded as sequences of 1s and 0s.

{% hint style="info" %}
Now, the data is not physically observable 1s and 0s, these binary digits symbolize the underlying electrical or magnetic states of the computer's memory components. For instance, a memory cell may consist of a tiny capacitor and transistor. A charged capacitor represents a 1, while a discharged capacitor signifies a 0. Alternatively, magnetic polarities of magnetic material may denote binary digits, with one polarity corresponding to a 1 and the opposite polarity to a 0.



Here's a brief overview of how computers represent different types of data:

1. Numerical data:
   * Integers: Integers are represented using binary notation. Positive integers are represented using a straightforward binary conversion, while negative integers are typically represented using a method called Two's Complement.
   * Floating-point numbers: Real numbers or decimals are represented using a standard called the IEEE 754 floating-point standard. It consists of three parts: the sign, the exponent, and the mantissa (or significand), which collectively represent the number in a scientific notation-like format.
2. Text data: Text data is represented using character encoding standards such as ASCII (American Standard Code for Information Interchange) or Unicode. Each character in the text is assigned a unique binary code that the computer can interpret and display.
3. Image data: Images are represented as a matrix of pixels, where each pixel corresponds to a specific color. The color information is represented using various color models, such as RGB (Red, Green, Blue) or CMYK (Cyan, Magenta, Yellow, Key/Black). Each color channel is represented by a specific number of bits, which determines the range of color values that can be represented.
4. Audio data: Audio data is typically represented as a continuous waveform, which is then sampled at regular intervals to create a digital representation. Each sample represents the amplitude of the waveform at a specific point in time, and the samples are stored using various audio formats and encoding techniques.
5. Video data: Video data is essentially a sequence of images (frames) displayed over time. Each frame is represented using image data formats, and the sequence of frames is stored using various video encoding and compression techniques to reduce the file size while maintaining an acceptable level of quality.
{% endhint %}





You might be wondering how 0s and 1s can represent anything useful.&#x20;

To facilitate human understanding, data can be represented using familiar alphabets. One such representation is the extended ASCII, which utilizes 8 bits to represent each character, allowing for 256 characters. For example, the word "Hello" is represented as follows:

H: 01001000 e: 01100101 l: 01101100 l: 01101100 o: 01101111



ASCII can be used to encode text files in computers. However, these encoded text files are not directly executable by computers. Computers need instructions to be translated into machine code, the only language they inherently understand.

Machine code comprises sequences of 1s and 0s that correspond to specific instructions for the computer's processor. By converting human-readable programming languages into machine code, computers can execute instructions and perform tasks as required.

## Machine Code

Computers today do not inherently understand high-level programming languages such as C, Java, or any others. While these languages are more convenient for human comprehension, they are not directly executable by computers. Computer hardware is designed to implement a simple set of instructions, such as loading a value from memory into a register or adding two numbers and storing the result.

The specific set of instructions a computer can support is defined by its Instruction Set Architecture (ISA). An ISA is a specification that outlines the supported instructions, registers, memory organization, and addressing modes that a computer's processor can execute. The ISA serves as the lowest level software interface to the computer. All instructions must ultimately be translated into this form, as the computer cannot understand anything else.

An instruction is a command that directs the processor to perform a specific operation. Each instruction typically consists of an operation code (opcode) and operands. The opcode identifies the operation to be performed, while the operands provide the necessary data or memory addresses involved in the operation. Some ISAs use fixed-length instructions, with each instruction having the same number of bits, while others use variable-length instructions, where the number of bits can vary between instructions.

Programming in Machine Code: An Example

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
