/* Write a program that will output a repetitive rectangle signal as below with 1ms high and 19ms low. */

.global output
#include <wiringPi.h>

output:
	MOV R8, LR
	BL wiringPiSetup
	
	MOV R0, #14
	MOV R1, #OUTPUT
	BL pinMode
	time:	.WORD 10
	loop: 	MOV R0, #14
		MOV R1, #HIGH
		BL digitalWrite
		delay 1
		
		MOV R0, #14
		MOV R1, #LOW
		BL digitalWrite
		delay 19
		
		LDR R3, time
		LDR R4, [R3]
		ADD R4, R4, #20
		STR R4, [R3]
		
		CMP R4, #1000
		BNE loop
	BX R8

.global input
input:
	PUSH LR
	BL wiringPiSetup
	
	MOV R0, #12
	LDR R1, #INPUT
	BL pinMode
	
	LDR R0, #12
	BL digitalRead
	POP LR
	BX LR

.global io
io:
	PUSH LR
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
	POP LR
	BX LR
