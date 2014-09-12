ECE382_Lab1
===========
created by Austin Bolinger
ECE 382: Lab 1
Start Date: 08 SEP 14
Edited: 08 SEP 14
Edited: 09 SEP 14
Edited: 10 SEP 14
End Date: 10 SEP 14

Lab 1 is creating a simple calculator in code composser in assembly language.

The purpose of this lab is to use what we have learned in class of assembly language to create a simple calculator. It will involve skills with the instruction set, addressing modes, conditional jumps, status register flags, assembler directives, the assembly process, and more. The calculator is simple because it does not have an interface or GUI. The instructions are a set of bytes in a series stored in ROM. The code needs to read every other bit as a number and followed by an operation. The answers after each operation need to be stored in RAM. The calculator needs to handle the add, subtract, clear, and end functions. The calculator for “B” and “A” functionality needs to handle overflow at 0 and 255 and perform multiplication respectively for those letter grades. To receive even more points in the “A” functionality multiplication part, the calculator needs to operate at O(nlogn) speed. 


##Prelab

###Pseudo Code

o	Equate operands to specified byte sequences 

o	Set apart RAM storage locations (x20)

oType a series of bytes into ROM for calculator sequence

o	If even byte, recognize as number

o	If odd byte, recognize as operand

-	Store answer, like accumulator, in progressing RAM locations, starting at 0x0201

-	Use answer from accumulator for next operand

-	If operation exceeds 255, max the answer at 255 (B functionality)

-	If operation falls below 0, min the answer at 0 (B functionality)

o	Loop back through until END_OP is recognized

o	Recognize ADD, SUBTRACT, MULTIPLY (A functionality), CLEAR, and END as operands

-	If ADD, use add

-	If SUBTRACT, use add with a twos complement

-	If MULTIPLY, look up multiply function in datasheet

-	If CLEAR, store a zero

-	If END, jump forever


###Flow Chart
![Flow Chart](https://github.com/Austinbolinger/ECE382_Lab1/blob/master/flowChart.JPG?raw=true "Flow Chart")

#B Functionality

This part needs to be able to handle the max and min of each calculation. If the numbers exceed 255 or fall below 0, the calculator needs to cap the answers at  the max and min. This means the calculator needs to recognize the when the Carry bit is set to “1”. 

#A Functionality 

This part needs to handle multiplication and hopefully at O(nlogn). To achieve this, the calculator loops through and recognizes even and odd numbers. Ever multiple of two, the calculator shifts the accumulator left effectively doubling the answer. At the end, if the operand was odd, the original number needs to be added to the accumulator.

#Test Cases

###Required Functionality

0x11, 0x11, 0x11, 0x11, 0x11, 0x44, 0x22, 0x22, 0x22, 0x11, 0xCC, 0x55

Result: 0x22, 0x33, 0x00, 0x00, 0xCC

###B Functionality

0x11, 0x11, 0x11, 0x11, 0x11, 0x11, 0x11, 0x11, 0xDD, 0x44, 0x08, 0x22, 0x09, 0x44, 0xFF, 0x22, 0xFD, 0x55

Result: 0x22, 0x33, 0x44, 0xFF, 0x00, 0x00, 0x00, 0x02

###A Functionality 

0x22, 0x11, 0x22, 0x22, 0x33, 0x33, 0x08, 0x44, 0x08, 0x22, 0x09, 0x44, 0xff, 0x11, 0xff, 0x44, 0xcc, 0x33, 0x02, 0x33, 0x00, 0x44, 0x33, 0x33, 0x08, 0x55

Result: 0x44, 0x11, 0x88, 0x00, 0x00, 0x00, 0xff, 0x00, 0xff, 0x00, 0x00, 0xff

#Results

