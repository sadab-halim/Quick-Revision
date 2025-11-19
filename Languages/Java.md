# Java

<details>
  <summary>01: Core Java Fundamentals.</summary>
  
### Java History, Editions, and Features

Java was created by James Gosling at Sun Microsystems and released in 1995. Its core philosophy is "Write Once, Run Anywhere" (WORA).

* **Editions**:
  * **Java SE (Standard Edition)**: The core Java platform for developing desktop, server, and console applications.
  * **Java EE (Enterprise Edition)**: Built on top of SE, it provides an API and runtime environment for developing and running large-scale, multi-tiered, and reliable network applications. Now managed by the Eclipse Foundation as Jakarta EE.
  * **Java ME (Micro Edition)**: A subset of SE for developing applications for mobile devices and embedded systems.
* **Key Features**:
  * **Platform Independent**: Java code is compiled into bytecode, which can run on any machine with a Java Virtual Machine (JVM).
  * **Object-Oriented**: Organizes software as a combination of different types of objects that incorporate both data and behavior.
  * **Simple and Familiar**: Designed to be easy to learn for programmers familiar with C++.
  * **Secure**: Provides a secure platform with features like a Security Manager and no explicit pointers.
  * **Robust**: Strong memory management, exception handling, and type-checking mechanisms.


### JVM vs JRE vs JDK (IMP)

This is a foundational and frequently asked interview question. The components are a superset of each other: JDK > JRE > JVM.


| Feature | JDK (Java Development Kit) | JRE (Java Runtime Environment) | JVM (Java Virtual Machine) |
| :-- | :-- | :-- | :-- |
| **Purpose** | For **developing** Java applications. | For **running** Java applications. | An **abstract machine** that executes Java bytecode. |
| **Contains** | JRE + Development Tools (like `javac`, `jdb`, `javadoc`). | JVM + Core Libraries and other supporting files. | Specification for a runtime environment; does not include libraries. |
| **Audience** | Java Developers. | End-users who only need to run Java programs. | Part of both JRE and JDK; a concept implemented by vendors. |
| **Analogy** | A full **mechanic's workshop** with tools to build and repair cars. | The **car engine and chassis** needed to drive a car. | The **combustion engine** itself, which makes the car move. |

### Java Compilation Process

The process involves compiling source code into platform-independent bytecode, which is then interpreted by the JVM.

1. **Source Code (`.java`)**: You write your Java code in a file, e.g., `MyProgram.java`.
2. **Compiler (`javac`)**: The JDK's compiler compiles the source file into a bytecode file (`.class`).

```bash
javac MyProgram.java
```

3. **Bytecode (`.class`)**: The output is `MyProgram.class`. This bytecode is not specific to any processor.
4. **JVM (`java`)**: The `java` command starts the JVM, which loads the `.class` file, verifies the bytecode, and executes it by converting it into native machine code.

```bash
java MyProgram
```


### Data Types

Java is a statically-typed language. Variables must be declared before they can be used.

* **Primitive Types**: Store simple values directly in memory (usually the stack).
  * **Integer types**: `byte` (8-bit), `short` (16-bit), `int` (32-bit), `long` (64-bit)
  * **Floating-point types**: `float` (32-bit), `double` (64-bit)
  * **Character type**: `char` (16-bit, Unicode)
  * **Boolean type**: `boolean` (`true` or `false`)
* **Reference Types**: Store a reference (memory address) to an object in the heap.
  * Include all objects created from classes (e.g., `String`, `Object`), arrays, and interfaces.
  * The default value for any reference variable is `null`.


### Variables, Constants, and Scope

* **Variables**:
  * **Instance Variables**: Belong to an object instance. Declared inside a class but outside any method.
  * **Static (Class) Variables**: Shared among all instances of a class. Declared with the `static` keyword.
  * **Local Variables**: Declared inside a method or block; their scope is limited to that block.
* **Constants**: Use the `final` keyword to create a variable whose value cannot be changed.

```java
final double PI = 3.14159;
```

* **`var` (Java 10+)**: Provides local variable type inference. The compiler infers the type from the right-hand side of the declaration.
  * **Best Practice**: Use `var` to improve code readability when the type is clear, e.g., `var userList = new ArrayList<User>();`.
  * **Pitfall**: `var` can only be used for local variables. It cannot be used for instance variables, method parameters, or return types.


### String Pool and Interning (IMP)

The String Pool (or String Constant Pool) is a special storage area in the Java heap (Metaspace in Java 8+ for literals) that stores unique string literals.

* **Analogy**: Think of the String Pool as a public library for strings. When you create a string literal `String s1 = "Java";`, the JVM checks the library. If "Java" isn't there, it adds it and gives `s1` a reference. When you create `String s2 = "Java";`, the JVM finds "Java" in the library and gives `s2` the *same* reference.
* Creating strings with `new` bypasses the pool initially.

```java
String s1 = "Hello"; // Goes into the pool
String s2 = "Hello"; // Reuses the reference from the pool
String s3 = new String("Hello"); // Creates a new object in the heap

System.out.println(s1 == s2); // true (same object)
System.out.println(s1 == s3); // false (different objects)
```


### String Immutability (IMP)

A `String` object's state cannot be changed after it is created. Any method that appears to modify a string (like `concat()`, `substring()`, `toUpperCase()`) actually creates and returns a *new* `String` object.

* **Benefits**:
  * **Thread Safety**: Strings can be shared across threads without synchronization.
  * **Security**: Cannot be modified after security checks.
  * **Caching**: The String Pool is possible because strings are immutable.
* **`intern()` method**: The `s3.intern()` method can be used to manually add a string to the pool (if not already present) and get the reference from the pool.

```java
String s4 = s3.intern();
System.out.println(s1 == s4); // true
```


### Pass-by-Value for Object References (IMP)

Java is **always pass-by-value**. This is a critical concept that is often misunderstood.

