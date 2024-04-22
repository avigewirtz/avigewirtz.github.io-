# Preprocessing stage

* preprocessor performs two main things&#x20;

<figure><img src="../../.gitbook/assets/Frame 1.png" alt=""><figcaption><p>Figure 4.2: Preprocessing Stage. (Click image to enlarge)</p></figcaption></figure>

Frst, we see that the preprocessor removed all comments from testcircle.c and circle.c. Second, we see that each #include directive was replaced with the contents of its specified header. Namely, circle.h for circle.c and testcircle.c, and stdio.h and stdlib.h for testcircle.h. stdio.h and stdlib.h are system header files, containing declarations of library functions and definitions of macros. stdio.h contains the declaration of printf and scanf, and stdlib contains the declaration of exit and the the definition of the EXIT\_FAILURE macro. Finally, we see that all macros were expanded. PI in circle.,c was replaced with 3.14159, and EXIT\_FAILURE was replaced with 1.&#x20;



{% hint style="info" %}
Note: The preprocessor actaully performs a lot more work then shown here. The full task of the preprocessor is stages 1-4 of the compilation stages outlined by the C standard.&#x20;
{% endhint %}



Difference is that .c files contain code in the preprocessing laguage. Preprocessing language can be thought of as a subset of the C language.&#x20;

Critical to understand that input to preprocessor is C code, and output is also C code. The difference is that&#x20;



## Conditional compilation

## role of header files
