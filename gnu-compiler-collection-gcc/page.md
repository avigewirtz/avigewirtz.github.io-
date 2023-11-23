# Page

### Outline:

* In early stages of learning C, programs are typically lmited to a single source file. However, as programs grow larger, it's a good idea to split up the program into multiple source files. Making your program modular makes it easier to understand and maintain. Besides for making your program easier to understand&#x20;

### Compiling multiple source files&#x20;

Suppose in the interest of modularity, we want to split our program into two files. This makes it easier to understand and maintain, especially as our program grows larger.&#x20;

Suppose we try to split it up as follows: we keep the gcd and lcm functions in intmath.c, but we move the main method into a new file named testintmath.c. The idea is for intmath.c to contain the implementation of the gcd and lcm functions, while testintmain.c serves as a client of intmath.c. However, splitting the program requires us to add prototypes for the gcd and lcm functions to testintmath.c. Now, our program looks like the following:&#x20;

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



To compile out program, we invoke gcc217 with intmath.c and testintmath.c, like so:

```
gcc217 intmath.c testintmath.c -o intmath
```

Which will generate an executable named intmath. In order to understand why we had to add the function prototypes, we need to understand how the compilation process works in C.&#x20;

### Seperate Compilation

When multiple source files are passed to GCC to be compiled, GCC does not compile the source files as a single unit. That is, it does not combine the source code of all files into one file and then compile that file into an executable. Instead, it compiles each source file _seperately_ into and stores each files corresponding machine code in an _object file_ with the same name as the source file but with a .o extension_._ Object files contain machine code, but they are not executable, since (1) they need not contain a main method; and (2) they may contain references to external functions or variables.  is essentially a machine code version of the corresponding source file, but its not execcutable, since (1) it contains references to functions or variables defined in other object files and need not contain a main method.  It then merges, or links, all the object files together to create an executable. This idea is demonstrating in Figure X using intmath.c and testintmath.c.&#x20;
