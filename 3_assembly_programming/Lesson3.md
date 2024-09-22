# Calculate string length
Why? Well sys_write requires that we pass it a pointer to the string we want to output in memory and the length in bytes we want to print out. If we were to modify our message string we would have to update the length in bytes that we pass to sys_write as well, otherwise it will not print correctly.

## Pointer Arithmetic
To calculate the length of the string we will use a technique called pointer arithmetic. Two registers are initialised pointing to the same address in memory. One register (in this case EAX) will be incremented forward one byte for each character in the output string until we reach the end of the string. The original pointer will then be subtracted from EAX. This is effectively like subtraction between two arrays and the result yields the number of elements between the two addresses. This result is then passed to sys_write replacing our hard coded count.

```asm
SECTION .data
msg     db      'Hello world!', 0Ah, 0
SECTION .text
global  _start

_start:
    mov     esi, msg
    xor     ecx, ecx

find_length:
    cmp byte    [esi+ecx], 0
    je      found
    inc     ecx
    jmp     find_length

found:
    mov     edx, ecx
    mov     ecx, msg
    mov     ebx, 1
    mov     eax, 4
    int     80h

    xor     ebx, ebx
    mov     eax, 1
    int     80h

```