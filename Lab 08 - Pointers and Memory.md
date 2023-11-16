- [[#Struct]]
- [[#Pointer]]
- [[#Dynamic Memory Allocation]]
- [[#Lab assignment hints]]

## Struct
- 3 ways to define and instantiate a __*struct*__
```c
// 1. typtedef
typedef struct StructTypeName_struct {
   type item1;
   type item2;
   ...
   type itemN;      
} StructTypeName;

StructTypeName myVar; // define a variable

// 2.
struct StructTypeName {
   type item1;
   type item2;
   ...
   type itemN;      
};
// in this case, keyword 'struct' is required when defining a variable
struct StructTypeName myVar;

// 3. anonymous struct
struct {
   type item1;
   type item2;
   ...
   type itemN;      
} myVar;
```
- use `.` operator to access member variables (e.g., `myVar.item1`)


```c
#include<stdio.h>

struct A { // (2)
    int x;
    float y;
};

struct { // (3)
    char z;
} b1, b2;

struct A foo() { // a function which returns a struct A
    struct A a;
    a.x = 1;
    a.y = 2.0;
    return a;
}

int main() {
    struct A a = foo();
    printf("%d, %.1f\n", a.x, a.y);
    
    b1.z = 'a';
    b2.z = 'b';
    printf("%c%c\n", b1.z, b2.z);
    
    return 0;
}
```

    1, 2.0
    ab


## Pointer
**Pointer**: A variable that holds a memory address.
- A 64-bit system can have a memory size of up to $2^{64}$ bytes theoretically, with each address represented by a 64-bit integer.
- Precede a variable with __reference operator__ `&` to get the memory address of it. $^{(1)}$
- Append `*` after a type to denote a pointer type. $^{(2)}$
- Prefix a pointer with __dereference operator__ `*` to retrieve the value stored in the memory address pointed to by the pointer. $^{(3)}$


```c
#include <stdio.h>

int main() {
    int var = 0x12345678;
    
    // "unsigned long" is a 64-bit integer type
    unsigned long addr = (unsigned long) &var; // (1)
    
    printf("Variable 'var' of type int:\n");
    printf("The beginning address of 'var' in hex: 0x%016lx\n", addr);
    printf("'var' occupies %d bytes (%d bits) of memory.\n", sizeof var, 8 * sizeof(var));
    
    // init a pointer from an address value
    int* ptr = (int*) addr; // (2)
    
    printf("\nPointer variable 'ptr' pointing to 'var':\n");
    printf("'ptr' occupies %d bytes (%d bits) of memory.\n", sizeof ptr, 8 * sizeof(ptr));
    printf("The value of the variable pointed to by 'ptr': %#x\n", *ptr); // (3)
    
    return 0;
}
```

    Variable 'var' of type int:
    The beginning address of 'var' in hex: 0x000000030567a0f8
    'var' occupies 4 bytes (32 bits) of memory.
    
    Pointer variable 'ptr' pointing to 'var':
    'ptr' occupies 8 bytes (64 bits) of memory.
    The value of the variable pointed to by 'ptr': 0x12345678


- pass __by reference__: pass the address
- pass __by value__: pass a copy of the variable


```c
#include <stdio.h>

void pass_by_value(int x) {
    x = 4;
}

void pass_by_reference(int* p_x) {
    *p_x = 4;
}

int main() {
    int x = 2;
    
    pass_by_value(x);
    printf("%d\n", x);
    
    pass_by_reference(&x);
    printf("%d\n", x);
    
    return 0;
}
```

    2
    4


## Dynamic Memory Allocation
- _void_\* [__*malloc*__](https://cplusplus.com/reference/cstdlib/malloc/) (*size_t* size): **Allocate**s a block of *size* bytes of memory, returning a pointer to the beginning of the block.
- _void_ [__*free*__](https://cplusplus.com/reference/cstdlib/free/) (_void_* ptr): **Release**s a block of memory pointed to by _ptr_.
```c
#include <stdlib.h> // standard library

typedef struct A_struct {
    int val;
    struct A_struct *ptr;
} A;

int main() {
    A* p_a = (A*) malloc(sizeof(A));
    
    // dynamically allocate memory for an array of type int of length 5
    int* iarr = (int*) malloc(sizeof(int) * 5);
    
    // dynamically allocate memory for an array of struct A of length 5
    A* arr = (A*) malloc(sizeof(A) * 5);
    
    // free the memory
    free(p_a);
    free(iarr);
    free(arr);

    return 0;
}
```

## Lab assignment hints
[Lab 08: Pointers (instructure.com)](https://tulane.instructure.com/courses/2271434/assignments/14343178)

### 42.14 LAB: Number sequences - memory allocation
**Concatenate**
- Implementing without loops: use function [memcpy](https://cplusplus.com/reference/cstring/memcpy/) from `<string.h>`

