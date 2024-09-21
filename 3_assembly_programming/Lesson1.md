```asm
; Hello World Program - asmtutor.com
; Compile with: nasm -f elf helloworld.asm
; Link with (64 bit systems require elf_i386 option): ld -m elf_i386 helloworld.o -o helloworld
; Run with: ./helloworld
 
SECTION .data
msg     db      'Hello World!', 0Ah     ; assign msg variable with your message string
 
SECTION .text
global  _start
 
_start:
 
    mov     edx, 13     ; number of bytes to write - one for each letter plus 0Ah (line feed character)
    mov     ecx, msg    ; move the memory address of our message string into ecx
    mov     ebx, 1      ; write to the STDOUT file
    mov     eax, 4      ; invoke SYS_WRITE (kernel opcode 4)
    int     80h
```

# Code Overview
1. SECTION .data : is used to declare initialized data.
2. SECTION .text : this section contains the actual code of the program

# Step by step explanation
1. SECTION .data
```asm
msg     dn      'Hello World!', 0Ah
```
- msg : defines a label msg that points to a string stored in memory
- db : define byte and is used to define a string of bytes
- 'Hello World!' is followed by 0Ah, which is a newline char.
2. Section .text
```asm
global  _start
```
- this makes the _start label visible to the linker as the entry point of the program
3. The _start label
- this is the entry point of the program. execution begins here.
4. inside the start
- it is important to know the syscall write takes 3 arguments and the code for write is 4.
```asm
mov     edx, 13
```
- this moves the value 13 into the edx. as we know that it is 13 chars long
- edx will hold the size_t count as 13
```asm
mov     ecx,msg
```
- this moves the address of the string msg into the ecx register
- ecx will hold the memory address of msg as char *buff
```asm
mov     ebx, 1
```
- this moves the value 1 into the ebx register.
- in linux, 1 is the file descriptor for STDOUT
```asm
mov     eax, 4
```
- this moves the value 4 (which is representative of syscall write) into the eax register
- when you perform an int 80h interrupt with eax set to 4, the os knows that you want to write data to a file descriptor