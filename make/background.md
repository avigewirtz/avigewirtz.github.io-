# Introduction

In a nutshell, `make` is a software tool that automates the process of incremental builds. The premise behind incremental builds is simple: when you rebuild your program after making a change to the source code, you rebuild only the affected files, not the entire program. This is especially important in large projects, where build times can become a bottleneck.

In this chapter, we'll first describe incremental builds and how to implement incremental builds manually. Then, we'll show how to automate the process with `make`.









* Consider two approaches to rebuilding testintmath after changes have been made to the source code. the first is&#x20;







Consdier the simplest appraoch to building testintmath. We simply run the following command:

```
gcc217 
```

In practice, however, this sort of command is rarely used for large projects, since it does not retain the intermediately generated object files.&#x20;
