# Introduction

The purpose of this chapter is to provide an overview of the GCC four-stage build process--namely, preprocessing, compilation, assembly, and linking. It is not intended to be a general-purpose GCC tutorial. For further resources on GCC, refer to the [further reading](../copy-of-gnu-compiler-collection-gcc/further-reading.md) section at the end of this chapter.&#x20;

This tutorial assumes you have basic knowledge of C programming language and understand the role of header files. Further, it assumes mor you have familiarity with building single and multi-file C programs with GCC.&#x20;

In this chapter, we will explore the four-stage build process using a multi-file C program as an example. The reason is that in my opinion, this makes the role separate compilation more obvious. &#x20;



### Why it matters

\<Why you should know how build works>

**Clarification of terminology**

Before we begin, it's important to clarify some terminology. In this chapter, we use the term build (as in "building a C program") to refer to the entire process (i.e., all four stages) of transforming C source code into executable machine code. We use the term "compilation" to refer to step 2 of the build process specifically.&#x20;

#### gcc217

In COS217, we use `gcc217` is used instead of `gcc`. It's important to understand that `gcc217` isn't a different compiler; it's simply an 'alias' set up on armlab for `gcc -Wall -Wextra -Wno-unused-parameter -ansi -pedantic`. In other words, when you invoke `gcc217`, you're really invoking `gcc -Wall -Wextra -Wno-unused-parameter -ansi -pedantic`.&#x20;

Let's break down what each of these options does:

1. **`-Wall`**: This option tells `gcc` to show you all ("all") warning messages.&#x20;
2. **`-Wextra`**: This goes beyond `-Wall`, showing you even more warnings.&#x20;
3. **`-Wno-unused-parameter`**: Sometimes, you might write a function with parameters (pieces of information) that you end up not using. Normally, `gcc` would warn you about this, but this option tells it not to worry about unused parameters.
4. **`-ansi`**: This ensures your code sticks to the ANSI standard, which is a set of rules for how C code should be written.&#x20;
5. **`-pedantic`**: This makes `gcc` even stricter,&#x20;

####
