- [[#Abstract Class]]
- [[#Interface]]
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


<!--
## Unit testing
### Purpose of using methods
- Improving program **readability**: decomposing a long piece of code into methods
- For **reuse**: avoiding writing redundant code
- **Modular programing**: dividing the functionality of a program into independent modules that can be developed and tested separately
- **Incremental development**: designing, implementing and testing a program incrementally (each time adding a little)

### Unit testing
Individually testing a small unit (method or class) of a program by writing a **testbench**, which is
- A program aiming to thoroughly test the target program via
  - a series of **test cases** (input-output pairs)
- Features of a good testbench:
  - Automatic checks: Compare actual outputs with expected outputs.
    - **Assertion statement**
```java
assert testExpression : detailedMessage;
```
  - Independent test cases
  - **100 code coverage**: Every line of code of the tested program is executed.
  - Including **border cases**: Unusual or extreme test cases.
-->


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
