## Summary

### Program Summary:
This assembly program converts a lowercase letter input by the user into its uppercase equivalent.

### Key Points:
- **Input**: Prompts the user to enter a lowercase letter.
- **Process**: 
  - Reads the character.
  - Converts it to uppercase by subtracting 20h from its ASCII value.
- **Output**: Displays the uppercase character.

### Messages:
- "Enter a lower case letter: "
- "In upper case it is: "

## Code

```
.model small
.stack 100h
.data
cr equ 0dh
lf equ 0ah
msg1 db 'enter a lower case letter : $'
msg2 db 0dh,0ah,'in upper case it is : $'
char db ?,'$'
.code
main proc

    mov ax,@data
    mov ds,ax
    
    lea dx,msg1
    mov ah,9
    int 21h
    
    mov ah,1
    int 21h
    sub al,20h
    mov char,al
    
    lea dx,msg2
    mov ah,9
    int 21h 
    
    mov dl,char
    mov ah,2
    int 21h
    
    mov ah,4ch
    int 21h
    
    main endp
end main
```
