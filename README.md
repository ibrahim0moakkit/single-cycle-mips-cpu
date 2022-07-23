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
###ALU decoder table
|  ALUOp | funct |ALUControl|
| ------- | ------- | -------- |
| 00 | x | 010 (add) |
| xx | x | 110 (sub) |
| 1x | 100000 (add) | 010 (add) |
| 1x | 100010 (sub) | 110 (sub) |
| 1x | 100100 (and) | 000(and) |
| 1x | 100101 (or) | 001 (or) |
| 1x | 101010 (slt) | 111 (slt) |












![single cycle mips cpu pic](https://user-images.githubusercontent.com/108411357/180609488-dd201f40-4677-4da3-8f10-106ea1fde0a7.png)




**********************************************



DONE BY IBRAHIM MOAKKIT🎩


