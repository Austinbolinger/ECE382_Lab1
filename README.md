ECE382_Lab1
===========
created by Austin Bolinger
ECE 382: Lab 1
Start Date: 08 SEP 14
Edited: 09 SEP 14
End Date: 09 SEP 14

Lab 1 is creating a simple calculator in code composser in assembly language.

##Prelab

###Pseudo Code
-	Equate operands to specified byte sequences 
-	Set apart RAM storage locations (x20)
-	Type a series of bytes into ROM for calculator sequence
-	If even byte, recognize as number
-	If odd byte, recognize as operand
o	Store answer, like accumulator, in progressing RAM locations, starting at 0x0201
o	Use answer from accumulator for next operand
o	If operation exceeds 255, max the answer at 255 (B functionality)
o	If operation falls below 0, min the answer at 0 (B functionality)
-	Loop back through until END_OP is recognized
-	Recognize ADD, SUBTRACT, MULTIPLY (A functionality), CLEAR, and END as operands
o	If ADD, use add
o	If SUBTRACT, use add with a twos complement
o	If MULTIPLY, look up multiply function in datasheet
o	If CLEAR, store a zero
o	If END, jump forever


###Flow Chart
![Flow Chart](https://github.com/Austinbolinger/ECE382_Lab1/blob/master/flowChart.JPG?raw=true "Flow Chart")
