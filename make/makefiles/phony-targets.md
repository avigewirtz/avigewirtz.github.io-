# Phony targets

In a makefile, a rule's target is typically the name of a file. For example, in rule three of our makefile:

```
intmath.o: intmath.c intmath.h
  gcc217 -c intmath.c
```

intmath.o represents a file, which is created (or updated) when the command `gcc217 -c intmath.c` is executed. We can trigger this rule by invoking:

```
make intmath.o
```

An interesting feature of make is that the target does not have to represent a file. For example, we can create the following rule:

```
sayHello:
    echo "Hello there!"
```

Where sayHello does not represent an existing file, nor would it be created via the rule's command, `echo "Hello there!"`. make will treat this like any other rule. Thus, if we invoke:

```
make sayHello
```

make will check if the file "sayHello" exists, and since it won’t find it, it will execute the command `echo "hello there!"`, which prints "hello there!" on stdout. But because a file named sayHello will never be created by this rule, we can invoke

```
make sayHello
```

as many times as we like, and the effect will be that every time we invoke it, `echo "hello world"` will be executed.&#x20;
