# Writing a Makefile

As mentioned earlier, a makefile is essentially a textual representation of a dependency graph. The transition from a dependency graph to a Makefile is quite straightforward. Let's demonstrate how to write a makefile for testintmath, whose dependency graph is shown below.&#x20;



<figure><img src="../../.gitbook/assets/Group 28 (1).png" alt="" width="563"><figcaption><p>Figure 6: testintmath dependency graph</p></figcaption></figure>

Create what is known as a "dependency rule" for each object file (intmath.o and testintmath.o) and for the executable (testintmath). A dependency rule has the following syntax:

```
target: dependencies
<tab> command
```

* **Target**: the file you want to build.
* **Dependencies**: the files that the target directly depends on.
* **Command**: the command to build the target

In our case, we have that results in a makefile with the following three rules: one for testintmath, one for intmath.o, and one for testintmath.o. With the dependency graph, it's very easy to see which files these targets directly depend on:

* testintmath directly depends on intmath.o and testintmath.o
* intmath.o dircetly depends on intmath.c and intmath.h
* testintmath.o directly depends on testintmath.c and intmath.h

This leads to the following makefile:

```makefile
testintmath: testintmath.o intmath.o
    gcc217 testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc217 -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc217 -c intmath.c
```

{% hint style="success" %}
### Comments

In a Makefile, everything following the `#` symbol on a line is treated as a comment:

```makefile
# This is a comment
```
{% endhint %}

## Running our makefile

type make&#x20;

make will look for file named xyz and begin at first target

if we want make to begin a specific target, invoke make followed by target name
