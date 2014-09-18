/* Write a program that will output a repetitive rectangle signal as below with 1ms high and 19ms low. */

.global output
output:
	MOV R8, LR
	BL wiringPiSetup
	
	MOV R0, #14
	MOV R1, #OUTPUT
	BL pinMode
	
	MOV R0, #14
	MOV R1, #HIGH
	BL digitalWrite
	
	MOV R0, #14
	MOV R1, #LOW
	BL digitalWrite
	BX R8

.global input
input:
	MOV R7, LR
	BL wiringPiSetup
	
	MOV R0, #12
	LDR R1, #INPUT
	BL pinMode
	
	LDR R0, #12
	BL digitalRead
	BX R7

.global io
io:
	MOV R6, LR
	BL wiringPiSetup
	
	MOV R0, #12
	MOV R1, #INPUT
	BL pinMode
	
	MOV R0, #14
	MOV R1, #OUTPUT
	BL pinMode
	
	LDR R0, #12
	BL digitalRead
	
	MOV R1, R0
	MOV R0, #14
	BL digitalWrite
	BX R6
