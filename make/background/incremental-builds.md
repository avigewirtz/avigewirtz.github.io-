# Incremental builds

Incremental builds is an approach where each build builds off the previous one. The first time you build a program you compile all of its source files, but in subsequent builds you compile only the source files that have changed since the last build or were affected by changes.&#x20;

They key to implementing incremental builds is to always build a program in two steps. In the first step, you compile the source files into object files. The key is that you only compile the source files who's resulting object files will be different from the ones you already have from the previous build. In the second step, you link all the object files (i.e., the "new" and "old" object files) together to produce the executable.&#x20;
