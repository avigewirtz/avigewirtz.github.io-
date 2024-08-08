# Phony Targets

Make's job is to bring targets up-to-date. Until now, we've assumed that targets represent files, which are brought up-to-date by creating them or updating them. In fact, however, targets need not represent files. They can represent labels for arbitrary commands or actions you want make to execute. Such targets are known as _phony_ targets.

Consider the following rule:

```makefile
clean: 
    rm -rf testintmath *.o
```

The target, clean, does not represent a file—that is, there is no file in our project directory named `clean`, and the command `rm -rf testintmath *.o` does not create such a file. Quite the contrary. This command deletes testintmathh and the object files (.o). Thisnis issue in situations where you want you rebuild testintmath from scratch. 

If we were to add this rule to our makefile and invoke:
 make clean

The effect is that rm -rf testintmath *.o will be executed, thereby "cleaning" the project directory. (Note that the name `clean` isn't special. We could have given the rule a different name, such as `cleanup`. `Clean` is just the conventional name for this kind of task in Makefiles)


`make` implements phony targets in a rather simple manner. After a rule is processed, `make` has no postcondition check to verify that the target was in fact built. Instead, it operates under the assumption that if a target's dependencies (if any) are satisfied and its commands (if any) are successfully run, the target is up-to-date. In the clean example, because the command `rm -rf testintmath *.o` was successfully run (i.e., exit status 0), `make` considers clean to be up-to-date (for the current invocation of `make`, that is). It does not actaully verify whether clean is created. 

Phony targets have two canonical use cases:

* As a label for one or more arbitrary commands you want make to execute. In the previous example, clean was used as a label for the command `rm -rf testintmath *.o`
* As an alias for one or more other targets, such that running the phony target is the same as running the target(s) directly.

In this section, we'll explore both use cases. Phony targets are easiest to explain by means of demonstration, so let's jump right into Makefile version 2, which contains three commonly used phony targets: `all`, `clean`, and `clobber`. Don't worry for now how they work. We'll go over each one in detail.

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

Let's start with the `clean` rule:

```
clean: 
    rm -f *.o testintmath 
```

The target, `clean`, does not represent a file—that is, there is no file in our project directory named `clean`, and the command `rm -f *.o testintmath` does not create such a file. Nevertheless, we can issue the command `make clean`, and the effect is that `rm -f *.o testintmath` will be executed:&#x20;

```bash
$ make clean
rm -f *.o testintmath 
$
```

This command deletes the executable `testintmath` as well as the object files (`*.o` specifies all files with a `.o` extension ), thereby "cleaning" the project directory. This is useful in situations where we want to rebuild `testintmath` from scratch. (Note that the name `clean` isn't special. We could have given the rule a different name, such as `delete_build_files`. `Clean` is just the conventional name for this kind of task in Makefiles)

Here's how `make` processes this rule. As with any other rule, `make` begins by checking if a file named `clean` exists in the working directory. Since there is no such file, `make` determines that `clean` needs to be built. In an attempt to build `clean`, `make` executes the command `rm -f testintmath *.o`. Because this command runs successfully (that it, returns exit status 0), `make` considers `clean` up-to-date (for the current invocation of `make`, that is). It does not actually verify whether `clean` is created.

You can see this full sequence of operations by invoking `make clean` with the `debug=-v` option. Here is the relevant part of the output:

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

In particular, notice how after executing the command `rm -f testintmath *.o`, `make` reports that it ``Successfully remade target file `clean'``.

Next, consider the `clobber` rule:

```
clobber: clean
  rm -f *~ \#*\# 
```

Here, the target is the phony target clobber, and its command is. However, it depends on clean. Therefor, running make clobber will first cause the clean rule to be processed. The effect is that first the executable and object files will be deleted, and then emacs backup and autosave files will be deleted. In other words, clobber extends clean.&#x20;

The command `rm -f *~ \#*\#` deletes Emacs backup (ending with `~`_)_ and autosave files (starting and ending with `#`). However, since `clobber` depends on `clean`, the command for `clean` will be executed before the `clobber` command. In effect, `clobber` extends `clean`.&#x20;

```bash
$ make clobber
rm -f *.o testintmath
rm -f *~ \#*\#
$
```

Let's break it down. make first checks if a file named `clobber` exists in the working directory. Since there is no such file, make determines that `clobber` is out-of-date and needs to be built. Before make can "build" clobber, however, it must first ensure that its dependency, clean, is up-to-date. So make moves on to clean. make sees that clean doesn't exist, so it executes the command rm -f testintmath \*.o in an attempt to build it. Since this command executes successfully, make considers clean up-to-date (for the current invocation of make, that is). Make then go back to clobber and runs the command `rm -f *~ \#*\#` .

Finally, consider the `all` rule:

```makefile
all: testintmath
```

In Makefiles, it's standard practice to make the default target a phony target named `all`. This target typically doesn't have any commands of its own and simply depends on one or more executables. In our case, `all` depends on `testintmath`. The effect is that with this when we run `make all`, make ensures that `testintmath` is up to date. This functionality is equivalent to executing `testintmath` directly. Essentially, `all` serves as an alias for `testintmath`, streamlining the build process by ensuring that the necessary dependencies are built and up to date.

points i want to make:

* standard practice in makefiles to make defauly target phony target all
* doesnt have any command. simply depends on executable(s). In our case, testintmath. effect is that we run make all, make ensures that testibtmath is up to date. functionality equivelant to executing testintmath directly. essentially, all serves as an alias for testintmath
* It may seem pointless

Here, the phony target `all` does not have any command. It simply depends on `testintmath`. The effect is that executing all is funtionality equivelant to executing testintmath. Notice that becaise all is the first target



Serves an an aliad for testintmath, whereby running make all is functionaly identical to running make testintmath:



{% hint style="info" %}
**Purpose of the 'all' target**

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
*   **.PHONY Directive**

    It should go without saying that the scheme we just described will only work if there is in fact no file named `clean` in the working directory. If there is such a file, running `make clean` will always yield:

    ```makefile
    $ make clean
    make: `clean' is up to date.
    $
    ```

    GNU Make offers a simple solution to this potential issue. Just list `clean` as a dependency of the special target .PHONY, like so:

    ```makefile
    .PHONY: clean
    clean: 
        rm -f *.o testintmath 
    ```

    With this declaration, this rule will work as intended even if there is a file named `clean` in the working directory. (Additionally, specifying that a target is phony tells `make` that this file does not follow the normal rules for making a target file from a source file. Therefore, make can optimize its normal rule search to improve performance. This is why declaring a target phony is useful even if you're not concerned about such a file actually existing.)
