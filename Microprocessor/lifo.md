This assembly program demonstrates basic stack operations by pushing and popping characters onto and from the stack. Here’s a breakdown of its functionality:

### Key Features:
1. **User Input**: It prompts the user to enter two characters one after the other.
2. **Push to Stack**: Each character entered by the user is pushed onto the stack.
3. **Pop from Stack**: The program pops the characters from the stack in the reverse order they were pushed and displays them.
4. **Output Messages**: Confirmation messages are displayed before and after popping each character to indicate the operation.

### Flow:
1. The program starts by displaying a prompt for the first character and pushes it onto the stack.
2. It prompts for the second character and also pushes it onto the stack.
3. After the second character is pushed, it pops the first character from the stack and displays it.
4. It then pops the second character from the stack and displays it.
5. Finally, the program exits gracefully.


## code
```
.model small
.stack 100h
.data
    a db 'Enter the first character to push on stack: $'  
    b db 'Enter the second character to push on stack: $'
    c db 'First character popped from the stack: $'
    d db 'Second character popped from the stack: $'
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
    lea dx, b
    int 21h
    
    mov ah, 1
    int 21h
    push ax  ; Push the 2nd character onto the stack
    
    mov ah, 9
    lea dx, newline
    int 21h
    
    mov ah, 9
    lea dx, c
    int 21h

    pop ax   ; Pop the first character from the stack

    mov ah, 2
    mov dl, al
    int 21h
    
    mov ah, 9
    lea dx, newline
    int 21h

    mov ah, 9
    lea dx, d
    int 21h

    pop ax   ; Pop the second character from the stack

    mov ah, 2
    mov dl, al
    int 21h
    
    mov ah, 4ch
    int 21h
main endp

end main
```
