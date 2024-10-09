## summary
This assembly program prompts the user to enter a single-digit number and determines if it is even or odd. It reads the input until the Enter key is pressed, checks the number by dividing it by 2, and displays a message indicating whether the number is "EVEN" or "ODD." Finally, it exits gracefully.

## code


```

.MODEL SMALL
.STACK 100H
.DATA
    
    MSG1    DB  'Enter a number: $'
    MSG2    DB  10,13,'The number is EVEN...!!!$'
    MSG3    DB  10,13,'The number is ODD...!!!$'


.CODE

MAIN PROC
    
    MOV AX, @DATA
    MOV DS, AX
    
    MOV AH, 9
    LEA DX, MSG1    
    INT 21H
    
    MOV BH, 0               ; initialize BH as 0 for previous digit
    MOV BL, 10D                 ; store 10 in BL to multiply and make number

INPUT:

    MOV AH, 1
    INT 21H
    
    CMP AL, 13D             ; check if ENTER is pressed (input is carriage-return or 13D)
    JE CHECK
    MOV BH, AL    
    JMP INPUT               ; Or take input as long as ENTER is not pressed
    
CHECK:
                            
    MOV BL, 2                   ; store 2 in BL to divide the number
    
    MOV AL, BH              ; get the number from BH
    
    DIV BL                  ; divide number by 2
    
    CMP AH, 0               ; check AH for remainder
    JE EVEN                     ; if remainder is 0, then EVEN

ODD:    
    MOV AH, 9
    LEA DX, MSG3
    INT 21H
    JMP EXIT
    
EVEN:
    
    MOV AH, 9
    LEA DX, MSG2
    INT 21H
    
EXIT:
    
    MOV AH, 4CH
    INT 21H
    MAIN ENDP
END MAIN
    
```
