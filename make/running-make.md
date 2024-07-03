# Running make

The general syntax to run `make` is:

```bash
make target
```

where `target` is the name of the file you want `make` to build. If you omit a target, `make` defaults to the first target in the makefile. In our case, that's `testintmath`. Thus, the command:

```bash
make
```

Is equivalent to:

```bash
make testintmath
```

In both cases, `make` will attempt to build `testintmath`. make prints on stdout each of the commands it executes to build the target. Say we're building our program for the first time. `make` will print and execute all three commands:

```bash
$ make
gcc -c testintmath.c
gcc -c intmath.c
gcc testintmath.o intmath.o -o testintmath
$
```

If we run `make` again immediately afterward, make will report that the target is up to date and not execute any commands:

```bash
$ make
make: `testintmath' is up to date.
$
```

It's important to recognize that `make` does not read a makefile from top to bottom, processing all rules within it. It starts with the first rule in the makefile or the rule specified on the command line and then processes only the rules that are reachable from it. So, for example, if we invoke:

```bash
make intmath.o
```

make will process the rule for `intmath.o` only. It will not process the rules for `testintmath.o` or `testintmath`.
