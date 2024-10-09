## Summary
This assembly program generates and displays the Fibonacci series based on user input. Here’s a breakdown of its functionality:

### Key Features:
1. **User Input**: The program prompts the user to enter a number representing how many Fibonacci numbers to display.
2. **Fibonacci Calculation**: It calculates Fibonacci numbers iteratively by adding the two previous numbers together.
3. **Output**: The program prints each Fibonacci number, formatted as three-digit numbers.

### Flow:
1. **Input Handling**:
   - It reads characters from the user until the Enter key is pressed.
   - Converts the entered characters from ASCII to a numerical value.
2. **Fibonacci Logic**:
   - Initializes the first two Fibonacci numbers (0 and 1).
   - Iteratively calculates the next Fibonacci number by adding the last two numbers.
   - The results are stored in a format suitable for display.
3. **Output**:
   - Each Fibonacci number is printed in a three-digit format, including leading zeros if necessary.
4. **Loop**:
   - Continues until the specified number of Fibonacci numbers has been calculated and displayed.

### Code Limitations:
- The program assumes the user will enter a valid number and does not handle invalid input.
- The Fibonacci series generation will stop once it has displayed the specified number of terms.

## code
```
.MODEL SMALL
.STACK 100H
.DATA    

    A   DB  0
    B   DB  1
    C   DB  ?
    
    D1  DB  ?
    D2  DB  ?
    D3  DB  ?
    
    MSG1    DB  'Enter a number: $'
    MSG2    DB  10,13,'The Fibonacci series: $' 
    
    ZERO    DB  '000 $'
    ONE     DB  '001 $' 


.CODE

MAIN PROC
    
    MOV AX, @DATA
    MOV DS, AX
    
    MOV AH, 9
    LEA DX, MSG1    
    INT 21H
    
    MOV CL, 0               
    MOV BL, 10D                 

INPUT:

    MOV AH, 1
    INT 21H
    
    CMP AL, 13D             
    JE NEXT

NUMBER:
                            
    SUB AL, 30H             
    MOV BH, AL                  
    MOV AL, CL              
    
    MUL BL                  
    ADD AL, BH                  
    MOV CL, AL              
    
    JMP INPUT               
    
NEXT:

    MOV AH, 9
    LEA DX, MSG2            
    INT 21H 
    
    CMP CL, 0
    JE EXIT
    
    MOV AH, 9
    LEA DX, ZERO
    INT 21H

    
    DEC CL
    CMP CL, 0
    JE EXIT
    
    LEA DX, ONE
    INT 21H
    
    DEC CL
    CMP CL, 0
    JE EXIT
    
        
CALCULATE: 

    MOV AL, A               
    ADD AL, B               
    MOV C, AL                   
    
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
    
    MOV DL, 20H             
    INT 21H
    
    MOV AL, B               
    MOV A, AL               
    MOV AL, C
    MOV B, AL               
    
    DEC CL
    CMP CL, 0               
    JNE CALCULATE
        
    
EXIT:
    
    MOV AH, 4CH
    INT 21H
    MAIN ENDP
END MAIN
    
    

```
