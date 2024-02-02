# Makefile Version 2: Phony targets

In a makefile, a rule's target typically represents the name of a file that is built when the rule's command is executed. For example, in the following rule:

```makefile
intmath.o: intmath.c intmath.h
  gcc217 -c intmath.c
```

The target is intmath.o, which is built when `gcc217 -c intmath.c` is executed. However, Make offers a flexible feature where the target doesn't actually have to represent a file. Instead, it can represent a label for a command you want make to execute. For example, consider the following rule:

```
sayHello:
    echo "Hello there!" 
```

The target, sayHello, does not represent a file in our directory, and the command `echo "hello there"` does not create such a file. If we were to invoke this rule on the command line, the effect would be that `echo "Hello there!"` would be executed:&#x20;

```bash
$ make sayHello
echo "Hello there!"
Hello there!
```

Here's how it works: Make checks for a file named 'sayHello' in the current directory. Since it doesn't find one, it runs the command `echo "Hello there!"`.&#x20;

Because this command doesn't create a file named 'sayHello', we can run `make sayHello` as many times as we like, and each time, Make will execute `echo "Hello there!"`, displaying the message again. For instance, if we execute `make sayHello` three times in a row, we'll get 'Hello there!' printed three times:

```bash
$ make sayHello
echo "Hello there!"
Hello there!
$ make sayHello
echo "Hello there!"
Hello there!
$ make sayHello
echo "Hello there!"
Hello there!
```

In other words, the sole purpose of a phony target in a Makefile is to enable the repeated execution of any arbitrary command. While using Make to execute a simple command like `echo "Hello there!"` might not seem very useful, there are numerous other commands that can significantly streamline workflow management. To illustrate this, let's enhance our Makefile with three standard phony targets: `all`, `clobber`, and `clean`:

```makefile
# Dependency rules for non-file targets
all: testintmath
clobber: clean
  rm -f *~ \#*\#
clean:
  rm -f testintmath *.o
  
# Dependency rules for file targets
testintmath: testintmath.o intmath.o
  gcc217 testintmath.o intmath.o –o testintmath
testintmath.o: testintmath.c intmath.h
  gcc217 -c testintmath.c
intmath.o: intmath.c intmath.h
  gcc217 -c intmath.c
```

#### Clean

This rule "cleans" the project directory by deleting all the files that were generated during the build process. Its command, `rm -f testintmath *.o`, removes the executable _testintmath_ as well as all files in the current directory with the _.o_ extension (i.e., object files). To trigger this rule, simply invoke:&#x20;

```
make clean
```

#### Clobber

clobber extends the functionality `clean` by also deleting Emacs backup and autosave files. `*~` specifies all files in the current directory that end with a \~ (tilde), and `\#*\#` specifies all files in the current directory that start and end with a # (hash).

#### All

The `all` target is often the default goal in many Makefiles, used to build the complete project. When you invoke `make` or `make all`, it triggers the build of `testintmath`, along with any other dependencies specified under this target. It's common practice to list all primary build targets under `all`.

{% hint style="info" %}
You might be wondering, "Why not just use `testintmath` directly like we did before? What's the point of `all`?" Truthfully, in our specific example, there isn't much of a benefit by adding `all`, except perhaps that it accommodates users who are used to typing `make all` out of habit, as it's a pretty standard practice.

But the real purpose of `all` shows up when you have multiple independent targets that you want to build via a single invocation of make. Imagine you're working on a project with two separate programs, say`hello1` and `hello2`. You can set up your Makefile like this:

```
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

In this scenario, since both `hello1` and `hello2` are linked to the `all` target, running make will build both executables. This is more convenient than having to run `make hello1` and `make hello2` separately.
{% endhint %}
