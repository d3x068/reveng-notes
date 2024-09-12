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

Pointers can be incremented and decremented. When you increment a pointer, it moves to the next memory location based on the size of the data type it points to.
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

void changeVal(int *p, int num){
    *p = num;
}

int main(int argc, char const *argv[])
{
    int a = 5;
    int *p = &a;
    printf("initial value of A : %d\n",a);
    changeVal(*p,10); // or you can use changeVal(&a,10)
    printf("value of A after passing by reference : %d\n",a);

    return 0;
}

```

7. Dynamic Memory Allocation

Pointers are used in dynamic memory allocation management. Functions like malloc(), free(), calloc(), and realloc () are require pointers.

```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char const *argv[]){
    int a = 5;
    int *ptr = (int *)malloc(sizeof(int));
    if (ptr != NULL){
        *ptr = 10;
        printf("value of ptr : %d\n",*ptr);
    }

    free(ptr);

    return 0;
}

```


# Structures, Unions, and Bitwise Operations

## Structures
a struct is user defined data types
```c
#include <stdio.h>
#include <stdlib.h>

struct Employee {
    int employee_id;
    char name[50];
    int age;
}

int main(){
    struct Employee ep1;
    ep1.employee_id = 123;
    ep1.age = 25;
    strcpy(ep1.name,"hacker");

    printf("employee with id : %d is %s and %d years old.\n",ep1.employee_id,ep1.name,ep1.age);

    return 0;
}
```


## Unions
A union allows storing different data types in the same memory location but can hold only one type at the time.
```c
#include <stdio.h>
#include <stdlib.h>

union Employee {
    int employee_id;
    char name[50];
    float age;
}

int main(){
    union Employee ep1;
    ep1.age = 25;
    ep1.employee_id = 123;
    strcpy(ep1.name,"hacker");

    printf("hello my name is %s.\n",ep1.name);
    return 0;
}
```

## Bitwise Operations
A bitwise operation commonly used in c and very useful in order to learn reverse engineering, especially for manipulating flags and working with binary data.

### Common Bitwise Operations
AND (&) OR (|) XOR (^) NOT (~) LEFT SHIFT (<<) RIGHT SHIFT (>>)

```C
int a = 5;
int b = 7;
printf("a AND b : %d \n",a & b);
```

# Function Pointers
Function pointers are used to point to functions instead of variables. Syntax : return_type (*pointer_name)(parameter_types,..)

```c
#include <stdio.h>
#include <stdlib.h>

void print_int(int num, int num2){
    printf("the number is : %d and %d\n",num,num2);
}


int main(){
    int a = 5;
    int b = 7;
    void (*fptr)(int,int);
    fptr = &print_int;
    fptr(5,7);

    return 0;
}

```

# Stack and Heap Memory Management
Goals : understanding how memory is managed, allocated, deallocated, and identifying common vuln like buffer overflow

## Stack
- Stack is a region of memory used for storing local variables, function parameters, and return addresses.
- Function Call Stack: when a function is created, a stack frame is created. local variables and return addresses are pushed onto the stack. when the function returns, the frame is popped off.
```c
void print_int(int num){
    printf("the number is : %d\n",num);
}
```

## Heap
Heap is a region of memory used for dynamic memory allocation malloc() and free(). Data stored in heap is persists between function calls until explicitly freed.
```c
int * ptr = (int *)malloc(sizeof(int)); // memory allocated in heap
*ptr = 10;
free(ptr); // memory deallocated in heap
```
# Arrays and Strings
Arrays and strings are basically blocks of memory.
## Arrays
Arrays are contiguous blocks of memory that store multiple elements of the same type.
```c
int arr1[] = {1,2,3,4,5};
```
## Strings
Strings in C are arrays of chars terminated by a null char "\0"
```c
char strings1[] = "Hello world!";
printf("%s",strings1);

```
# Recursion

# Working with Files