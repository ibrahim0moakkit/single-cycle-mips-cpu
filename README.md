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




### main decoder table

WHERE "controls" terminal (in verilog code) is
               
               
               controls = regwrite regdst alusrc branch memwrite memtoreg jump aluop


|  Instruction | Opcode |RegWrite|RegDst|ALUSrc|Branch|MemWrite|MemtoReg|Jump|ALUOp|
| ------- | ------- | -------- | ------- | ------- | ------ | ------- | ------| --- | -----|
| R-Type | 000000 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 10|
| lw | 100011 | 1 | 0 | 1 | 0 | 0 | 1| 0 | 00|
| sw | 101011 | 0 | x | 1 | 0 | 1 | x| 0 | 00|
| beq | 000100 | 0 | x | 0 | 1 | 0 | x| 0 | 01|
| addi | 001000 | 1 | 0 | 1 | 0 | 0 | 0| 0 | 00|
| j | 000010 | 0 | x | x | x | 0 | x| 1 | xx|
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



           addi $2, $0, 5 # ALUOut=5 Machine code: 20020005 , $2=5

           addi $3, $0, 12 #   ALUOut=12 Machine code: 2003000c  , $3=12
           
           addi $7, $3, -9 # ALUOut=3 Machine code: 2067fff7   , $7=3
           
           or $4, $7, $2 # ALUOut=7 Machine code: 00e22025 , $4=7
           
           and $5, $3, $4 #  ALUOut=4  Machine code: 00642824 $5=4
           
           add $5, $5, $4 #  ALUOut=11 Machine code: 00a42820 $5=11
           
           beq $5, $7, end #     Machine code: 10a7000a
           
           slt $4, $3, $4 #   ALUOut=0    Machine code:0064202a
           
           slt $4, $7, $2 # ALUOut=1  Machine code: 00e2202a

           add $7, $4, $5 # ALUOut=12 Machine code: 00853820
           
           sub $7, $7, $2 # ALUOut=7 30 Machine code: 00e23822
           
           sw $7, 68($3) # ALUOut=80  Machine code: ac670044
           
           lw $2, 80($0) #ALUOut=80 Machine code: 8c020050
         
           sw $2, 84($0) # ALUOut=84 Machine code: ac020054



as an example to test our code lets take the line "add $5, $5, $4" 

first the opcode is 00000 

and controls = 110000010 which indicates the operation is R-TYPE instruction from the main decoder table

then ALUOp = 10 which tells us from the ALUOo encoding table to look at funct field as shown in the above tabel

and then alucontrol = 010 and funct = 100000 which indicat that our operation is add.

this line should give us ALUOut = 11 by summing srca + srcb as shown in the figure below



![simulation](https://user-images.githubusercontent.com/108411357/180621475-8a65e3b7-0d30-4cdf-ad01-cf6f1d51b620.png)


rearranged the design to make it easy to write code

you have controller module and datapath module, and you have mips module which consists of both controller and datapath modules 

top module consists of (instruction memory, data memory, datapath, controller) modules


![mipsdesign](https://user-images.githubusercontent.com/108411357/181879643-948a21b5-dbbd-40c2-8999-2784339f11d2.jpg)



********************************************************




DONE BY IBRAHIM MOAKKIT🎩


