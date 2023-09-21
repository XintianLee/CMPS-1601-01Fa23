- [[#Unit testing]]
- [[#Input/Output optional]]
  - [[#Output streams]]
  - [[#Input streams]]
- [[#Data Structures]]
  - [[#Array vs Linked List]]
  - [[#Stack]]
- [[#Lab assignment hints]]

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


## Input/Output #optional
### Output streams
- java.io.**OutputStream** : *abstract* class for writing <u>bytes</u>
  - java.io.FilterOutputStream
    - java.io.**PrintStream** : able to print representations of various data values conveniently (e.g., __*System.out*__)

#### Create a String using stream
- java.io.Writer
  - java.io.**StringWriter** : a character stream
  - java.io.**PrintWriter** : prints formatted representations of objects to a text-output stream.


```Java
StringWriter charStream = new StringWriter();
PrintWriter sprintWriter = new PrintWriter(charStream);

sprintWriter.printf("%03d %.2f stream", 1, 2.345); // write to the character stream

String resultStr = charStream.toString(); // get the buffer content as a String
System.out.println(resultStr);
```

    001 2.35 stream


#### File output
- java.io.OutputStream
  - java.io.**FileOutputStream** : writes <u>bytes</u> to a `File` or to a `FileDescriptor`


```Java
try {
    PrintWriter fprintWriter = new PrintWriter("text.txt"); // This is equivalent to:
    // FileOutputStream foutStream = new FileOutputStream("text.txt");
    // PrintWriter fprintWriter = new PrintWriter(foutStream);
    
    fprintWriter.println(resultStr); // print to the file
    
    fprintWriter.close(); // close the stream to release any system resources associated with it
} catch(FileNotFoundException e) {
    // print into ...
} catch(IOException e) {
    // print into ...
}
```

### Input streams
- java.io.**InputStream** : *abstract* class for reading <u>bytes</u> (e.g., __*System.in*__)

#### Read from a String
- java.util.**Scanner**


```Java
Scanner strScanner = new Scanner(resultStr);

System.out.println(strScanner.nextInt());
System.out.println(strScanner.nextDouble());
System.out.println(strScanner.next());
```

    1
    2.35
    stream


#### File input
- java.io.InputStream
  - java.io.**FileInputStream** : obtains input <u>bytes</u> from a file


```Java
try {
    Scanner fileScanner = new Scanner(new FileInputStream("text.txt"));
    
    while (fileScanner.hasNext())
        System.out.println(fileScanner.next());
    
    fileScanner.close();
} catch(FileNotFoundException e) {
    // print into ...
}
```

    001
    2.35
    stream


## Data Structures
### Array vs Linked List
- **_Array_**: stores an ordered list of elements (usually in a contiguous block of memory), where each element is directly accessible by a <u>positional index</u>.
  - efficient for accessing elements (at any position)
  - insertion/deletion operations require shifting all the subsequent elements to new positions in memory
- **_Linked list_**: stores an ordered list of elements in <u>nodes</u>, where each node stores data and has a _pointer_ to the next node.
  - must traverse the list starting from the head node to access a specific element
  - efficient for insetion and deletion operations, especially when compared to arrays

> The size of an array is typically fixed at initialization. We use dynamic data structures (e.g., [vector](https://cplusplus.com/reference/vector/vector/) in C++ and [ArrayList](https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/util/ArrayList.html) in Java) when we want the size to change as needed, and arrays are often used as the underlying data structures to implement them.

### Stack
**_Stacks_** are a type of container, specifically designed to operate in a **_LIFO_** context (**last-in first-out**), where elements are inserted and extracted only from one end of the container.

- [Stack](https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/util/Stack.html) in Java
- [stack](https://cplusplus.com/reference/stack/stack/) in C++


```Java
Stack<Integer> stack = new Stack<>();

// Common operations:

// Push
stack.push(1); // 1 <-
stack.push(2); // 1, 2 <-
stack.push(3); // 1, 2, 3 <-

// Get size
System.out.println("Stack size: " + stack.size());

// Peek
System.out.println("Element at peek: " + stack.peek());

// Is empty
while (!stack.empty()) // while the stack is not empty
// Pop
    System.out.println("Element poped: " + stack.pop());
```

    Stack size: 3
    Element at peek: 3
    Element poped: 3
    Element poped: 2
    Element poped: 1


## Lab assignment hints
[Lab 05: Stacks (instructure.com)](https://tulane.instructure.com/courses/2271434/assignments/14343174)

### 19.1 LAB: Mismatched Brackets Checker
`readInFile`
- See [File input](#File-input)

`containsMismatchedBrackets`
- See this [draft flowchart](https://wavetulane-my.sharepoint.com/:u:/g/personal/xli71_tulane_edu/EbSxmJiA9FhHon7neqeYunQBiuKBLiSlmW0FLqaa731MuA?e=2Y6ipj) for reference
- Use single quotes around a character:
  - E.g., `'('` is treated as a `Character` while `"("` is a `String`.


```Java

```
