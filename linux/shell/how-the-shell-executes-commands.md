# Examples

*   `javac hello.java`

    `javac` is the Java compiler that translates Java source code into Java Bytecode. The shell interprets `javac` as an executable program, and `hello.java` as the argument to this program. The shell uses a system call to create a new process and then loads the `javac` program into the new process's memory. `javac` then reads the `hello.java` file and compiles it into Java Bytecode, creating a file named `Hello.class`.
*   `java Hello`

    `java` is the Java Runtime Environment (JRE) that executes Java Bytecode. The shell interprets `java` as an executable program, and `Hello` as the argument to this program. The shell uses a system call to create a new process and then loads the `java` program into the new process's memory. `java` then reads the H`ello.class` file and executes the Java Bytecode contained within.
*   `gcc hello.c -o hello`

    `gcc` is the GNU Compiler Collection, a compiler for various programming languages including C. The shell interprets `gcc` as an executable program, and `hello.c`, `-o`, and `hello` as arguments to this program. The shell uses a system call to create a new process and then loads the `gcc` program into the new process's memory. `gcc` then reads the `hello.c` file and compiles it into an executable file named `hello`.
*   `./hello`

    `./hello` is a command to execute the `hello` program in the current directory. The `.` in `./` specifies the current directory, and `/hello` is the program to run. The shell uses a system call to create a new process and then loads the `hello` program into the new process's memory. The `hello` program then runs.

In all these cases, the shell is using system calls to create new processes, load programs into those processes' memory, and start their execution. The shell is also passing the arguments provided on the command line to those programs.
