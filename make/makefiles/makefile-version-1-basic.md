# Writing a Makefile

makefile contain sytanx for rules.

Next, we populate the Makefile with a textual representation of `testintmath`'s dependency graph. This consists of a _dependency rule_ for each object file (`intmath.o`, `testintmath.o`) and for the executable (`testintmath`). A dependency rule has the following syntax:

```
target: dependencies
<tab> command
```

* **Target**: The file you want to build (e.g., `testintmath`).
* **Dependencies**: The files that the target _directly_ depends on (e.g., `intmath.o`, `testintmath.o`).
* **Command**: The command to build the target (e.g., `gcc217 intmath.o testintmath.o -o testintmath`). **Note:** The command must be preceded by a tab.

In our case, we create three dependency rules: one for `testintmath`, one for `testintmath.o`, and one for `intmath.o`. Figuring our which files each of these targets directly depends on can sometimes be challenging, but with our dependency graph, the dependencies are obvious:

* `testintmath` directly depends on `testintmath.o` and `intmath.o`
* `testintmath.o` directly depends on `tetsintmath.c` and `intmath.h`
* `intmath.o` directly depends on `intmath.c` and `intmath.h`

This results in the following makefile:

```makefile
testintmath: testintmath.o intmath.o
    gcc217 testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc217 -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc217 -c intmath.c
```

## Running our makefile

The general syntax to run a makefile is:

```bash
make target
```

If you omit a target, `make` defaults to the first target in the makefile.&#x20;

To build `testintmath`, we can invoke `make` without arguments and it'll default to `testintmath`, since `testintmath` is the first target in our makefile:

```bash
make
```

If we wanted to build `intmath.o` alone, we'd invoke:

```bash
make intmath.o
```

{% hint style="info" %}
`make` does not read a makefile from top to bottom, processing all rules within it. It starts with the default rule or the rule specified on the command line, and then processes only the rules that are reachable from it.&#x20;
{% endhint %}
