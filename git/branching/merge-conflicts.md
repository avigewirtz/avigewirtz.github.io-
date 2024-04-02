# Merge conflicts

Hopefully it is rare, which it should be if you use good Git discipline with yourself and if when working with a partner you each use good Git discipline and you communicate clearly. As a concrete piece of advice, try to avoid conflicts by (1) pulling from your GitHub repository before starting each programming task, and (2) pushing to your GitHub repository as soon as the programming task is finished to your satisfaction.

The following sequence of commands illustrates a conflict and how to resolve it.

Let's assume you and your partner are working on a simple "Hello, World" C program. The project has a file called hello.c file that looks like this:

```c
#include <stdio.h>
int main() {
    printf("Hello, World!\n");
    return 0; 
}
```

1. Your partner navigates to the local repository and pulls the latest changes from the GitHub repository to their local repository. This ensures they have the most recent version of the project.

```bash
cd hello_world_project 
git pull
```

1. You do the same on your computer, making sure both you and your partner have the latest changes.

```bash
cd hello_world_project
git pull
```

3. Your partner adds a comment above the main() function in the hello.c file and then stages and commits the changes.&#x20;

```bash
git add hello.c 
git commit -m "Added a comment to hello.c"
```

Your partner's version of hello.c:

```c
#include <stdio.h>
// This is the new comment added by your partner
int main() {
    printf("Hello, World!\n");
    return 0;
}
```

4. Meanwhile, you change the "Hello, World!" message to "Hello, everyone!" and stage and commit the change:

```bash
git add hello.c 
git commit -m "Changed “‘Hello World’ to ‘Hello Everyone’"
```

Your version of hello.c:

```c
#include <stdio.h>
int main() {
    printf("Hello, everyone!\n");
    return 0; 
 }
```

5. Your partner now pushes their changes to the GitHub repository:

```bash
git push origin main
```

6. You try to push your changes, but Git detects a conflict because both you and your partner have made changes to `hello.c`. Your push attempt fails.
7. To resolve the conflict, Git suggests pulling the latest changes from the GitHub repository, which you do.

```bash
git push origin main
```

8. Git detects the conflict in hello.c and adds conflict markers to show the conflicting changes. The conflict markers in hello.c might look like this:

```c
#include <stdio.h>

<<<<<<< HEAD 
 // This is the new comment added by your partner
=======
>>>>>>> your-branch
int main() {
    printf("<<<<<<< HEAD\n");
    printf("Hello, everyone!\n");
    printf("=======\n");
    printf("Hello, World!\n");
    printf(">>>>>>> your-branch\n");
    return 0;
}
```

9. To resolve the conflict, you need to edit the file and decide whether to keep your change, your partner's change, or merge both changes. In this case, you decide to keep both changes (the new comment and “Hello, everyone!”). The modified file without conflict markers looks like this:&#x20;

```c
#include <stdio.h>
// This is the new comment added by your partner
int main() {
    printf("Hello, everyone!\n");
    return 0;
}
```

10. After resolving the conflict, you stage the updated hello.c and commit the changes with a descriptive message.

```bash
git add hello.c 
git commit -m "Resolved conflicts"
```

11. Finally, you push the resolved changes to the GitHub repository, and the operation succeeds.

```bash
git push origin main
```
