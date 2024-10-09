## summary

This assembly program displays a binary string (`"01011"`), then swaps each '0' with '1' and each '1' with '0' in the string. After the swapping process, it prints the modified string. Finally, the program exits gracefully. 

### Key Points:
- **Input String**: The binary string is stored as `'01011$'`.
- **Swapping Logic**: The program uses a loop to iterate through each character, checking if it's '0' or '1' and swapping them accordingly.
- **Display**: The original and modified strings are displayed using DOS interrupts.
## code

```
.model small
.stack 100h
.data
bin db '01011$'

.code
swap_zero:
mov byte ptr [si], '1'
inc si
jmp swap_loop

swap_one:
mov byte ptr [si], '0'
inc si
jmp swap_loop


main proc
    mov ax, @data
    mov ds, ax

    ; Display the original string
    mov ah, 9
    lea dx, bin
    int 21h

    ; Swap '0' and '1' in the string
    lea si, bin
    mov cx, 5  ; Assuming the string length is 5

    swap_loop:
    mov al, [si]
    cmp al, '0'
    je swap_zero
    cmp al, '1'
    je swap_one

    inc si
    loop swap_loop

    ; Display the modified string
    mov ah,2
    mov dl,10
    int 21h
    mov dl,13
    int 21h
    
      mov ah, 9
    lea dx, bin
    int 21h


    ; Exit the program
    mov ah, 4Ch
    int 21h

    main endp
end main

```
