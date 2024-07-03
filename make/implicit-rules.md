# Final Word

#### Implicit Rules

Much of the information we entered in our dependency rules can in fact be inferred by make. Consider the following rule, for example:

```makefile
intmath.o: intmath.c intmath.h
    $(CC) $(CFLAGS) -c intmath.c
```

make can infer from the target name, intmath.o, that one of its dependencies is intmath.c. Further, it can infer that the command to build intmath.o is depends on 
