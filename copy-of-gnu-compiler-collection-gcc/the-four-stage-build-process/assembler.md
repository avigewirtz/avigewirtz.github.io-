# Assembly Stage

The third stage in the compilation process is assembly. In this stage, the assembler translates the assembly language instructions into machine language instructions. Machine language is the native language of the processor–that is, the \


Main.c and circle.c will be stored in main.o and circle.o. \


At this point, the code is no longer human-readable. If you try to view the contents of the object files with a text editor, you’ll see plain gibberish, since the files are no longer text files. If you want to view the raw data, you can view it in binary with the following commands:

\


xxd -b main.o&#x20;

xxd -b circle.o

\
\


Explain why the object files aren’t executable.&#x20;