* **For Primitive Types**: A copy of the primitive value is passed to the method. Changes inside the method do not affect the original variable.
* **For Reference Types (Objects)**: A copy of the **reference value** (the memory address) is passed to the method.
  * **Analogy**: You have a paper with your home address on it (the reference variable). You give a *photocopy* of that paper to a friend (passing the reference by value). Your friend can use the address on the photocopy to go to your home and paint the walls (modify the object's internal state). However, if your friend scribbles a new address on their photocopy, it doesn't change the address on your original paper (the original reference variable cannot be reassigned).
* **Common Pitfall**: Believing a method can re-assign an object reference passed into it. The method can only change the internal state of the object the reference points to.


### Wrapper Classes \& Autoboxing (IMP)

Wrapper classes provide a way to use primitive data types as objects.

* `int` -> `Integer`, `char` -> `Character`, `boolean` -> `Boolean`, etc.
* **Autoboxing**: Automatic conversion of a primitive type to its corresponding wrapper class object.

```java
Integer myInt = 100; // Autoboxing: compiler converts int to Integer
```

* **Unboxing**: Automatic conversion of a wrapper object to its primitive type.

```java
int newInt = myInt; // Unboxing: compiler converts Integer to int
```

* **Common Pitfalls**:
  * **`NullPointerException`**: Unboxing a `null` reference will cause a `NullPointerException`.

```java
Integer value = null;
int primitive = value; // Throws NullPointerException
```

    * **Inefficient Comparison**: Using `==` to compare two wrapper objects checks for reference equality, not value equality. This may work for small numbers (due to caching, typically -128 to 127) but fails for others. **Best Practice**: Always use the `.equals()` method to compare the values of wrapper objects.
    * **Performance**: Creating many wrapper objects in a tight loop can be less performant than using primitives due to object creation overhead.

</details>

---

<details>
  <summary>02: Object-Oriented Programming (OOP)</summary>

### Classes and Objects

* **Class**: A blueprint or template for creating objects. It defines properties (fields) and behaviors (methods).
* **Object**: An instance of a class. It has a state (values of its fields) and behavior (its methods).
* **Analogy**: A `Car` class is the blueprint. Your specific car, a red Toyota with a particular VIN, is an object (an instance) of the `Car` class.


### OOP Principles (IMP)

These four principles are the foundation of OOP and are frequently discussed in interviews.


| Principle | Description | Analogy |
| :-- | :-- | :-- |
| **Encapsulation** | **Bundling data (fields) and methods that operate on the data into a single unit (a class).** It hides the internal state from the outside. Achieved using `private` access modifiers and public getters/setters. | A **capsule** for medicine. The outer shell hides the complex chemical formula inside, and you interact with it through a simple, controlled interface (swallowing it). |
| **Inheritance** | **A mechanism where a new class (subclass/child) acquires the properties and behaviors of an existing class (superclass/parent).** Promotes code reuse. Uses the `extends` keyword. | You **inherit** traits like eye color and height from your parents. You are a specialized version of your parents, with all their basic human features plus your own unique ones. |
| **Polymorphism** | **The ability of an object to take on many forms.** The most common use is when a parent class reference is used to refer to a child class object. It allows a single action to be performed in different ways. | The "start" button on different devices. On a **car**, it starts the engine. On a **TV**, it turns on the screen. The action is "start," but the implementation is different. |
| **Abstraction** | **Hiding complex implementation details and showing only the essential features of the object.** Achieved using `abstract` classes and `interfaces`. | Driving a **car**. You only need to know how to use the steering wheel, pedals, and gearstick. You don't need to know how the engine, transmission, or electronics work internally. |

### Access Modifiers

These control the visibility of classes, fields, and methods.


| Modifier | Same Class | Same Package | Subclass (Different Package) | World (Different Package) |
| :-- | :-- | :-- | :-- | :-- |
| `public` | Yes | Yes | Yes | Yes |
| `protected` | Yes | Yes | Yes | No |
| `default` | Yes | Yes | No | No |
| `private` | Yes | No | No | No |

### Constructors

A special method used to initialize objects. It has the same name as the class and no return type.

* **Overloaded Constructors**: A class can have multiple constructors with different parameter lists.
* **Private Constructors**: Used to prevent a class from being instantiated from outside. Common in Singleton patterns or utility classes.
* **Constructor Chaining**: Calling one constructor from another within the same class using `this()` or from the superclass using `super()`. `this()` or `super()` must be the very first statement in a constructor.

```java
public class Employee {
    private String name;
    private String department;

    // Default constructor chaining to another constructor
    public Employee() {
        this("Default Name", "Unassigned"); // Calls the parameterized constructor
    }

    public Employee(String name, String department) {
        this.name = name;
        this.department = department;
    }
}
```


### Method Overloading vs. Overriding (IMP)

| Feature | Method Overloading (Compile-time Polymorphism) | Method Overriding (Runtime Polymorphism) |
| :-- | :-- | :-- |
| **Purpose** | Increases the readability of the program. | To provide a specific implementation of a method already provided by its superclass. |
| **Location** | Occurs within the same class. | Occurs in two classes that have an IS-A (inheritance) relationship. |
| **Parameters** | Must have a different number or type of parameters. | Must have the same parameters. |
| **Return Type** | Can be different. | Must be the same (or a covariant type since Java 5). |
| **`static` methods** | Can be overloaded. | Cannot be overridden (this is called method hiding). |
| **`private` methods** | Can be overloaded. | Cannot be overridden as they are not visible in the subclass. |

### `static` and `final` Keywords

* **`static`**: The member belongs to the **class** itself, not to any individual object instance.
  * **Static Variable**: A single copy is shared among all objects of the class.
  * **Static Method**: Can be called without creating an object of the class. Cannot use `this` or access instance variables directly.
  * **Static Block**: Executed once when the class is first loaded into memory.
* **`final`**: A modifier to indicate that something cannot be changed.
  * **Final Variable**: A constant. Must be initialized at declaration or in the constructor.
  * **Final Method**: Cannot be overridden by a subclass.
  * **Final Class**: Cannot be extended (inherited from). `String` is a classic example of a `final` class.


### Abstract Classes vs. Interfaces (IMP)

| Feature | Abstract Class | Interface |
| :-- | :-- | :-- |
| **Methods** | Can have abstract and non-abstract (concrete) methods. | Can only have abstract methods (before Java 8). Java 8+ allows `default` and `static` methods. |
| **Fields** | Can have `final`, `non-final`, `static`, and `non-static` variables. | Variables are implicitly `public static final`. |
| **Inheritance** | A class can extend only **one** abstract class. | A class can implement **multiple** interfaces. |
| **Constructor** | Has a constructor (called via `super()` during subclass instantiation). | Does not have a constructor. |
| **When to use** | When creating a base class for closely related objects that share common code (IS-A relationship). | When defining a capability or contract that different, unrelated classes can implement (HAS-A capability). |
| **Java 8+ Note** | The lines have blurred. `default` methods allow interfaces to provide implementation, but they still cannot have state (instance variables). |  |

### `Object` Class Methods (IMP)

Every class in Java implicitly extends the `Object` class. Its key methods are:

* **`equals(Object obj)`**: Checks if two objects are "equal." The default implementation checks for reference equality (`==`). It's a best practice to override it for value-based equality.
* **`hashCode()`**: Returns an integer hash code value for the object. **Crucial Rule**: If `a.equals(b)` is true, then `a.hashCode()` must be equal to `b.hashCode()`. The reverse is not required. This is essential for hash-based collections like `HashMap` and `HashSet`.
* **`toString()`**: Returns a string representation of the object. It's good practice to override it to provide meaningful output.
* **`clone()`**: Creates and returns a copy of the object. Requires implementing the marker `Cloneable` interface.
* **`finalize()`**: Deprecated since Java 9. Was called by the garbage collector before an object is reclaimed.


### Composition vs. Inheritance (IMP)

A fundamental design principle question. "Favor Composition over Inheritance."

* **Inheritance (IS-A)**: `Car` **is a** `Vehicle`. It creates a tight coupling between the superclass and subclass. Changes in the superclass can break the subclass.
* **Composition (HAS-A)**: `Car` **has an** `Engine`. The `Car` class contains an instance of the `Engine` class. It's more flexible, as the `Engine` implementation can be changed at runtime without affecting the `Car`.

```java
// Composition
class Engine {
    public void start() {}
}

class Car {
    private Engine engine; // Car HAS-A Engine

    public Car(Engine engine) {
        this.engine = engine;
    }

    public void start() {
        engine.start();
    }
}
```


### Newer OOP-Related Features

* **Sealed Classes (Java 17)**: Restricts which other classes may extend or implement them. Provides more control over your inheritance hierarchy than `final`.

```java
// Only Circle and Square can extend Shape
public sealed class Shape permits Circle, Square { ... }
```

* **Covariant Return Types (Java 5+)**: An overridden method in a subclass can have a more specific return type than the one in the superclass.

```java
class SuperClass {
    Object get() { return new Object(); }
}

class SubClass extends SuperClass {
    @Override
    String get() { // String is a subclass of Object
        return "Hello"; 
    }
}
```

</details>

---

<details>
  <summary>03: Advanced Java Features</summary>

### Interface Evolution (Java 8+)

Interfaces, originally pure abstract types, have evolved significantly.[^4_1][^4_2][^4_3]

* **`default` Methods (Java 8)**: Allows an interface to provide a default implementation for a method. This helps evolve APIs without breaking existing implementing classes.

```java
interface Vehicle {
    void start(); // Abstract method

    default void honk() {
        System.out.println("Beep beep!"); // Default implementation
    }
}
```

* **`static` Methods (Java 8)**: Interfaces can have static utility methods that are related to the interface but are not tied to an object instance.[^4_4][^4_3]

```java
interface VehicleFactory {
    static Vehicle createCar() {
        // Logic to create a car
        return new Car();
    }
}
```

* **`private` Methods (Java 9)**: Allows `default` and `static` methods to share code within the interface itself, without exposing that helper logic to implementing classes.[^4_3]


### Functional Interfaces and Lambda Expressions (IMP) (Java 8)

These features form the basis of functional programming in Java.

* **Functional Interface**: An interface with exactly one abstract method (a SAM or Single Abstract Method interface). The `@FunctionalInterface` annotation is optional but recommended as it helps the compiler enforce this rule.[^4_5][^4_6]
  * **Common examples**: `Runnable`, `Comparator`, `ActionListener`.[^4_5]
  * **`java.util.function` package**: Java 8 introduced a new package with common functional interfaces like `Predicate`, `Consumer`, `Function`, and `Supplier`.[^4_7][^4_5]
* **Lambda Expression**: A short, anonymous function that provides an implementation for a functional interface's abstract method.[^4_8][^4_9]
  * **Analogy**: A lambda is like a sticky note with a quick instruction. Instead of writing a formal, named document (a class) for a simple, one-off task, you just jot it down right where you need it.
  * **Syntax**: `(parameters) -> expression` or `(parameters) -> { statements; }`.[^4_8]

```java
// Old way: anonymous class
Runnable r1 = new Runnable() {
    @Override
    public void run() {
        System.out.println("Running in a separate thread.");
    }
};

// New way: lambda expression
Runnable r2 = () -> System.out.println("Running in a separate thread.");
```


### Method References (Java 8)

A shorthand syntax for a lambda expression that only calls a single method.


| Type | Syntax | Lambda Equivalent |
| :-- | :-- | :-- |
| **Static** | `ClassName::staticMethodName` | `(args) -> ClassName.method(args)` |
| **Instance (Bound)** | `objectRef::instanceMethodName` | `(args) -> objectRef.method(args)` |
| **Instance (Unbound)** | `ClassName::instanceMethodName` | `(obj, args) -> obj.method(args)` |
| **Constructor** | `ClassName::new` | `(args) -> new ClassName(args)` |

### Streams API (IMP) (Java 8)

A powerful API for processing sequences of elements in a declarative way. A stream is not a data structure; it takes input from sources like Collections or arrays.[^4_10][^4_11]

* **Analogy**: Think of a stream as a manufacturing assembly line for data. The data elements move along a conveyor belt, and at each station (operation), something is done to them.
* **Pipeline Structure**:

1. **Source**: Where the stream comes from (e.g., `list.stream()`).
2. **Intermediate Operations**: Transformations that return a new stream (e.g., `filter`, `map`, `sorted`). These are **lazy**; they don't execute until a terminal operation is called.
3. **Terminal Operation**: Produces a result or a side-effect (e.g., `collect`, `forEach`, `reduce`). This is **eager** and triggers the processing of the stream.

```java
// Example: Get the names of the first 3 active users, sorted, in uppercase.
List<User> users = ...;
List<String> userNames = users.stream() // 1. Source
    .filter(User::isActive)              // 2. Intermediate Op
    .sorted(Comparator.comparing(User::getRegistrationDate)) // 2. Intermediate Op
    .map(User::getName)                  // 2. Intermediate Op
    .map(String::toUpperCase)            // 2. Intermediate Op
    .limit(3)                            // 2. Intermediate Op
    .collect(Collectors.toList());       // 3. Terminal Op
```


### Optional API (IMP) (Java 8)

A container object used to represent the presence or absence of a value, designed to help avoid `NullPointerException`.[^4_12]

* **Usage**: Primarily intended as a **return type** for methods that might not have a result to return.
* **Best Practices**:
  * **DO** use it as a return type.
  * **DON'T** use it for fields of a class (it's not `Serializable` and adds overhead).[^4_13]
  * **DON'T** use it as a parameter for methods. A method can just be overloaded.
  * **DO** prefer functional methods like `map`, `flatMap`, `filter`, and `ifPresent` over calling `isPresent()` and `get()`.
* **Common Pitfall**: Calling `.get()` without first checking `isPresent()`. This will throw a `NoSuchElementException`. A safer alternative is `orElse()` or `orElseThrow()`.

