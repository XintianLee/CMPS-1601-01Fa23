## Links
- [Assignment](https://tulane.instructure.com/courses/2271434/assignments/14343171)

## Derived class (_subclass_)
- derived from another class, called a **base class** (_superclass_)
- <span style="color:brown">inherit</span>s the properties (member variables and methods) of the base class
```java
class DerivedClass extends BaseClass { /*...*/ }
```

## Protected member

| Access Specifier | Accessiblity |
| :------------ | :---------- |
| private       | self        |
| no specifier  | self + classes in the same package |
| **protected** | self + classes in the same package + **derived classes** |
| public        | anyone      |


```Java
class BaseClass {
    private String var1 = "var1: base class private member field";
    protected String var2 = "var2: base class protected member field";
    
    public void printMemberFields() {
        System.out.println("From superclass object:");
        System.out.println(var1);
        System.out.println(var2);
    }
}

class DerivedClass extends BaseClass {
    private String var3 = "var3: derived class private member field";
    
    public void printMemberFields() {
        System.out.println("\nFrom subclass object:");
        //System.out.println(var1);
        System.out.println(var2);
        System.out.println(var3);
    }
}
```


```Java
new BaseClass().printMemberFields();

new DerivedClass().printMemberFields();
```

    From superclass object:
    var1: base class private member field
    var2: base class protected member field
    
    From subclass object:
    var2: base class protected member field
    var3: derived class private member field


## Overriding member methods
- __*@Override*__ annotation
  - the compiler verifies that an identical base class method exists

- implicit variable __*super*__ (vs __*this*__)
  - a reference variable used to access superclass's members (including constructors)


```Java
class BaseClass {
    private String memberField; // private member field
    public BaseClass(String memberField) { // constructor
        this.memberField = memberField;
    }
    public void memberMethod() {
        System.out.println("BaseClass private member field: " + memberField);
    }
}

class DerivedClass extends BaseClass {
    public DerivedClass() {
        super("initialized from derived class"); // call BaseClass constructor
    }
    @Override
    public void memberMethod() {
        System.out.println("DerivedClass memberMethod called");
        super.memberMethod();
    }
}
```


```Java
new DerivedClass().memberMethod()
```

    DerivedClass memberMethod called
    BaseClass private member field: initialized from derived class


## The Object class
- built-in **_Object_ class**
  - base class for all other classes
- `toString` method
  - returns a `String` representation of the object


```Java
System.out.println(new DerivedClass());
```

    DerivedClass@2d07093d



```Java
class DerivedClass {
    @Override
    public String toString() {
        return "a DerivedClass instance";
    }
}
```


```Java
System.out.println(new DerivedClass());
```

    a DerivedClass instance


- `equals` method


```Java
String str1 = "string";
String str2 = new String("string");
String str3 = "string";

System.out.println(str1 == str2); // == operator compares the references not the values
System.out.println(str1.equals(str2));

System.out.println(str1 == str3);
```

    false
    true
    true


## Lab assignment hints
### 7.4 LAB: Bank accounts
`BankAccount`
- `toString`: use [String.format](https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/lang/String.html#format(java.lang.String,java.lang.Object...)) to make formatted strings
  - The [syntax](https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/util/Formatter.html#syntax) of the format specifiers for general, character, and numeric types: <pre>%[<span style="color:red">argument_index</span>&dollar;]\[<span style="color:orange">flags</span>][<span style="color:green">width</span>]\[.<span style="color:blue">precision</span>]<span style="color:purple">conversion</span></pre>
  - E.g., <pre>String.format("π = %<span style="color:red">1</span>&dollar;<span style="color:orange">+</span><span style="color:green">10</span>.<span style="color:blue">4</span><span style="color:purple">f</span>", Math.PI)</pre>

`CheckingAccount`
- override `deposit` and `withdraw` to count transactions


```Java
String.format("π = %1$+10.4f", Math.PI);
```

    π =    +3.1416

```Java
String param1 = "a string";
int param2 = 5;
double param3 = 4.25915;

// %s : string
// %d : decimal integer
// %f : floating point decimal
String formatted = String.format("%s, %d, %.4f", param1, param2, param3);
System.out.println(formatted);
```

    a string, 5, 4.2592

