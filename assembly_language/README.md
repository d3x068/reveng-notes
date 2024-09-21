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
Instruction are the basic operations the cpu executes. it really depends on the architecture.
1. Data Movement and Arithmatic
```asm
MOV EAX, 5      ; Move the value 5 into register eax
MOV EBX, EAX    ; copy the value in eax into register ebx


PUSH    EAX     ; push the value in eax onto the stack
POP     EBX     ; pop the top of the stack into ebx

ADD EAX, EBX    ; add the value of ebx to eax
SUB EAX, 10     ; substract the value in eax with 10
```
2. Control flow
- JMP label : unconditional jump to label
- CALL function : call specific function, saving the address of function onto the stack
- RET : return from a function by popping the return address from the stack
- conditional jumps based on flags: JE (jump if equal), JNE (jump if not equal), JG (jump if greater), etc.

### Memory Addressing
How data is accessed. both x86 and arm have different approaches. in x86:
- Immediate : the operand is a constant value
```asm
MOV eax, 10     ; move the immediate value 10 into eax
```
- direct : the operand is a memory address
```asm
MOV eax, [0x00403010]   ; move the value at memory address 0x00403010 into eax
```
- register indirect : the memory address is held in a register
```asm
MOV eax, [ebx]      ; move the value at the memory address in ebx into eax
```
- indexed : the memory address is computed using a base register and an index
```asm
MOV eax, [ebx + ecx * 4]    ; move the value at the memory address (ebx + ecx * 4) into eax
```

### Stack
The stack is a region of memory used for temp storage of data, such as local variables,  return addresses, and function arguments.
- PUSH
- POP
- Calling a function
- Function prologue -> sets up the stack frame
```asm
PUSH    ebp         ; save the old base pointer
MOV     ebp, esp    ; set the new base pointer
SUB     esp, 16     ; allocate space for local var
```
- Function epilogue -> cleans up the stack
```asm
MOV     esp, ebp    ; restore the stack pointer
POP     ebp         ; restore the old base pointer
RET                 ; return to the caller
```

### Flags
Flags are special bits in the CPU that store the results of operations (such as whether a number is zero, negative, or if an overflow occurred).
- Zero flag (ZF) : set if the result of an operation is zero. (JZ for JUMP if Zero, and JE, Jump if equal)
- Sign flag (SF) : set if the result is negative.
- Carry Flag (CF): set if there is an unsigned overflow
- Overflow Flag (OF) : set if signed overflow occurs.
- Parity Flag (PF) : set if the number of set bits in the result is even.
```asm
CMP     eax, 0      ; compare eax with 0
JE      zero_label  ; jump if eax == 0
```
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
    PUSH 10           ; Push second argument (b) onto the stack
    PUSH 5           ; Push first argument (a) onto the stack
    CALL _add         ; Call the add function

    ; Store the result and return
    MOV [result], EAX ; Store the result in memory
    RET

```

# The Stack and Function Calls Example
```asm
section .text
    global _start

_start:
    ; Save the current value of the registers
    PUSH EAX             ; Save EAX on the stack
    PUSH EBX             ; Save EBX on the stack

    ; Now modify the registers
    MOV EAX, 5           ; Set EAX to 5
    MOV EBX, 10          ; Set EBX to 10

    ; Do some operations
    ADD EAX, EBX         ; EAX = EAX + EBX

    ; Restore the original register values
    POP EBX              ; Restore the original EBX value
    POP EAX              ; Restore the original EAX value

    ; Exit
    MOV EAX, 1           ; Syscall number for exit
    MOV EBX, 0           ; Return code 0
    INT 0x80             ; Make the system call

```

# Disassembly and Reverse Engineering
Common RE Steps :
1. Load the binary : open the executable in a disassembler
2. Identify functions : look for function calls and names (like _main, _add).
3. Examine registers : trace how data moves between registers and memory.
4. analyze control flow : follow jumps (JMP, CALL, etc) to understand the program's flow
5. understand the stack : pay attention to how functions use the stack for parameters, return values, and local variables.