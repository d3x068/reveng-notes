# Pointers and Memory Management

A pointer is a variable that stores the memory address of another variable.
Syntax : (datatype) * (var_name);

## Key Concepts of Pointers
1. Pointer Declaration : The * symbol is used to declare a pointer variable
2. Address-of Operator : The & symbol is used to get the address of a variable
3. Dereference Operator: The * symbol is used to access the value at the memory address stored by the pointer.

```c
#include <stdio.h>

int main(int argc, char const *argv[])
{
    int a = 5;
    int *ptr = &a;

    printf("the value of a : %d\n",a);
    printf("the address of a : %p\n",&a);
    printf("the address of ptr : %p\n",ptr);
    printf("dereference of ptr : %d\n",*ptr);

    return 0;
}
```

4. Pointer Arithmatic
pointers can be incremented and decremented. When you increment a pointer, it moves to the next memory location based on the size of the data type it points to.
```c
int arr[] = {1,2,3,4};
int *ptr = arr; // arr is actually the same with &arr[0]

printf("address stored in ptr is %p. Dereferences : %d\n",ptr,*ptr);
ptr++;
printf("address stored in ptr is %p. Dereferences : %d\n",ptr,*ptr);

```

5. Pointer to Pointer
A pointer to a pointer is a form of multi-level pointer, which stores the address of another pointer.
```c
int a = 5;
int *p1 = &a;
int **p2 = &p1;

printf("address stored in ptr2 is %p. Dereferences : %d\n",p2,**p2);

```

6. Pointers in Function
Pointers can be passed to functions to allow the function to modify the original variable's value (Also known as pass by reference).
```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char const *argv[])
{
    

    return 0;
}

```


# Structures, Unions, and Bitwise Operations

# Function Pointers

# Stack and Heap Memory Management

# Arrays and Strings

# Recursion

# Working with Files