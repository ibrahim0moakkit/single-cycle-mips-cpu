# single-cycle-mips-cpu
32-bit single cycle mips processor


Can perform:

## R-Type insructions:

-add

-sub

-and

-or

-slt (set less than)


## I-Type instructions:

-addi

-sw

-lw


## J-Type instructions:

-j

-beq




###main decoder table
|  Instruction | Opcode |RegWrite|RegDst|ALUSrc|Branch|MemWrite|MemtoReg|ALUOp|Jump|
| ------- | ------- | -------- | ------- | ------- | ------ | ------- | ------| --- | -----|
| R-Type | 000000 | 1 | 1 | 0 | 0 | 0 | 0 | 10 | 0|
| lw | 100011 | 1 | 0 | 1 | 0 | 0 | 1| 00 | 0|
| sw | 101011 | 0 | x | 1 | 0 | 1 | x| 00 | 0|
| beq | 000100 | 0 | x | 0 | 1 | 0 | x| 01 | 0|
| addi | 001000 | 1 | 0 | 1 | 0 | 0 | 0| 00 | 0|
| j | 000010 | 0 | x | x | x | 0 | x| xx | 1|
***************************************************
### ALU decoder table
|  ALUOp | funct |ALUControl|
| ------- | ------- | -------- |
| 00 | x | 010 (add) |
| xx | x | 110 (sub) |
| 1x | 100000 (add) | 010 (add) |
| 1x | 100010 (sub) | 110 (sub) |
| 1x | 100100 (and) | 000(and) |
| 1x | 100101 (or) | 001 (or) |
| 1x | 101010 (slt) | 111 (slt) |


*******************************************************
### ALUOp encoding table
| ALUOp  | meaning |
| ------------- | ------------- |
| 00  | add |
| 01  | subtract  |
| 10  | look at funct field  |
| 11  | SHOULD NEVER HAPPEN  |










![single cycle mips cpu pic](https://user-images.githubusercontent.com/108411357/180609488-dd201f40-4677-4da3-8f10-106ea1fde0a7.png)




**********************************************

In memfile.txt we have the machine code for our program that we will run



main:      addi $2, $0, 5 # initialize $2  5 0 Machine code: 20020005
           addi $3, $0, 12 # initialize $3  12 4 Machine code: 2003000c
           addi $7, $3, 9 # initialize $7  3 8 Machine code: 2067fff7
           or $4, $7, $2 # $4  3 or 5  7 c Machine code: 00e22025
           and $5, $3, $4 # $5  12 and 7  4 10 Machine code: 00642824
           add $5, $5, $4 # $5  4  7  11 14 Machine code: 00a42820
           beq $5, $7, end # shouldn’t be taken 18 10a7000a
           slt $4, $3, $4 # $4  12  7  0 1c 0064202a
           beq $4, $0, around # should be taken 20 10800001
           addi $5, $0, 0 # shouldn’t happen 24 20050000
around:    slt $4, $7, $2 # $4  3  5  1 28 00e2202a
           add $7, $4, $5 # $7  1  11  12 2c 00853820
           sub $7, $7, $2 # $7  12  5  7 30 00e23822
           sw $7, 68($3) # [80]  7 34 ac670044
           lw $2, 80($0) # $2  [80]  7 38 8c020050
           j end # should be taken 3c 08000011
           addi $2, $0, 1 # shouldn’t happen 40 20020001
end: sw $2, 84($0) # write adr 84  7 44 ac020054








DONE BY IBRAHIM MOAKKIT🎩


