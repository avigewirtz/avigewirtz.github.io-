# Preprocessing stage

We can invoke the preprocessor alone by using the -E option:

```bash
gcc217 -E testcircle.c -o testcirle.i
gcc217 -E circle.c -o circle.i
```

The sequence of operations performed by the preprocessor is shown in Figure 4.2. Let's analytze each one-by-one, comparing the original code (testcircle.c and circle.c) with the preprocessed code (testcircle.i and circle.i).&#x20;

* First, the preprocessor removes all commends, repacing each one with whitespace.
*

<figure><img src="../../.gitbook/assets/Frame 1.png" alt=""><figcaption><p>Figure 4.2: Preprocessing Stage. (Click to enlarge)</p></figcaption></figure>

Frst, we see that the preprocessor removed all comments from testcircle.c and circle.c. Second, we see that each #include directive was replaced with the contents of its specified header. Namely, circle.h for circle.c and testcircle.c, and stdio.h and stdlib.h for testcircle.h. stdio.h and stdlib.h are system header files, containing declarations of library functions and definitions of macros. stdio.h contains the declaration of printf and scanf, and stdlib contains the declaration of exit and the the definition of the EXIT\_FAILURE macro. Finally, we see that all macros were expanded. PI in circle.,c was replaced with 3.14159, and EXIT\_FAILURE was replaced with 1.&#x20;
