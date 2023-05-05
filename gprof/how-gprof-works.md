# How Gprof Works

Gprof operates by instrumenting the program's binary during compilation and linking. The GCC Compiler provides the '-pg' flag to enable Gprof profiling. This flag inserts additional code into the binary, allowing Gprof to collect data at runtime. Once the program is executed, a profile data file, usually named _gmon.out_, is generated. Gprof then processes this file to generate a human-readable report.\


\
