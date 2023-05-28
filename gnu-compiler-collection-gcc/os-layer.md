# OS layer

Operating systems provide another crucial layer of abstraction on top of assembly language, helping manage resources and tasks in a way that simplifies the programming process. The operating system handles many tasks behind the scenes, like memory management, process scheduling, input/output operations, and more, which impact the structure and behavior of assembly programs.

1. **System Calls:** System calls are the primary means by which a program interacts with the operating system. These are special functions provided by the OS that allow programs to request services such as file operations, network access, creating new processes, and so on. System calls are usually made via specific assembly instructions (like 'INT' in x86 for interrupt), with the required system call number and parameters placed in certain registers.
2. **Standard Libraries:** Operating systems often come with standard libraries, which are pre-written code that programs can use. These libraries provide higher-level functions for tasks such as string manipulation, mathematical computations, and more, often implemented in assembly or a low-level language for efficiency.
3. **Executable Format and Program Structure:** The operating system defines the format of executable files and the structure of programs in memory. This includes aspects such as where the code section starts, where data can be located, how the stack is managed, and more. Assembly programs need to follow these conventions to be correctly loaded and executed by the OS.
4. **Memory Management:** Operating systems handle the complex task of memory management. They provide the abstraction of a continuous memory space to programs, even though the actual memory might be fragmented or partially located on disk. They also isolate the memory of different processes to prevent them from interfering with each other.
5. **Multitasking and Process Management:** Operating systems allow for multitasking, where multiple processes seem to run simultaneously. This affects assembly programs as they must be designed to handle context switches, where execution is paused and then resumed later.
6. **Device Abstraction:** Operating systems provide a uniform interface to a variety of hardware devices. This allows assembly programs to interact with different devices in a consistent manner, without needing to know the specific details of each device's operation.

In summary, the operating system provides a variety of services and abstractions that simplify assembly programming. These abstractions allow programmers to focus more on the logic of their programs, rather than the low-level details of hardware interaction and resource management.







The operating system, along with the conventions of the assembly language itself, helps dictate the structure of an assembly file. Most assembly programs are divided into different sections. Each section serves a specific purpose and aligns with how the operating system expects to handle that part of the program. Here's a breakdown of some of the typical sections:

1. **.text section:** This is where the actual code of the program goes. Instructions that the CPU will execute are placed in this section. The OS marks this memory area as executable but not writable to protect the integrity of the code.
2. **.data section:** This section is used for declaring initialized static or global variables used by the program that will retain their values between function calls. The data here is changeable, and the OS usually marks this area as readable and writable, but not executable.
3. **.bss section:** The "Block Started by Symbol" section is used for declaring variables that are not initialized yet. The OS will automatically clear this section when the program is loaded, effectively setting all values to zero. Like the .data section, it is readable and writable, but not executable.
4. **.rodata section:** "Read-Only Data" section is for constants and other data that should not be changed during the execution of the program. The OS marks this memory area as readable and executable, but not writable, to prevent accidental or malicious modifications.
5. **.stack section:** This is a special section that the OS sets up for the program to use as a stack - a region of memory that grows and shrinks automatically as functions are called and return, and where local variables are typically allocated.
6. **.heap section:** This isn't usually explicitly declared in the assembly program, but is instead set up by the OS for dynamic memory allocation during runtime, like with the malloc and free functions in C.

The assembly source code usually starts with directives that identify these sections and then the appropriate code or data is placed under each section directive. The layout helps the assembler and linker generate the correct machine code and also helps the OS to correctly load and run the program.

It's important to note that these are conventional names and can vary between different assembly languages and operating systems. The key concept is that assembly files are typically divided into sections based on the purpose of the data they contain, and the OS uses these divisions to correctly manage the program's execution.
