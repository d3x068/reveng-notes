# Intro to Assembly Language
Each assembly language instruction represents one machine instruction, and it depends on the CPU architecture (x86, ARM, etc).

## Key Concepts
### Registers
small, fast storage locations in the CPU used for operations. 
1. Common registers in x86 :
- EAX, EBX, ECX, EDX : general purpose registers. Used for storing temp data, counters, pointers, etc.
- ESP : stack pointer.
- EBP : base pointer.
- EIP : instruction pointer.
```assembly
MOV EAX, 5      ; Move the value 5 into the eax register
ADD EAX, 3      ; Add 3 to the value in eax. Now eax holds 8.
MOV [var], EAX  ; Store the value from eax into memory (at address var)
```
2. Common registers in ARM
arm uses a simplified set of instructions. ARM typically has 16 general-purpose registers which include :
- R0-R12: general purpose registers. R0-R3 are used to pass function arguments and return values
- R13 (SP - Stack Pointer): points to the top of the stack
- R14 (LR - Link register): stores the return address when a function is called (similar to RET in x86)
- R15 (PC - program counter): holds the address of the next instruction to execute (similar to EIP in x86)
```asm
MOV R0, #5      ; Move the value 5 into register R0
ADD R1, R0, #3  ; Add 3 to the value in R0. store result in R1 (R1 now holds 8)
STR R1, [var]   ; Store the value from R1 into memory (at address 'var')
```
### Instructions
Commands for the CPU
### Memory Addressing
How data is accessed
### Stack
### Flags

# Basic Instructions

# Assembly Example : Simple Function
```c
int add(int a,int b){
    return a + b;
}

int main(){
    int result = add(5,10);
    return result;
}
```

```assembly
section .text
global _main

_add:
    ; Function prologue (setting up the stack)
    PUSH EBP          ; Save base pointer
    MOV EBP, ESP      ; Set up stack frame

    ; Add the two parameters (a, b)
    MOV EAX, [EBP+8]  ; Load first argument (a) into EAX
    ADD EAX, [EBP+12] ; Add second argument (b) to EAX

    ; Function epilogue (cleaning up the stack)
    POP EBP           ; Restore base pointer
    RET               ; Return

_main:
    ; Call the add function
    PUSH 20           ; Push second argument (b) onto the stack
    PUSH 10           ; Push first argument (a) onto the stack
    CALL _add         ; Call the add function

    ; Store the result and return
    MOV [result], EAX ; Store the result in memory
    RET

```


# Registers and Memory Access

# The Stack and Function Calls

# Disassembly and Reverse Engineering