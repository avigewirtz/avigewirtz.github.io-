# Makefiles

A makefile is essentially a textual representation of a dependency graph.  It consists of rules. A rule typically has the following syntax:

```
target: dependencies
<tab> command
```

In most cases, target is the file that the rule builds, dependencies are the files needed to build the target, and command is the command that make will execute to build the target.  For example, in the following rule:

```
intmath.o: intmath.c intmath.h
  gcc217 -c intmath.c
```

the target is intmath.o, the command is gcc217 -c intmath.c, and the dependencies...

{% hint style="danger" %}
One of the most common errors in writing Makefiles is prefixing the command with spaces (ASCII character 32) instead of a tab (ASCII character 9). This can happen when editing a Makefile in a text editor that automatically converts tabs to spaces. This will lead to the following error:

```
   *** missing separator.  Stop.
```
{% endhint %}

Here’s a simple makefile for our testintmath program:

{% code title="makefile" lineNumbers="true" %}
```makefile
testintmath: testintmath.o intmath.o
  gcc217 testintmath.o intmath.o –o testintmath
  
testintmath.o: testintmath.c intmath.h
  gcc217 -c testintmath.c
  
intmath.o: intmath.c intmath.h
  gcc217 -c intmath.c
```
{% endcode %}







Let's go over the first rule in our makefile detail. &#x20;

{% code title="Rule 1" %}
```make
testintmath: testintmath.o intmath.o
    gcc217 testintmath.o intmath.o -o testintmath
```
{% endcode %}

* **Target**: `testintmath`
* **Dependencies**: `testintmath.o`, `intmath.o`
* **Command**: `gcc217 testintmath.o intmath.o -o testintmath`

This rule states that the executable `testintmath` depends on two object files: `testintmath.o` and `intmath.o`. The command on will be triggered if either `testintmath.o` or `intmath.o` is newer than `testintmath`, or if `testintmath` does not exist.



<figure><img src="../../.gitbook/assets/Screenshot 2024-01-25 at 7.23.18 PM (2).png" alt=""><figcaption></figcaption></figure>

\
