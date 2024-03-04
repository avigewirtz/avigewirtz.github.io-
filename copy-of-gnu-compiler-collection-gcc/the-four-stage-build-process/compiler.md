# Compilation Stage

The second stage in the GCC compilation process involves the C compiler itself, which translates the preprocessed source code into assembly language. The assembly versions of main.c and circle.c are stored in main.s and circle.s respectively.&#x20;

\


Assembly language is essentially a human-readable version of the target processor’s machine language. Unlike C which abstracts away hardware details like registers and memory addresses, assembly deals directly with registers and memory addresses.

Additionally, assembly language doesn't have constructs like if-else statements, for or while loops, or functions in the traditional sense. Instead, it has basic instructions for moving data, arithmetic operations, and explicit jump and branch instructions for control flow. &#x20;

\


Main.s and circle.s are text files, so you can view their contents with a text editor like Emacs. Below is a&#x20;

\


To illustrate the difference in abstraction and syntax between a high-level language like C and assembly, let's consider&#x20;



{% tabs %}
{% tab title="circle.s arm" %}
```javascript
	.file	"circle.c"
	.text
	.p2align 4
	.globl	calculateArea
	.type	calculateArea, @function
calculateArea:
.LFB0:
	.cfi_startproc
	movapd	%xmm0, %xmm1
	movsd	.LC0(%rip), %xmm0
	mulsd	%xmm1, %xmm0
	mulsd	%xmm1, %xmm0
	ret
	.cfi_endproc
.LFE0:
	.size	calculateArea, .-calculateArea
	.section	.rodata.cst8,"aM",@progbits,8
	.align 8
.LC0:
	.long	-266631570
	.long	1074340345
	.ident	"GCC: (GNU) 11.3.0"
	.section	.note.GNU-stack,"",@progbits
```
{% endtab %}

{% tab title="circle.s x86" %}
```python
        .section        __TEXT,__text,regular,pure_instructions
        .build_version macos, 14, 0     sdk_version 14, 2
        .section        __TEXT,__literal8,8byte_literals
        .p2align        3, 0x0                          ## -- Begin function calculateArea
LCPI0_0:
        .quad   0x400921f9f01b866e              ## double 3.1415899999999999
LCPI0_1:
        .quad   0x401921f9f01b866e              ## double 6.2831799999999998
        .section        __TEXT,__text,regular,pure_instructions
        .globl  _calculateArea
        .p2align        4, 0x90
_calculateArea:                         ## @calculateArea
        .cfi_startproc
## %bb.0:
        pushq   %rbp
        .cfi_def_cfa_offset 16
        .cfi_offset %rbp, -16 
        movq    %rsp, %rbp
        .cfi_def_cfa_register %rbp
        movsd   %xmm0, -8(%rbp)
        movsd   -8(%rbp), %xmm0                 ## xmm0 = mem[0],zero
        movsd   LCPI0_1(%rip), %xmm1            ## xmm1 = mem[0],zero
        divsd   %xmm1, %xmm0
        movsd   %xmm0, -16(%rbp)
        movsd   LCPI0_0(%rip), %xmm0            ## xmm0 = mem[0],zero
        mulsd   -16(%rbp), %xmm0
        mulsd   -16(%rbp), %xmm0
        popq    %rbp
        retq
        .cfi_endproc
                                        ## -- End function
.subsections_via_symbols
```
{% endtab %}

