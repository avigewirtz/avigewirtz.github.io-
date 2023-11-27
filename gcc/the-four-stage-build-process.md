# The Four Stage Build Process

###

The aim of this chapter is to describe in detail how GCC transforms source files to an executable file. Compilation is a multi-stage process&#x20;

### Overview of the compilation process

The sequence of stages executed by a single invocation of GCC consists of up to the following:

1. Preprocessing&#x20;
2. Compilation proper
3. Assembly
4. Linking

As an example, we will examine these compilation stages individually using the program ‘intmath.c’, which calculates the greatest common divisor (gcd) and least common multiple (lcm) of two integers:



**Build process**

The compilation of a C program actually involves four distinct stages: preprocessing, compilation proper, assembly, and linking. Show diagram of files. explain that while each of these are generated, they are by default discarded by GCC. Let's elaborate these four stages and examine them in relation to intmath.c.&#x20;

### Note on terminology

Compiling refers to the translating a language from one form into another. In&#x20;

<figure><img src="../.gitbook/assets/Group 81.png" alt=""><figcaption></figcaption></figure>