```java
Optional<User> findUserById(long id) {
    // ... logic to find user
    return Optional.ofNullable(user);
}

// Bad practice
Optional<User> userOpt = findUserById(1L);
if (userOpt.isPresent()) {
    System.out.println(userOpt.get().getName());
}

// Good practice
findUserById(1L)
    .map(User::getName)
    .ifPresent(System.out::println);

// Safely getting the value or a default
User user = findUserById(1L).orElse(new GuestUser());
```


### Modern Language Features

| Feature | Java Version | Description \& Example |
| :-- | :-- | :-- |
| **`var` (Local-Variable Type Inference)** | 10 | Reduces boilerplate for local variable declarations. The compiler infers the type. `var userList = new ArrayList<User>();` |
| **Enhanced `switch` Expressions** | 14 | Can be used as an expression that returns a value. Uses `->` syntax and eliminates fall-through, removing the need for `break`. |
| **Text Blocks** | 15 | Simplifies creating multiline strings. `String html = """<html><body><p>Hello, World</p></body></html>""";` |
| **Records** (IMP) | 16 | Immutable data carrier classes. The compiler auto-generates the constructor, getters, `equals()`, `hashCode()`, and `toString()`. `public record User(Long id, String name) {}` |
| **Pattern Matching for `instanceof`** (IMP) | 16 | Combines a type check and a cast into one operation. `if (obj instanceof String s) { System.out.println(s.toUpperCase()); }` |
| **Sealed Classes** | 17 | Restricts which classes can extend or implement a given class/interface. `public sealed class Shape permits Circle, Square {}` |
| **Virtual Threads** (IMP) | 21 | Lightweight threads managed by the JVM, drastically increasing concurrency throughput for I/O-bound applications. `Thread.startVirtualThread(() -> { ... });` |
| **Pattern Matching for `switch`** | 21 | Allows `switch` to branch on the type of an object and bind it to a variable. `switch (obj) { case String s -> ...; case Integer i -> ...; default -> ...; }` |


</details>

---

<details>
  <summary>04: Exception Handling</summary>

### Checked vs. Unchecked Exceptions (IMP)

This is a core distinction in Java's exception hierarchy. All exceptions descend from the `Throwable` class.

* **Analogy**:
  * **Checked Exception**: Like a **required travel visa**. Before you travel (compile), you must prove you have a plan for it—either by getting the visa (`try-catch`) or by declaring on your itinerary that you'll deal with it at a border crossing (`throws`).
  * **Unchecked Exception**: Like a **sudden traffic jam**. You can't be expected to plan for every possible traffic jam. These are unexpected runtime problems.

| Category | Description | Examples | Handling |
| :-- | :-- | :-- | :-- |
| **Checked Exceptions** | Exceptions that are checked at **compile-time**. The compiler forces you to handle them using `try-catch` or declare them with `throws`. Inherit from `Exception` (but not `RuntimeException`). | `IOException`, `SQLException`, `ClassNotFoundException` | Must be caught or declared. Represents recoverable conditions. |
| **Unchecked Exceptions** | Exceptions that occur at **runtime**. They are not checked at compile-time. Inherit from `RuntimeException`. They usually indicate programming errors. | `NullPointerException`, `ArrayIndexOutOfBoundsException`, `IllegalArgumentException` | Can be caught, but it's not required. Often, the best fix is to correct the code logic. |
| **Errors** | Severe problems that a reasonable application should not try to catch. They are related to the JVM environment itself. Inherit from `Error`. | `OutOfMemoryError`, `StackOverflowError` | Generally not handled. The application usually cannot recover. |

### `try-catch-finally` and `try-with-resources` (IMP)

These blocks are the primary tools for handling exceptions.[^5_1][^5_3][^5_4]

* **`try`**: Encloses the code that might throw an exception.[^5_6]
* **`catch`**: Catches and handles a specific type of exception. You can have multiple `catch` blocks for a single `try` block, ordered from most specific to most general.[^5_2]
* **`finally`**: This block **always executes** after the `try-catch` block, regardless of whether an exception was thrown or caught. It's used for cleanup code, like closing files or database connections.[^5_3]
  * **Pitfall**: If both `catch` and `finally` throw an exception, the one from the `finally` block will be propagated, and the original exception from the `catch` block will be suppressed.[^5_5]

```java
// Standard try-catch-finally
FileReader fr = null;
try {
    fr = new FileReader("file.txt");
    // ... read from file
} catch (FileNotFoundException e) {
    // Handle file not found
} catch (IOException e) {
    // Handle other I/O errors
} finally {
    if (fr != null) {
        try {
            fr.close(); // Closing resources can also throw exceptions
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

* **`try-with-resources` (Java 7+)**: A more elegant and safer way to handle resources that implement the `AutoCloseable` interface. It automatically closes the resources declared within the parentheses.
  * **Best Practice**: Always use `try-with-resources` for managing resources like streams, readers, and database connections to prevent resource leaks.

```java
// Clean and safe resource handling with try-with-resources
try (FileReader fr = new FileReader("file.txt");
     BufferedReader br = new BufferedReader(fr)) { // Multiple resources allowed
    // ... read from file
} catch (IOException e) {
    // Handle exceptions
}
// fr and br are automatically closed here.
```


### `throw` vs. `throws`

These two keywords are often confused.


| Keyword | Usage | Example |
| :-- | :-- | :-- |
| **`throw`** | Used **inside a method** to explicitly throw a single exception instance. | `throw new IllegalArgumentException("Invalid input");` |
| **`throws`** | Used in a **method signature** to declare the types of checked exceptions the method might throw. It delegates the handling responsibility to the calling method. | `public void readFile() throws IOException;` |

### Custom Exception Creation

You can create your own exceptions to represent business-specific errors.

* **Best Practice**: Create a checked exception if you expect the client code to recover from it. Create an unchecked exception if it represents a programming error.

```java
// Custom Checked Exception
public class InsufficientFundsException extends Exception {
    public InsufficientFundsException(String message) {
        super(message);
    }
}

