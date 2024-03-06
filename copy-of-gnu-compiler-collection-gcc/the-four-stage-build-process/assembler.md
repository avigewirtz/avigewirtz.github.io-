# Assembly Stage

The assembler translates testcircle.s and circle.s into relocateble object files testcircle.o and circle.o. These files are essentially machine code versions of testcircle.s and circle.s, but they are not executable. Testcircle.o is still missing the definition of calculateArea(), printf(), scanf(), and exit(), and circle.o does not contain a main() function.&#x20;

<figure><img src="../../.gitbook/assets/Group 26 (1).png" alt=""><figcaption></figcaption></figure>

At this point, the code is no longer human-readable. If you try to view the contents of the object files with a text editor, you’ll see plain gibberish, since the files are no longer text files. If you want to view the raw data, you can view it in binary using the xxd program the following commands:\


xxd -b main.o&#x20;

xxd -b circle.o

\
