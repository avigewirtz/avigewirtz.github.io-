# How Information is Represented in Computers

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









Before we delve into the fundamental principles of how computers represent and process information, such as numbers and text, it’s useful to begin by revisiting how humans represent information.

Humans use a multitude of systems and symbols to represent information. Take, for example, our representation of numbers. The decimal or base-10 system, which is the most commonly used numerical system, employs ten unique symbols, or digits: 0 through 9. These digits can be combined in a myriad of ways to represent an infinite array of numerical values.

The value of a specific digit within a number is dependent on its position. For instance, in the number 345, the '3' is situated in the hundreds place, the '4' is in the tens place, and the '5' is in the ones place. Consequently, its value is expressed as 3_100 + 4_10 + 5\*1. This system is based on powers of ten, where each digit's position represents a power of ten (the rightmost digit is 10^0, the next one is 10^1, and so on). A generalized formula for this representation can be:

$$\text{Value} = \sum_{n=0}^{N} \text{Digit}_n \times 10^n$$

Here, Digit\_n refers to the digit at the nth position from the right and N is the total number of digits minus one.

Negative numbers are represented using a minus (-) symbol in front of the number. For example, -3 represents a value that is 3 less than 0.&#x20;

Fractions in decimal representation are written using a decimal point (.). Numbers to the left of the decimal point represent whole numbers, and numbers to the right of the decimal point represent fractions of a whole number. For example, the number 3.5 represents a value of 3 whole numbers and one half (or 0.5).

Likewise, consider how humans represent characters. The English language, for instance, utilizes 26 unique symbols—the alphabets—which can be combined to form words, sentences, and paragraphs, thereby representing and communicating vast amounts of information.

Interestingly, computers employ a similar approach to store data. However, instead of the decimal system used by humans, computers use a binary or base-2 system. This system uses just two symbols, traditionally denoted as 0 and 1.

In the binary system, we can represent the same information as in the decimal system; we just need more bits to do so. For example, the number 2 in decimal can be represented as 10 in binary.

While the decimal number system and the English alphabet are convenient for human communication, they are not optimal for the design and operation of computers. The essence of information representation in computers revolves around differentiating between two states, which can easily be signified by '0' (off state) and '1' (on state). The physical manifestation of these values can differ significantly depending on the technology in use. It could be a high or low electrical charge or voltage, different levels of light intensity, magnetization directions, or other physical properties or

\


































\
\


Interestingly, computers employ a similar approach to store data. However, unlike the decimal system used by humans, computers use a binary or base-2 system. This system uses just two symbols, traditionally denoted as 0 and 1.

\


In the binary system, we can represent the same information as in the decimal system, we just need more bits to do so. For example, the number 2 in decimal can be represented as 10 in binary.













\


While the decimal number system and the English alphabet are convenient for human communication, they are not optimal for the design and operation of computers.

The essence of information representation in computers revolves around differentiating between two states, which can easily be signified by '0' (off state) and '1' (on state). The physical manifestation of these values can differ significantly depending on the technology in use. It could be a high or low electrical charge or voltage, different levels of light intensity, magnetization directions, or other physical properties or phenomena.

\


The primary reason for computers using binary is that the most fundamental operations in computers are based on electrical states, which are most efficiently represented as binary (two-state) values: 'on' or 'off', represented by 1 and 0 respectively. As such, we use the binary system to represent information in computers. Each binary digit is a bit, which is the most basic unit of data in computing. All types of information that computers store and process -- whether numbers, text, images, audio, or video -- are represented in binary.

\
\
\


At first glance, it might seem hard to fathom how we can represent complex information with just two symbols, 0 and 1.&#x20;

\
\
\


Integers

\
\


Integers in binary can be represented in two ways: as unsigned integers and as signed integers. Unsigned integers are always positive and start from zero.

\
\
\
\


For example, the number 1234 can be broken down as:

1 \* 10^3 (1000) + 2 \* 10^2 (200) + 3 \* 10^1 (30) + 4 \* 10^0 (4)

Like the decimal system, the binary numeral system, or base-2 system, is also positional. However, it uses only two distinct digits: 0 and 1. This means every binary digit, or bit, can represent only two values, compared to ten for the decimal system. In the binary system, the rightmost digit represents units (2^0), the next represents twos (2^1), the next represents fours (2^2), and so on. For example, the binary number 1011 can be broken down as:

1 \* 2^3 (8) + 0 \* 2^2 (0) + 1 \* 2^1 (2) + 1 \* 2^0 (1)

Which is equivalent to the decimal number 11.

\
\
\
\
\
\
\
\