// Usage
public void withdraw(double amount) throws InsufficientFundsException {
    if (balance < amount) {
        throw new InsufficientFundsException("Not enough balance.");
    }
    // ...
}
```


### Advanced Exception Handling Concepts

* **Exception Chaining**: Wrapping an exception within another one to add more context, without losing the original cause.

```java
try {
    // ... code that throws LowLevelException
} catch (LowLevelException e) {
    // Chain the original exception
    throw new HighLevelException("High-level operation failed", e);
}
```

* **Suppressed Exceptions (Java 7+)**: When two exceptions occur (e.g., one in the `try` block and another in the `finally` block while closing a resource), one gets suppressed. With `try-with-resources`, exceptions thrown during the automatic closing of a resource are automatically suppressed. You can access them via `Throwable.getSuppressed()`.
* **Multi-catch Block (Java 7+)**: Allows you to catch multiple exception types in a single `catch` block if the handling logic is the same.

```java
try {
    // ...
} catch (IOException | SQLException e) {
    // Handle both IO and SQL exceptions here
    logger.error("Error processing data", e);
}
```


### Best Practices for Exception Handling

1. **Don't swallow exceptions**: An empty `catch` block is a major red flag. At a minimum, log the exception.
2. **Be specific in `catch` blocks**: Catch specific exceptions (`FileNotFoundException`) before general ones (`IOException`). Avoid catching `Exception` or `Throwable` unless necessary.
3. **Use `finally` or `try-with-resources` for cleanup**: Ensure resources are always released.
4. **Throw early, catch late**: A method should throw an exception as soon as it detects an error. The exception should be caught by a higher-level handler that is equipped to deal with the problem.
5. **Use unchecked exceptions for programming errors**: `NullPointerException`, `IllegalArgumentException`, etc., usually mean the code needs to be fixed, not that a handler needs to be added.


</details>

---

<details>
  <summary>05: Collections Framework</summary>

### Introduction to the Collections Framework (IMP)

The Java Collections Framework is a unified architecture for representing and manipulating collections. It provides interfaces, implementations, and algorithms to work with groups of objects.

* **Analogy**: Think of the framework as a set of specialized **storage containers**. `List` is like a **numbered shelf** where order matters. `Set` is like a **bag of unique items** where duplicates are ignored. `Map` is like a **dictionary** where you look up a definition (value) by its word (key).


### Core Interfaces

The framework is built around a set of core interfaces.


| Interface | Description | Common Implementations | Key Characteristics |
| :-- | :-- | :-- | :-- |
| **`Collection`** | The root interface. Represents a group of objects. | (Indirectly: `ArrayList`, `HashSet`, etc.) | Basic operations like `add()`, `remove()`, `size()`, `contains()`. |
| **`List`** | An **ordered** collection (a sequence) that allows **duplicate** elements. Access is by integer index. | `ArrayList`, `LinkedList`, `Vector`, `Stack` | Ordered, indexed access, allows duplicates. |
| **`Set`** | A collection that contains **no duplicate** elements. | `HashSet`, `LinkedHashSet`, `TreeSet` | Unordered (mostly), no duplicates. |
| **`Queue`** | A collection used to hold elements prior to processing. Typically orders elements in a FIFO manner. | `LinkedList`, `PriorityQueue` | First-In, First-Out (FIFO) or priority order. |
| **`Map`** | An object that maps **keys to values**. Keys must be unique. (Note: Does not extend `Collection`.) | `HashMap`, `LinkedHashMap`, `TreeMap`, `Hashtable` | Key-value pairs, unique keys. |

### Key Implementations (IMP)

Understanding the trade-offs between implementations is crucial for interviews.

#### List Implementations

| Class | Underlying Data Structure | Performance Characteristics | Best For |
| :-- | :-- | :-- | :-- |
| **`ArrayList`** | Dynamic Array | Fast for random access (`get(i)` is O(1)). Slow for additions/removals in the middle (O(n)). | General-purpose list where random access is more frequent than insertion and deletion. **(Most common)** |
| **`LinkedList`** | Doubly-Linked List | Fast for additions/removals at the beginning/end/middle (if you have an iterator). Slow for random access (O(n)). | Scenarios with many insertions/deletions, especially when used as a `Queue` or `Deque`. |

#### Set Implementations

| Class | Underlying Data Structure | Ordering | Performance | Nulls Allowed? |
| :-- | :-- | :-- | :-- | :-- |
| **`HashSet`** | `HashMap` | **Unordered**. Iteration order is not guaranteed. | O(1) for add/remove/contains. | Yes (one) |
| **`LinkedHashSet`** | `HashMap` + `LinkedList` | **Insertion order**. Iterates in the order elements were added. | O(1) for add/remove/contains. | Yes (one) |
| **`TreeSet`** | Red-Black Tree (`TreeMap`) | **Sorted order**. Natural order or by a `Comparator`. | O(log n) for add/remove/contains. | No (pre-Java 7) / Yes (Java 7+ but requires custom comparator) |

#### Map Implementations (IMP)

| Class | Underlying Data Structure | Key Ordering | Performance | Thread-Safety | Null Keys/Values? |
| :-- | :-- | :-- | :-- | :-- | :-- |
| **`HashMap`** | Hash Table (Array of nodes) | **Unordered**. | O(1) average for `get`/`put`. | No | One `null` key, multiple `null` values. |
| **`LinkedHashMap`** | `HashMap` + `LinkedList` | **Insertion order**. | O(1) average for `get`/`put`. | No | One `null` key, multiple `null` values. |
| **`TreeMap`** | Red-Black Tree | **Sorted order** by key. | O(log n) for `get`/`put`. | No | No `null` keys. Multiple `null` values allowed. |
| **`Hashtable`** | Hash Table | **Unordered**. | O(1) average. | **Yes (synchronized)** | **No** `null` keys or values. |

* **HashMap vs. Hashtable (IMP)**: A classic interview question.
  * **Synchronization**: `HashMap` is non-synchronized and not thread-safe. `Hashtable` is synchronized and thread-safe.
  * **Performance**: `HashMap` is faster because it's not synchronized. `Hashtable`'s synchronization creates overhead.
  * **Nulls**: `HashMap` allows one `null` key and multiple `null` values. `Hashtable` allows neither.
  * **Modern Replacement**: For thread-safe maps, `ConcurrentHashMap` is vastly preferred over `Hashtable`.


### How `HashMap` Works (IMP)

Interviewers frequently ask for an explanation of `HashMap`'s internal workings.

1. **`hashCode()` and `equals()` Contract**: `HashMap` relies on the `hashCode()` and `equals()` methods of the key objects. The contract is: if `a.equals(b)`, then `a.hashCode()` must equal `b.hashCode()`.
2. **`put(K key, V value)`**:
  * The `hashCode()` of the key is calculated.
  * This hash is used to find an index (a "bucket") in the underlying array: `index = hashCode % array.length`.
  * **No Collision**: If the bucket is empty, the new key-value pair is stored as a `Node` object.
  * **Collision**: If the bucket already contains one or more nodes, the new node is added to that bucket's list.
    * The `equals()` method is used to check if the incoming key already exists in the linked list. If yes, the old value is replaced.
    * If not, the new node is appended to the end of the list.
3. **`get(K key)`**:
  * The key's `hashCode()` is used to find the correct bucket.
  * The linked list (or tree) in that bucket is traversed, using the `equals()` method to find the exact key. The corresponding value is then returned.

* **Java 8 Improvement**: When the number of nodes in a single bucket exceeds a threshold (`TREEIFY_THRESHOLD`, default is 8), the linked list is converted into a **balanced red-black tree**. This improves lookup performance in worst-case scenarios from O(n) to O(log n).


### Concurrent Collections (IMP)

These are thread-safe collections designed for multi-threaded environments. They offer better performance than wrapping standard collections with `Collections.synchronized...()`.

* **`ConcurrentHashMap`**: The preferred thread-safe map. It provides fine-grained locking (lock-striping), meaning different threads can write to different parts of the map simultaneously. Reads are generally non-blocking.
* **`CopyOnWriteArrayList`**: A thread-safe `List` where all mutative operations (`add`, `set`, etc.) create a fresh copy of the underlying array. It's expensive for writes but very fast for reads, as reads don't require any locks. Best for read-mostly scenarios.
* **Blocking Queues**: Interfaces like `BlockingQueue` (with implementations like `ArrayBlockingQueue`, `LinkedBlockingQueue`) are central to producer-consumer patterns. Methods like `put()` and `take()` will block until the operation can be completed.


### `Collections` and `Arrays` Utility Classes

* **`Collections`**: Provides static utility methods for collections (e.g., `sort()`, `reverse()`, `shuffle()`, `synchronizedList()`).
* **`Arrays`**: Provides static utility methods for arrays (e.g., `sort()`, `binarySearch()`, `asList()`).
  * **Pitfall**: `Arrays.asList()` returns a fixed-size `List` backed by the original array. You cannot add or remove elements from it. Changes to the array will be reflected in the list and vice-versa.


</details>

---

<details>
  <summary>06: Multithreading & Concurrency</summary>

### Process vs. Thread (IMP)

This is a fundamental concept in concurrency.

* **Analogy**: A **process** is like a **restaurant**. It has its own dedicated space (memory), kitchen staff (resources), and a license to operate (process ID). A **thread** is like a **waiter** in that restaurant. Multiple waiters can work simultaneously, serving different tables. They all share the same kitchen and resources but work on independent tasks. If one waiter makes a mistake, it might affect their table, but the whole restaurant doesn't necessarily shut down.

| Feature | Process | Thread |
| :-- | :-- | :-- |
| **Definition** | An executing instance of a program. | The smallest unit of execution within a process. |
| **Memory** | Each process has its own separate memory space. | Threads of the same process share the memory space. |
| **Communication** | Inter-Process Communication (IPC) is slow and complex. | Inter-Thread Communication is fast and efficient. |
| **Creation** | Creating a process is heavyweight and slow. | Creating a thread is lightweight and fast. |
| **Isolation** | Processes are isolated from each other. | Threads are not isolated from each other. |

### Thread Creation and Lifecycle

**Ways to Create a Thread**:

1. **Extend `Thread` class**: Subclass the `Thread` class and override its `run()` method.
2. **Implement `Runnable` interface (IMP)**: Implement the `Runnable` interface and pass an instance of it to a `Thread`'s constructor. **This is the preferred approach** as it allows the class to extend other classes (Java doesn't support multiple inheritance).
* **Thread Lifecycle States**:
  * **NEW**: The thread has been created but not yet started.
  * **RUNNABLE**: The thread is executing in the JVM or is ready to be run by the thread scheduler.
  * **BLOCKED**: The thread is waiting to acquire a monitor lock.
  * **WAITING**: The thread is waiting indefinitely for another thread to perform a particular action (e.g., after calling `Object.wait()` or `Thread.join()`).
  * **TIMED_WAITING**: The thread is waiting for a specified period (e.g., after calling `Thread.sleep(time)`).
  * **TERMINATED**: The thread has completed its execution.


### `volatile` and `synchronized` Keywords (IMP)

These are essential for managing shared state between threads.


| Keyword | `volatile` | `synchronized` |
| :-- | :-- | :-- |
| **Purpose** | Guarantees that the value of a variable is always read from/written to main memory, ensuring **visibility**. | Provides **mutual exclusion** (only one thread can execute a block of code at a time) and ensures **visibility**. |
| **Mechanism** | Ensures a "happens-before" relationship for reads/writes of that specific variable. | Acquires a monitor lock on an object. All other threads trying to acquire the same lock will be blocked. |
| **Atomicity** | Does **not** guarantee atomicity for compound operations (like `count++`, which is read-write). | Guarantees atomicity for the entire block or method it protects. |
| **When to Use** | For simple flags or variables where visibility is the only concern and operations are atomic (e.g., single write). | To protect blocks of code that modify shared state, ensuring both atomicity and visibility. |

### Thread Pools and `ExecutorService` (IMP)

Creating new threads is expensive. Thread pools manage a set of worker threads to execute tasks, avoiding the overhead of thread creation.

* **Analogy**: A thread pool is like a team of **delivery drivers** at a dispatch center. Instead of hiring a new driver for every single delivery (creating a new thread), the center keeps a fixed number of drivers on standby. When a delivery request comes in (a `Runnable` task), an available driver is assigned. If all drivers are busy, the request waits in a queue.
* **`ExecutorService`**: An interface for managing and running asynchronous tasks.
* **`Executors` factory class**: Provides convenient methods for creating common types of thread pools.
  * `newFixedThreadPool(int n)`: A pool with a fixed number of threads.
  * `newCachedThreadPool()`: A pool that creates new threads as needed but will reuse previously constructed threads when they are available. Good for many short-lived tasks.
  * `newSingleThreadExecutor()`: A pool with a single thread to execute tasks sequentially.
* **`ThreadPoolExecutor`**: The underlying implementation class, which offers fine-grained control over pool parameters (core size, max size, keep-alive time, etc.).


### `Future`, `Callable`, and `CompletableFuture`

* **`Callable<V>`**: Similar to `Runnable`, but its `call()` method can **return a result** and **throw a checked exception**.
* **`Future<V>`**: Represents the result of an asynchronous computation. It's a placeholder for a value that will be available later. You can use its `get()` method to retrieve the result, which will block until the computation is complete.
* **`CompletableFuture<T>` (Java 8+) (IMP)**: A major enhancement over `Future`. It can be explicitly completed, and it supports a vast number of callback-style operations (`thenApply`, `thenCompose`, `thenAccept`, etc.) to build a pipeline of asynchronous computations without blocking. It is the foundation of modern asynchronous programming in Java.

```java
// Using CompletableFuture
CompletableFuture.supplyAsync(() -> fetchUserData(userId)) // Runs in a background thread
    .thenApply(user -> processUserData(user))
    .thenAccept(processedData -> displayData(processedData))
    .exceptionally(ex -> {
        log.error("Failed to process user data", ex);
        return null;
    });
