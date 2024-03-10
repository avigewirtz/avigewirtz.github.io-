# Linking Stage

Our program is currently distributed across two files: testcircle.o and circle.o. While both of these files contain machine code, neither of them is executable on its own. `circle.o` lacks a `main` function, and `testcircle.o` contains references to four external functions: `calculateArea`  (defined in circle.o), and `printf`, `scanf`, and `exit` (defined in C Standard Library).

To produce an executable file, the linker combines all these files--testcircle.o, circle.o, and C library--together, resolving all external references in our program. The output is the executable file testcircle. This process is shown in Figure 6.&#x20;

<figure><img src="../../.gitbook/assets/Group 28 (3).png" alt=""><figcaption></figcaption></figure>

