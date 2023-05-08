# Assembly Language

Assembly language uses mnemonics, which are short, human-readable text representations of opcodes. They provide a more convenient way to program, making the code human-readable. Mnemonics are specific to a computer's Instruction Set Architecture (ISA) and correspond directly to processor operations like addition, subtraction, loading data, branching, and halting.

For example, the "ADD" mnemonic represents the opcode for addition, while "LOAD" represents the opcode for loading data from memory into a register.

Labels are another useful feature of assembly language, providing a more human-readable way of referring to memory addresses and simplifying the process of writing and maintaining assembly code. Labels are especially helpful for branching, looping, or other control structures that require jumps to different code parts.

```armasm
LOAD R10, [255]    ; Read from memory address 255 (stdin) and store it in register R10
LOAD R11, [255]    ; Read a byte from memory address 255 (stdin) and store it in register R11
MOV R12, #0        ; Set register R12 to 0
MOV R1, #1         ; Set register R1 to 1

LOOP_START:        ; Label for the start of the loop
BZ R10, LOOP_END   ; If the value in register R10 equals 0, jump to address LOOP_END
ADD R12, R11, R12  ; Add the values in registers R11 and R12 and store the result in register R12
SUB R10, R10, R1   ; Decrement register R10 by 1 (the value in register R1)
JMP LOOP_START     ; Jump back to the start of the loop

LOOP_END:          ; Label for the end of the loop
STORE R12, [255]   ; Write the value in register R12 to memory address 255 (stdout)
HALT               ; Halt the program
```



Assembly languages offer many other features, such assembler directives, which are commands or instructions that guide the assembler during the assembly process. Assembler directives perform various tasks, such as defining constants, reserving memory space, specifying memory address origins, defining data elements, and controlling the assembly process.



## Drawbacks of Assembly

* Platform-dependant: Assembly language is specific to a computer's Instruction Set Architecture (ISA)
* Longer to write: more time-consuming and labor-intensive than using high-level languages, which offer more abstract and simplified syntax, built-in functions, libraries, and data structures
