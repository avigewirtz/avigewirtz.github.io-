# Running make

The general syntax to run `make` is:

```bash
make target
```

where `target` is the name of the target in your Makefile that you want `make` to build. If you omit a target, `make` defaults to the first target in the makefile. In our case, that's `testintmath`. Thus, the command:

```bash
make
```

Is equivalent to:

```bash
make testintmath
```

In both cases, `make` will attempt to build `testintmath`. If `testintmath` is either out of date or does not exist, `make` will execute and display each command it runs to build it. Say we run `make` when all targets are out of date or do not exist. The output will look like this:

```bash
$ make
gcc217 -c testintmath.c
gcc217 -c intmath.c
gcc217 testintmath.o intmath.o -o testintmath
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
