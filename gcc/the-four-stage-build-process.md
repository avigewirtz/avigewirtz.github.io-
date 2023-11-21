# The Four Stage Build Process

<figure><img src="../.gitbook/assets/Group 80.png" alt=""><figcaption></figcaption></figure>





### Compiling a simple C program&#x20;

Suppose we have a C program that computes the greatest common divisor (gcd) and least common multiple (lcm) of the integers 2 and 3. To keep things simple, we’ll avoid preproccessor directives or external dependencies.&#x20;

```c
int gcd(int i, int j) {
    int temp;
    while (j != 0) {
        temp = i % j;
        i = j;
        j = temp;
    } 
    return i;
} 

int lcm(int i, int j) {
    return (i / gcd(i, j)) * j;
}

int main(void) {
    gcd(2, 3);
    lcm(2, 3);
    return 0; 
}
```

We will assume that the source code is stored in a file called ‘intmath.c’.&#x20;

In order to make intmath.c execvutabe, we need to convert it to machine code, which is the only language the computer understands. To do this, we can invoke gcc217 like so:&#x20;

```bash
gcc217 intmath.c -o intmath
```

This compiles the source code in ‘intmath.c’ to machine code and stores it in an executable file ‘intmath’. The output file for the machine code is specified using the ‘-o’ option. This option is usually given as the last argument on the command line. If it is omitted, the output is written to a default file called ‘a.out’.&#x20;

Note that if a file with the same name as the executable file already exists in the current directory it will be overwritten.&#x20;

### Compiling multiple source files&#x20;

Suppose in the interest of modularity we want to split our program into two files. This makes it easier to understand and maintain, especially as our program grows larger. Suppose we try to split it up as follows: we keep the gcd and lcm functions in intmath.c, but we move the main method into a new file named testintmath.c. The idea is for intmath.c to contain the implementation of the gcd and lcm functions, while testintmain.c serves as a client of intmath.c. Now, our program looks like the following:&#x20;

intmath.c:

```c
int gcd(int i, int j) {
    int temp;
    while (j != 0) {
        temp = i % j;
        i = j;
        j = temp;
    } 
    return i;
} 

int lcm(int i, int j) {
    return (i / gcd(i, j)) * j;
}
```

testintmath.c:

```c
int gcd(int i, int j);
int lcm(int i, int j);

int main(void) {
    int greatest_common_divisor = gcd(2, 3);
    int least_common_multiple = lcm(2, 3);
    return 0; 
}
```



To compile out program, In order to understand why we had to add the function prototypes, we need to understand how compilation works in C.&#x20;

### Seperate Compilation

When multiple source files are passed to GCC to be compiled, GCC does not compile the source files as a single unit. That is, it does not combine the source code of all files into one file containing all the source code of the program and then compile that single source file into an executable. Instead, it compiles each source file seperately and stores each files corresponding machine code in an file called an object file. It then merges, or links, all the object files together to create an executable.&#x20;

Let's examine how this works with intmath.c and testintmath.c. Only after each source file has been compiled does it merge, or link, each files' corresponding machine code into one file, which can then be executed. This idea is shown in Figure X, which uses \
