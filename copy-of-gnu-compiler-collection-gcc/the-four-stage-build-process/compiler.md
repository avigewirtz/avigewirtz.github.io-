# Compilation Stage

The second stage in the GCC compilation process involves the C compiler itself, which translates the preprocessed source code into assembly language. The assembly versions of main.c and circle.c are stored in main.s and circle.s respectively.&#x20;

\


Assembly language is essentially a human-readable version of the target processor’s machine language. Unlike C which abstracts away hardware details like registers and memory addresses, assembly deals directly with registers and memory addresses.

Additionally, assembly language doesn't have constructs like if-else statements, for or while loops, or functions in the traditional sense. Instead, it has basic instructions for moving data, arithmetic operations, and explicit jump and branch instructions for control flow. &#x20;

\


Main.s and circle.s are text files, so you can view their contents with a text editor like Emacs. Below is a&#x20;

\


To illustrate the difference in abstraction and syntax between a high-level language like C and assembly, let's consider&#x20;

\
\
\
\


In this assembly code, the function takes a floating-point value (circumference) as input, saves it on the stack, retrieves a constant value (2 \* PI), performs a floating-point division to calculate the radius, and then returns the result. This process involves direct manipulation of CPU registers and memory addresses, showcasing the low-level nature of assembly programming.

\


#### Characteristics of C vs. Assembly&#x20;

* Abstraction Level
*
  * C: C abstracts away hardware details, allowing programmers to focus more on the logic or what they want to do. It simplifies programming by hiding the complexity of the hardware.
  * Assembly: Requires explicit, low-level instructions. It provides direct control over hardware, but with this comes the need for detailed knowledge of the processor's architecture.
* Portability
*
  * C: Highly portable across various hardware platforms. The same C code can usually be compiled on different systems with minimal changes, thanks to the standardization of the C language and its compilers.
  * Assembly: Not portable. Assembly code is written for a specific processor architecture. Programs written in assembly for one type of processor cannot be run on another without significant modifications, due to differences in instruction sets, memory management, and hardware operations.
* Functionality to Code Size Ratio
*
  * C: Offers a good ratio of functionality to code size. A single line of C code can perform complex tasks, making the code more concise and easier to manage.
  * Assembly: Has a poor ratio of functionality to code size. Each instruction in assembly performs a very basic task, requiring more lines of code to accomplish the same task as a high-level language like C.
* Low-Level Access and Control
*
  * C: While being a high-level language, C still provides some degree of low-level access to memory and system resources, which is why it's often used for system programming.
  * Assembly: Offers the most direct and detailed control over the system's hardware. It allows for precise manipulation of CPU registers, memory addresses, and system resources, but this comes at the cost of increased complexity and potential for errors.

\
\


ASIDE: WHY Can’t assembly be converted from one form to another?&#x20;

\
\


Below are the assembly versions of main.c and circle.c for the armv8-a architecture, stored in main.s and circle.s respectively.&#x20;

