## Summary

### Program Summary:
This assembly program reads an integer \( N \) and prints all even numbers from 0 to \( N \).

### Key Points:
- **Input**: Prompts user for \( N \).
- **Process**: Loops through and generates even numbers.
- **Output**: Displays the even numbers.

### Messages:
- "Enter the value of N:"
- "Even numbers are:" 


## Code

```
.MODEL SMALL
.STACK 100H
.DATA

    N       DB ?
    A       DB ?
    C       DB ?
    D       DW ?
    resmul  DB 6 DUP('$') 
    newline db 0Dh, 0Ah, '$' 

    D1      DB ?
    D2      DB ?
    D3      DB ? 
    
    MSG1    DB 'Enter the value of N:  $'
    MSG2    DB 10, 13, 'Even numbers are: $'
    MSG3    DB 10, 13, 'ODD numbers are: $'
    MSG4    DB 10, 13, 'Result of DIVISION: $'

.CODE

MAIN PROC

    MOV AX, @DATA
    MOV DS, AX

    MOV AH, 9
    LEA DX, MSG1
    INT 21H

    MOV BH, 0       
    MOV BL, 10      

INPUT1:

    MOV AH, 1
    INT 21H

    CMP AL, 13     
    JE Even      

NUMBER1:

    SUB AL, 30H    
    MOV CL, AL     
    MOV AL, BH     

    MUL BL         
    ADD AL, CL     
    MOV BH, AL     

    JMP INPUT1     

Even:
    mov N,bh
    mov ah, 9
    lea dx, newline 
    int 21h 
    lea dx, MSG2
    int 21h
    
    
    MOV A,0       
    mov ah,0
    mov al,A
evenloop:

    
    MOV SI, OFFSET resmul + 5
    mov [resmul + 0],0
    mov [resmul + 1],0
    mov [resmul + 2],0
    mov [resmul + 3],0
    mov [resmul + 4],0
    mov [resmul + 5],0
    mov cx,3

EXTRACT_DIGITS:
    mov bx,10

    XOR DX, DX      

    DIV bx          

    ADD DL, '0'     

    MOV [SI], DL    

    DEC SI          

    DEC CX          

    JNZ EXTRACT_DIGITS 

    
    mov [resmul + 6],'$'
    MOV AH, 9
    LEA DX, resmul
    INT 21H


    add A,2  
    mov ah,0 
    mov al,A
    mov bl,A
    cmp bl,N 
    JNG evenloop
    
exit:
    mov ah,4CH
    int 21H
    main ENDP
END main



    
```
