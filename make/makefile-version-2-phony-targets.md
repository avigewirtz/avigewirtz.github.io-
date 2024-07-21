# Phony targets

Make's job is to bring targets up-to-date. Until now, we've assumed that targets represent files, which are brought up-to-date by creating them or updating them. In fact, however, targets need not represent files. They can represent labels for arbitrary commands or actions you want make to execute. Such targets are known as _phony_ targets.

`make` implements phony targets is quite a simple manner. After a rule is processed, `make` has no postcondition check to verify that the target "file" was in fact built. Instead, it operates under the assumption that if a target's dependencies (if any) are satisfied and its commands (if any) are successfully run, the target is up-to-date. Phony targets have two canonical use cases:

* As a label for one or more arbitrary commands you want make to execute.
* As an alias for one or more other targets, such that running the phony target is the same as running the target(s) directly.

In this section, we'll explore both use cases. Take a look at Makefile version 2, shown below, which contains three commonly used phony targets: `all`, `clean`, and `clobber`. Don't worry for now how they work. We'll go over each one by one.

{% code title="makefile version 2" %}
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
  
# Dependency rules for file targets
testintmath: testintmath.o intmath.o
  gcc testintmath.o intmath.o –o testintmath
  
testintmath.o: testintmath.c intmath.h
  gcc -c testintmath.c
  
intmath.o: intmath.c intmath.h
  gcc -c intmath.c
```
{% endcode %}
Consider the `clean` rule:

```
clean: 
    rm -f *.o testintmath 
```

The target, clean, does not represent a file—that is, there is no file in our prohect directory named `clean`, and the command `rm -f *.o testintmath` does not create such a file. Nevertheless, we can run this rule, and the effect is that `rm -f *.o testintmath` will be executed:



In this rule, the target is clean, which does not correspond to a file in our project directory, and we give it the command rm -f .o testintmath, which, when run, has the effect of deleting testintmwrh and all objevt files in tje working directiry. When we invoke make clean, the effect is that the command rm -f \*.o testintmath gets executed:

```
$ make clean
rm -f *.o testintmath 
$
```

Here's how it works. Like any other rule, `make` checks if a file named `clean` exists in the working directory. Since there is no such file, `make` determines that `clean` needs to be built. In an attempt to build `clean`, `make` executes the command rm -f testintmath \*.o. Because this command runs successfuly(that it, returns exit status 0), make considers clean up-to-date (for the current invocation of make, that is). It does not actaully verify that clean is created.

We can see this full sequence of operations by invoking make clean with the debug=-v option. This prints out. Your output should look like the following:

```
$ make clean --debug=v
GNU Make 3.81
Copyright (C) 2006  Free Software Foundation, Inc.
This is free software; see the source for copying conditions.
There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE.

This program built for i386-apple-darwin11.3.0
Reading makefiles...
Reading makefile `makefile'...
Updating goal targets....
Considering target file `clean'.
 File `clean' does not exist.
 Finished prerequisites of target file `clean'.
Must remake target `clean'.
rm -f testintmath *.o
Successfully remade target file `clean'.
$ 
```

In the above output, notice how after make executes the command `rm -f testintmath *.o`, it reports that ``Successfully remade target file `clean'``.  Of course, however, a file named clean was not in fact created. Therefore, we can run make clean again, and the effect will be that the command `rm -f *.o testintmath` will be executed:

```
$ make clean
rm -f *.o testintmath 
$
```

{% hint style="info" %}
Note that the name `clean` isn't special. We could have named the rule anything we want, such as `delete_build_files`. `Clean` is just the conventional name for this kind of task in Makefiles.
{% endhint %}

{% hint style="warning" %}
#### .PHONY Directive

It should go without saying that this scheme only works if there is in fact no file named `clean` in the working directory. If there is such a file, running `make clean` will always yield:

```makefile
$ make clean
make: `clean' is up to date.
$
```

GNU Make offers a simple solution to this potential issue. Just declare `clean` as phony, like so:

```makefile
.PHONY: clean
clean: 
    rm -f *.o testintmath 
