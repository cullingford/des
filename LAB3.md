/* Write a program that will output a repetitive rectangle signal as below with 1ms high and 19ms low. */

.global output
#include <wiringPi.h> /* Is this necessary? */

output:	MOV R8, LR
	BL wiringPiSetup
	
	MOV R0, #14
	MOV R1, #OUTPUT
	BL pinMode
	
	LDR R0, [time]	/* Error!? */
	MOV R1, #0
	STR R1, [R0]
	
	loop: 	MOV R0, #14
		MOV R1, #HIGH
		BL digitalWrite
		delay 1
		
		MOV R0, #14
		MOV R1, #LOW
		BL digitalWrite
		delay 19
		
		LDR R2, [time]	/* Error!? */
		LDR R3, time	/* Warning!? */
		ADD R3, R3, #20
		STR R3, [R2]
		
		CMP R3, #1000
		BNE loop
	BX R8

.data
.align 4
time:	.WORD 16

.global input
input:	PUSH LR
	BL wiringPiSetup
	
	MOV R0, #12
	LDR R1, #INPUT
	BL pinMode
	
	LDR R0, #12
	BL digitalRead
	POP LR
	BX LR

.global io
io:	PUSH LR
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