```


### Locks

The `java.util.concurrent.locks` package provides more advanced and flexible locking mechanisms than the `synchronized` keyword.

* **`Lock` Interface**: Key methods are `lock()`, `unlock()`, and `tryLock()`.
  * **Best Practice**: Always use a `try-finally` block to ensure the lock is released, even if an exception occurs.
* **`ReentrantLock`**: A re-entrant, mutual exclusion lock with the same basic behavior as `synchronized` but with extended capabilities like fairness policies and interruptible lock acquisition.
* **`ReadWriteLock`**: Maintains a pair of associated locks, one for read-only operations and one for writing. Multiple threads can hold a read lock simultaneously, but only one thread can hold the write lock. Ideal for data structures that are read much more often than they are written to.


### Atomic Variables

The `java.util.concurrent.atomic` package provides classes like `AtomicInteger`, `AtomicLong`, and `AtomicReference` that support lock-free, thread-safe programming on single variables.

* They use low-level hardware instructions like **Compare-And-Swap (CAS)** to ensure atomic operations without using locks, offering better performance under high contention.
* **Use Case**: Perfect for counters, sequence generators, or updating a single reference in a concurrent environment.

```java
AtomicInteger counter = new AtomicInteger(0);
// Thread-safe increment without locks
counter.incrementAndGet();
```


### Virtual Threads (Java 21) (IMP)

A revolutionary feature for high-throughput concurrent applications.

* **Analogy**: **Platform threads** (traditional threads) are like **professional chefs**. They are highly skilled but very expensive and limited in number. You can only hire so many before your kitchen (OS) is overwhelmed. **Virtual threads** are like **kitchen assistants**. You can have thousands of them. Each one can handle a simple step of a recipe (a task). When an assistant has to wait for an ingredient to arrive (an I/O operation), they step aside and let another assistant use the counter space (the platform thread). They are cheap, plentiful, and dramatically increase the kitchen's overall output.

| Feature | Platform Threads (Traditional) | Virtual Threads (Project Loom) |
| :-- | :-- | :-- |
| **Mapping** | Thin wrapper over an OS thread (1:1 mapping). | Managed by the JVM, not the OS. Many virtual threads run on a single platform thread (M:N mapping). |
| **Weight** | **Heavyweight**. Limited by OS resources. | **Lightweight**. Can create millions. |
| **Blocking Behavior** | Blocking a platform thread is expensive. | When a virtual thread blocks on I/O, it **unmounts** from its platform thread, freeing it for other work. |
| **Best For** | CPU-intensive tasks. | **I/O-bound tasks** (e.g., waiting for network calls, database queries). |


</details>

---

<details>
  <summary>07: JVM Internals \& Performance</summary>

### JVM Architecture (IMP)

Understanding the components of the Java Virtual Machine is critical for diagnosing memory issues and tuning performance.

* **Analogy**: Think of the JVM as a **highly organized workshop** for running your Java code.
  * **Class Loader Subsystem**: The **loading dock** where raw materials (`.class` files) are brought in, verified, and prepared.
  * **Runtime Data Areas**: The **main factory floor** with different specialized zones for storing tools, work-in-progress, and finished goods.
  * **Execution Engine**: The **machinery and workers** (Interpreter, JIT Compiler, Garbage Collector) that actually execute the tasks.

### Class Loader Subsystem

Responsible for loading classes into memory. It follows a delegation model.

1. **Bootstrap Class Loader**: The "god" loader. Loads core Java APIs from `rt.jar` (or `jmods` in Java 9+). It's written in native code and has no parent.
2. **Extension Class Loader** (deprecated in Java 9, now Platform Class Loader): Loads classes from the extensions directory.
3. **Application (System) Class Loader**: Loads classes from the application classpath (`-cp`). This is the loader for your own application's classes.

* **Delegation Principle (IMP)**: When a class needs to be loaded, the request is first delegated **up** to the parent class loader. A loader will only attempt to load a class if its parent cannot find it. This prevents core Java classes from being spoofed by application code and ensures that each class is loaded only once.


### Runtime Data Areas (IMP)

This is where the JVM stores data during program execution.


| Area | Description | Per-Thread or Shared? | Analogy |
| :-- | :-- | :-- | :-- |
| **Method Area** | Stores per-class structures like the runtime constant pool, field and method data, and the code for methods. **Metaspace** (since Java 8) is the implementation of the Method Area in native memory. | **Shared** | A **library of blueprints**. It holds the definition and instructions for every type of object you might create. |
| **Heap** | Stores all **objects** and their instance variables, as well as arrays. This is the largest memory area and is managed by the Garbage Collector. Divided into Young (Eden, S0, S1) and Old Generations. | **Shared** | The **main warehouse**. All created products (objects) are stored here until they are no longer needed and can be thrown out. |
| **JVM Stack** | Stores **local variables**, operand stacks, and frame data for each method invocation. Each thread has its own private stack. A new frame is created for each method call. | **Per-Thread** | A **worker's personal workbench**. For each task (method call), the worker gets a new set of instructions and local tools (variables) on their bench. When the task is done, that set is cleared. |
| **PC Registers** | Stores the address of the current JVM instruction being executed for each thread. | **Per-Thread** | A **worker's personal to-do list bookmark**. It points to the exact step the worker is currently on for their assigned task. |
| **Native Method Stack** | Stores information for native (non-Java) method calls. | **Per-Thread** | A workbench for tasks that require **specialized, non-Java tools** (e.g., C++ libraries). |

* **Stack vs. Heap (IMP)**: A frequent interview topic.
  * **Heap**: For objects (`new MyClass()`). Managed by the Garbage Collector. Can lead to `OutOfMemoryError` if it fills up.
  * **Stack**: For primitive local variables and object references. Memory is automatically managed as stack frames are popped. Can lead to `StackOverflowError` if there's infinite recursion.


### Garbage Collection (GC) (IMP)

The process of automatically reclaiming heap memory occupied by objects that are no longer reachable by the application.

* **Generational Hypothesis**: Most objects die young.
* **GC Process**:

1. **Mark**: The GC identifies all live objects by traversing the object graph starting from "GC Roots" (e.g., local variables on the stack, static variables).
2. **Sweep/Compact**: Unreachable objects are identified as garbage. The memory they occupy is either marked as free (sweeping) or live objects are moved together to eliminate fragmentation (compacting).
* **Key GC Algorithms**:
  * **G1 GC (Garbage-First)**: The default GC since Java 9. It divides the heap into regions and prioritizes collecting regions with the most garbage. Aims for predictable pause times.
  * **ZGC \& Shenandoah**: Ultra-low-latency GCs designed for very large heaps (terabytes). They perform most of their work concurrently with the application, resulting in pause times of less than a millisecond.


### JIT (Just-In-Time) Compiler

The JVM's Execution Engine starts by interpreting bytecode, which is slow. To improve performance, the JIT compiler analyzes frequently executed "hot" code and compiles it down to highly optimized native machine code on the fly.

* **Tiered Compilation**: A process where the JVM uses both a client (C1) and server (C2) JIT compiler.
  * **Level 1 (C1)**: Compiles code quickly with light optimizations for faster startup.
  * **Level 4 (C2)**: Kicks in for very hot methods, performing aggressive optimizations for maximum performance.


### Java Memory Model (JMM)

The JMM defines the rules for how threads interact through memory, specifically addressing visibility and ordering of variable access. It specifies the "happens-before" relationship, which is a guarantee that memory writes by one specific statement are visible to another specific statement. Keywords like `volatile` and `synchronized` are used to enforce these rules.

### Profiling and Monitoring Tools

* **`jps`**: Lists running Java processes.
* **`jstat`**: Monitors GC and class loading statistics.
* **`jmap`**: Creates a heap dump to analyze memory usage and find memory leaks.
* **`jstack`**: Creates a thread dump to analyze thread states, find deadlocks, and diagnose performance issues.
* **VisualVM \& JConsole**: GUI tools that combine the functionality of the above command-line tools for real-time monitoring of CPU, heap, threads, and GC activity.

</details>

---

<details>
  <summary>08: File I/O and NIO</summary>

### Legacy I/O (`java.io`)

The original I/O API in Java, introduced in JDK 1.0. It is **stream-based**, **blocking**, and character or byte-oriented.

* **Analogy**: Legacy I/O is like reading a book **one word at a time**, from start to finish. You are blocked from doing anything else until you've finished reading the section you need. If the book is very long, this can be slow.
* **Key Classes**:
  * **Stream Classes**: For handling binary data (bytes).
    * `InputStream`/`OutputStream`: Abstract base classes for byte input and output.
    * `FileInputStream`/`FileOutputStream`: For reading from and writing to files.
  * **Reader/Writer Classes**: For handling character data (text). They automatically handle character encoding.
    * `Reader`/`Writer`: Abstract base classes for character input and output.
    * `FileReader`/`FileWriter`: For reading from and writing to text files.
* **Decorator Streams**: These "wrap" other streams to add functionality.
  * `BufferedInputStream`/`BufferedReader`: Adds buffering to reduce the number of physical reads/writes, significantly improving performance.
  * `ObjectInputStream`/`ObjectOutputStream`: For serializing and deserializing objects.
* **Common Pitfall**: Forgetting to wrap file streams with buffered streams. Reading a file one byte at a time is extremely inefficient.

```java
// Inefficient
FileInputStream fis = new FileInputStream("data.bin");

