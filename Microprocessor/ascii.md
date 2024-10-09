## Summary

### Program Summary:
This assembly program prints the ASCII characters from 0 to 255.

### Key Points:
- **Setup**: Uses DOS interrupt `21h` to print characters.
- **Loop**: 
  - Initializes `dl` to 0 (the first ASCII character).
  - Decrements `cx` from 256 to control the loop for 256 iterations.
- **Output**: Each character corresponding to the current value of `dl` is printed.

### Exit:
The program exits cleanly using DOS interrupt `4Ch`. 

### Notes:
- Ensure the console supports displaying all ASCII characters, as some may not be visible or printable.

## Code

```
.model small
.stack 100h
.code
main proc
    mov ah,2
    mov cx,256
    mov dl,0
print_loop:
int 21h
inc dl
dec cx
jnz print_loop   

mov ah,4ch
int 21h

main endp
end main
```