{% tab title="testcirle.s arm" %}
```armasm
	.file	"testcircle.c"
	.text
	.section	.rodata.str1.1,"aMS",@progbits,1
.LC0:
	.string	"Enter radius of circle: "
.LC1:
	.string	"%lf"
	.section	.rodata.str1.8,"aMS",@progbits,1
	.align 8
.LC3:
	.string	"Invalid input. Must be a positive number."
	.align 8
.LC4:
	.string	"The area of the circle is: %.2f\n"
	.section	.text.startup,"ax",@progbits
	.p2align 4
	.globl	main
	.type	main, @function
main:
.LFB39:
	.cfi_startproc
	subq	$24, %rsp
	.cfi_def_cfa_offset 32
	leaq	.LC0(%rip), %rsi
	movl	$1, %edi
	movq	%fs:40, %rax
	movq	%rax, 8(%rsp)
	xorl	%eax, %eax
	call	__printf_chk@PLT
	xorl	%eax, %eax
	movq	%rsp, %rsi
	leaq	.LC1(%rip), %rdi
	call	__isoc99_scanf@PLT
	cmpl	$1, %eax
	jne	.L2
	movsd	(%rsp), %xmm0
	pxor	%xmm1, %xmm1
	comisd	%xmm0, %xmm1
	jnb	.L2
	call	calculateArea@PLT
	movl	$1, %edi
	movl	$1, %eax
	leaq	.LC4(%rip), %rsi
	call	__printf_chk@PLT
	movq	8(%rsp), %rax
	subq	%fs:40, %rax
	jne	.L9
	xorl	%eax, %eax
	addq	$24, %rsp
	.cfi_remember_state
	.cfi_def_cfa_offset 8
	ret
.L2:
	.cfi_restore_state
	leaq	.LC3(%rip), %rdi
	call	puts@PLT
	movl	$1, %edi
	call	exit@PLT
.L9:
	call	__stack_chk_fail@PLT
	.cfi_endproc
.LFE39:
	.size	main, .-main
	.ident	"GCC: (GNU) 11.3.0"
	.section	.note.GNU-stack,"",@progbits

```
{% endtab %}

{% tab title="testcircle.s x86" %}
```armasm
 .section        __TEXT,__text,regular,pure_instructions
        .build_version macos, 14, 0     sdk_version 14, 2
        .globl  _main                           ## -- Begin function main
        .p2align        4, 0x90
_main:                                  ## @main
        .cfi_startproc
## %bb.0:
        pushq   %rbp
        .cfi_def_cfa_offset 16
        .cfi_offset %rbp, -16
        movq    %rsp, %rbp
        .cfi_def_cfa_register %rbp
        subq    $32, %rsp
        movl    $0, -4(%rbp)
        leaq    L_.str(%rip), %rdi
        movb    $0, %al
        callq   _printf
        leaq    L_.str.1(%rip), %rdi
        leaq    -16(%rbp), %rsi
        movb    $0, %al
        callq   _scanf
        cmpl    $1, %eax
        jne     LBB0_2
## %bb.1:
        xorps   %xmm0, %xmm0
        ucomisd -16(%rbp), %xmm0
        jb      LBB0_3
LBB0_2:
        leaq    L_.str.2(%rip), %rdi
        xorl    %eax, %eax
                                        ## kill: def $al killed $al killed $eax
        callq   _printf
        movl    $1, %edi
        callq   _exit
LBB0_3:
        movsd   -16(%rbp), %xmm0                ## xmm0 = mem[0],zero
        callq   _calculateArea
        movsd   %xmm0, -24(%rbp)
        movsd   -24(%rbp), %xmm0                ## xmm0 = mem[0],zero
        leaq    L_.str.3(%rip), %rdi
        movb    $1, %al
        callq   _printf
        xorl    %eax, %eax
        addq    $32, %rsp
        popq    %rbp
        retq
        .cfi_endproc
                                        ## -- End function
        .section        __TEXT,__cstring,cstring_literals
L_.str:                                 ## @.str
        .asciz  "Enter the circumference of the circle (positive number): "


L_.str.1:                               ## @.str.1
        .asciz  "%lf"


L_.str.2:                               ## @.str.2
        .asciz  "Invalid input. Circumference must be a positive number."


L_.str.3:                               ## @.str.3
        .asciz  "The area of the circle is: %.2f"


.subsections_via_symbols
```

&#x20; &#x20;

\

{% endtab %}
{% endtabs %}



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

