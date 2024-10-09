## Summary

### Program Summary:
This assembly program converts an uppercase letter input by the user into its lowercase equivalent.

### Key Points:
- **Input**: Prompts the user to enter an uppercase letter.
- **Process**: 
  - Reads the character.
  - Converts it to lowercase by adding 20h to its ASCII value.
- **Output**: Displays the lowercase character.

### Messages:
- "Enter an upper case letter: "
- "In lower case it is: "

## Code

```
.model small
.stack 100h
.data
cr equ 0dh
lf equ 0ah
msg1 db 'enter a upper case letter : $'
msg2 db 0dh,0ah,'in lower case it is : $'
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
    add al,20h
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
