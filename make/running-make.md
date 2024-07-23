# Running make

The basic syntax to run `make` is:

```bash
make target
```

where `target` is the name of the file you want `make` to build (see, however, [phony targets](makefile-version-2-phony-targets.md)). If you omit a target, `make` defaults to the first target in the Makefile. In our case, that's `testintmath`. Thus, the command:

```bash
make
```

Is equivalent to:

```bash
make testintmath
```

If `testintmath` is either out of date or does not exist, `make` will execute the commands needed to bring `testintmath` up to date. By default, `make` prints each of the commands it executes. Say we run `make` when all targets are out of date or do not exist. The output will look like this:

```bash
$ make
gcc -c testintmath.c
gcc -c intmath.c
gcc testintmath.o intmath.o -o testintmath
$
```

If we run `make` again immediately afterward, it will detect that `testintmath` is up to date and not execute any commands:

```bash
$ make
make: `testintmath' is up to date.
$
```

{% hint style="info" %}
It's important to recognize that `make` does not read a Makefile from top to bottom, processing all rules within it. It starts with the first rule or the rule specified on the command line and then processes only the rules that are reachable from it. So, for example, if we run:

```bash
make intmath.o
```

make will process the rule for `intmath.o` only. It will not process the rules for `testintmath.o` or `testintmath`, since they are not reachable from it.
{% endhint %}
