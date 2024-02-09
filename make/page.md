# Page

Imagine you’re working on a C program consisting of 1000 source files and you make a change to just one file. You wouldn't want to recompile all 1000 files for this single change to take effect, as it would be extremely time-consuming. Instead, you’d want to recompile only the file you've updated. Thankfully, GCC (and other C compilers) enable you to do just that.&#x20;

To recompile a single file in GCC, you can use the following command:

```bash
gcc -c file.c
```

Where `file.c` is the name of the source file you have modified. This `-c` flag tells GCC to compile the source file into an object file (`.o`) but not to link it. This object file can then be linked with the other (unchanged) object files to create the final executable.

To link the object files together into the final executable, you would run:

```bash
gcc -o my_program *.o
```

Where `my_program` is the name you want to give to your compiled program. This step is necessary to create the final executable after recompiling only the changed source files.
