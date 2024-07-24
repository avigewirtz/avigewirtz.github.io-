# Running make

With the Makefile set up, you can now build `testintmath` using `make`. The basic syntax to run make is:

```makefile
make target
```

where `target` is the name of the file you want `make` to build (see, however, [phony targets](makefile-version-2-phony-targets.md)). If you omit a target, make defaults to the first target in the Makefile, which in our case is `testintmath`. Therefore, you can build `testintmath` by simply running:

```bash
make
```

If `testintmath` is already up-to-date, make will simply report that fact and halt. Otherwise, it will execute the necessary commands to bring `testintmath` up-to-date. By default, `make` prints the commands it executes on stdout. Let's examine the behavior of `make` with our newly created Makefile.&#x20;

Assume we're building `testintmath` for the first time. Running make, you should see the following output:

```bash
$ make
gcc -c testintmath.c
gcc -c intmath.c
gcc testintmath.o intmath.o -o testintmath
$
```

Observe that `make` compiles both source files into object files, then links them to create the `testintmath` executable.&#x20;

Now, let's run `make` again immediately afterward:

```bash
$ make
make: 'testintmath' is up to date.
$
```

`make` detects that no files have been modified since the last build, so no action is necessary.&#x20;

Next, let's "modify" `intmath.c`. We can do this by running:&#x20;

```bash
$ touch intmath.c
```

The `touch` command updates the file's "last modified" timestamp without changing its contents. This simulates the effect of modifying the file. Running make:

```bash
$ make
gcc -c intmath.c
gcc testintmath.o intmath.o -o testintmath
$
```

Observe that `make` recompiles only`intmath.c` and relinks the executable. It doesn't recompile `testintmath.c` as it hasn't been modified.

Now, let's simulate a change to the header file:

```bash
$ touch intmath.h
$ make
gcc -c testintmath.c
gcc -c intmath.c
gcc testintmath.o intmath.o -o testintmath
$
```

In this case, `make` recompiles both source files. This is because both include `intmath.h`, so changes to the header file necessitate recompilation of all dependent source files.

{% hint style="info" %}
It's important to recognize that `make` does not read a Makefile from top to bottom, processing all rules within it. It starts with the default rule or the rule specified on the command line and then processes only the rules that are reachable from it. So, for example, if we run:

```bash
make intmath.o
```

make will process the rule for `intmath.o` only. It will not process the rules for `testintmath.o` or `testintmath`, since they are not reachable from it.
{% endhint %}

#### Useful Command Line Options

