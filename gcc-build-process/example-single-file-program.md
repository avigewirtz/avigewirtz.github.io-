# Example: Single-file Program

Let's now examine four stage process using a real program as an example.&#x20;

{% code title="charcount.c" %}
```c
#include <stdio.h>
/* Write to stdout the number of
 chars in stdin. Return 0. */
int main(void) {
 int c;
 int charCount = 0;
 c = getchar();
 while (c != EOF) {
 charCount++;
 c = getchar();
 }
 printf("%d\n", charCount);
 return 0;
}
```
{% endcode %}

### Preprocessing Stage

The build process begins with preprocessing. We invoke the preprocessor on `charcount.c` with the -E option:

```bash
gcc217 -E charcount.c -o charcount.i
```

The result is the preprocessed file `charcount.i`. As we mentioned earlier, the preprocessor performs two main tasks: It removes comments, which are of no use to the compiler, and handles preprocessor directives (lines in the code that begin with a `#`). Our code has only a single preprocessor directive: `#include <stdio.h>`. This instructs the preprocessor to grab the contents of `stdio.h` and paste it directly into the current file where the `#include` directive appears. stdio.h is a big file, containing somewhere on the order of 1000 lines. It contains declarations of standard I/O functions, such as printf.&#x20;

```c
int printf(const char *format, ...);
```

Additionally, it contains many preprocessor macros of it's own, all of which are now added to our program. Of note is the following preprocessor directive:

```c
#define EOF -1
```

#### Examining Preprocessed Output

You can view the preprocessed files with a text editor like emacs. Let’s examine `testcircle.i` and `circle.i` to see what precisely was done by the preprocessor. A side-by-side comparison is shown in Figure 12.

First, we see that the preprocessor removed all comments from `testcircle.c` and `circle.c`. Second, it replaced each `#include` directive with the contents of its specified header: `circle.h` for both `circle.c` and `testcircle.c`, and `stdio.h` and `stdlib.h` for `testcircle.c`. Finally, all macros were expanded: `PI` in `circle.c` was replaced with `3.14159`, and `EXIT_FAILURE` was replaced with `1`.

{% hint style="success" %}
You can think of the preprocessor as a "search-and-replace" tool:

* It replaces each comment with a whitespace character.
* It replaces each `#include` directive with the contents of the specified file.
* It replaces each macro with its value.
{% endhint %}

{% hint style="info" %}
**Understanding the Role of Header Files**

Our program uses the printf function, which is not defined anuywhere in our source code. The definition of printf will be inserted by the linker, which operates in the last stage of the build process. This means that during the first three phases of the build process, the definition of `printf` is not known.

This scheme, in which externally defined functions like `printf` are inserted into the program at the end of the build process, has many benefits – most notably, it saves us the time of having to recompile printf every time we use it. However, this scheme does present a challenge. One of the compiler's jobs is to type-check function calls, ensuring they are called with the correct number and types of arguments and return the correct type. Without access to the printf definition, how does the compiler obtain this information?

The solution is that we insert the declaration of printf into our program before compilation begins. The declaration for printf is: \<fll in>.This specifies its function's name, return type, and the number and types of its arguments. It's a way of informing the compiler, "\<fill in." This enables the compiler to generate correct code for function calls and detect potential errors even without the function definition.&#x20;

In the early days of C, before the preprocessor existed, programmers had to manually insert the signatures of any externally defined functions their program used. As you can imagine, this was tedious and error-prone. For example, if your program used 20 externally defined functions, you would have to add all their declarations at the top of your file. Worse yet, if one of them changed and you didn't update it, subtle and hard-to-find runtime errors could occur.

The solution was to adopt a file-inclusion mechanism. In this scheme, related declarations are bundled into a header file. For example, all standard I/O functions are bundled into the header file `stdio.h`. Now, to use I/O library functions, you simply `#include <stdio.h>` in your file, rather than manually adding all the relevant declarations. If any of the declarations in `stdio.h` change, the updated information will be automatically added to your file the next time it's compiled. If any of the updates cause an error, it will be caught at compile time rather than runtime.
{% endhint %}







