# The compiler and assembler

Often, the easiest way to understand the role of software is to explore what development was like before it existed. Back in the day, there was no preprocessor, compiler, assembler, or linker. All coding was done in machine code--a binary language comprised of 0s and 1s. We'll build our way up.&#x20;





Machine code

* Each computer comes with an instruction set architecture, which describes the set up of instructions that the processor can execute. All the intructions in the ISA are in 1s and 0s.&#x20;
* all coding was done in binary--1s and os.&#x20;
* Each sequence of 0s and 1s represents a specific instruction that the computer's processor can directly understand and execute.

```
0111100000000000
1000110011111111
1100110001010101
0001100010001100
1100000001010001
1001100011111111
0000000000000000

10: MOV R0 #1
11: LOAD R1 M17
12: PRINT R1
13: BRZ R1 M16
14: SUB R1 R1 R0
15: BR M12
16: HALT
17: 5


            LOAD R8 #0
LOOP_START: LOAD R0 STDIO
            BRZ R0 LOOP_END
            ADD R8 R8 R12
            BRZ R0 LOOP_START
LOOP_END:   STORE R8 STDIO
            HALT
```



```
Address | instruction 
-----------------------------
10:     |  ld r10 m20   
11:     |  brz r10, m18      
12:     |  lda r12, #0     
13:     |  lda r1, #1   
14:     |  brz r10, m18   
15:     |  add r12, r12, r11
16:     |  sub r10, r10, r1 
17:     |  jmpr m14       
18:     |  str r12 m255   
19:     |  hlt     
-----------------------------
```
