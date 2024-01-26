# Phony targets

In a makefile, a rule's target is typically the name of a file that is to be built by the rule's command. For example, in the following rule:

```
intmath.o: intmath.c intmath.h
  gcc217 -c intmath.c
```

intmath.o represents a file, which is built when the command `gcc217 -c intmath.c` is executed.&#x20;

An interesting feature of make is that the target does not actually verify have to be the name of a file that is built by the rule's command. For example, we can create the following rule:

```
sayHello:
    echo "Hello there!"
```

even though sayHello does not represent a file that will be built via the rule's command, `echo "Hello there!"`. Thus, if we invoke:

```
make sayHello
```

make will check if the file "sayHello" exists, and since it won’t find it, it will execute the command `echo "hello there!"`, which prints "hello there!" on stdout. But because a file named sayHello will never be created by this rule, we can invoke

```
make sayHello
```

as many times as we like, and the effect will be that every time we invoke it, `echo "hello world"` will be executed. Targets that do not represent files are called _phony_ targets.&#x20;

## Common phony targets

There are three phony targets that are common in makefiles: all, clean, and clobber.&#x20;

all
