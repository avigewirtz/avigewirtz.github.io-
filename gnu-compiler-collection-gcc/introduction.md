# Introduction

<details>

<summary>Aside: gcc217</summary>

In COS217, `gcc217` is used instead of `gcc`. It's important to understand that `gcc217` isn't a different compiler; it's simply a shortcut, or an 'alias', set up on armlab to make your life easier. When you type `gcc217`, it's the same as typing gcc with the following options: `gcc -Wall -Wextra -Wno-unused-parameter -ansi -pedantic`. Let's break down what each of these options does:

1. **`-Wall`**: This option tells `gcc` to show you all ("all") warning messages.&#x20;
2. **`-Wextra`**: This goes beyond `-Wall`, showing you even more warnings.&#x20;
3. **`-Wno-unused-parameter`**: Sometimes, you might write a function with parameters (pieces of information) that you end up not using. Normally, `gcc` would warn you about this, but this option tells it not to worry about unused parameters.
4. **`-ansi`**: This ensures your code sticks to the ANSI standard, which is a set of rules for how C code should be written.&#x20;
5. **`-pedantic`**: This makes `gcc` even stricter,&#x20;

So, whenever you use `gcc217` on ArmLab, you're automatically including all these helpful settings. It's a way to make sure you're writing good, clean code and learning the best practices in programming!

</details>
