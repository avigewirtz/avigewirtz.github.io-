# Preprocessing Stage

In the first stage of the build process, testcircle.c and circle.c are sent to the preprocessor, which outputs testcircle.i and circle.i. The modifications are shown in Figure 2.&#x20;

<div data-full-width="true">

<figure><img src="../../.gitbook/assets/Group 19 (4).png" alt=""><figcaption></figcaption></figure>

</div>

Let's now examine the precise modifications the preprocessor makes by comparing testcircle.i and circle.i with testcircle.c and circle.c.&#x20;

* **Comments Removal.** First, we see that testcircle.i and circle.i do not contain comments. All comments in circle.c and testcircle.c were removed.
* **File Inclusion**. Second, we see that the preprocessor fetched the header files specified via #include directives in testcircle.c and circle.c and added their contents in the place where their their include directives appeared. In testcircle.i, we see the contents of the stdio.h, stdlib.h, and circle.h in the place where their directives appeared. Note that stdio and stdlib.h are large files, so we only show the relevant parts. For circle.c, the preprocessor inserted the contents of circle.h.&#x20;
* **Macro expansion**. Finally, we see that all macros have been expanded. PI in circle.c was replaced with 3.14159, and EXIT\_FAILURE in testcircle.c was replaced with 1. EXIT\_FAILURE is a macro defined in stdlib.h.
