# Introduction

GCC build programs in four sequential stages: preprocessing, compilaiton, assembly, and linking. The purpose of this chapter is to provide an overview of each stage of the process. It is not intended to be a general-purpose GCC tutorial. For further resources on GCC, refer to the [further reading](../copy-of-gnu-compiler-collection-gcc/further-reading.md) section at the end of this chapter.&#x20;

{% hint style="info" %}
**Note on Terminology**

In this chapter, we use the term "build" (as in "building a C program") to refer to the entire process (i.e., all four stages) of transforming a C program from source code to executable machine code. We use the term "compilation" to refer to step 2 of the build process specifically.&#x20;
{% endhint %}

{% hint style="info" %}
**Aside: What is gcc217?**

In COS217, we use `gcc217` instead of `gcc`. It's important to understand that `gcc217` is not a different compiler; it is simply an [alias](../the-linux-command-line/useful-command-line-features/aliases.md) set up on Armlab for `gcc -Wall -Wextra -Wno-unused-parameter -ansi -pedantic`. In other words, when you invoke `gcc217`, you're really invoking `gcc` `-Wall` `-Wextra` `-Wno-unused-parameter -ansi -pedantic`. For details on what each option does, please refer to the GCC manpage.
{% endhint %}