// Efficient
BufferedInputStream bis = new BufferedInputStream(new FileInputStream("data.bin"));
```


### NIO (`java.nio`) - Non-blocking I/O (IMP)

Introduced in Java 1.4, NIO (New I/O) provides a more modern, high-performance alternative to `java.io`. It is **buffer-oriented** and **non-blocking**.

* **Analogy**: NIO is like being a **chef in a busy kitchen with multiple orders**. Instead of working on one dish from start to finish (blocking), you check a central order wheel (`Selector`) to see which dish is ready for the next step (e.g., one is ready to be plated, another is done simmering). This allows you to handle many dishes concurrently with a single pair of hands (a single thread).
* **Core Components**:

1. **Channels**: A conduit for data that connects to an I/O source (like a file or a socket). Data is read from the channel into a buffer, or written from a buffer into a channel. Examples: `FileChannel`, `SocketChannel`.
2. **Buffers**: A fixed-size block of memory into which data is read or from which data is written. You "flip" the buffer to switch between reading and writing modes. Key properties: `capacity`, `position`, `limit`.
3. **Selectors**: Allows a single thread to manage multiple channels. A thread can register channels with a selector and then wait for an event (e.g., connection ready, data available for read) on any of them. This is the key to scalable network I/O.

| Feature | Legacy I/O (`java.io`) | NIO (`java.nio`) |
| :-- | :-- | :-- |
| **Orientation** | Stream-oriented (data read sequentially) | Buffer-oriented (data read into a buffer block) |
| **Blocking Model** | Blocking (thread waits until I/O is complete) | Non-blocking (thread can do other work while waiting) |
| **Direction** | One-way (separate streams for input and output) | Two-way (a channel can be used for both reading and writing) |
| **Primary Use Case** | Simple, sequential file access. | High-performance network applications, file locking. |

### NIO.2 (`java.nio.file`) - The Modern File API (Java 7+)

NIO.2 builds on NIO to provide a comprehensive, modern API for file system operations. It largely replaces the old `java.io.File` class.

* **`Path`**: The cornerstone of NIO.2. It's a platform-independent representation of a file or directory path. It replaces `java.io.File`.
* **`Files`**: A utility class with dozens of static methods for common file operations. This is where most of your interaction will happen.
  * `Files.exists(path)`
  * `Files.createDirectory(path)`
  * `Files.copy(sourcePath, targetPath)`
  * `Files.move(sourcePath, targetPath)`
  * `Files.delete(path)`
  * `Files.readAllBytes(path)` (for small files)
  * `Files.readAllLines(path)` (for small text files)
  * `Files.newBufferedReader(path)` / `Files.newBufferedWriter(path)` (for large files, returns a buffered stream)
* **`DirectoryStream`**: An efficient way to iterate over the contents of a directory. It's used within a `try-with-resources` block.

```java
Path dir = Paths.get("some/directory");
try (DirectoryStream<Path> stream = Files.newDirectoryStream(dir, "*.java")) {
    for (Path entry : stream) {
        System.out.println(entry.getFileName());
    }
}
```

* **`Files.walkFileTree`**: A powerful method for recursively traversing a directory structure using the Visitor pattern.


### Other Important I/O Concepts

* **Memory-Mapped Files (`MappedByteBuffer`)**: A feature of NIO that maps a region of a file directly into memory. This allows you to treat a file as if it were a very large array in memory, offering extremely fast I/O for certain use cases (like IPC or large file processing). It bypasses the user-space buffers and OS page cache.
* **`Scanner`**: A utility class for parsing primitive types and strings from an input source. While convenient, it can be slower than using a `BufferedReader` for performance-critical applications due to its regex-based parsing.
* **Charset Encoding/Decoding**: Handling character data requires converting between bytes and characters using a `Charset` (e.g., `UTF-8`, `ISO-8859-1`). `java.io.InputStreamReader` and `java.io.OutputStreamWriter` are the bridge classes for this in legacy I/O. NIO.2 methods often provide an overload to specify the charset.

</details>

---

<details>
  <summary>09: Reflection & Annotations</summary>

### Reflection API (IMP)

The Reflection API is a powerful feature that allows a Java program to examine and modify its own structure and behavior at **runtime**. It provides the ability to inspect classes, interfaces, fields, and methods without knowing their names at compile time.

* **Analogy**: Reflection is like having a **universal remote control and a detailed instruction manual for any electronic device**. Even if you've never seen the device before, you can use the manual (`Class` object) to discover its buttons (`Method` objects) and settings (`Field` objects), and then use the remote to press those buttons and change those settings dynamically.
* **Core Classes** in `java.lang.reflect`:
  * **`Class`**: The entry point for all reflection operations. `MyClass.class`, `obj.getClass()`, and `Class.forName("com.mypackage.MyClass")` are ways to get a `Class` object.
  * **`Constructor`**: Provides information about and access to a single constructor for a class.
  * **`Method`**: Provides information about and access to a single method on a class or interface.
  * **`Field`**: Provides information about and access to a single field of a class or interface.
* **Common Use Cases**:
  * **Frameworks and Libraries**: Frameworks like Spring and Hibernate use reflection extensively for dependency injection, ORM (Object-Relational Mapping), and proxy creation.
  * **IDE Autocompletion**: Integrated Development Environments use reflection to inspect objects and suggest available methods and fields.
  * **JUnit**: The testing framework uses reflection to find and invoke methods annotated with `@Test`.
* **Key Operations**:
  * **Inspecting a Class**: Get methods, constructors, fields, and annotations.
  * **Instantiating an Object**: `constructor.newInstance(...)`.
  * **Invoking a Method**: `method.invoke(objectInstance, args...)`.
  * **Accessing a Field**: `field.get(objectInstance)` and `field.set(objectInstance, value)`.
* **Accessing Private Members (IMP)**: A common interview question is how to access private members. Reflection can bypass access control checks.

```java
MyClass obj = new MyClass();
Field privateField = MyClass.class.getDeclaredField("privateValue");
privateField.setAccessible(true); // This is the key step!
privateField.set(obj, "new value");
```

* **Disadvantages and Pitfalls**:
  * **Performance Overhead**: Reflection is significantly slower than direct method calls because it involves dynamic type resolution.
  * **Security Risks**: `setAccessible(true)` can break encapsulation and violate security constraints.
  * **Reduced Type Safety**: Issues that would normally be caught at compile time (like calling a non-existent method) only appear as exceptions at runtime.
  * **Refactoring Issues**: Automated refactoring tools might not be able to update code that uses reflection (e.g., method names passed as strings).
  * **Best Practice**: Use reflection as a last resort. If there is a direct, statically-typed way to do something, prefer it.


### Annotations

Annotations provide metadata about the program. They are added to the code itself but do not directly affect its execution. They can be read at compile-time by tools or at runtime via reflection.

* **Analogy**: Annotations are like **sticky notes or labels** you put on your code. A `@Test` note tells the JUnit runner "this is a test method." An `@Override` note tells the compiler "make sure this method is actually overriding something." The code itself doesn't change, but other tools can read these notes and act accordingly.
* **Types of Annotations**:
  * **Marker Annotations**: Annotations with no members (e.g., `@Override`).
  * **Single-Value Annotations**: Annotations with one member (e.g., `@SuppressWarnings("unchecked")`).
  * **Full Annotations**: Annotations with multiple members (e.g., `@WebServlet(name="MyServlet", urlPatterns={"/home"})`).
* **Built-in Java Annotations**:
  * **`@Override`**: Indicates that a method is intended to override a method in a superclass. The compiler will issue an error if it doesn't.
  * **`@Deprecated`**: Marks a method or class as obsolete. The compiler will issue a warning if it's used.
  * **`@SuppressWarnings`**: Instructs the compiler to suppress specific warnings.
  * **`@FunctionalInterface`**: (Java 8) Indicates that an interface is intended to be a functional interface.
  * **`@SafeVarargs`**: Suppresses warnings for methods with generic varargs parameters.
* **Meta-Annotations**: Annotations that are used to annotate other annotations.
  * **`@Retention`**: Specifies how long the annotation should be retained.
    * `RetentionPolicy.SOURCE`: Retained only in the source file, discarded by the compiler.
    * `RetentionPolicy.CLASS`: Retained in the `.class` file, but not available at runtime (default).
    * `RetentionPolicy.RUNTIME`: Retained in the `.class` file and available at runtime via reflection. **(IMP for frameworks)**
  * **`@Target`**: Specifies the kinds of program elements (class, method, field, etc.) to which the annotation can be applied.
  * **`@Inherited`**: Indicates that the annotation should be inherited by subclasses.
  * **`@Documented`**: Indicates that the annotation should be included in the Javadoc.
* **Creating Custom Annotations**: You can define your own annotations using the `@interface` keyword. They are commonly used in frameworks to enable declarative configuration.

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface JsonField {
    public String value() default "";
}

class User {
    @JsonField("user_name")
    private String userName;
}
```

</details>

---

<details>
  <summary>10: JDBC \& Database Access</summary>

### JDBC Architecture and API (IMP)

JDBC (Java Database Connectivity) is a standard Java API for connecting and executing queries with a database. It is part of the Java SE platform.

* **Analogy**: JDBC is like a **universal adapter for power outlets**. Your Java application is a device with a standard plug. The database is a wall socket in a foreign country. The JDBC Driver is the specific adapter for that country (e.g., a UK adapter for a UK socket) that allows your device to connect and draw power.
* **Core Components**:
  * **`DriverManager`**: The central management class. It uses the service provider mechanism to find and load registered JDBC drivers.
  * **`Driver`**: The specific implementation that communicates with a particular database vendor (e.g., MySQL Driver, PostgreSQL Driver).
  * **`Connection`**: Represents a connection (session) with a specific database.
  * **`Statement`**: Represents a static SQL statement.
  * **`PreparedStatement`**: Represents a precompiled SQL statement that can be executed multiple times efficiently.
  * **`CallableStatement`**: Used to execute SQL stored procedures.
  * **`ResultSet`**: A table of data representing a database result set, which is generated by executing a statement. It maintains a cursor pointing to its current row of data.


