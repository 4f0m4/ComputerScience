## Summary

This assembly program reads a string input from the user, reverses it, and then displays the reversed string. Here’s a breakdown of its functionality:

### Key Features:
1. **Input Prompt**: It displays a message asking the user to enter a string.
2. **String Input**: It reads characters one by one until the Enter key (carriage return) is pressed, storing them in a buffer.
3. **String Reversal**: After input is complete, it reverses the string by decrementing the pointer and printing characters in reverse order.
4. **Output**: It displays the reversed string to the console.

### Key Points:
- **Data Section**: The program defines strings for messages and a buffer for the input string.
- **Looping**: The program uses loops to read input and display the reversed string.
- **Character Handling**: It processes each character and displays it in reverse order.

## code

```
.MODEL SMALL
.STACK 100H
.DATA
    MSG1        DB 'Enter a string: $'
    MSG2        DB 10, 13, 'Reversed string: $'
    inputStr    DB 100          ; Maximum string length
    newline db 0Dh, 0Ah, '$' ; Newline character sequence


.code
main proc
    mov ax,@data
    mov ds,ax
    mov si,offset inputStr 
    
    ;display msg
    mov ah, 9
    lea dx, MSG1
    int 21h

input: 
    mov ah,1
    int 21h
    cmp al,13
    je printline
    mov [si],al
    inc si
    jmp input 
    
printline:
     mov ah,2
     mov dl, 0Dh
     int 21h
     mov ah,2
     mov dl, 0Ah
     int 21h 
     ;display msg
     mov ah, 9
     lea dx, MSG2
     int 21h

display:

    dec si
    cmp [si],'$'
    je exit
    
    mov ah,2
    mov dx, [si]
    int 21h
    
    
    
    jmp display 
    
exit:
 MOV AH, 4CH
    INT 21H

MAIN ENDP
END MAIN
```