```

With this declaration, this rule will work as intended even if there is a file named `clean` in the working directory.
{% endhint %}

Suppose we want to extend `clean` by also deleting Emacs backup and autosave files. We can achive this by adding the following rule to our Makefile:

```
clobber: clean
  rm -f *~ \#*\# 
```

Here, the rule is clobber--so called because it purpose is to thoroughly clean the project directory--and the command is rm -f \*\~ \\#\*\\#. Notice, however, that clobber depends on clean, so before clobber get's processed, clean will be processed. Invoking this rule:

```
$ make clobber
rm -f testintmath *.o
rm -f *~ \#*\# 
$ 
```

#### Phony targets as an alias for other target(s)

The two examples we went over demonstrate the use of phony targets as labels for arbitrary commands you want make to run. Let's now consider its second use case--as an alias for other target(s). This is useful for grouping multiple targets under a single, more user-friendly name. Suppose we want to build testintmath.o and intmath.o but not link them. We could achieve this by running:

```
make intmath.o testintmath.o
```

Alternatively, as a shortcut we could add a rule like the following:

```
obj: testintmath.o intmath.o
```

and now achieve the same result by simply running:

```
make obj
```

In other words, obj essentially serves as an alias for testintmath.o intmath.o, whereby running make obj is identical to running make intmath.o testintmath.o.&#x20;

Notice that this rule has no command. That's perfectly fine. So long as&#x20;

In makefiles it is common to \<explain all target>.&#x20;

#### Makefile version 2

Makefile version 2, shown below, integrates three of the phony targets we just discussed: `all`, `clean`, and `clobber`.&#x20;

{% code title="makefile version 2" %}
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

```makefile
clean:
  rm -f testintmath *.o
```

There is no file in our working directory named `clean`, and the command `rm -f testintmath *.o` does not create such a file. Instead, it serves as a label for the command `rm -f testintmath *.o`, meaning that when we run `make clean`, the effect is that `rm -f testintmath *.o` gets executed:

```bash
$ make clean
rm -f testintmath *.o
$ 
```

This command deletes `testintmath` as well as all object files (`.o`), effectively "cleaning" the project directory. (Note that the name `clean` isn't special. We could have named the rule anything we want, such as `delete_temp_files`. `Clean` is just the conventional name for this kind of task in Makefiles.)

Here's how it works under the hood. Like any other rule, `make` checks if a file named `clean` exists in the working directory. Since there is no such file, `make` determines that `clean` is out-of-date and needs to be built. In an attempt to build `clean`, `make` executes its corresponding command, rm -f testintmath \*.o. At this point, make considers clean to be up-to-date. It does not actaully verify that clean is created.

Consider the `clobber` rule:

```
clobber: clean
  rm -f *~ \#*\# 
```

clobber is a phony target that depends on another phony target--clean. When we run this rule, the effect is that both rm -f testintmath \*.o and rm -f \*\~ \\#\*\\# are executed:

```
$ make clobber
rm -f testintmath *.o
rm -f *~ \#*\# 
$ 
```

Here's how it works. make first checks if a file named `clobber` exists in the working directory. Since there is no such file, make determines that `clobber` is out-of-date and needs to be built. Before make can "build" clobber, however, it must first ensure that its dependency, clean, is up-to-date. So make moves on to clean. make sees that clean doesn't exist, so it executes the command rm -f testintmath \*.o in an attempt to build it. Since this command executes successfully, make considers clean up-to-date (for the current invocation of make, that is). Make then go back to clobber and runs the command rm -f \*\~ \\#\*\\# . This command has the effect of deleting Emacs backup files.

The clean and clobber phony targets demonstrate how phony tatgets enabke us to use make to execute commands that don't incolve building files. Another canocial use case of phony yatgets is to serve as an alias from one or more other garegts such that run the alias is equivelant to running the target(s) directly. Consider the all phony target:

```makefile
all: testintmath
```

all does not represent a file, and this rule has no command. The affect of running this rule is that make ; hiwever, unlike coean and cllbber, it has no corresponding command. Instead, it essentially serves as an alias for testintmath, meaning that the affect of running make all is the same as running make testintmath. If we run all, the

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

