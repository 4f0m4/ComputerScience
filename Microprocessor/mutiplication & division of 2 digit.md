## Summary
This assembly program:

1. **Inputs Two Numbers**: Reads digits from the user.
2. **Calculates Multiplication**: Multiplies the two numbers and displays the result.
3. **Calculates Division**: Divides the first number by the second and displays the result, including the decimal part.

### Key Sections:
- **Input Handling**: Reads and constructs numbers.
- **Multiplication**: Uses `MUL` for multiplication.
- **Division**: Uses `DIV` and formats the output.

Results are displayed with appropriate messages.

## Code

```
.MODEL SMALL
.STACK 100H
.DATA

    A       DB ?
    B       DB ?
    C       DB ?
    D       DB ?
    resmul  DB 6 DUP('$') 

    D1      DB ?
    D2      DB ?
    D3      DB ? 
    
    MSG1    DB 'Enter the first number: $'
    MSG2    DB 10, 13, 'Enter the second number: $'
    MSG3    DB 10, 13, 'Result of MULTIPLICATION: $'
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
    JE SECOND      

NUMBER1:

    SUB AL, 30H    
    MOV CL, AL     
    MOV AL, BH     

    MUL BL         
    ADD AL, CL     
    MOV BH, AL     

    JMP INPUT1     

SECOND:

    MOV A, BH       
    mov C, BH

    MOV AH, 9
    LEA DX, MSG2
    INT 21H

    MOV BH, 0       
    MOV BL, 10      

INPUT2:

    MOV AH, 1
    INT 21H

    CMP AL, 13     
    JE CALCULATE

NUMBER2:

    SUB AL, 30H    
    MOV CL, AL     
    MOV AL, BH     

    MUL BL         
    ADD AL, CL     
    MOV BH, AL     

    JMP INPUT2     

CALCULATE:

    MOV B, BH       
    mov D, BH


MULTIPLICATION:

    MOV AH, 9
    LEA DX, MSG3
    INT 21H

    MOV AX, 0       
    MOV AL, A       

    MUL B           

    MOV CX, 6      

    
    MOV SI, OFFSET resmul + 5

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


Division:

    MOV AH, 9
    LEA DX, MSG4            
    INT 21H
                                
    MOV AX, 0               
    XOR DX, DX 
    XOR bX, bX
    XOR cX, cX  
    MOV AL, C                   
    
    DIV D                   
    
    MOV BH, AH              
    
    
DISPLAY:
        
    MOV DL, 100D            
    
    MOV AH, 0
    DIV DL                  
    MOV D1, AL                  
    
    MOV DL, 10D             
   
    MOV AL, AH              
    MOV AH, 0
    DIV DL                  
    MOV D2, AL                  
    
    MOV D3, AH              
    
    MOV AH, 2               
    
    MOV DL, D1              
    ADD DL, 30H                 
    INT 21H                 
    
    MOV DL, D2              
    ADD DL, 30H             
    INT 21H
    
    MOV DL, D3              
    ADD DL, 30H             
    INT 21H 
    
    MOV DL, 46D             
    INT 21H
    
    MOV CL, 8               
    
    
POINT:

    MOV AX, 0               
    MOV AL, BH              
    
    MOV DL, 10D             
    MUL DL                      
    
    DIV B                   
    
    MOV BH, AH              
    
    MOV AH, 2                
    MOV DL, AL              
    ADD DL, 30H
    INT 21H
    
    DEC CL
    CMP CL, 0               
    JNE POINT   





    
    MOV AH, 4CH
    INT 21H

MAIN ENDP
END MAIN
```
