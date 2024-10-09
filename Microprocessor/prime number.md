## Summary

### Program Summary:
This assembly program checks if a given number is prime.

### Key Points:
- **Input**: Prompts the user to enter a number.
- **Process**: 
  - Converts the input character to a number.
  - Checks if the number is prime by dividing it by all integers from 2 up to the number itself.
- **Output**: Displays whether the number is prime or not.

### Messages:
- "Enter a number:"
- "The number is PRIME...!!!"
- "The number is NOT PRIME...!!!"


## code

```
.MODEL SMALL
.STACK 100H
.DATA
    
    MSG1    DB  'Enter a number: $'
    MSG2    DB  10,13,'The number is PRIME...!!!$'
    MSG3    DB  10,13,'The number is NOT PRIME...!!!$'


.CODE

MAIN PROC
    
    MOV AX, @DATA
    MOV DS, AX
    
    MOV AH, 9
    LEA DX, MSG1    
    INT 21H
    
    MOV BH, 0               
    MOV BL, 10D                 

INPUT:

    MOV AH, 1
    INT 21H
    
    CMP AL, 13D             
    JE CHECK

NUMBER:
                            
    SUB AL, 30H             
    MOV CL, AL                  
    MOV AL, BH              
    
    MUL BL                  
    ADD AL, CL                  
    MOV BH, AL              
    
    JMP INPUT               
    
CHECK:
    
    CMP BH, 1               
    JLE NOT_PRIME               
    
    MOV CL, 2               
    
    MOV AX, 0               
    
    MOV AL, BH              
    DIV CL                      
    
    MOV CL, AL              
    
ISPRIME:
                            
    CMP CL, 1               
    JE PRIME                    
    
    MOV AX, 0               
    
    MOV AL, BH              
    DIV CL                      
    
    DEC CL                  
    CMP AH, 0                   
    JE NOT_PRIME                    
    JMP ISPRIME
                            
PRIME:  
  
    MOV AH, 9
    LEA DX, MSG2
    INT 21H
    JMP EXIT
    
NOT_PRIME:
    
    MOV AH, 9
    LEA DX, MSG3
    INT 21H
    
EXIT:
    
    MOV AH, 4CH
    INT 21H
    MAIN ENDP
END MAIN
    
    
```
