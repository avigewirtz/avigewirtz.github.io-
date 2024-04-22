# makefiles

As we saw in the previous section, it's possible to use manually implement incremental builds. However, doing so is tedious an error prone. It requires you to:

1. Keep track of which files have been modified
2. Understand the dependencies between all the program's files

Make automates the incremental build process. make gets the information to build your program by reading a user-created file known as a makefile, which is essentially a textual representation of your program's dependency graph. It describes the relationships among files in your program and provides make with the commands to build them.

## Naming your makefile

You can name your makefile 'makefile' or 'Makefile' (or even 'GNUmakefile', if you're using GNU Make). GNU recommends 'Makefile'.&#x20;
