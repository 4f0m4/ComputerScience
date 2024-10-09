## Summary
This assembly program prompts the user to enter two three-digit numbers and reads the digits separately. It then subtracts the corresponding digits of the second number from the first using BCD (Binary-Coded Decimal) arithmetic, adjusting for any necessary borrowing. Finally, it displays the result of the subtraction as a three-digit number.

## code


```
 .model small
.stack 100h
.data
    a db 'Enter two three-digit numbers:$'
    newline db 0Dh, 0Ah, '$' ; Newline character sequence
    num1 db 0, 0, 0        ; Variable to store the first number as three separate digits
    num2 db 0, 0, 0        ; Variable to store the second number as three separate digits
    result db 0, 0, 0    ; Variable to store the result as three separate digits

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

    ; Subtract the digits
    mov al, [num1 + 2] ; Third digit of the first number
    sub al, [num2 + 2] ; Subtract the third digit of the second number
    das                ; Adjust for BCD arithmetic (subtraction)
    mov [result + 2], al ; Store the third digit of the result

    mov al, [num1 + 1] ; Second digit of the first number
    sub al, [num2 + 1] ; Subtract the second digit of the second number
    das                ; Adjust for BCD arithmetic (subtraction)
    mov [result + 1], al ; Store the second digit of the result

    mov al, [num1]     ; First digit of the first number
    sub al, [num2]     ; Subtract the first digit of the second number
    das                ; Adjust for BCD arithmetic (subtraction)
    mov [result ], al ; Store the first digit of the result

   

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

    mov ah, 9
    lea dx, newline ; Print a final newline
    int 21h

    mov ah, 4ch
    int 21h
main endp

end main

```
