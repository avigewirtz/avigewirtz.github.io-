# Introduction

The purpose of this chapter is to provide an overview of the GCC build process--namely, preprocessing, compilation, assembly, and linking. It is not intended to be a general-purpose GCC tutorial. For further resources on GCC, refer to the [further reading](../copy-of-gnu-compiler-collection-gcc/further-reading.md) section at the end of this chapter.&#x20;

This tutorial assumes you have basic knowledge of the C programming language and understand the role of header files.

To illustrate the build process, we will follow the journey of a multi-file C program from source code to executable.

### It Pays to Understand How the Build Process Works

\<fill in>

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
