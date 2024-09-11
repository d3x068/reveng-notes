# Pointers and Memory Management

A pointer is a variable that stores the memory address of another variable.
Syntax :

## Key Concepts of Pointers
1. Pointer Declaration : The * symbol is used to declare a pointer variable
2. Address-of Operator : The & symbol is used to get the address of a variable
3. Dereference Operator: The * symbol is used to access the value at the memory address stored by the pointer.

```
#include <stdio.h>

int main(int argc, char const *argv[])
{
    int a = 5;
    int *ptr = &a;

    printf("the value of a : %d\n",a);
    printf("the address of a : %d\n",&a);
    printf("the address of ptr : %d\n",ptr);
    printf("dereference of ptr : %d\n",*ptr);

    return 0;
}
```


# Structures, Unions, and Bitwise Operations

# Function Pointers

# Stack and Heap Memory Management

# Arrays and Strings

# Recursion

# Working with Files