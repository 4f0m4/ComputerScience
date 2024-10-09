
## summary
This assembly program demonstrates basic stack operations by pushing two characters onto the stack. Here’s a concise breakdown of its functionality:

### Key Features:
1. **User Input**: It prompts the user to enter two characters sequentially.
2. **Push to Stack**: Each entered character is pushed onto the stack using the `push` instruction.
3. **Output Messages**: After each push operation, it displays confirmation messages to indicate that the characters have been successfully pushed onto the stack.
4. **Newline Handling**: It includes newlines for better formatting in the output.

### Flow:
1. The program starts by displaying a prompt for the first character.
2. After the user inputs the character, it is pushed onto the stack, followed by a confirmation message.
3. It repeats the process for the second character.
4. Finally, it exits gracefully.

## code
```
.model small
.stack 100h
.data
    a db 'Enter the first character to push on stack: $'  
    b db 'Enter the second character to push on stack: $'
    c db 'First character pushed on the stack',0Dh, 0Ah, '$'
    d db 'Second character pushed on the stack',0Dh, 0Ah, '$'
    newline db 0Dh, 0Ah, '$' ; Newline character sequence
   

.code
main proc
    mov ax, @data
    mov ds, ax
    
    mov ah, 9
    lea dx, a
    int 21h
    
    mov ah, 1
    int 21h
    push ax  ; Push the first character onto the stack
    
    mov ah, 9
    lea dx, newline
    int 21h 
    
     mov ah, 9
    lea dx, c
    int 21h 
    
     mov ah, 9
    lea dx, newline
    int 21h
    
    mov ah, 9
    lea dx, b
    int 21h
    
    mov ah, 1
    int 21h
    push ax  ; Push the 2nd character onto the stack
    
    mov ah, 9
    lea dx, newline
    int 21h
    
    mov ah, 9
    lea dx, d
    int 21h

   
    
    mov ah, 4ch
    int 21h
main endp

end main
```
