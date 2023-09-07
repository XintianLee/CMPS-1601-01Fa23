- [[#Polymorphism]]
- [[#Generics]]
- [[#ArrayList]]
  - [[#Sorting]]
- [[#Lab assignment hints]]

## Polymorphism
- able to determine program behavior depending on data types (1)
- derived/base class reference conversion: runtime polymorphism


```Java
class Base {
    public void print() {
        System.out.println("This is Base class.");
    }
}

class Derived extends Base { // define a subclass of class Base
    @Override
    public void print() { // override the method in class Base
        System.out.println("This is Derived class.");
    }
    
    public void print2() { // Derived's own member method
        System.out.println("This is Derived's print2.");
    }
}
```


```Java
// declare a Base type variable and initialize it with an instance of Derived type
Base v = new Derived();
```


```Java
v.print(); // (1) excute based on underlying data type Derived
```

    This is Derived class.



```Java
v.print2(); // print2 is not a member of Base
```


    |   v.print2(); // print2 is not a member of Base

    cannot find symbol

      symbol:   method print2()

    


## Generics
- having special type parameters indicating generic data types
- generic method
  ```java
  modifiers <Type1 extends BoundType1, Type2 extends BoundType2> 
  ReturnType methodName(parameters) {
      ... 
  }
  ```
- generic class
  ```java
  modifiers class ClassName <Type1 extends BoundType1, Type2 extends BoundType2> {
      ...
  }
  ```

### Generic method example

```Java
public static <T extends Comparable<T>> T min(T a, T b) {
    return a.compareTo(b) <= 0 ? a : b; // If a <= b, return a; otherwise return b.
}
```

- **type parameter(s)**: `T`
- **type bound** (optional): `Comparable<T>` (means type `T` must have implemented interface `Comparable<T>`)
- return type: `T`
- method name: `min`
- parameters: `T a`, `T b`


```Java
System.out.println(min(4, 5)); // Integer as T
System.out.println(min("four", "five")); // String as T
```

    4
    five


### Generic class example

```Java
public class Pair <T1, T2> {
    private T1 first;
    private T2 second;
    
    public Pair(T1 first, T2 second) {
        this.first = first;
        this.second = second;
    }
    
    @Override
    public String toString() {
        return String.format("(%s, %s)", first, second);
    }
}
```


```Java
System.out.println(new Pair(4, "four"));
```

    (4, four)


## ArrayList
```java
import java.util.ArrayList; // Java built-in generic class
```
- an ordered list of reference type items
> [!info]
> See [ArrayList](https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/util/ArrayList.html) for reference.
- Create an empty `ArryaList` of type `Integer`


  ```Java
  ArrayList<Integer> integers = new ArrayList<>();
  ```

- `add`: Appends a specified element to the end of the list.
  ```Java
  for (int i = 0; i < 5; i++)
      integers.add(i + 1);
  ```

- `size`: Returns the number of elements in the list.
- `get`: Returns the element at the specified position.
  ```Java
  for (int i = 0; i < integers.size(); i++)
      System.out.print(integers.get(i) + " ");
  ```
  ```
  1 2 3 4 5 
  ```

- iteration
  ```Java
  for (Integer num: integers)
      System.out.print(num + " ");
  ```
  ```
  1 2 3 4 5 
  ``` 

An example using [[#Polymorphism]]:
```Java
ArrayList<Base> list = new ArrayList();
list.add(new Base()); // a Base class object
list.add(new Derived()); // a Derived class object

for (Base elem: list)
    elem.print(); // runtime polymorphism
```

    This is Base class.
    This is Derived class.

### Sorting

```Java
import java.util.List; // the interface implemented by ArrayList
import java.util.Collections;
```


```Java
List<Integer> nums = new ArrayList(List.of(16, 4, 9, 1, 25));
System.out.println(nums);
```

    [16, 4, 9, 1, 25]



```Java
Collections.sort(nums); // sort in natrual order (depending on the implementation of compareTo)
System.out.println(nums);
```

    [1, 4, 9, 16, 25]



```Java
nums.sort(null); // equivalent to the way above
System.out.println(nums);
```

    [1, 4, 9, 16, 25]


#### Customize the order
- user-defined class type: implementing interface **Comparator**, or <ins>overriding method [*compareTo*](https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/lang/Comparable.html#compareTo(T))</ins> of *Comparable*
- built-in data type: implementing interface [**Comparator**](https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/util/Comparator.html)
  ```Java
  import java.util.Comparator
  ```

- Use an **anonymous inner class** to implement the interface:

  ```Java
  Comparator comparator = new Comparator<Integer>() {
      @Override
      public int compare(Integer a, Integer b) { // reverse order
          return b - a;
      }
  };

  Collections.sort(nums, comparator);
  System.out.println(nums);
  ```
  ```
  [25, 16, 9, 4, 1]
  ```

- Use a **lambda expression** (even simpler)

  ```Java
  nums.sort((a, b) -> - a.compareTo(b)); // in descending order
  System.out.println(nums);

  nums.sort((a, b) -> Math.abs(a - 7) - Math.abs(b - 7)); // distance to 7
  System.out.println(nums);
  ```

  ```
  [25, 16, 9, 4, 1]
  [9, 4, 1, 16, 25]
  ```


## Lab assignment hints
[Lab 03: Generics](https://tulane.instructure.com/courses/2271434/assignments/14343173)
> [!info]
> See the [[#Generics|definition]] and [[#Generic class example|example]] of **generic class** for reference.

### 11.1 LAB: Grocery shopping list (LinkedList)
- The usage of [**LinkedList**](https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/util/LinkedList.html) is similar to that of [**ArrayList**](#ArrayList).

### 11.3 LAB: What order? (generic methods)
- Use `compareTo` to compare two variables (see this [[#Generic method example|example]]).

### 14.4 LAB: Pairs (generic classes)
**Precedence** of comparisons
- E.g., 2 member fields: fieldA, fieldB
  - precedence of comparisons: fieldB > fieldA
- In `compareTo`: compare fieldB first
  - this.fieldB **not** equal to other.fieldB: return -1 or 1
  - equal: compare fieldA
    - this.fieldA equal to other.fieldA: reutrn 0
    - otherwise: return -1 or 1

Compare 2 generic type variables
- E.g., 2 variables of type T: T a, T b
  - Instead of writing `a < b`, `a > b` or `a == b`
    - use `compareTo`: `a.compareTo(b) < 0`, `a.compareTo(b) > 0` or `a.compareTo(b) == 0`

