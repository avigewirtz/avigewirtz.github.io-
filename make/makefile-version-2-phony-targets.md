# Phony Targets

Make's job is to bring targets up-to-date. Until now, we've assumed that targets represent files, which are brought up-to-date by creating them or updating them. In fact, however, targets need not represent files. They can represent labels for arbitrary commands or actions you want make to execute. Such targets are known as _phony_ targets.

Consider the following rule:

```makefile
clean: 
    rm -rf testintmath *.o
```

The target, clean, does not represent a file—that is, there is no file in our project directory named `clean`, and the command `rm -rf testintmath *.o` does not create such a file. Quite the contrary. This command deletes `testintmath` and the object files (`.o`). This is useful in situations where you want you rebuild `testintmath` from scratch.

If we were to add this rule to our makefile and invoke `make clean`, the effect is that `rm -f *.o testintmath` will be executed, thereby "cleaning" the project directory:

```bash
$ make clean
rm -f *.o testintmath 
$
```

(Note that the name `clean` isn't special. We could have given the rule a different name, such as `cleanup`. `Clean` is simply the conventional name for this kind of task in Makefiles)

`make` implements phony targets in a rather simple manner. After a rule is processed, `make` has no postcondition check to verify that the target was in fact built. Instead, it operates under the assumption that if a target's dependencies (if any) are satisfied and its commands (if any) are successfully run, the target is up-to-date. In the `clean` example, because the command `rm -rf testintmath *.o` executed successfully (i.e., returned exit status 0), `make` considers `clean` to be up-to-date (for the current invocation of `make`, that is). It does not actually verify whether `clean` is created.

You can see the underlying process by which make processes `clean` by invoking this rule with the `debug=-v` option. Here is the relevant part of the output:

```
$ make clean --debug=v
Considering target file `clean'.
 File `clean' does not exist.
 Finished prerequisites of target file `clean'.
Must remake target `clean'.
rm -f testintmath *.o
Successfully remade target file `clean'.
$ 
```

In particular, notice how after executing the command `rm -f testintmath *.o`, `make` reports that it ``Successfully remade target file `clean'``. This should convince you that `make` really &#x20;

{% hint style="warning" %}


**.PHONY Directive**

It should go without saying that the scheme we just described will only work if there is in fact no file named `clean` in the working directory. If such a file exists, `make clean` will always yield:

```makefile
$ make clean
make: `clean' is up to date.
$
```

GNU Make offers a simple solution to this potential naming conflict. Llist `clean` as a dependency of the special target `.PHONY`, like so:

```makefile
.PHONY: clean
clean: 
    rm -f *.o testintmath 
```

With this declaration, this rule will work as intended even if there is a file named `clean` in the working directory.
{% endhint %}

#### Phony Targets Use Cases

Phony targets have two canonical use cases:

* As a label for one or more arbitrary commands you want `mak`e to execute. In the previous example, clean was used as a label for the command `rm -rf testintmath *.o`
* As an alias for one or more other targets, such that running the phony target is the same as running the target(s) directly.

Our makefile doesn't lend itself well to the second use case, so the examples that follow will be somewhat contrived.

Suppose you often want to build the object files but not link them. You could invoke:

```
make testintmath.o intmath.o
```

And this will get the job done, but typing this out every time is annoying. Alternatively, you could add a rule like the following to our makefile:

```
obj: testintmath.o intmath.o
```

Now, you can build both testintmath.o and intmath.o by simple invoking:

```
make obj
```

Essentially, obj serves as an alias for testintmath.o and intmath.o, enabling us to group theser two independent targets together. explain how rule is processed



Another use case of an alias phony target is for a really long or hard to type target.&#x20;



#### Makefile version 2

Makefile version 2, which contains three commonly used phony targets: `all`, `clean`, and `clobber`. Don't worry for now how they work. We'll go over each one in detail.

{% code title="Makefile version 2" %}
```makefile
# Dependency rules for non-file targets

# Default target (i.e., target to use when make is invoked without specifying a target)
all: testintmath
  
# Deletes all object files (.o) and the executable 
clean:
  rm -f testintmath *.o
  
# Extends clean by also deleting Emacs backup and autosave files ('*~' specifies 
# all files that end with a '~', and '\#*\#' specifies all files that start and end with a '#')
clobber: clean
  rm -f *~ \#*\# 
  
objects: testintmath.o intmath.o
  
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

&#x20;(Additionally, declaring a target phony tells `make` that this file does not follow the normal rules for making a target file from a source file. Therefore, make can optimize its normal rule search to improve performance. This is why declaring a target phony is useful even if you're not concerned about such a file actually existing.)

You might be wondering what purpose the `all` target serves in our program compared to simply using `testintmath` as the default target. Truthfully, it doesn't serve any real purpose, except perhaps for accommodating users who might invoke `make all` out of habit.

The real purpose of `all` is to group multiple independent targets and effectively make them all default targets. For example, suppose we have a project with two executables:`hello1` and `hello2`. Making `hello1` and `hello2` dependencies of `all` effectively makes them both default targets (which will be triggered when we run `make`).

```makefile
all: hello1 hello2

hello1: hello1.c
	gcc -c hello1.c

hello2: hello2.c
	gcc -c hello2.c
```
{% endhint %}

#### Characteritics of phony targets

* will always run
* It rarely makes sense to use a phony target as a prerequisite of a real file since the phony is always out of date and will always cause the target file to be remade.
