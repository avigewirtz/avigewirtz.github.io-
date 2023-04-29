# Ignoring Files

In the Decomment assignment, you build decomment.c using distinct gcc217 preproccess, compile, assemble, and link commands. These commands generate the following four output files:&#x20;

* decomment.i: Preprocessed output
* decomment.s: Assembly code
* decomment.o: Object file
* decomment: Executable file

Because these files are not part of the source code, you may not want to include them in your Git repository. In such a case, you don’t want to include them when you stage all files in your repository, such as with&#x20;

git add .&#x20;

\


Instead, add them to a .gitignore file to prevent them from being accidentally committed.

Here's an example of what your .gitignore file could contain:

| <p># Build output files </p><p>*.i </p><p>*.s </p><p>*.o </p><p>decomment</p> |
| ----------------------------------------------------------------------------- |

After creating or updating the .gitignore file, you should stage and commit it to the repository:

| git add .gitignore |
| ------------------ |
