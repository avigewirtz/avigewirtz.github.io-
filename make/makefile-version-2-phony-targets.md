# Phony targets

`make` assumes that each target represents a file that is built when its corresponding command is run. However, it has no verification mechanism to check whether the target was actually built by the command. Instead, it operates under the assumption that if a target's command is successfully run, the target is up-to-date. This is not a bug in `make` but a deliberate design choice, as it enables the use of so-called _phony_ targets—targets that do not correspond to actual files but represent labels for arbitrary commands or actions you want `make` to execute.&#x20;

Phony targets are easiest to illustrate by means of an example, so let's jump right into makefile version 2, shown below, which contains three commonly used phony targets:  `all`, `clean`, and `clobber`. Don't worry for now how they work for now. We'll go over each one by one.&#x20;

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

Let's start with the `clean` rule:

```makefile
clean:
  rm -f testintmath *.o
```

There is no file in our working directory named `clean`, and the command `rm -f testintmath *.o` does not create such a file. Here's how make processes this rule when we run:

```bash
make clean
```

Like any other rule, `make` checks if a file named `clean` exists in the working directory. Since there is no such file, `make` determines that `clean` is out-of-date and needs to be built. In an attempt to build `clean`, `make` executes its corresponding command:

```makefile
$ make clean
rm -f testintmath *.o
$ 
```

Of course, however, this command does not actually create a file named `clean`. Quite the contrary. It deletes `testintmath` as well as all object files (`.o`), effectively "cleaning" the project directory. (Note that the name `clean` isn't special. We could have named the rule anything we want, such as `delete_temp_files`. `Clean` is just the conventional name for this kind of task in Makefiles.)&#x20;

The reason this works is make does not have a postcondition check to verify that `clean` is in fact created. All it concerned with is that the command is successfully executed (i.e., it returns an exit status of 0).

The important point to recognize is that because this command will never create a file named clean, clean will always be considered out of date, and the command will be executed. For example, here's the output when we run make clean three times in a row:

```makefile
$ make clean
rm -f testintmath *.o
$ make clean
rm -f testintmath *.o
$ make clean
rm -f testintmath *.o
$
```

Let's now consider the `clobber` rule:

```
clobber: clean
  rm -f *~ \#*\# 
```

Like `clean`, clobber does not represent a file--that is, there is no file in the working directory named clobber, and the command  `rm -f *~ \#*\#`  does not create such a file. clobber is a bit more interesting than clean, however. Not only is it a phony target itself, it depends on a phony target--clean.&#x20;

make first checks if a file named `clobber` exists in the working directory. Since there is no such file, make determines that `clobber` is out-of-date and needs to be built. Clobber depends on clean, however, so before executing the command, it must first ensure that clean is up-to-date. make sees that clean doesn't exist, so it executes the command rm -f testintmath \*.o. Despite the fact that clean was not created, make considered it up-to-date (for the current invocation of make), and it therefores considers clobbers dependencies satisfied. It therefore runs the command rm -f \*\~ \\#\*\\# . This command has the effect of deleting Emacs backup files.  Make executes the command rm -f testintmath \*.o. Then it returns to clobber.&#x20;


The clean and clobber phony targets demonstrate how phony tatgets enabke us to use make to execute commands that don't incolve building files. Another canocial use case of phony yatgets is to serve as an alias from one or more other garegts. Consider the all phony target:

```makefile
all: testintmath
```
all does not represent a file; hiwever, unlike coean and cllbber, it has no corresponding command. Instead, it essentially serves as an alias for testintmath, meaning that the affect of running make all is the same as running make testintmath. 
If we run all, the 

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
