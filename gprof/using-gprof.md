# Using Gprof

To use Gprof, follow these steps:

1. Compile and link the program with the `-pg` flag:

```bash
gcc -pg -o program.c program
```

2. Execute the instrumented binary, which generates the _gmon.out_ file:

```bash
./program
```

3. . Run Gprof to analyze the profile data and generate a report:

```bash
gprof program gmon.out > gprof_report.txt
```
