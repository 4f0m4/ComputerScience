## Summary
This assembly program reads a single-digit number as input, representing a grade, and determines the corresponding letter grade based on predefined thresholds:

- **Grades**:
  - A: 90 and above
  - B: 80-89
  - C: 70-79
  - D: 60-69
  - F: below 60

It displays messages for input and the calculated grade using DOS interrupt calls. The program includes a helper function to print strings and another to print a single character.

## code

```
.model small
.stack 100h

.data
    input_msg db 'Enter the number: $'
    grade_msg db 'The grade is: $'
    newline db 13, 10, '$'

.code
    main proc

    mov ax, @data
    mov ds, ax

    mov si, offset input_msg
    call print_string

    mov ah, 01h       ; Read character function
    int 21h           ; Read input character
    sub al, '0'       ; Convert ASCII to numeric value

    cmp al, 90        ; Compare input with grade A
    jge grade_A       ; If input >= 90, jump to grade A

    cmp al, 80        ; Compare input with grade B
    jge grade_B       ; If input >= 80, jump to grade B

    cmp al, 70        ; Compare input with grade C
    jge grade_C       ; If input >= 70, jump to grade C

    cmp al, 60        ; Compare input with grade D
    jge grade_D       ; If input >= 60, jump to grade D

    jmp grade_F       ; Default: jump to grade F

grade_A:
    mov si, offset grade_msg
    call print_string
    mov dl, 'A'
    call print_character
    jmp exit

grade_B:
    mov si, offset grade_msg
    call print_string
    mov dl, 'B'
    call print_character
    jmp exit

grade_C:
    mov si, offset grade_msg
    call print_string
    mov dl, 'C'
    call print_character
    jmp exit

grade_D:
    mov si, offset grade_msg
    call print_string
    mov dl, 'D'
    call print_character
    jmp exit

grade_F:
    mov si, offset grade_msg
    call print_string
    mov dl, 'F'
    call print_character

exit:
    mov si, offset newline
    call print_string

    mov ah, 4Ch       ; Exit to DOS function
    int 21h           ; Call DOS interrupt

print_string:
    mov ah, 02h       ; Print character function

print_string_loop:
    mov dl, [si]
    cmp dl, '$'
    je print_string_end
    int 21h
    inc si
    jmp print_string_loop

print_string_end:
    ret

print_character:
    int 21h           ; Call DOS interrupt
    ret

end main

```
