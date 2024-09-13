# Intro to Assembly Language
Each assembly language instruction represents one machine instruction, and it depends on the CPU architecture (x86, ARM, etc).

## Key Concepts
### Registers
small, fast storage locations in the CPU used for operations. Common registers in x86 :
- EAX, EBX, ECX, EDX : general purpose registers
- ESP : stack pointer.
- EBP : base pointer.
- EIP : instruction pointer.
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