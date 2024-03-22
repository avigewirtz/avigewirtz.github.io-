# git add

`git add` is a command that allows you to stage changes in your working directory, preparing them to be committed to the repository. Staging changes means that you're telling Git you want to include those specific changes in the next commit. This is useful for organizing your work into logical units or separating unrelated changes.

In the following examples, we will use [Decomment](https://github.com/COS217/Decomment) repository as a reference:

1.  **Adding a file.** Suppose you've created a new file named `decomment.c` that contains the main implementation of the Decomment project. After creating the file, you would stage it using `git add`:

    ```bash
    git add decomment.c
    ```
2. **Modifying a file.**&#x20;
   * Suppose you've made changes to `decomment.c`, such as adding a new function or improving existing code. After making the changes, you would stage the modified file again:

```bash
git add decomment.c
```

* Similarly, suppose you've populated the readme file, as required at the end of the assignment. If you want to include the populated readme file in your Git repository, you would stage the updated file: git add read

```bash
git add readme
```

#### Common usage:

*   **Staging a single file:**

    ```bash
    git add FILE_NAME
    ```
*   **Staging multiple files:**

    ```bash
    git add FILE1 FILE2
    ```
*   **Staging all changes in the working directory:**

    ```bash
    git add .
    ```
