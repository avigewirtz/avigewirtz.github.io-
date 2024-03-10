# Compilation Stage

The second stage involves compilation itself. Here, the compiler translates testcircle.i and circle.i into assembly-language, stored in testcircle.s and circle.s. Compilation is the most complex stage of the build process. It involves translating C source code into a completely different language. This is where the code is checked for errors. Figure 4.3 shows what the arm64 assembly looks like.&#x20;

<figure><img src="../../.gitbook/assets/Group 20 (5).png" alt=""><figcaption></figcaption></figure>

## Characteristics of Assembly Language

A detailed explanation of assembly language is beyond the scope of this chapter. You can find a high level-overview in appendix 8. Arm64 assemvly will be covered in detail in the second hald of the course. For now, we will simply provide a few general points about assembly: &#x20;

* Extremely low-level language. Essentially human readable verson of target processor's machine language. Typically a one-to-one mapping between assembly language instruction and machine language instruction.&#x20;
* Specific to target architecture. each architecture has it's own assembly language.
* Not portable. In simple terms, this means that if I gave you assembly language program written for an architecture like x86 and told you to run it on an architecture like ARM, you'd have a very hard time doing so.&#x20;
* architecture Because assembly is esssentially a human readable version of the target processors machine code, just like machine language isn't portable (i.e., machine language program written for for an X86 will not run on an ARM), assembly language isn't either portable. Meaning, assembly language written for x86 cannot be translated into machine languag einstruciton for arm. compiler knows which assembly language to compile to
