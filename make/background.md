# Motivation for Make

Imagine you working on a C project and you make changes to a few files. The next step is to rebuild your executable to see those changes take effect. If your project is on the smaller side, recompiling every source file is a simple and sensible approach. But, what if your project is much larger, say around 1000 source files? In that scenario, you wouldn't want to recompile every source file, since that would be extremely time-consuming and a drain on system resources. Thankfully, there's no need to go down that road. You can adopt a more efficient approach, recompiling only the files that were changed or affected by the changes.

In this chapter, we will focus on the most efficient approach of doing so--using a build system like make. To motivate your understanding of how make works and your appreictation for the benefits it offers, we will first go over how to do this maually, using basic gcc commmands.&#x20;

As an example, we will use the program shown in Figure 1, which consists of three source files: intmath.c, testintmath.c, and intmath.h. \


<figure><img src="../.gitbook/assets/Screenshot 2024-02-05 at 6.58.16 PM.png" alt=""><figcaption></figcaption></figure>

#### Manual approach to partial builds

