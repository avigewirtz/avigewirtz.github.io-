# Introduction

In a nutshell, make is a software tool that automates the process of incremental builds. The key to understanding make is understanding what incremental builds are and how to implement it manually. Once you understand this, the mechanics and role of make become obvious.&#x20;

{% hint style="warning" %}
Before reading this chapter, ensure you're familiar with the GCC build process. An overview is provided in [GCC Build Process](broken-reference).
{% endhint %}



Incremental builds is an approach where each build builds off the previous one. The first time you build a program, you compile all of its source files. In subsequent builds, however, you compile only the source files that have changed since the last build or were affected by changes.

They key to implementing incremental builds is to always build a program in two steps. In the first step, you compile the source files into object files. This is done by invoking `gcc217` with the `-c` option. The caveat is that you only compile those source files that would produce object files different from those generated in the previous build. In the second step, you link all the object files (i.e., the "new" and "old" object files) together to produce the executable.&#x20;