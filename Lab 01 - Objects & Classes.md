## Links
- [Assignment](https://tulane.instructure.com/courses/2271434/assignments/14343170)
## Variable, Input and Output #IO
### Variable
Declare a variable (**strong typing**)
> [!abstract] Syntax
> ```java
> DataType varName[ = expression];
> ```
```java
int a;
boolean c = true;
double d = 1.0 / 3.0;
String s = "d";
```
### Input
Standard input stream: `System.in`
```java
import java.util.Scanner;
```
```java
// Wrap System.in with a Scanner
Scanner scnr = new Scanner(System.in);

a = scnr.nextInt()
```
  Input:
```
4
```
### Output
Standard output stream: `System.out`
- Print: `print` & `println`
  ```java
  // Print to System.out
  System.out.print(
      // concatenate string and variable with +
      a + " * " + 2 + " = "
  );
  
  // Print and then terminate the line.
  System.out.println(a * 2);
  ```
    Output:
  ```
  4 * 2 = 8
  ```
- Print a formatted string: `printf`
  ```java
  String formatStr = "The value of %s is %.3f \n";
  System.out.printf(formatStr, s, d);
  ```
    Output:
  ```
  The value of d is 0.333
  ```
## Control Statements and Arrays
### _if_ statement #If
> [!abstract] Syntax
> ```java
> if (expression1) { /* statements */ }
> else if (expression2) { /* statements */ }
> /* ... */
> else { /* statements */ }
> ```
```java
if (a < 3) {
    // statements
} else if (c) {
    System.out.println("2nd branch");
} else ;
```
Output:
```
2nd branch
```
### _while_ loop #While #later
> [!abstract] Syntax
> ```java
> while (conditionExpression) { /* Loop body */ }
> ```
```java
int i = 5;

while (i > 0) {
    System.out.print(i + " ");
    i = i - 1;
}
```
Output:
```
5 4 3 2 1 
```
### _for_ loop #For #later
> [!abstract] Syntax
> ```java
> for (initialExpression; conditionExpression; updateExpression) {
>     /* Loop body */
> }
> ```
```java
for (int i = 5; i > 0; i = i - 1)
    System.out.print(i + " ");
```
Output:
```
5 4 3 2 1 
```
### Arrays #Array #later
> [!abstract] Syntax
> ```java
> DataType[] arrayName = new DataType[numElements];
> ```
- Specify
    - data type
    - size of the array
- Use `.length` to get the size
```java
int[] arr = new int[10]; // declare an int array of length 10
arr[0] = arr[1] = 1; // index starts from 0

for (int i = 2; i < arr.length; ++i)
    arr[i] = arr[i - 1] + arr[i - 2];

// access last element of arr
System.out.println(arr[arr.length - 1]);
```
Output:
```
55
```
## #Method
- A named list of statements
- Definition
> [!abstract] Syntax
> ```java
> ReturnDataType methodName(Param1DataType param1Name, Param2DataType param2Name) {
>     ReturnDataType returnVar;
>     /* statements */
>     return returnVar;
> }
> ```
- Specify type of the returned value (or **void**)
- Call / Invoke
> [!abstract] Syntax
> ```java
> ReturnDataType ret = methodName(argument1, argument2);
> ```
## #Class
- #Object
    - a grouping of __variable__s and __method__s
    - an instance of some **class**
- **Class**
    - defines a _data type_ that can group variables and methods to form an **object**
- Abstraction / Encapsulation
    - provides high-level interfaces to the user
    - hides low-level internal details from the user
```java
// class definition
class A {
    // member variables / fields
    int memberVar;
    // member methods
    void memberMethod() { /* Do something. */ }
}
```
- #Reference
    - a variable type that refers to an object
    - **_new_** operator allocates memory for an object
  ```java
  // create an object of class A, and declare a variable obj referring to it
  A obj = new A();
  Scanner scnr = new Scanner(System.in);
  ```
- access class members: `.`
  ```java
  obj.memberMethod();
  scnr.nextInt();
  ```
- **Access modifier**s (for member fields or methods) #Access-Modifier
    - **private**: only member methods can access
    - **public**: both member methods and class user (object) can access
    - **static**: globally accessible, associated with a class not an object
### Special member methods

- #Mutator (setter) & #Accessor (getter)
    - change or get the value of a private field
  ```java
  class A {
      private String var;
      public String getVar() { return var; }
      public void setVar(String v) { var = v; }
  }
  ```
- #Constructor
    - initializes the member fields of an object
    - has exact the same name as the class
  ```java
  class A {
      private String var;

      // default constructor: no parameter
      public A() { var = 0; }

      // overloaded constructor
      public A(String var) {
          // use implicit parameter "this" to refer to
          // the object itself inside its member methods
          this.var = var;
      }
  }

  // invoke default constructor
  A obj = new A();

  // invoke overloaded constructor
  Scanner scnr = new Scanner(System.in);
  ```
