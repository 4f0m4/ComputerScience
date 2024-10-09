## summary
The code displays the message "Farhana Mahbuba bearing roll 20102045" on the screen using DOS interrupts. It then terminates the program gracefully.

## code
```
.model small
.stack 100h
.data
    msg db 'Farhana Mahbuba bearing roll 20102045$'

.code
main proc
    mov ax, @data
    mov ds, ax

    mov ah, 9
    lea dx, msg
    int 21h

    mov ah, 4ch
    int 21h
main endp

end main
```
