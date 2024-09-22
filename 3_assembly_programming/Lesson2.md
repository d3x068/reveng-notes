# Proper program exit
After successfully learning how to execute a system call in Lesson 1 we now need to learn about one of the most important system calls in the kernel, sys_exit.

```asm
SECTION .data
msg     db      'Hello World!',0Ah

SECTION .text
global  _start

_start:

    mov     edx, 13
    mov     ecx, msg
    mov     ebx, 1
    mov     eax, 4
    int     80h

    mov     ebx, 0
    mov     eax, 1
    int     80h
```
## 64 bit
```asm
SECTION .data
msg     db      'Hello world!',0Ah

SECTION .text
global  _start

_start:
        mov     rdx, 13
        mov     rsi, msg
        mov     rdi, 1
        mov     rax, 1
        syscall

        mov     rax, 60
        xor     rdi, rdi
        syscall

```
```
$ nasm -f elf64 hello64.asm
$ ld hello64.o -o hello64
```