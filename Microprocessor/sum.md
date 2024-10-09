
## summary
This assembly program prompts the user to enter two three-digit numbers, reads the digits, and calculates their sum using BCD (Binary-Coded Decimal) arithmetic. It then displays the result, showing the sum as a four-digit number, including any carry from the addition.

## code

```
.model small
.stack 100h
.data
    a db 'Enter two three-digit numbers:$'
    newline db 0Dh, 0Ah, '$' ; Newline character sequence
    num1 db 0, 0, 0        ; Variable to store the first number as three separate digits
    num2 db 0, 0, 0        ; Variable to store the second number as three separate digits
    result db 0, 0, 0, 0      ; Variable to store the result as three separate digits

.code
main proc
    mov ax, @data
    mov ds, ax

    mov ah, 9
    lea dx, a
    int 21h

    ; Read the first digit
    mov ah, 1
    int 21h
    sub al, '0'
    mov [num1], al

    ; Read the second digit
    mov ah, 1
    int 21h
    sub al, '0'
    mov [num1 + 1], al

    ; Read the third digit
    mov ah, 1
    int 21h
    sub al, '0'
    mov [num1 + 2], al

    mov ah, 9
    lea dx, newline ; Print a newline
    int 21h

    mov ah, 9
    lea dx, a
    int 21h

    ; Read the first digit of the second number
    mov ah, 1
    int 21h
    sub al, '0'
    mov [num2], al

    ; Read the second digit of the second number
    mov ah, 1
    int 21h
    sub al, '0'
    mov [num2 + 1], al

    ; Read the third digit of the second number
    mov ah, 1
    int 21h
    sub al, '0'
    mov [num2 + 2], al

    mov ah, 9
    lea dx, newline ; Print another newline
    int 21h

    ; Calculate the sum of the digits
    mov al, [num1 + 2] ; Third digit of the first number
    add al, [num2 + 2] ; Third digit of the second number
    aam                ; Adjust for BCD arithmetic
    mov [result + 3], al ; Store the third digit of the result
    

    mov al, [num1 + 1] ; Second digit of the first number
    add al, [num2 + 1] ; Second digit of the second number 
    add al, ah         ; Add carry from previous addition
    aam                ; Adjust for BCD arithmetic
    mov [result + 2], al ; Store the second digit of the result

    mov al, [num1]     ; First digit of the first number
    add al, [num2]     ; First digit of the second number
    add al, ah         ; Add carry from previous addition
    aam                ; Adjust for BCD arithmetic
    mov [result+ 1], al   ; Store the first digit of the result  
    
    mov [result], ah   ; Store the carry digit of the result

    ; Display the result
    mov ah, 2
    mov dl, [result]
    add dl, '0'        ; Convert integer to ASCII
    int 21h

    mov dl, [result + 1]
    add dl, '0'        ; Convert integer to ASCII
    int 21h

    mov dl, [result + 2]
    add dl, '0'        ; Convert integer to ASCII
    int 21h
    
    mov dl, [result + 3]
    add dl, '0'        ; Convert integer to ASCII
    int 21h

    mov ah, 9
    lea dx, newline ; Print a final newline
    int 21h

    mov ah, 4ch
    int 21h
main endp

end main
```