SIGN BIT METHOD:

\


The simplest way to denote negative integers in binary is by using the sign bit method. In this method, the leftmost bit is used to represent the sign of the number: '0' for positive and '1' for negative. The remaining bits are used to represent the magnitude (absolute value) of the number.

While this method is simple and intuitive, it has a significant drawback. It allows for a "positive zero" (0000) and a "negative zero" (1000), which can complicate calculations and result in inefficient usage of available bits.

\
\
\
\
\


* Ones complement: Another method is to flip all the bits of the positive number, which is called its one's complement. However, this has the disadvantage of having two representations for zero (0000 and 1111 for a 4-bit system).
* Twos complement: To solve the problem of one's complement, two's complement is used, which is obtained by adding one to the one's complement of the number. This is the most commonly used method to represent negative numbers in computers as it simplifies the hardware required for addition and subtraction.

\
\


Floating point:

\


Real numbers, or numbers with fractions, are typically represented in computers using a format known as floating-point representation. The IEEE 754 standard is a commonly used format for representing floating-point numbers. It includes three parts: the sign bit (which indicates whether the number is positive or negative), the exponent (which is used to multiply the fraction by a power of 2), and the mantissa or significand (which holds the actual fraction).

\
\
\


Character Encoding

Character encoding is the process of assigning a unique number to each character that a computer might need to handle: not just every letter in every case for every script, but also numerals, punctuation marks, common symbols, and control characters that do non-printing jobs like signaling the end of a line. The specific numbers that get assigned depend on the encoding scheme being used.

2.1 ASCII

One of the earliest and simplest encoding schemes is the American Standard Code for Information Interchange (ASCII). ASCII uses 7 bits to represent each character, which means it can define 2^7 or 128 unique characters. This was enough for every upper-case and lower-case letter in English, every digit, and a range of common punctuation and special characters. ASCII also included a number of control characters to handle tasks like carriage returns and line feeds.

2.2 Extended ASCII and ISO 8859

To provide for additional characters, several variations of ASCII extended the character size to 8 bits, allowing for 256 unique characters. These included several "Extended ASCII" sets that added graphics and line-drawing characters. Meanwhile, the ISO 8859 standard defined several different 8-bit character sets for different scripts including Latin scripts, Greek, Arabic, Hebrew, and others.

2.3 Unicode

ASCII and its 8-bit expansions quickly proved inadequate for the demands of global computing, which required handling many different scripts simultaneously and scripts with more than 256 characters like Chinese. The Unicode standard was developed to resolve this issue.

Unicode can represent over a million unique characters, which is enough to cover all modern scripts, a wide range of historic scripts, and a variety of symbols, including emoji. The first 128 characters of Unicode are the same as ASCII for compatibility.

3\. Encoding Unicode: UTF-8, UTF-16, and UTF-32

The challenge with Unicode is representing up to a million-plus characters in a way that's efficient for scripts that only use a few hundred. UTF-8, UTF-16, and UTF-32 are three common ways of doing this.

3.1 UTF-8

UTF-8 is a variable-length encoding that uses 8 bits (1 byte) for the first 128 characters for compatibility with ASCII, but can use up to 4 bytes for other characters. It's used extensively on the internet due to its backwards compatibility with ASCII and its efficiency with scripts that use Latin characters.

3.2 UTF-16

UTF-16 is also variable-length, and can use either 2 or 4 bytes to represent a character. It's more efficient than UTF-8 for scripts that use a larger number of characters, like Chinese, Japanese, and Korean.

3.3 UTF-32

UTF-32 uses 4 bytes for all characters. It has the advantage of simplicity, since every character uses the same amount of space, but is generally less space-efficient than UTF-8 or UTF-16.

\
\
\
\


<details>

<summary>A brief overview of how computers represent images, audio, and video</summary>

* Images: Images are represented as a matrix of pixels, where each pixel corresponds to a specific color. The color information is represented using various color models, such as RGB (Red, Green, Blue) or CMYK (Cyan, Magenta, Yellow, Key/Black). Each color channel is represented by a specific number of bits, which determines the range of color values that can be represented.

<!---->

* Audio: Audio data is typically represented as a continuous waveform, which is then sampled at regular intervals to create a digital representation. Each sample represents the amplitude of the waveform at a specific point in time, and the samples are stored using various audio formats and encoding techniques.

<!---->

* Video: Video data is essentially a sequence of images (frames) displayed over time. Each frame is represented using image data formats, and the sequence of frames is stored using various video encoding and compression techniques to reduce the file size while maintaining an acceptable level of quality.

</details>
