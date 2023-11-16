- [[#IO]]
- [[#Array & Vector]]
- [[#Reference Type]]
- [[#Class]]
- [[#Lab Assignment Hints]]

## IO

### C-style IO
```cpp
#include <cstdio>

int main() {
    printf("Hello world!\n");
    return 0;
}
```

### iostream
- namespace `std`: classes and functions defined in the namespace of C++ standard library
- `cout`: object of **standard output stream**
- operator `<<`: insert fommatted output
- `endl`: insert newline and flush
```cpp
#include <iostream>

int main() {
    std::cout << "Hello world!" << std::endl;
    return 0;
}
```

```cpp
#include <iostream>
using namespace std; // declare to avoid the prefix std:: later

int main() {
    cout << "Hello world!" << endl;
    return 0;
}
```

- `cin`: object of **standard input stream**
- operator `>>`: extract formatted input
- [`getline`](https://cplusplus.com/reference/string/string/getline/): extract a line from the input stream
```cpp
#include <iostream>
using namespace std;

int main() {
    int num;
    cin >> num; // read an interger
    cout << num << endl;
    
    cin.ignore(); // skip the '\n' following the input interger
    string line;
    getline(cin, line); // read until `\n` reached
    cout << "^" << line << "$" << endl;
    return 0;
}
```
```
123
123
Hello world!
^Hello world!$
```

## Array & Vector

### Array
```cpp
int n = 10;
int arr1[n];
int *arr2 = new int[n]; // dynamic array
int arr3[] = {1, 2, 3, 5, 8};
```

### Vector
- a sequence container representing an array that can changes in size (similar to ArrayList in Java)
```cpp
#include <vector>
using namespace std;

int main() {
    vector<int> vec1; // instantiate an empty vector for int
    vector<int> vec2(5, 0); // initialize vec2 with 5 0s
    return 0;
}
```

- `size`: return the number of elements in the vector
- `empty`: test whether vector is empty
- `push_back`: add an element at the end
```cpp
vector<int> vec;
vec.push_back(1);
if (!vec.empty())
    cout << vec.size() << endl;
```
```
1
```

#### Iteration
- iterator: the usage is similar to pointer
  - `begin`: pointing to the first element in the sequence
  - `end`: pointing to the *past-the-end* element in the sequence
- index
- range-based for loop (for-each loop)
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int arr[] = {1, 2, 3, 5, 8};
    vector<int> vec(begin(arr), end(arr)); // initialize vec with arr
    
    // via iterator
    for (vector<int>::iterator it = vec.begin(); it != vec.end(); ++it)
        cout << *it << " ";
    cout << endl;
    
    // use auto type (since c++11)
    for (auto it = vec.begin(); it != vec.end(); ++it)
        cout << *it << " ";
    cout << endl;
    
    // via index
    for (int i = 0; i < vec.size(); ++i)
        cout << vec[i] << " ";
    cout << endl;
    
    // via for-each loop (since c++11)
    for (int elem: vec)
        cout << elem << " ";
    cout << endl;
    
    return 0;
}
```
```
1 2 3 5 8 
1 2 3 5 8 
1 2 3 5 8 
1 2 3 5 8 
```

## Reference Type
Introduced in C++ to replace the use of pointers in C.
```cpp
#include <iostream>
#include <vector>
using namespace std;

// pass by reference
void arithmeticAdd(vector<int>& vec, int addend) {
    for (int& elem: vec) // use reference type
        elem += addend;
}

int main() {
    vector<int> nums(5, 1); // initialize nums with 5 1s
    arithmeticAdd(nums, 3); // arithmeticAdd will change the contents of nums
    for (int num: nums)
        cout << num << " ";
    return 0;
}
```
```
4 4 4 4 4
```

## Class

- `.h` file: declare classes
```cpp
// A.h
#ifndef __A_H__ // these macros prevent "A.h" from being included more than once
#define __A_H__

#include <iostream>
#include <vector>
using namespace std;

class A {
    vector<int> nums;
public:
    A();
    A(int); // parameter name can be omitted in declaration
    void printNums() const; // const means no class member will change within the function
};

#endif
```

- define class members in a `.cpp` file
```cpp
// A.cpp
#include "A.h"

A::A() {} // default constructor

A::A(int n): nums(n, 0) {} // using member initializer list: initialize nums with n 0s

void A::printNums() const {
    for (int i = 0; i < nums.size(); i++)
        cout << nums[i] << " ";
    cout << endl;
}
```

- instantiation
```cpp
#include "A.h"

int main() {
    A a1; // calling default constructor
    A a2(2);
    A* pa = new A(4); // dynamic object
    
    a2.printNums();
    pa->printNums();
    return 0;
}
```
```
0 0 
0 0 0 0 
```

## Lab Assignment Hints
[Lab 09: C++ Classes and Objects (instructure.com)](https://tulane.instructure.com/courses/2271434/assignments/14343179)

### 53.3 LAB: Online shopping cart (Part 1)
- Use [`getline`](https://cplusplus.com/reference/string/string/getline/) to get a line as a `string` from `cin`

### 53.4 LAB: Online shopping cart (Part 2)
- Use [erase](https://cplusplus.com/reference/vector/vector/erase/) to remove element(s) from vector

`printMenu`
- Use `cin.ignore()` to skip any `'\n'` character left in stdin after reading a *char* or *int* if followed by `getline`, otherwise the following `getline` will read an empty string
