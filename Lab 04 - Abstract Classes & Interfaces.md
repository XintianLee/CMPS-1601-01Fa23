- [[#Abstract Class]]
- [[#Interface]]
- [[#Exceptions and debugging]]
- [[#Lab assignment hints]]

## Abstract Class
**Abstract class**
- serves as a base class (superclass) to *guide* the design of subclasses (1)
- cannot itself be *instantiated* as an object (2)
  - can still have constructors which can be called via ***super*** in subclasses (2.1)
- contains **abstract method**(s) other than usual member fields and methods (3)

**Abstract method**
- in the (abstract) base class (4)
  - not implemented
  - declared as a **method signature** which defines the method's name and parameters
- in the subclass (5)
  - must be implemented


```Java
// (1) define an abstract class
abstract class AbstractBaseClass {
    // member field(s)
    private String var1;
    
    // member method(s)
    public AbstractBaseClass(String var1) { // (2.1) constructor
        this.var1 = var1;
    }
    public String getVar1() { return var1; }
    
    // (3) abstract method(s)
    public abstract int abstractMethod(int param1); // (4)
}
```


```Java
// (2)
AbstractBaseClass objAbstr = new AbstractBaseClass("Abstract");
```


    |   AbstractBaseClass objAbstr = new AbstractBaseClass("Abstract");

    AbstractBaseClass is abstract; cannot be instantiated

    



```Java
// inherits an abstract class
class SubClass extends AbstractBaseClass {
    // member field(s)
    private int var2;
    
    // constructor(s)
    public SubClass(String var1, int var2) {
        super(var1); // (2.1)
        this.var2 = var2;
    }
    
    // (5) implementation of abstract method(s)
    @Override
    public int abstractMethod(int param1) {
        return param1 * var2;
    }
}
```


```Java
// (*) concrete class: not abstract
SubClass obj = new SubClass("Concrete", 3); // call SubClass constructor

System.out.println(obj.getVar1()); // getVar1: defined in AbstractBaseClass

System.out.println(obj.abstractMethod(7)); // abstractMethod: implemented in Subclass
```

    Concrete
    21


## Interface
**Interface**
- specifies a set of abstract methods (1)
  - method signatures without keywork *abstract* (2)
- member fields (if any) must be *static* and *final* (3)

**Implementing class**
- must override and define all abstract methods specified by the interface (4)
- can **implement** multiple interfaces (5)
  - while a subclass can inherit at most one superclass


```Java
interface InterfaceA {
    // (1) member method(s)
    public void abstractMethod1(); // (2)
    public void abstractMethod2(String param1);
}

interface InterfaceB {
    // (3) member field(s)
    public static final int CONSTANT = 17;
    
    // (1) member method(s)
    public void abstractMethod3(int param1);
}

// (5) implements 2 interfaces
class ImplementingClass implements InterfaceA, InterfaceB {
    // (4)
    @Override
    public void abstractMethod1() { /* Implementation */ }
    @Override
    public void abstractMethod2(String param1) { /* Implementation */ }
    @Override
    public void abstractMethod3(int param1) { /* Implementation */ }
}
```

## Exceptions and debugging

### Debugging
1. predict problem
2. test to validate
	- insert ==print== statements

### Exceptions
> [!info]
> See [Lesson: Exceptions (The Java™ Tutorials > Essential Java Classes) (oracle.com)](https://docs.oracle.com/javase/tutorial/essential/exceptions/index.html) for reference.

#### Handling exceptions
```java
try {
    // statements
} catch (ExceptionType name) {
    // handle the catched exception
} catch (ExceptionType1|ExceptionType2 name) {

} finally {
    // ALWAYS executes when the `try` block exits
}
```
> [!example]
> ```java
> // a list of 5 integers
> List<Integer> nums = new ArrayList(List.of(16, 4, 9, 1, 25));
> 
> try { // try accessing the 6th element
>     System.out.println(nums.get(5));
> } catch (IndexOutOfBoundsException e) {
>     System.err.println("Caught IndexOutOfBoundsException: "
>                        + e.getMessage());
> }
> ```
> <p style="color:red">Caught <a href="https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/IndexOutOfBoundsException.html">IndexOutOfBoundsException</a>: Index 5 out of bounds for length 5</p>

#### Throwing exceptions
```java
throw new ExceptionType("Error message");
```
> [!example]
> ```java
> try { // throw an exception of a general type
>     throw new Exception("An unexpected condition");
> } catch (Exception e) {
>     System.err.println("Caught Exception: " + e.getMessage());
> }
> ```
> <p style="color:red">Caught <a href="https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Exception.html">Exception</a>: An unexpected condition</p>

> [!info]
> See [Exception (Java SE 21 & JDK 21) (oracle.com)](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Exception.html) for reference.

**checked** vs **unchecked** exceptions
- should be able to ==anticipate==: e.g., `FileNotFoundException`
  - either handle it with *try-catch*
  - allow a method further up the call stack to handle it
    - specifying the exceptions thrown by a method
      ```java
      ReturnType MethodName(ParameterType param) throws ExceptionType1, ExceptionType2 {
          // statements without handling ExceptionType1 and ExceptionType2
      }
      ```
- usually cannot anticipate (hardware or logic errors): `RuntimeException` and its subclasses
  > [!info]
  > See [RuntimeException (Java SE 21 & JDK 21) (oracle.com)](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/RuntimeException.html) for reference.


## Lab assignment hints
[Lab 04: Abstract Classes & Interfaces (instructure.com)](https://tulane.instructure.com/courses/2271434/assignments/14343172)

### 14.1 LAB: Shapes Hierarchy
- All member variables should be declared **private**.
  - Use **super** to call constructors which initialize them or update *static* ones if needed.

```java
public abstract class Shape implements Comparable<Shape> {
    /* ... */
    @Override
    public int compareTo(Shape o) { /* ... */ }
}
```

### 14.2 LAB: Artisans
- All member variables should be declared **private**. Choose data type carefully.

`Baker`
- `buyMaterials`
  - Even when the Baker runs out of money to buy more butter, they can still continually buy flour.
  - Not necessary to use a loop here.
- `bakeBread`/`bakeCake`
  - For easier override of the method `makeGoods`, write <del>`void bakeBread()`/`void bakeCake()`</del> <ins>`boolean bakeBread()`/`boolean bakeCake()`</ins> instead.
    - If ingredients are insufficient, return `false`; otherwise bake a cake/bread and return `true`.

[[Lab 03 - Generics#14.4 LAB Pairs (generic classes)]]
