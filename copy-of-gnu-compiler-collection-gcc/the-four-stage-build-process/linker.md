---
description: "\x1A1"
---

# Linking Stage

}/

Although each of these files contains machine code, theyre they are not executable. testcircle.o is still missing the definitions of calculateArea(), printf(), scanf(), and exit(), and circle.o does not contain a main() function. &#x20;





<figure><img src="../../.gitbook/assets/Group 28 (3).png" alt=""><figcaption></figcaption></figure>













The final stage is linking. The object code from `intmath.c` is not yet a complete executable program. It requires linking with other object files and libraries. For example, the standard I/O functions utilized in `intmath.c` are part of external libraries that need to be connected with our program. The linking stage amalgamates the object code with these necessary libraries to create the final executable.

We will assume that the source code is stored in a file called ‘intmath.c’.&#x20;

In order to make intmath.c executabe, we need to convert it to machine code, which is the only language the computer understands. To do this, we can invoke gcc217 like so:&#x20;

```bash
gcc217 intmath.c -o intmath
```

This compiles the source code in ‘intmath.c’ to machine code and stores it in an executable file ‘intmath’. The output file for the machine code is specified using the ‘-o’ option. This option is usually given as the last argument on the command line. If it is omitted, the output is written to a default file called ‘a.out’.&#x20;

Note that if a file with the same name as the executable file already exists in the current directory it will be overwritten.&#x20;

