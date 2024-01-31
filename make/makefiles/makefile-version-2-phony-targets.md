# Makefile Version 2: Phony targets

In a makefile, a rule's target typically represents the name of a file that is built when the rule's command is executed. For example, in the following rule:

```makefile
intmath.o: intmath.c intmath.h
  gcc217 -c intmath.c
```

The target is intmath.o, which is built when `gcc217 -c intmath.c` is executed.&#x20;

A useful feature of make is that a rule's target need not actually represent a file. For example, consider the following rule:

```
sayHello:
    echo "Hello there!" 
```

The target is 'sayHello', it contains no dependencies (which is perfectly valid), and the command is `echo "Hello there!"`. However, we have no file in our directory named 'sayHello', and the command `echo "hello there"` does not create such a file. What would happen if were to add this rule to our makefile and invoke `make sayHello` on the command line? Let's try it out:

```bash
$ make sayHello
echo "Hello there!"
Hello there!
```

As you can see, this causes the command `echo "Hello there!"` to be executed, printing 'Hello there!' on stdout.&#x20;

How it works is, make checks if a file named 'sayHello' exists. Because it does not, make executes the command echo "Hello there!". But because a file named 'sayHello' was not created, we can invoke make sayHello as many times as we'd like on the command line, and `echo "Hello there!"` will be executed every time. For example, let's invoke `make sayHello` three times:

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



In other words, sayHello serves as a label for a command we want make to execute. Such a target is called a phony target.&#x20;

As this example hopefully demonstrates, the purpose of a phony target is to serve as a label for a command you want make to execute. Of course, enabling make to execute echo "Hello there!" is not particulurly useful. Let's not update our makefile with a few standard phony targets, which we'll explain in detail:&#x20;

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

#### All

#### Clean

clean is used to delete the files that were generated during the build process. It's a way to "clean up" your project directory, so you can start a fresh build. `rm -f testintmath *.o` removes _testintmath_ as well as all files in the current directory with the _.o_ extension.

#### Clobber

The `clobber` rule is typically used to extend the functionality of the `clean` rule. It not only removes the files generated during the build process (as done by the `clean` rule) but also gets rid of backup and temporary files that are often created by text editors or development environments.`*~`:  Specifies all files in the current directory that end with a \~ (i.e., `example.c~`), and `\#*\#` specifies all files in the current directory that start and end with # (i.e.,`#example.c#`). These files are Emacs backup and autosave files.

#### All

The `all` target is often the default goal in many Makefiles, used to build the complete project. When you invoke `make` or `make all`, it triggers the build of `testintmath`, along with any other dependencies specified under this target. It's a common practice to list all primary build targets under `all`.

{% hint style="info" %}
If you have multiple independent targets you want to run via a single invocation of make, you can do so by making them all a dependency of a single target. Standard practice is to call such a target all. For example, suppose we have two executables: hello1 and hello2.&#x20;

```
all: hello1 hello2

hello1: hello1.0
	gcc hello1.o -o hello1
	
hello2: hello2.0
	gcc hello2.o -o hello2

hello1.o: hello1.c
	gcc -c hello1.c

hello2.o: hello2.c
	gcc -c hello2.c
```
{% endhint %}