### Steps to Connect to a Database

This is a fundamental procedural question.

1. **Load and Register the Driver**: (Mostly automatic now) In modern JDBC (4.0+), drivers are loaded automatically from the classpath.
2. **Establish a Connection**: Use `DriverManager.getConnection()` with the database URL, username, and password.
3. **Create a Statement**: Create a `Statement` or `PreparedStatement` object from the `Connection`.
4. **Execute the Query**: Use methods like `executeQuery()` (for `SELECT`) or `executeUpdate()` (for `INSERT`, `UPDATE`, `DELETE`).
5. **Process the `ResultSet`**: If it's a query, iterate through the `ResultSet` to retrieve the data.
6. **Close Resources**: **Crucially**, close the `ResultSet`, `Statement`, and `Connection` in a `finally` block or use a `try-with-resources` statement to prevent resource leaks.
```java
// Best practice using try-with-resources
String url = "jdbc:mysql://localhost:3306/mydatabase";
String user = "user";
String password = "password";
String sql = "SELECT id, name FROM users WHERE id = ?";

try (Connection conn = DriverManager.getConnection(url, user, password);
     PreparedStatement pstmt = conn.prepareStatement(sql)) {
    
    pstmt.setInt(1, 101); // Set the parameter for the WHERE clause
    
    try (ResultSet rs = pstmt.executeQuery()) {
        while (rs.next()) {
            int id = rs.getInt("id");
            String name = rs.getString("name");
            System.out.printf("ID: %d, Name: %s%n", id, name);
        }
    }
} catch (SQLException e) {
    e.printStackTrace();
}
```


### `Statement` vs. `PreparedStatement` vs. `CallableStatement` (IMP)

| Type | Description | When to Use |
| :-- | :-- | :-- |
| **`Statement`** | Executes a static, simple SQL query. The query string is sent to the database every time. | For simple, one-time queries that don't take parameters. Rarely used in modern apps. |
| **`PreparedStatement`** | **(Preferred)** Executes a precompiled SQL query with parameters (`?`). The query plan is cached by the database, leading to better performance for repeated execution. It also **prevents SQL injection attacks**. | For almost all SQL queries, especially those with dynamic input parameters. |
| **`CallableStatement`** | Executes a database stored procedure. Supports `IN`, `OUT`, and `INOUT` parameters. | Only when you need to call stored procedures. |

* **SQL Injection (IMP)**: A critical security vulnerability where malicious SQL code is inserted into a query. `PreparedStatement` prevents this by treating user input strictly as data, not as executable SQL code.


### Transactions and Connection Pooling

* **Transactions**: A sequence of operations performed as a single logical unit of work. JDBC connections are in **auto-commit mode** by default, meaning every SQL statement is its own transaction.
  * To manage transactions manually, you must call `connection.setAutoCommit(false)`.
  * Then, you can group statements together and call `connection.commit()` to make the changes permanent, or `connection.rollback()` to undo them if an error occurs.
* **Connection Pooling**: Establishing a database connection is an expensive operation. A connection pool is a cache of database connection objects. Instead of creating a new connection for every request, the application borrows one from the pool and returns it when done.
  * **Benefits**: Dramatically improves performance and scalability.
  * **Popular Implementations**: **HikariCP** (the de-facto standard in the Spring Boot ecosystem for its high performance and reliability), Apache DBCP2.


### ORM vs. JDBC

* **JDBC**: Provides low-level control. You write the SQL. It's fast and flexible but can be verbose and requires manual mapping of `ResultSet` data to Java objects (boilerplate code).
* **ORM (Object-Relational Mapping)**: Frameworks like **Hibernate** (which implements the **JPA** - Jakarta Persistence API standard) map Java objects directly to database tables.
  * **Pros**: Reduces boilerplate code, abstracts away SQL, provides caching.
  * **Cons**: Can have a steep learning curve, may generate inefficient queries, and hides the underlying database logic, which can make debugging complex issues harder.


</details>

---

<details>
  <summary>11: Generics</summary>

### What are Generics? (IMP)

Generics, introduced in Java 5, allow you to create classes, interfaces, and methods that can work with different data types while providing **compile-time type safety**. They enable you to write flexible and reusable code that is less prone to runtime errors.[^6_1][^6_3][^6_5][^6_8]

* **Analogy**: Think of a generic class as a **customizable container**. When you manufacture a plain box, you can put anything inside it. But if you try to take something out, you have to guess what it is. With generics, you label the box "For Books Only" or "For Apples Only" (`List<Book>` or `List<Apple>`). Now, you can't accidentally put a shoe in the "Apples" box (compile-time error), and when you take something out, you know it's an apple (no casting needed).


### Why Use Generics?

1. **Stronger Type Checks at Compile Time**: Catches invalid type usage before the code is run. Without generics, you would get a `ClassCastException` at runtime.[^6_2][^6_4]
2. **Elimination of Casts**: Code becomes cleaner and easier to read without explicit casting.[^6_5]
3. **Enabling Generic Algorithms**: Allows developers to implement algorithms that work on collections of different types in a reusable and type-safe way.[^6_3]
```java
// Before Generics (Java 1.4 and earlier)
List list = new ArrayList();
list.add("hello");
String s = (String) list.get(0); // Explicit cast required
list.add(123); // Compiles fine, but will cause ClassCastException later

// With Generics (Java 5+)
List<String> stringList = new ArrayList<>();
stringList.add("hello");
String s = stringList.get(0); // No cast needed
// stringList.add(123); // Compile-time error!
```


### Generic Types and Methods

* **Generic Class**: A class defined with a type parameter, typically denoted by a single uppercase letter like `T` (for Type), `E` (for Element), or `K, V` (for Key, Value).[^6_3]

```java
public class Box<T> {
    private T content;

    public void set(T content) { this.content = content; }
    public T get() { return this.content; }
}

// Usage
Box<Integer> integerBox = new Box<>();
integerBox.set(10);
```

* **Generic Method**: A method with its own type parameter, declared before the return type. These are useful for static utility methods that operate on different types.[^6_6]

```java
public class Util {
    public static <T> void printArray(T[] array) {
        for (T element : array) {
            System.out.printf("%s ", element);
        }
    }
}
```


### Wildcards (IMP)

Wildcards (`?`) represent an unknown type and are used to add flexibility to how generics are used, especially in method parameters.


| Wildcard Type | Syntax | Description | Analogy |
| :-- | :-- | :-- | :-- |
| **Upper Bounded** | `List<? extends Number>` | A list of `Number` or any subtype of `Number` (e.g., `Integer`, `Double`). It's a **producer**; you can safely read (`get`) elements as `Number`s, but you cannot add (`put`) anything to it (except `null`). | A basket of **apples**. You can take an apple out, and you know it's a fruit. But you can't put a new fruit in because you don't know if it's the *exact* same type of apple. |
| **Unbounded** | `List<?>` | A list of an unknown type. Useful when the methods being used don't depend on the type (e.g., `list.size()`, `list.clear()`). Similar to upper-bounded, you cannot add elements. | A **mystery box**. You can check its size or empty it, but you can't safely take anything out (without casting to `Object`) or put anything in, as you don't know what's inside. |
| **Lower Bounded** | `List<? super Integer>` | A list of `Integer` or any supertype of `Integer` (e.g., `Number`, `Object`). It's a **consumer**; you can safely add (`put`) an `Integer` (or its subtypes), but when you read (`get`), you are only guaranteed an `Object`. | A basket for **all kinds of fruits**. You can put an apple into it, because an apple is a fruit. But if you take something out, you only know it's a fruit, not whether it's an apple or a banana. |

* **PECS Mnemonic**: A common interview topic for remembering when to use `extends` and `super`.
  * **P**roducer **E**xtends: If you are only reading items from a collection, use `extends`.
  * **C**onsumer **S**uper: If you are only adding items to a collection, use `super`.


### Type Erasure (IMP)

This is a critical, behind-the-scenes concept in Java generics.

* **What it is**: The Java compiler enforces type safety at compile time, but then **erases** the generic type information to generate bytecode that is compatible with older JVMs that don't know about generics.
* **How it works**:

