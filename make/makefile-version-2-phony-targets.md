# Phony targets

In `make`, a target typically represents a file that is built when its corresponding command is run. However, Make has no verification mechanism to check whether the target file was actually built by the command. Instead, it operates under the assumption that if a target's command is successfully run, the target is up-to-date. This is not a bug in make but a a deliberate design choice, as it enables the use of so-called _phony_ targets—targets that are not intended to correspond to actual files but instead represent labels for commands or actions that `make` should execute.&#x20;

Phony targets are easiest to illustrate by means of an example, so let's jump right into makefile version 2, shown below, which contains three commonly used phony targets:  `all`, `clean`, and `clobber`. Don't worry for now how they work. We'll go over each one by one.&#x20;

{% code title="makefile version 2" %}
```makefile
# Dependency rules for non-file targets

.PHONY: all clean clobber
# Default target (i.e., target to use when make is invoked without specifying a target)
all: testintmath
  
# Deletes all object files (.o) and the executable 
clean:
  rm -f testintmath *.o
  
# Extends clean by also deleting Emacs backup and autosave files ('*~' specifies 
# all files that end with a '~', and '\#*\#' specifies all files that start and end with a '#')
clobber: clean
  rm -f *~ \#*\# 
  
# Dependency rules for file targets
testintmath: testintmath.o intmath.o
  gcc testintmath.o intmath.o –o testintmath
  
testintmath.o: testintmath.c intmath.h
  gcc -c testintmath.c
  
intmath.o: intmath.c intmath.h
  gcc -c intmath.c
```
{% endcode %}





{% hint style="info" %}
**Purpose of the 'all' target**

You might be wondering what purpose the `all` target serves in our program compared to simply using `testintmath` as the default target. Truthfully, it doesn't serve any real purpose, except perhaps for accommodating users who might invoke `make all` out of habit.

The real purpose of `all` is to group multiple independent targets and effectively make them all default targets. For example, suppose we have a project with two executables:`hello1` and `hello2`. Making `hello1` and `hello2` dependencies of `all` effectively makes them both default targets (which will be triggered when we run `make`).

```makefile
all: hello1 hello2

hello1: hello1.o
	gcc hello1.o -o hello1
	
hello2: hello2.o
	gcc hello2.o -o hello2

hello1.o: hello1.c
	gcc -c hello1.c

hello2.o: hello2.c
	gcc -c hello2.c
```
{% endhint %}





#### .PHONY Directive

It should go without saying that this scheme only works if there is in fact never a file named `hello` in the working directory. If there is such a file, it will always be considered up to date, and running `make hello` will always yield:

```makefile
$ make hello
make: `hello' is up to date.
$
```

GNU Make offers a simple solution to guard against this potential issue. Just declare `hello` to be phony, like so:

```makefile
.PHONY: hello
```

With this declaration, `make hello` will always run the specified command, even if there is a file named `hello`.
