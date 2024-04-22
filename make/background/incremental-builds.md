# Incremental builds

Incremental builds is an approach where each build builds off the previous one. The first time you build a program you build the entire thing, but in subsequent build you only rebuild parts that have been affected by changes.

They key to implementing incremental builds is to always build a program in two steps: In the first step, each of the files is translated into an object file. In the second step, each of the .o files is linked to produce the executable.&#x20;

When building a program, you only rebuild the .o files that have been affected by changes in the source code, and then link all the .o files together to generate the executable.&#x20;
