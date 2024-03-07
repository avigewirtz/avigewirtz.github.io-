# Assembly Stage

The assembler translates the assembly-language in testcircle.s and circle.s into machine language, storing the results in testcircle.o and circle.o. Machine language consists of binary (1s and 0s) instructions that  --instructions in sequences of 1s and 0s that the CPU "understands." The machine languagecan storing them in testcircle.o and circle.o. At this point, changes from text file to binary file. To view them, you cannot use a text editor like, since the files are not text files.&#x20;

<figure><img src="../../.gitbook/assets/Group 26 (1).png" alt=""><figcaption></figcaption></figure>

Although each of these files contains machine code, theyre they are not executable. testcircle.o is still missing the definitions of calculateArea(), printf(), scanf(), and exit(), and circle.o does not contain a main() function.&#x20;
