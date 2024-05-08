# Introduction

GCC build programs in four sequential stages: preprocessing, compilaiton, assembly, and linking. The purpose of this chapter is to provide an overview of each stage of the process. It is not intended to be a general-purpose GCC tutorial. For further resources on GCC, refer to the [further reading](../copy-of-gnu-compiler-collection-gcc/further-reading.md) section at the end of this chapter.&#x20;

{% hint style="info" %}
**Note on Terminology**

In this chapter, we use the term "build" (as in "building a C program") to refer to the entire process (i.e., all four stages) of transforming a C program from source code to executable machine code. We use the term "compilation" to refer to step 2 of the build process specifically.&#x20;
{% endhint %}