1. Replaces all generic type parameters in generic types with their bounds, or with `Object` if the type parameter is unbounded. So `Box<T>` becomes `Box<Object>`.
2. Inserts type casts where necessary to preserve type safety.
3. Generates bridge methods to maintain polymorphism in extended generic types.
* **Consequences and Pitfalls**:
  * You cannot get the type parameter at runtime (e.g., you can't do `if (list instanceof List<String>)`).
  * You cannot create an instance of a type parameter (e.g., `new T()`).
  * You cannot create an array of a generic type (e.g., `new T`).[^6_10]


### Raw Types

A raw type is the name of a generic class or interface used without its type arguments.

```java
Box rawBox = new Box(); // Raw type - compiler issues a warning
rawBox.set(10);        // Valid
rawBox.set("hello");   // Also valid, defeats the purpose of generics
```

* **Best Practice**: Avoid using raw types. They are a bridge to legacy code and completely subvert the type safety that generics provide.

</details>

---

<details>
  <summary>12: Serialization \& Deserialization</summary>

### What is Serialization? (IMP)

Serialization is the process of converting a Java object's state into a byte stream. Deserialization is the reverse process: reconstructing the object from that byte stream.

* **Analogy**: Serialization is like **dehydrating and vacuum-packing food for storage or travel**. You take a complex, structured meal (the object), convert it into a flat, durable, and portable format (the byte stream). Deserialization is like adding water and reheating it to get the original meal back.
* **Primary Use Cases**:
  * **Persistence**: Saving an object's state to a file or database to be retrieved later.
  * **Communication**: Sending an object over a network to another application or service (e.g., in Remote Method Invocation - RMI).
  * **Caching**: Storing objects in memory for quick retrieval.


### `Serializable` vs. `Externalizable` Interfaces (IMP)

These two interfaces from `java.io` are the primary ways to make an object serializable.


| Feature | `Serializable` Interface | `Externalizable` Interface |
| :-- | :-- | :-- |
| **Type** | A **marker interface**. It has no methods. | An interface with two methods: `writeExternal(ObjectOutput out)` and `readExternal(ObjectInput in)`. |
| **Process** | **Automatic**. The JVM handles the entire serialization process by default using reflection to save the object's fields. | **Manual/Programmatic**. You have full control and must explicitly write and read the state of the object inside these two methods. |
| **Control** | Less control. You can customize it with `writeObject` and `readObject`, but the default is automatic. | **Complete control**. You decide exactly what gets written and in what format. |
| **Performance** | Can be slower due to reflection overhead. | Generally faster as it avoids reflection. |
| **Constructor** | During deserialization, the constructor of the nearest non-serializable superclass is called. | During deserialization, the class's **public no-arg constructor** is **always** called before `readExternal` is invoked. |
| **When to Use** | Simple, convenient, and suitable for most use cases. | When you need fine-grained control over the serialized format, need to improve performance, or need to handle complex object graphs. |

### The `Serializable` Workflow

To make a class serializable, you simply implement the `Serializable` interface.

```java
import java.io.Serializable;

public class User implements Serializable {
    private String username;
    private transient String password; // 'transient' fields are ignored
    private static int userCount = 0; // 'static' fields are not serialized
    // ...
}
```

* **`transient` Keyword (IMP)**: The `transient` keyword is used to mark a field that should **not** be serialized. This is crucial for sensitive data like passwords or for fields that can be recalculated and don't need to be persisted.
* **`static` Fields**: Static fields belong to the class, not the object instance, so they are **not** part of the object's state and are not serialized.


### `serialVersionUID` (IMP)

This is a version number for a serializable class. It is a `private static final long` field.

* **Purpose**: During deserialization, the JVM checks the `serialVersionUID` of the serialized object against the `serialVersionUID` of the loaded class. If they don't match, it throws an `InvalidClassException`.
* **Why it's critical**: It ensures that a serialized object is compatible with the class that is trying to deserialize it. If you change a class (e.g., add a field) without changing the `serialVersionUID`, you might be able to deserialize an old object, but it can lead to unexpected behavior.
* **Best Practice**: **Always declare `serialVersionUID` explicitly**. If you don't, the compiler will generate one based on the class structure (fields, methods, etc.). This auto-generated ID can change unexpectedly with minor code modifications, breaking deserialization for previously saved objects.

```java
private static final long serialVersionUID = 1L;
```


### Customizing Serialization (`writeObject` and `readObject`)

Even when using `Serializable`, you can gain control over the process by providing these two methods in your class.

* **`private void writeObject(java.io.ObjectOutputStream out) throws IOException`**: If this method exists, it will be called to save the object's state. You are responsible for writing the fields to the stream, typically by calling `out.defaultWriteObject()` first and then adding any custom logic.
* **`private void readObject(java.io.ObjectInputStream in) throws IOException, ClassNotFoundException`**: This method is called to read the object's state from the stream. You typically call `in.defaultReadObject()` first and then read any custom data.
* **Use Case**: Encrypting a field before writing it, or initializing `transient` fields after deserialization.


### Security Vulnerabilities in Deserialization (IMP)

Deserialization of untrusted data is a notorious security risk, often referred to as the "billion-dollar mistake" of Java.

* **The Problem**: If an attacker can control the byte stream being deserialized, they can potentially instantiate any `Serializable` class available on the application's classpath. By crafting a malicious object chain (using "gadget chains" from libraries like Apache Commons Collections), they can trigger code execution on the server, leading to Remote Code Execution (RCE).
* **Best Practices**:

1. **Never deserialize untrusted data.**
2. If you must, use a "look-ahead" deserialization mechanism or a `ObjectInputFilter` (Java 9+) to validate the classes being deserialized before they are instantiated.
3. **Prefer safer serialization formats like JSON or Protocol Buffers** over Java's native serialization for communication and persistence. Libraries like Jackson or Gson are standard for this.


### `readResolve()` and `writeReplace()`

These methods provide advanced control over the object that is actually serialized or deserialized.

* **`writeReplace()`**: If present, this method is called *before* serialization. It allows you to nominate a different object to be serialized in place of the original.
* **`readResolve()`**: If present, this method is called *after* deserialization. It allows you to replace the newly created deserialized object with a different one.
* **Primary Use Case**: Enforcing the **Singleton pattern**. By implementing `readResolve()` to return the singleton instance (`INSTANCE`), you can prevent deserialization from creating new instances of your singleton class. This is a common interview question.


</details>


---

<details>
  <summary>13: Java APIs \& Utilities</summary>

### `java.lang.String` vs. `StringBuilder` vs. `StringBuffer` (IMP)

This is a classic and frequent interview question focusing on string manipulation, immutability, and thread safety.

* **Analogy**:
  * **`String`**: Like a **stone tablet**. Once you carve something into it, it cannot be changed. To "add" to it, you must take a new, larger tablet and copy the old text plus the new text. This is sturdy and safe but inefficient for many changes.
  * **`StringBuilder`**: Like a **whiteboard**. You can easily add, erase, and change the text on it. It's fast and efficient for a single person to use.
  * **`StringBuffer`**: Like the **same whiteboard, but in a busy meeting room**. Only one person can write on it at a time (it's synchronized) to prevent a jumbled mess. This makes it safe for multiple people (threads) but slower than if you had the board to yourself.

| Feature | `String` | `StringBuilder` (Java 5+) | `StringBuffer` (Legacy) |
| :-- | :-- | :-- | :-- |
| **Mutability** | **Immutable**. | **Mutable**. | **Mutable**. |
| **Thread Safety** | **Thread-safe** (due to immutability). | **Not thread-safe**. | **Thread-safe** (methods are `synchronized`). |
| **Performance** | Slow for frequent modifications (creates new objects). | **Fastest**. Highly efficient for string concatenations in a loop. | Slower than `StringBuilder` due to synchronization overhead. |
| **When to Use** | For string values that will not change. | In a single-threaded environment for building complex strings (e.g., in a loop). **This is the modern choice.** | In a multi-threaded environment where a mutable string must be shared across threads. (Rarely needed; `ConcurrentHashMap` or other concurrent structures are often better designs). |

### `java.util.Objects`, `java.util.Arrays`, `java.util.Collections`

These are indispensable utility classes providing static helper methods.

* **`Objects` (Java 7+)**: Provides `static` utility methods for operating on objects. These methods are null-safe.
  * `Objects.requireNonNull(obj, "Message")`: Throws a `NullPointerException` if the object is null. Excellent for validating parameters in constructors and methods.
  * `Objects.equals(a, b)`: Compares two objects for equality, correctly handling cases where one or both are `null`.
  * `Objects.hash(values...)`: Generates a hash code for a sequence of values. Useful for implementing `hashCode()` methods.
* **`Arrays`**: Provides `static` methods for manipulating arrays.
  * `Arrays.sort()`: Sorts an array.
  * `Arrays.binarySearch()`: Searches a sorted array.
  * `Arrays.equals()` / `Arrays.deepEquals()`: Compares arrays for equality.
  * `Arrays.asList()`: Returns a fixed-size list backed by an array.
  * `Arrays.stream()`: (Java 8) Creates a `Stream` from an array.
* **`Collections`**: Provides `static` methods for operating on or returning collections.
  * `Collections.sort()` / `Collections.reverse()`: Modifies a list's order.
  * `Collections.shuffle()`: Randomly permutes a list.
  * `Collections.synchronized...()`: Returns a thread-safe wrapper around a collection (e.g., `synchronizedList`).
  * `Collections.unmodifiable...()`: Returns an unmodifiable view of a collection.
  * `Collections.emptyList()` / `emptySet()` / `emptyMap()`: Returns a type-safe, immutable empty collection.


### Wrapper Classes \& Autoboxing

* **Wrapper Classes**: (`Integer`, `Double`, `Boolean`, etc.) provide an object representation for primitive types. They are essential for use in generics (e.g., `List<Integer>`, not `List<int>`).
* **Autoboxing/Unboxing**: The automatic conversion between primitives and their wrapper types.
  * **Autoboxing**: `Integer i = 100;` (primitive `int` to `Integer` object).
  * **Unboxing**: `int j = i;` (`Integer` object to primitive `int`).
  * **Pitfall (IMP)**: Unboxing a `null` wrapper reference will throw a `NullPointerException`. Be cautious when using wrappers in mathematical expressions or assigning them to primitives.


### Other Key Utilities

* **`java.util.UUID`**: Generates universally unique identifiers. `UUID.randomUUID()` is commonly used to create unique IDs for database records, transactions, etc.
* **`java.util.Random` \& `java.security.SecureRandom`**:
  * `Random`: Generates a stream of pseudorandom numbers. Sufficient for most non-critical applications.
  * `SecureRandom`: A cryptographically strong random number generator. **Use this** for security-sensitive contexts like generating session IDs, tokens, or cryptographic keys.
* **Regex (`java.util.regex`)**:
  * **`Pattern`**: A compiled representation of a regular expression. Compiling a pattern is expensive, so it should be reused.
  * **`Matcher`**: The engine that performs matching operations on a character sequence by interpreting a `Pattern`.
* **`java.util.ServiceLoader` (SPI Mechanism)**:
  * **SPI (Service Provider Interface)** is a mechanism for achieving loose coupling and extensibility. An application defines a service (an interface), and multiple providers can implement that service.
  * `ServiceLoader` is a utility that discovers and loads implementations of a service interface from the classpath. This is how JDBC finds database drivers.


</details>

---

