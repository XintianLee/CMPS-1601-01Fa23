- [[#Basic I/O]]
- [[#C String]]
- [Lab assignment hints](#Lab-assignment-hints)

Compared to Java, C is a **procedural-oriented** programming language and therefore does not have the concept of "class".  
Based on what we've learned so far, the syntax of C is very similar to that of Java.

## Basic I/O
### printf & scanf
- [**printf**](https://cplusplus.com/reference/cstdio/printf/) Writes a formatted C string to the standard output (stdout)

```C
#include <stdio.h> // the standard library of IO

int main() {
    printf ("Characters: %c %c \n", 'a', 65); // use '\n' to add a new line at the end
    printf ("Decimals: %d %ld\n", 1977, 650000L);
    printf ("Preceding with blanks: %10d \n", 1977);
    printf ("Preceding with zeros: %010d \n", 1977);
    printf ("Some different radices: %d %x %o %#x %#o \n", 100, 100, 100, 100, 100);
    printf ("floats: %4.2f %+.0e %E \n", 3.1416, 3.1416, 3.1416);
    printf ("Width trick: %*d \n", 5, 10);
    printf ("%s \n", "A string");
    
    return 0; // exit status code, 0 means success
}
```

    Characters: a A 
    Decimals: 1977 650000
    Preceding with blanks:       1977 
    Preceding with zeros: 0000001977 
    Some different radices: 100 64 144 0x64 0144 
    floats: 3.14 +3e+00 3.141600E+00 
    Width trick:    10 
    A string 


- [**scanf**](https://cplusplus.com/reference/cstdio/scanf/) Reads data from standard input (stdin) and stores them according to the format string and the additional arguments.

```C
#include <stdio.h>

int main() {
    int num1, num2;
    
    scanf("%x %d", &num1, &num2); // note the '&' preceding the variable
    printf("num1: %+d\n", num1);
    printf("num2: %+d\n", num2);
    
    scanf("%d", &num1);
    printf("char: '%c'\n", num1);
    return 0;
}
```

    ff 34
    num1: +255
    num2: +34
    49
    char: '1'


## C String
C does not have a built-in string type. Instead, a C-style string is represented as an array of characters, which terminates with a null character `'\0'` to indicate the end of the string.

```C
#include <stdio.h>

void cut_c_string(char c_str[], int pos) {
    c_str[pos] = '\0';
}

int main() {
    unsigned MAX_STRING_LENGTH = 256;
    // If an array is not initialized at declaration, its length must be specified.
    char str[MAX_STRING_LENGTH]; // a char array named "str"
    
    scanf("%s", str); // no '&' before the variable "str",
    printf("string entered: %s\n", str);
    
    cut_c_string(str, 5); // end the string at position 5
    printf("string altered: %s\n", str);
    return 0;
}
```

    helloworld
    string entered: helloworld
    string altered: hello


### Common functions
> [!info]
> See [C Strings](https://cplusplus.com/reference/cstring/) for reference.
- **strcpy** : Copy string
- **strlen** : Get string length
- **strcmp** : Compare two strings

```C
#include <stdio.h>
#include <string.h> // library for string operations

int main() {
    char str1[] = "Hello world!";
    char str2[40];
    strcpy(str2, str1); // strcpy: copy string str1 to str2
    printf("%s\n", str2);
    
    printf("length: %d\n", strlen(str1)); // strlen
    
    int ret = strcmp(str1, str2); // strcmp
    if (ret == 0) // return 0 if the two string are equal
        printf("str1 equals str2\n");
    else
        printf("unequal\n");
    return 0;
}
```

    Hello world!
    length: 12
    str1 equals str2


## Lab assignment hints
[Lab 07: C Functions and Arrays (instructure.com)](https://tulane.instructure.com/courses/2271434/assignments/14343177)

### 41.2 LAB: Convert to binary - functions
- Create the string by assigning characters iteratively
  - Remember to terminate the string with `'\0'`
- Use `strlen` to get the length of a string

