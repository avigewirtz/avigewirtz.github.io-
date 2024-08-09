# Phony Targets

Make's job is to bring targets up-to-date. Until now, we've assumed that targets represent files, which are brought up-to-date by creating them or updating them. In fact, however, targets need not represent files. They can represent labels for arbitrary commands or actions you want make to execute. Such targets are known as _phony_ targets.

Consider the following rule:

```makefile
clean: 
    rm -rf testintmath *.o
```

The target, `clean`, does not represent a file—that is, there is no file in our project directory named `clean`, and the command `rm -rf testintmath *.o` does not create such a file. Quite the contrary. This command deletes `testintmath` and the object files (`.o`). This is useful in situations where you want you rebuild `testintmath` from scratch.

If we were to add this rule to our Makefile and invoke `make clean`, the effect is that `rm -f *.o testintmath` will be executed, thereby "cleaning" the project directory:

```bash
$ make clean
rm -f *.o testintmath 
$
```

(Note that the name `clean` isn't special. It's simply the conventional name for this kind of task in Makefiles)

`make` implements phony targets in a rather simple manner. When a rule is processed, `make` has no postcondition check to verify that the target was in fact built. Instead, it operates under the assumption that if a target's dependencies (if any) are satisfied and its commands (if any) are successfully run (i.e., exit status 0), the target is up-to-date. In our example, because both of these conditions are satisfied (the command `rm -rf testintmath *.o` was successfully executed and there are no dependencies) `make` considers `clean` to be up-to-date (for the current invocation of `make`, that is). It does not actually verify whether `clean` is created.

You can observe the underlying process by which make processes `clean` by invoking this rule with the `debug=-v` option. Here is the relevant part of the output:

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

In particular, notice how after executing the command `rm -f testintmath *.o`, `make` reports that it ``Successfully remade target file `clean'``. This should convince you that `make` really considers `clean` to be up-to-date after its command is executed, even though no such file was created.  &#x20;

{% hint style="warning" %}


**.PHONY Directive**

It should go without saying that the scheme we just described will only work if there is in fact no file named `clean` in the working directory. If such a file exists, `make clean` will always yield:

```makefile
$ make clean
make: `clean' is up to date.
$
```

GNU Make offers a simple solution to this potential naming conflict. List `clean` as a dependency of the special target `.PHONY`, like so:

```makefile
.PHONY: clean
clean: 
    rm -f *.o testintmath 
```

With this declaration, the rule will work as intended even if there is a file named `clean` in the working directory.
{% endhint %}

The `clean` rule demonstrates the use of phony targets as labels for arbitrary commands. Another common use case of phony targets is as an alias for one or more other targets, such that running the phony target is functionally equivalent to running the target(s) directly. Our Makefile doesn't lend itself well to this use case, so the example that follows will be somewhat contrived.

Suppose you often want to build the object files but not link them. You could run:

```
make testintmath.o intmath.o
```

and this will get the job done, but typing this out every time is annoying. Alternatively, you could add following rule to the Makefile:

```
obj: testintmath.o intmath.o
```

Now, you can build both targets by simply invoking:

```
make obj
```

Essentially, `obj` serves as an alias for `testintmath.o` and `intmath.o`. This rule takes advantage of the fact that calling a target causes its dependencies to be processed. 

An interesting observation that we're not actually concerned about a file named obj existing in the project directory, since even if it did exist this rule would work as intended. Nevertheless, declaring it .PHONY is good practice, this allows make to optimize its rule handling procedure (For example, many will not look for an implicit time to build obj). 


#x20;

#### Standard Phony Targets

By convention, there are many phony targets standard among Makefiles. Let's now update our Makefile by adding three of them:  `all`, `clean`, and `clobber`.&#x20;

{% code title="Makefile version 2" %}
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

&#x20;

You might be wondering what purpose the `all` target serves in our program compared to simply using `testintmath` as the default target. Truthfully, it doesn't serve any real purpose, except perhaps for accommodating users who might invoke `make all` out of habit.
{% endhint %}

#### Characteritics of phony targets

* will always run
* It rarely makes sense to use a phony target as a prerequisite of a real file since the phony is always out of date and will always cause the target file to be remade.
