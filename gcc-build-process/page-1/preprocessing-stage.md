# Preprocessing stage

As we mentioned earlier, the preprocessor performs two main tasks: It removes comments, which are of no use to the compiler, and handles preprocessor directives, which are lines in the code that begin with a #. Our program makes use of three types of preprocessor directives: `#include`, `#define`, and `#ifndef`/ `#endif`. These directives control file inclusion, macro definition, and conditional compilation respectively.

#### File inclusion

The `#include` directive instructs the preprocessor to grab the contents of a specified file and paste it directly into the current file where the `#include` directive appears. For example, in `testcircle.c`, the preprocessor replaces `#include <stdio.h>` with the contents of `stdio.h`, a system header file that contains, among other things, declarations of standard I/O functions such as `printf` and `scanf`.

{% hint style="info" %}
ASIDE BOX: #included files are typically header files, but technically any file can be included. 
{% endhint %}

{% hint style="info" %}
ASIDE BOX: There are two syntaxes for the `#include` directive: with angle brackets (e.g., `#include <stdio.h>`), and with double quotes (e.g., `#include "circle.h"`). The difference between these two lies in how the preprocessor searches for the specified file, with the precise details being implementation-defined. In general, files included with angle brackets are searched for in system directories only, while those included with double quotes are searched for in the working directory first.
{% endhint %}

#### Macro definition

The `#define` directive creates a preprocessor macro, which is essentially an alias for a specific value or code snippet. In circle.c, for example, `#define PI 3.14159` creates the macro `PI` and assigns it the value `3.14159`.  Whenever `PI` is subsequently used in `circle.c`, the preprocessor replaces it with `3.14159`.&#x20;

#### Conditional compilation

The #ifndef / #else directives, which we use in intmath.h, are part of a set of directives knows as conditional directives. These are used to control which parts of the source code are sent to the compiler. They are commonly used to prevent the contentd of a header file from being included twice in yhe same compilation unit.Here's how the #ifndef / #endif directives work in circle.h:

```
#ifndef CIRCLE_H
#define CIRCLE_H

double circleArea(double radius);

#endif
```

{% hint style="info" %}
ASIDE BOX: You can think of the preprocessor as a "search-and-replace" tool:

* It replaces each comment with a whitespace character.
* It replaces each `#include` directive with the contents of the specified file.
* It replaces each macro with its value.
{% endhint %}

### Examining `testcircle.i` and `circle.i`

You can examine the preprocessed files with a text editor. Let’s examine `testcircle.i` and `circle.i` to see what precisely was done by the preprocessor.

<figure><img src="../../.gitbook/assets/Group 19 (5).png" alt=""><figcaption></figcaption></figure>

First, we see that the preprocessor removed all comments from `testcircle.c` and `circle.c`. Second, we see that each `#include` directive was replaced with the contents of its specified header, namely `circle.h` for `circle.c` and `testcircle.c`, and `stdio.h` and `stdlib.h` for `testcircle.h`. `stdio.h` and `stdlib.h` are system header files, containing declarations of library functions and definitions of macros. `stdio.h` includes the declaration of `printf` and `scanf`, and `stdlib.h` includes the declaration of `exit` and the definition of the `EXIT_FAILURE` macro. Finally, we see that all macros were expanded: `PI` in `circle.c` was replaced with 3.14159, and `EXIT_FAILURE` was replaced with 1.
