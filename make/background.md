# Introduction

In a nutshell, `make` is a software tool that automates the process of incremental builds. The premise behind incremental builds is simple: when you rebuild your program after making a change to the source code, you rebuild only the affected files, not the entire program. This is especially important in large projects, where build times can become a bottleneck.

In this chapter, we'll first describe how incremental builds work in C. Then, we'll show how to automate the process with `make`.
