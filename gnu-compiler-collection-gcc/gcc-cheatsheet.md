# GCC Cheatsheet

{% hint style="info" %}
Note: `gcc217` is a shell alias for `gcc -Wall -Wextra -Wno-unused-parameter -ansi -pedantic`
{% endhint %}

| Command                                    | Explanation                                                       |
| ------------------------------------------ | ----------------------------------------------------------------- |
| `gcc217 program.c`                         | Builds `program.c` to default executable `a.out`.                 |
| `gcc217 program.c -o program`              | Builds`program.c` to executable `program`.                        |
| `gcc217 -E program.c -o program.i`         | Preprocesses `program.c` to `program.i`.                          |
| `gcc217 -S program.c`                      | Preprocesses and compiles `program.c` to assembly `program.s`.    |
| `gcc217 -c program.c`                      | Preprocesses, compiles, and assembles `program.c` to `program.o`. |
| `gcc217 program.o -o program`              | Links `program.o` to executable `program`.                        |
| `gcc217 --save-temps program.c -o program` | Builds program.c and and saves all intermediate files.            |
| `gcc217 -g program.c`                      | Builds program.c with debugging information.                      |

