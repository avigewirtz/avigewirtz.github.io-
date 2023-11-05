# Background

When you're programming, you often need to perform tasks that many others have done many times before, like printing on stdout, calculating the square root of a number, or  . Instead of writing the code for these tasks from scratch every time, programming languages provide libraries, full of pre-written code for these common tasks. For example, consider this simple hello.c program, which prints "hello, world" to stdout:

```c
#include <stdio.h>

int main(void)
{
   printf("hello, world\n");
   return 0;
}
```

The printf() function is from the standard C library. Whenever we want to print to stdout we can simply call printf() rather than have to write the code from scratch.&#x20;

&#x20;
