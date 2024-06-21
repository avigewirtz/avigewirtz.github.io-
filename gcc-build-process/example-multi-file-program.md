# Example: Multi-file Program

Until now, the source code of our program was contained within a single file. As we know, the source code of a C program may be distributed across any number of files. Suppose we divide our program into two `.c` files, `foo.c`, and `bar.c`. We build our program by supplying both files as arguments to `gcc217`:

```bash
gcc217 foo.c bar.c -o foobar
```



The sequence of operations performed by `gcc` is summarized in Figure 12. The critical point to recognize here is that the first three stages of the build process (i.e., preprocessing, compilation, and assembly) are performed on each file independently. Thus, definitions in foo.\* are not visible to the compiler when its processing bar.\*, and vice versa. Here too, the definitions are resolved at link time.

<figure><img src="../.gitbook/assets/Frame 29.png" alt=""><figcaption></figcaption></figure>
