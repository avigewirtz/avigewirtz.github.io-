# Introduction

_Building_ a C program refers to the process of transforming it from one or more source files into a single file that can be loaded into memory and executed. GCC builds C programs in four sequential stages: preprocessing, compilation, assembly, and linking. The goal of this chapter is to provide an overview of of each of these stages. It is not intended to be a general-purpose GCC tutorial. For more resources on GCC, please refer to the [further reading](../copy-of-gnu-compiler-collection-gcc/further-reading.md) section at the end of this chapter.

{% hint style="info" %}
**Note on Terminology**

In this chapter, I use the term "build" (as in "building a C program") to refer to the entire process (i.e., all four stages) of transforming a C program from source code to executable. I use the term "compilation" to refer specifically to step 2 of the build process.
{% endhint %}

{% hint style="info" %}
**What is gcc217?**

In COS217, we use `gcc217` instead of `gcc`. It's important to understand that `gcc217` is not a different compiler; it is simply a shell [alias](../the-linux-command-line/useful-command-line-features.md#aliases) on Armlab for `gcc -Wall -Wextra -Wno-unused-parameter -ansi -pedantic`. In other words, when you invoke `gcc217`, you're really invoking `gcc -Wall -Wextra -Wno-unused-parameter -ansi -pedantic`. For details on what each option does, please refer to the `gcc` manpage.
{% endhint %}
