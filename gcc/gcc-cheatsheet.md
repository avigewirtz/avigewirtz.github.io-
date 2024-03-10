# GCC Cheatsheet

{% hint style="info" %}
`gcc217` is an alias for `gcc -Wall -Wextra -Wno-unused-parameter -ansi -pedantic`
{% endhint %}

| Command                                    | Explanation                                         |
| ------------------------------------------ | --------------------------------------------------- |
| `gcc217 program.c`                         | Compiles `program.c` to default executable `a.out`. |
| `gcc217 program.c -o program`              | Compiles `program.c` to executable `program`.       |
| `gcc217 -E program.c -o program.i`         | Preprocesses `program.c` to `program.i`.            |
| `gcc217 -S program.c`                      | Compiles `program.c` to assembly `program.s`.       |
| `gcc217 -c program.c`                      | Compiles `program.c` to object file `program.o`.    |
| `gcc217 program.o -o program`              | Links `program.o` to executable `program`.          |
| `gcc217 --save-temps program.c -o program` | Compiles and saves all intermediate files.          |
| `gcc217 -g program.c`                      | Compiles with debugging information.                |

