ECE382_Lab1 - Simple Calculator
===========
created by Austin Bolinger
ECE 382: Lab 1
Start Date: 08 SEP 14
Edited: 08 SEP 14
Edited: 09 SEP 14
Edited: 10 SEP 14
End Date: 10 SEP 14

Lab 1 is creating a simple calculator in code composer  in assembly language.

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

#Hardware Schematic

![MSP430G2553](http://www.kerrywong.com/blog/wp-content/uploads/2012/03/MSP430G2ExtProg3.jpg?raw=true "MSP430G2553")

![MSP430G2553 Schematic](http://cnx.org/resources/485bbea47ead3338e654ae805f15bc09/graphics3.png?raw=true "MSP430G2553 Schematic")

#CODE
###Required Functionality Code
https://github.com/Austinbolinger/ECE382_Lab1/blob/master/lab1RequiredFunctionality.txt
###B Functionality Code
https://github.com/Austinbolinger/ECE382_Lab1/blob/master/lab1BFunctionality.txt
###A Functionality Code
https://github.com/Austinbolinger/ECE382_Lab1/blob/master/lab1AFunctionality.txt

#Debugging/Testing
### Modified Code
https://github.com/Austinbolinger/ECE382_Lab1/blob/master/TouchUp.txt
### Final Code
https://github.com/Austinbolinger/ECE382_Lab1/blob/master/finalTurnIn.txt

Debugging involved a step by step process. I started my process by checking the required functionality. I first made sure each register I need was initialized with a zero like I requested in my code. Then, I moved on to checking that my labels like myProgram and myResults existed. I found out with the help of Dr. York that I needed to initialize ROM before my stop dog watch and reset functions otherwise the program interrupts the code as hex code. After my program was initialized correctly, I stepped through my addition process. I noticed that the addition worked nicely but that was literally all my program did. After talking to C2C Niquette, I understood the importance of a program counter. I thought I could just ask myProgram to increment, but was unable to without the help of another variable register that counted for me. I also realized that I was not doing conditional jumps but unconditional jumps which would never allow for anything but a jump to addition.

Next up, B functionality debugging. This one required an understanding of the Carry flag. I made a code for over flow for addition and multiply and an overflow for subtraction. The both checked for the carry flag set, but one set the result array to 255 and the other to 0. I noticed while debugging that I checked for the carry flag in the wrong spot so it never jumped to that function. After moving the check to right after the math portion, I than noticed that my overflow function needed to increment the counters. 

Last is A functionality. This was hard and took a lot of time to analyze how to go about this. I settled on attempting the O(logn) time. After many hours of working on the code logic I needed to shift and add to create code with the shortest run time, I found out that how I thought code for multiplication and shifting worked was wrong. I determined that the code was not worth the time to recode. I did not look it up online because I am lame. So my multiplication function does not work properly. 

#Results
I showed my results for the required and B functionality to Dr. York. Both work fine and do not seem to error in any way. Multiplication does not work correctly.

#Documentation
Worked in class and got help occasionally  from Dr. York, he checked my logic behind my ideas

C2C Niquette - explained how and why I need to use a pointer for each of my arrays(crucial), otherwise the array would never	increment properly.
