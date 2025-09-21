# Java

## Core Java Fundamentals
### Java History, Editions, and Features
* **Java Editions**:
    * **SE (Standard Edition)**: The core platform for developing applications for desktops, servers, and embedded systems.
    * **EE (Enterprise Edition)**: Built on top of SE, it provides an API and runtime environment for developing and running large-scale, multi-tiered, and reliable network applications.
    * **ME (Micro Edition)**: A subset of SE for developing applications for mobile devices and embedded systems with limited resources.
* **Key Features**:
    * **Platform Independent**: "Write Once, Run Anywhere" (WORA) is achieved via the Java Virtual Machine (JVM).
    * **Object-Oriented**: Organizes software around data, or objects, rather than functions and logic.
    * **Simple and Secure**: Designed to be easy to learn and includes a robust security model.
    * **Multithreaded**: Supports concurrent execution of multiple parts of a program.
    * **Robust**: Strong memory management and exception handling.


### JVM vs JRE vs JDK

These three components are central to Java development and execution.


| Feature | JDK (Java Development Kit) | JRE (Java Runtime Environment) | JVM (Java Virtual Machine) |
| :-- | :-- | :-- | :-- |
| **Primary Purpose** | To develop Java applications. | To run compiled Java applications. | To execute Java bytecode. |
| **Contains** | JRE + Development Tools (Compiler `javac`, debugger `jdb`). | JVM + Java Class Libraries. | A specification for an abstract computing machine. |
| **Audience** | Developers. | End-users. | Part of both JRE and JDK, not used directly. |
| **Analogy** | A full **workshop** with tools to build furniture (JRE) and blueprints to execute (JVM). | The **furniture** itself, ready to be used. | The **instructions** or blueprint for how the furniture works. |

### Java Compilation and Execution

The process involves compiling source code into platform-neutral bytecode, which is then interpreted by the JVM.

1. **Write**: You write Java source code in a `.java` file (e.g., `MyProgram.java`).
2. **Compile**: The Java compiler (`javac`) compiles the source code into bytecode, creating a `.class` file (e.g., `MyProgram.class`).
3. **Run**: The `java` command starts the JVM, which loads the `.class` file, verifies the bytecode, and executes it.

* **Analogy**: Bytecode is like a universal recipe written in a standard format. The JVM is like a chef who can read this universal recipe and cook the meal (run the program) in their specific kitchen (Operating System).


### Data Types

Java has two categories of data types: primitive and reference.

* **Primitive Types**: The eight fundamental data types.
    * **byte**: 8-bit integer.
    * **short**: 16-bit integer.
    * **int**: 32-bit integer.
    * **long**: 64-bit integer.
    * **float**: 32-bit floating-point.
    * **double**: 64-bit floating-point.
    * **char**: 16-bit Unicode character.
    * **boolean**: `true` or `false`.
* **Reference Types**: Variables that store the memory address of an object (e.g., `String`, `Object`, arrays, and any user-created class). They do not store the object itself.


### Variables, Constants, Scope, and var

Variables store data, constants store fixed data, and scope defines visibility.

* **Variables**:
    * **Instance Variables**: Declared in a class but outside a method. Each object has its own copy.
    * **Static Variables**: Declared with the `static` keyword. Shared among all objects of the class.
    * **Local Variables**: Declared inside a method or block. Exist only within that scope.
* **Constants**: Declared using the `final` keyword. Their value cannot be changed once assigned.

```java
final double PI = 3.14159;
```

* **Scope**: Refers to the visibility of a variable. A variable is only accessible within the block (`{...}`) it was declared in.
* **var (Local Variable Type Inference)**:
    * **Java 10+ Note**: The `var` keyword allows the compiler to infer the type of a local variable from its initializer. It cannot be used for instance variables, method parameters, or return types.

```java
var message = "Hello, Java 10!"; // Inferred as String
var userList = new ArrayList<String>(); // Inferred as ArrayList<String>
```


### Operators and Control Flow

* **Operators**: Arithmetic (`+`, `-`, `*`, `/`, `%`), Relational (`==`, `!=`, `>`, `<`), Logical (`&&`, `||`, `!`), and more.
* **Control Flow**:
    * **if-else**: Conditional branching.
    * **switch**: Multi-way branching.
        * **Java 14+ Note**: Enhanced `switch` expressions simplify code and can return a value.

```java
int day = 3;
String dayType = switch (day) {
    case 1, 2, 3, 4, 5 -> "Weekday";
    case 6, 7 -> "Weekend";
    default -> "Invalid day";
};
```

    * **Loops**: `for` (traditional and for-each), `while`, and `do-while`.


### Arrays

Arrays are fixed-size, ordered collections of elements of the same type.

* **Declaration and Initialization**:

```java
// Declaration
int[] numbers;
// Initialization
numbers = new int[5]; // An array of 5 integers
// Combined
String[] names = {"Alice", "Bob", "Charlie"};
```

* **Multidimensional Arrays**: Arrays of arrays.

```java
int[][] matrix = { {1, 2}, {3, 4} };
```


### Command-Line Arguments

The `main` method's `String[] args` parameter receives arguments passed from the command line.

```java
public class Greeter {
    public static void main(String[] args) {
        if (args.length > 0) {
            System.out.println("Hello, " + args[0]);
        } else {
            System.out.println("Hello, World!");
        }
    }
}
```

* **Execution**: `java Greeter John` will print "Hello, John".


### Java Coding Conventions

* **Best Practice**: Following conventions improves readability.
    * **Classes**: `UpperCamelCase` (e.g., `MyClass`).
    * **Methods/Variables**: `lowerCamelCase` (e.g., `myMethod`, `userName`).
    * **Constants**: `UPPER_SNAKE_CASE` (e.g., `MAX_SIZE`).
    * **Packages**: `lowercase.reverse.domain` (e.g., `com.mycompany.app`).


### String Immutability, Pool, and Interning

* **Immutability**: `String` objects are immutable. Once created, their value cannot be changed. Any modification (like concatenation) creates a new `String` object.
* **String Pool**: An area in the heap where Java stores string literals. This allows for re-use of strings, saving memory.
    * **Analogy**: The String Pool is a shared library of commonly used phrases. When you need a phrase like "Hello", Java gives you a reference to the existing one in the library instead of creating a new copy.
* **intern() method**: This method can be called on a `String` object. It checks if an equal string exists in the pool. If yes, it returns the pool's reference; otherwise, it adds the string to the pool and returns a reference to it.

```java
String s1 = "Test"; // Stored in the pool
String s2 = new String("Test"); // Created in heap, outside the pool
System.out.println(s1 == s2); // false
s2 = s2.intern(); // s2 now points to the pool's "Test"
System.out.println(s1 == s2); // true
```


### Pass-by-Value for Object References

* **Common Pitfall**: A frequent misunderstanding is that Java is "pass-by-reference" for objects. Java is *always* **pass-by-value**.
    * For **primitives**, the value itself is copied.
    * For **objects**, the value of the reference (the memory address) is copied.
* **Analogy**: You write your home address on a piece of paper. If you pass this paper to a friend (pass the reference by value), they get a *copy* of the address.
    * They can go to your house and paint the door (modify the object's state).
    * They cannot change your original piece of paper to a new address (re-assign the original reference variable).


### Wrapper Classes and Autoboxing

Wrapper classes convert primitive types into objects.

* `int` -> `Integer`, `char` -> `Character`, etc.
* **Autoboxing**: Automatic conversion of a primitive to its corresponding wrapper object.
* **Unboxing**: Automatic conversion of a wrapper object to its corresponding primitive.

```java
Integer a = 100; // Autoboxing (int to Integer)
int b = a;       // Unboxing (Integer to int)
```

* **Common Pitfall**: Unboxing a `null` wrapper reference will cause a `NullPointerException`. Be cautious when using wrapper types in collections or as return types.

```java
Integer myValue = null;
int primitiveValue = myValue; // Throws NullPointerException
```


### Java Memory Model: Stack and Heap

* **Stack Memory**: Stores local variables (primitives) and references to objects. Memory is allocated and deallocated automatically as methods are called and returned (LIFO). Each thread has its own stack.
* **Heap Memory**: Stores all objects and arrays. This memory is shared among all threads. The Garbage Collector manages deallocation.

***

## Object-Oriented Programming (OOP)

This section covers the principles and constructs that form the foundation of Java's object-oriented nature.

### Classes and Objects

* **Class**: A blueprint or template for creating objects. It defines the properties (fields) and behaviors (methods) that its objects will have.
* **Object**: An instance of a class. It has state (values of its fields) and behavior (defined by its methods).
* **Analogy**: A `Car` class is like a blueprint for a car. It specifies that a car will have a `color` and can `drive()`. An object, like `myRedCar`, is a tangible car built from that blueprint with a specific `color` (red).

```java
// Class (Blueprint)
class Car {
    String color; // Field

    void drive() { // Method
        System.out.println("The car is driving.");
    }
}

// Object (Instance)
Car myCar = new Car();
myCar.color = "Red";
myCar.drive();
```


### OOP Principles

Java is built on four core principles of OOP.

1. **Encapsulation**: Bundling data (fields) and the methods that operate on that data into a single unit (a class). It restricts direct access to an object's components, which is a key part of data hiding.
    * **Best Practice**: Make fields `private` and provide `public` getter and setter methods to control access.
2. **Inheritance**: A mechanism where a new class (subclass or child) acquires the properties and behaviors of an existing class (superclass or parent). It promotes code reuse.
    * Use the `extends` keyword.
3. **Polymorphism**: "Many forms." Allows an object to be treated as an instance of its parent class, enabling a single action to be performed in different ways. This is achieved through method overriding and overloading.
4. **Abstraction**: Hiding complex implementation details and showing only the essential features of an object. This is achieved using `abstract` classes and `interfaces`.

### Access Modifiers

Access modifiers control the visibility of classes, fields, and methods.


| Modifier | Same Class | Same Package | Subclass (Different Package) | World (Different Package) |
| :-- | :-- | :-- | :-- | :-- |
| `public` | Yes | Yes | Yes | Yes |
| `protected` | Yes | Yes | Yes | No |
| `default` | Yes | Yes | No | No |
| `private` | Yes | No | No | No |

### Constructors

A special method used to initialize objects. It has the same name as the class and no return type.

* **Overloaded Constructors**: A class can have multiple constructors with different parameter lists.
* **Private Constructor**: Prevents instantiation of a class from outside. Useful for Singleton patterns or utility classes.
* **Constructor Chaining**: Calling one constructor from another. Use `this()` to call a constructor in the same class and `super()` to call a parent class constructor. `this()` or `super()` must be the first statement.

```java
class Employee {
    String name;
    String role;

    Employee(String name) {
        this(name, "Default Role"); // Chaining to the other constructor
    }

    Employee(String name, String role) {
        this.name = name;
        this.role = role;
    }
}
```


### `this` and `super` Keywords

* **`this`**: Refers to the current object instance. Used to:
    * Differentiate between instance variables and local variables.
    * Call another constructor in the same class (`this()`).
    * Pass the current object as an argument to another method.
* **`super`**: Refers to the immediate parent class object. Used to:
    * Access methods of the parent class that have been overridden.
    * Call the parent class constructor (`super()`).


### Method Overloading vs. Overriding

| Feature | Method Overloading | Method Overriding |
| :-- | :-- | :-- |
| **Purpose** | To have methods with the same name but different parameters. | To provide a specific implementation for a method already defined in a parent class. |
| **Location** | Occurs within the same class. | Involves two classes (parent and child). |
| **Signature** | Must have a different method signature (number or type of parameters). | Must have the same method signature. |
| **Return Type** | Can be different. | Must be the same or a covariant type. |
| **Binding** | Resolved at compile time (Static Polymorphism). | Resolved at runtime (Dynamic Polymorphism). |

### Static Members

Static members belong to the class itself, not to any specific instance.

* **Static Variable**: One copy is shared among all objects of the class.
* **Static Method**: Can be called without creating an object of the class. Cannot access non-static members directly.
* **Static Block**: A block of code that runs once, when the class is first loaded into memory. Used for initializing static variables.


### Final Keyword

The `final` keyword is used to create constants and restrict inheritance/overriding.

* **`final` variable**: Its value cannot be changed. It's a constant.
* **`final` method**: Cannot be overridden by a subclass.
* **`final` class**: Cannot be extended (inherited from).


### Inner Classes

A class defined within another class.

1. **Static Nested Class**: A `static` class inside another class. Does not have access to the outer class's non-static members.
2. **Inner Class (Non-static)**: Has access to all members of the outer class, including `private` ones.
3. **Local Inner Class**: Defined inside a method. Its scope is limited to the method.
4. **Anonymous Inner Class**: A class without a name, used for one-time implementation of an interface or class. Lambdas often replace them since Java 8.

### Abstract Classes vs. Interfaces

| Feature | Abstract Class | Interface |
| :-- | :-- | :-- |
| **Purpose** | To provide a common base for related classes (is-a relationship). | To define a contract that classes must adhere to (can-do relationship). |
| **Multiple Inheritance** | No, a class can extend only one abstract class. | Yes, a class can implement multiple interfaces. |
| **Fields** | Can have `final`, `non-final`, `static`, and `non-static` fields. | Fields are implicitly `public static final`. |
| **Constructors** | Can have constructors (called via `super()` from subclasses). | Cannot have constructors. |
| **Methods** | Can have both abstract and concrete (implemented) methods. | Before Java 8, only abstract. Since Java 8, can have `default` and `static` methods. Since Java 9, can have `private` methods. |
| **When to Use** | When you need to share code among several closely related classes. | When you need to define a capability for disparate classes. |

### Sealed Classes (Java 17+)

* **Java 17 Note**: `sealed` classes and interfaces restrict which other classes or interfaces may extend or implement them. This provides more control over inheritance hierarchies.
* The `permits` clause specifies the allowed subclasses.

```java
public sealed class Shape permits Circle, Square, Triangle {
    // ...
}

public final class Circle extends Shape { /* ... */ } // Subclasses must be final, sealed, or non-sealed
public final class Square extends Shape { /* ... */ }
public non-sealed class Triangle extends Shape { /* ... */ } // Can be extended by any class
```


### `Object` Class Methods

Every class in Java implicitly extends the `Object` class. Key methods to know:

* `equals(Object obj)`: Checks for equality between two objects.
    * **Best Practice**: Always override `hashCode()` when you override `equals()`.
* `hashCode()`: Returns a hash code value for the object, used by hash-based collections like `HashMap`.
* `toString()`: Returns a string representation of the object.
* `clone()`: Creates and returns a copy of the object.


### Cloning and `Cloneable` Interface

* The `Cloneable` interface is a marker interface (no methods). A class must implement it to indicate that `Object.clone()` is allowed.
* **Common Pitfall**: The default `clone()` performs a **shallow copy**. It copies primitives but only references to objects. If the object contains other objects, you might need to implement a **deep copy** by overriding `clone()`.


### Covariant Return Types

From Java 5, a subclass can override a parent method and change its return type, provided the new type is a subtype of the original.

```java
class Animal {
    Animal getSelf() {
        return this;
    }
}

class Dog extends Animal {
    @Override
    Dog getSelf() { // Covariant return type (Dog is a subtype of Animal)
        return this;
    }
}
```


### Composition vs. Inheritance

Two primary ways to reuse code.

* **Inheritance (IS-A relationship)**: "A `Dog` is an `Animal`".
* **Composition (HAS-A relationship)**: "A `Car` has an `Engine`".
* **Best Practice**: Favor **composition over inheritance**. It offers more flexibility and is less fragile. Inheritance creates a tight coupling between parent and child classes, which can be hard to maintain.

***

## Advanced Java Features

This section covers key features introduced in Java 8 and later versions, which have significantly modernized the language.

### Interfaces (Evolved)

Interfaces have evolved beyond being pure abstraction contracts.

* **Java 8 Note**:
    * **`default` methods**: Allow adding new methods to interfaces without breaking existing implementing classes. They provide a default implementation.
    * **`static` methods**: Utility methods that are part of the interface but are not tied to an instance. They can be called directly on the interface.
* **Java 9 Note**:
    * **`private` methods**: Can be added to share code between `default` methods within the interface itself, avoiding code duplication.


### Functional Interfaces and `@FunctionalInterface`

A functional interface is an interface that contains exactly one abstract method.

* **Java 8 Note**: The `@FunctionalInterface` annotation is optional but recommended. The compiler will trigger an error if the annotated interface does not meet the criteria.
* Examples: `Runnable`, `Callable`, `Comparator`. `java.util.function` package provides many like `Predicate<T>`, `Function<T, R>`, `Consumer<T>`, `Supplier<T>`.

```java
@FunctionalInterface
interface Greeter {
    void sayHello(String name);
}
```


### Lambda Expressions

* **Java 8 Note**: Lambdas provide a concise way to implement a functional interface. They are essentially anonymous functions.
* **Syntax**: `(parameters) -> { body }` or `(parameters) -> expression`

```java
// Before Java 8 (Anonymous Class)
Runnable r1 = new Runnable() {
    @Override
    public void run() {
        System.out.println("Running in a thread");
    }
};

// With Lambda Expression
Runnable r2 = () -> System.out.println("Running in a thread");
```


### Method References

* **Java 8 Note**: A shorthand syntax for a lambda expression that executes just one method.

| Type | Syntax | Lambda Equivalent |
| :-- | :-- | :-- |
| **Static Method** | `ClassName::staticMethodName` | `(args) -> ClassName.staticMethodName(args)` |
| **Instance Method (Object)** | `objectRef::instanceMethodName` | `(args) -> objectRef.instanceMethodName(args)` |
| **Instance Method (Class)** | `ClassName::instanceMethodName` | `(obj, args) -> obj.instanceMethodName(args)` |
| **Constructor** | `ClassName::new` | `(args) -> new ClassName(args)` |

### Streams API

* **Java 8 Note**: Provides a declarative way to process sequences of elements. Streams are not data structures; they carry values from a source through a pipeline of operations.
* **Key Operations**:
    * **Intermediate**: Return a new stream. They are lazy.
        * `filter(Predicate<T>)`: Selects elements that match a criteria.
        * `map(Function<T, R>)`: Transforms each element.
        * `sorted()`: Sorts the elements.
    * **Terminal**: Produce a result or side-effect. They trigger the stream processing.
        * `forEach(Consumer<T>)`: Performs an action for each element.
        * `collect(Collectors.toList())`: Collects elements into a collection.
        * `reduce()`: Combines elements into a single result.
        * `count()`: Returns the number of elements.

```java
List<String> names = List.of("Alice", "Bob", "ANNA", "Charlie");

List<String> filteredNames = names.stream()
    .filter(name -> name.startsWith("A")) // Intermediate
    .map(String::toUpperCase)             // Intermediate
    .collect(Collectors.toList());        // Terminal -> ["ALICE", "ANNA"]
```


### `Optional` API

* **Java 8 Note**: A container object that may or may not contain a non-null value. Its purpose is to avoid `NullPointerException`.
* **Common Pitfall**: Avoid `if (opt.isPresent()) { opt.get(); }`. This is no better than a null check.
* **Best Practices**: Use alternative methods.
    * `orElse(T other)`: Return the value if present, otherwise return `other`.
    * `orElseGet(Supplier<T> other)`: Return the value if present, otherwise return the result of a supplier.
    * `orElseThrow()`: Return the value if present, otherwise throw an exception.
    * `ifPresent(Consumer<T> consumer)`: Execute a block of code only if a value is present.

```java
Optional<String> name = Optional.ofNullable(findNameById(123));
String finalName = name.orElse("Unknown");
```


### Date \& Time API (`java.time`)

* **Java 8 Note**: A modern, immutable, and more intuitive API for handling dates and times, replacing the old `java.util.Date` and `Calendar`.
* **Key Classes**:
    * `LocalDate`: Date without time (e.g., `2025-09-21`).
    * `LocalTime`: Time without date (e.g., `18:30:00`).
    * `LocalDateTime`: Date with time.
    * `ZonedDateTime`: Date-time with a time zone.
    * `Duration`: A time-based amount of time (e.g., "30 seconds").
    * `Period`: A date-based amount of time (e.g., "2 years, 3 months").


### `var` (Local-Variable Type Inference)

* **Java 10 Note**: Allows the compiler to infer the type of a local variable, reducing boilerplate.
* **Limitations**: Cannot be used for fields, method parameters, or return types. The variable must be initialized on the same line.


### Enhanced `switch` Expressions

* **Java 14 Note**: `switch` can be used as an expression that returns a value. The `->` syntax avoids fall-through and removes the need for `break`.

```java
int month = 4;
String season = switch (month) {
    case 12, 1, 2 -> "Winter";
    case 3, 4, 5 -> "Spring";
    // ...
    default -> "Unknown";
};
```


### Text Blocks

* **Java 15 Note**: Simplify the creation of multi-line string literals, avoiding the clutter of explicit newlines (`\n`) and concatenation.

```java
// Before Java 15
String json = "{\n" +
              "  \"name\": \"John\",\n" +
              "  \"age\": 30\n" +
              "}";

// With Text Blocks
String textBlockJson = """
                       {
                         "name": "John",
                         "age": 30
                       }
                       """;
```


### Records

* **Java 16 Note**: A concise syntax for creating immutable data carrier classes. The compiler automatically generates a constructor, getters, `equals()`, `hashCode()`, and `toString()`.

```java
// A lot of boilerplate
class PointClass {
    private final int x;
    private final int y;
    // constructor, getters, equals, hashCode, toString...
}

// Concise and immutable
public record Point(int x, int y) {}

// Usage
Point p = new Point(10, 20);
System.out.println(p.x()); // Accessor method
```


### Pattern Matching

* **`instanceof` (Java 16)**: Simplifies type checking and casting.

```java
// Before
if (obj instanceof String) {
    String s = (String) obj;
    System.out.println(s.toUpperCase());
}

// After
if (obj instanceof String s) {
    System.out.println(s.toUpperCase());
}
```

* **`switch` (Java 21)**: Allows `switch` statements and expressions to test an object against type patterns.
    * **Pattern Guards**: The `when` clause adds a further condition to a case label.

```java
static String format(Object obj) {
    return switch (obj) {
        case Integer i -> String.format("int %d", i);
        case Long l    -> String.format("long %d", l);
        case String s when s.length() > 5 -> "Long String"; // Pattern guard
        case String s  -> "String";
        default        -> "unknown";
    };
}
```


### Virtual Threads

* **Java 21 Note (Project Loom)**: Lightweight threads managed by the JVM, not the OS. They are cheap to create and block on, making them ideal for high-throughput I/O-bound applications.
* **Analogy**: **Platform Threads** are like professional chefs. You can only have a few in a kitchen (OS limit), and if one is waiting for an ingredient, they are stuck. **Virtual Threads** are like having countless kitchen assistants. If one has to wait, they step aside, and another takes their place immediately, keeping the kitchen highly efficient.
* **Best Practice**: Use `Executors.newVirtualThreadPerTaskExecutor()` to easily run tasks on virtual threads.


### Java Modules

* **Java 9 Note (Project Jigsaw)**: A system for organizing code into modules, providing reliable configuration and strong encapsulation.
* Defined in a `module-info.java` file, which specifies a module's dependencies (`requires`) and exported packages (`exports`).

***
Would you like to continue with "Section 4: Exception Handling"?

---

## Exception Handling

Exception handling provides a robust way to manage runtime errors, allowing a program to handle disruptions gracefully instead of crashing.

* **Analogy**: Think of your program as a chef in a kitchen. The main workflow is the recipe (`try` block). An **exception** is an unexpected problem, like running out of an ingredient or a fire starting.
    * `catch` block: A specific plan for that problem (e.g., "If out of salt, use soy sauce").
    * `finally` block: The cleanup routine that always happens, like washing the dishes, regardless of whether the recipe succeeded or failed.


### Checked vs. Unchecked Exceptions

Java categorizes exceptions into two main types, which dictates how they must be handled.


| Type | Checked Exceptions | Unchecked Exceptions (Runtime Exceptions) |
| :-- | :-- | :-- |
| **Parent Class** | `Exception` (but not `RuntimeException`) | `RuntimeException` and `Error` |
| **Compile-Time Check** | **Yes**. The compiler forces you to handle them (`try-catch` or `throws`). | **No**. The compiler does not check for handling. |
| **When they occur** | Predictable, recoverable errors (e.g., file not found, network issue). | Programming errors or unexpected system failures (e.g., null pointer, bad index). |
| **Examples** | `IOException`, `SQLException`, `ClassNotFoundException` | `NullPointerException`, `ArrayIndexOutOfBoundsException`, `IllegalArgumentException` |
| **Handling Strategy** | You are *required* to anticipate and handle them. | You *can* handle them, but it's often better to fix the underlying bug. |

### `try-catch-finally` and `try-with-resources`

* **`try`**: Encloses the code that might throw an exception.
* **`catch`**: Catches and handles a specific type of exception. You can have multiple `catch` blocks.
* **`finally`**: An optional block that **always executes**, whether an exception was thrown or not. It's used for cleanup code (e.g., closing files, releasing network sockets).
* **`try-with-resources` (Java 7+)**: A superior alternative to `finally` for resource management. It automatically closes any resource that implements the `AutoCloseable` interface.
    * **Best Practice**: Always use `try-with-resources` for managing resources like streams, connections, and scanners to prevent resource leaks.

```java
// Old way with finally
Scanner scanner = null;
try {
    scanner = new Scanner(new File("test.txt"));
    while (scanner.hasNext()) {
        System.out.println(scanner.nextLine());
    }
} catch (FileNotFoundException e) {
    e.printStackTrace();
} finally {
    if (scanner != null) {
        scanner.close(); // Manual cleanup
    }
}

// Modern way with try-with-resources
try (Scanner scanner = new Scanner(new File("test.txt"))) {
    while (scanner.hasNext()) {
        System.out.println(scanner.nextLine());
    }
} catch (FileNotFoundException e) { // Resource is closed automatically
    e.printStackTrace();
}
```


### `throw` vs. `throws`

This is a common point of confusion.

* **`throw`**: A keyword used to **manually throw an exception** at a specific point in the code. It is followed by an instance of an exception object.
* **`throws`**: A keyword used in a **method signature** to declare that the method might throw one or more specified checked exceptions. It delegates the responsibility of handling the exception to the caller.

```java
// 'throws' declares the potential problem
void processFile(String fileName) throws FileNotFoundException {
    if (fileName == null) {
        // 'throw' creates and triggers the problem
        throw new IllegalArgumentException("File name cannot be null."); // Unchecked
    }
    // Code that might throw a FileNotFoundException (Checked)
    FileReader reader = new FileReader(fileName);
}
```


### Custom Exception Creation

You can create your own exception classes to represent specific problems in your application's domain.

* **Best Practice**: Extend `Exception` for a checked exception or `RuntimeException` for an unchecked exception.

```java
// Custom checked exception
class InsufficientFundsException extends Exception {
    public InsufficientFundsException(String message) {
        super(message);
    }
}

// Usage
public void withdraw(double amount) throws InsufficientFundsException {
    if (balance < amount) {
        throw new InsufficientFundsException("Not enough funds to withdraw " + amount);
    }
    // ...
}
```


### Exception Chaining

Exception chaining is the practice of wrapping an exception within another one. This is useful for adding context while preserving the original cause of the error.

* The original exception is called the **cause**.
* Use the `initCause(Throwable)` method or pass the cause to the constructor.

```java
void dataAccessMethod() {
    try {
        // ... code that throws SQLException
    } catch (SQLException e) {
        // Wrap the specific low-level exception in a more general, application-specific one
        throw new DataAccessException("Failed to access data", e); // e is the cause
    }
}
```


### Suppressed Exceptions

* Relevant to `try-with-resources`. If an exception is thrown in the `try` block and *another* exception is thrown when auto-closing the resource, the second exception is "suppressed."
* The primary exception is thrown, and the suppressed exception is attached to it, so you don't lose information. You can retrieve it via `getSuppressed()`.


### Multi-catch Block

* **Java 7 Note**: Allows you to catch multiple exception types in a single `catch` block, reducing code duplication.
* The caught exception variable (`e`) is implicitly `final`.

```java
// Before Java 7
try {
    // ...
} catch (IOException ex) {
    logger.log(ex);
    throw ex;
} catch (SQLException ex) {
    logger.log(ex);
    throw ex;
}

// With multi-catch
try {
    // ...
} catch (IOException | SQLException ex) { // Concise syntax
    logger.log(ex);
    throw ex;
}
```


### Best Practices for Exception Handling

* **Don't swallow exceptions**: An empty `catch` block is a major red flag. At a minimum, log the exception.
* **Catch specific exceptions**: Avoid catching the generic `Exception` or `Throwable`. Catch the most specific exception class possible to handle errors appropriately.
* **Use `try-with-resources`**: Prefer it over `finally` for resource management.
* **Don't use exceptions for control flow**: Exceptions are for exceptional conditions, not for normal program logic (e.g., breaking out of a loop).
* **Document exceptions**: Use the `@throws` Javadoc tag to inform callers about the checked exceptions a method can throw.

***

## Collections Framework

The Java Collections Framework provides a unified architecture for storing and manipulating groups of objects. It consists of interfaces, implementations, and algorithms.

* **Analogy**: Think of the framework as a set of different types of containers.
    * A **`List`** is like a numbered rack of storage bins; items are kept in order and you can have identical items in different bins.
    * A **`Set`** is like a bag of unique items; order doesn't matter, and you can't have duplicates.
    * A **`Map`** is like a dictionary or a phone book; it stores pairs of keys (words/names) and values (definitions/numbers).


### Core Interfaces Hierarchy

The framework is built around a set of core interfaces.

* `Iterable`: The root interface, allows an object to be the target of the "for-each loop."
* `Collection`: The foundation of the framework, represents a group of objects.
    * `List`: An **ordered** collection (a sequence) that **allows duplicate** elements. Access is by index.
    * `Set`: A collection that contains **no duplicate** elements.
    * `Queue`: A collection used to hold elements prior to processing, typically in a **FIFO** (First-In, First-Out) order.
* `Map`: An object that maps **keys to values**. It is not part of the `Collection` hierarchy but is considered part of the framework. Keys must be unique.


### Common Implementations

#### List Implementations

| Feature | `ArrayList` | `LinkedList` | `Vector` |
| :-- | :-- | :-- | :-- |
| **Underlying DS** | Dynamic Array | Doubly-Linked List | Dynamic Array |
| **Performance** | Fast for random access (`get(i)`). Slow for insertion/deletion in the middle. | Fast for insertion/deletion. Slow for random access. | Similar to `ArrayList` but slower due to synchronization. |
| **Synchronization** | Not synchronized. | Not synchronized. | Synchronized (thread-safe). |
| **Best Use Case** | When you need fast random access and mostly read or append to the list. | When you have frequent insertions/deletions in the middle of the list. | Legacy code. Prefer `ArrayList` with explicit synchronization if needed. |

#### Set Implementations

| Feature | `HashSet` | `LinkedHashSet` | `TreeSet` |
| :-- | :-- | :-- | :-- |
| **Ordering** | Unordered. | **Insertion order** is maintained. | **Sorted order** (natural or by a `Comparator`). |
| **Underlying DS** | `HashMap` | `LinkedList` + `HashMap` | Red-Black Tree (`TreeMap`) |
| **Performance** | O(1) for `add`, `remove`, `contains` (average). | O(1) for `add`, `remove`, `contains` (average), but slightly slower than `HashSet`. | O(log n) for `add`, `remove`, `contains`. |
| **Nulls** | Allows one `null` element. | Allows one `null` element. | Does not allow `null` (unless `Comparator` handles it). |
| **Best Use Case** | When you need a set and don't care about order. | When you need a set that maintains the order of insertion. | When you need a set that is always sorted. |

#### Map Implementations

| Feature | `HashMap` | `LinkedHashMap` | `TreeMap` | `Hashtable` |
| :-- | :-- | :-- | :-- | :-- |
| **Ordering** | Unordered. | Insertion order. | Sorted by key. | Unordered. |
| **Nulls** | Allows one `null` key and multiple `null` values. | Allows one `null` key and multiple `null` values. | Does not allow `null` keys. | Does not allow `null` keys or `null` values. |
| **Synchronization** | Not synchronized. | Not synchronized. | Not synchronized. | Synchronized (thread-safe). |
| **Performance** | O(1) for `get`, `put`. | O(1) for `get`, `put`. | O(log n) for `get`, `put`. | Slower than `HashMap` due to synchronization. |
| **Best Use Case** | General-purpose key-value storage. | When you need to iterate over keys in insertion order (e.g., caches). | When you need a map sorted by its keys. | Legacy code. Prefer `ConcurrentHashMap` for thread-safe operations. |

### Iteration: `Iterator` and `for-each`

* **`Iterator`**: The standard way to traverse a collection. Provides `hasNext()`, `next()`, and an optional `remove()` method.
* **`ListIterator`**: An extension of `Iterator` for `List`s, allowing bidirectional traversal (`hasPrevious()`, `previous()`) and element modification (`set()`, `add()`).
* **`for-each` loop**: Syntactic sugar over the `Iterator`.

```java
List<String> list = List.of("A", "B", "C");
// Under the hood, this uses an iterator.
for (String item : list) {
    System.out.println(item);
}
```


### Sorting: `Comparable` and `Comparator`

These interfaces define how objects are ordered and sorted.

* **`Comparable<T>`**: For **natural ordering**. A class implements `Comparable` to define its single, default sort order. The `compareTo()` method must be implemented.
* **`Comparator<T>`**: For **custom or multiple orderings**. A `Comparator` is implemented in a separate class or as a lambda. It can be passed to sorting methods like `Collections.sort()` or `Stream.sorted()`.

```java
// Comparable for natural ordering
class Student implements Comparable<Student> {
    int id;
    String name;
    @Override
    public int compareTo(Student other) {
        return Integer.compare(this.id, other.id); // Natural order is by ID
    }
}

// Comparator for a custom order
class SortByName implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return s1.name.compareTo(s2.name);
    }
}
// Usage with a lambda (Java 8+)
students.sort((s1, s2) -> s1.name.compareTo(s2.name));
```


### `Collections` Utility Class

Provides static utility methods for operating on collections, such as:

* `sort(List<T> list)`: Sorts a list.
* `reverse(List<?> list)`: Reverses the order of elements.
* `shuffle(List<?> list)`: Randomly shuffles elements.
* `binarySearch(List<? extends Comparable<?>> list, T key)`: Efficiently searches a sorted list.
* `synchronizedCollection(Collection<T> c)`: Returns a thread-safe wrapper.
* `unmodifiableList(List<? extends T> list)`: Returns an unmodifiable view of a list.


### Fail-Fast vs. Fail-Safe Iterators

* **Fail-Fast**: The iterator immediately throws a `ConcurrentModificationException` if the collection is structurally modified (e.g., add/remove elements) from outside the iterator after it has been created.
    * **Implementations**: `ArrayList`, `HashMap`, `HashSet`.
* **Fail-Safe**: The iterator works on a clone or a snapshot of the collection. It does not throw an exception if the underlying collection is modified.
    * **Implementations**: `ConcurrentHashMap`, `CopyOnWriteArrayList`.


### `equals()` and `hashCode()` Contract

* **Critical Best Practice**: When you store objects in a hash-based collection (`HashSet`, `HashMap`), you **must** correctly override both `equals()` and `hashCode()`.
* **The Contract**:

1. If `obj1.equals(obj2)` is true, then `obj1.hashCode()` **must** be equal to `obj2.hashCode()`.
2. If `obj1.hashCode()` is not equal to `obj2.hashCode()`, then `obj1.equals(obj2)` **must** be false.
* **Common Pitfall**: Overriding `equals()` without overriding `hashCode()` will lead to objects being "lost" in hash-based collections because the collection looks in the wrong "bucket."


### Modern Collection Features

* **Java 8**: `Stream` API for powerful, declarative data processing. `forEach()` method on `Iterable`.
* **Java 9**: Static factory methods for creating immutable collections concisely.
    * `List.of("a", "b")`, `Set.of(1, 2)`, `Map.of("k1", "v1", "k2", "v2")`.
    * **Note**: These collections are truly immutable, reject `null` elements/keys/values, and have a fixed size.

***

## Multithreading \& Concurrency

Concurrency allows a program to do multiple things at the same time, improving throughput and responsiveness.

### Process vs. Thread

* **Process**: An instance of a program running in its own memory space (e.g., your browser, a code editor). Processes are isolated from each other.
* **Thread**: The smallest unit of execution within a process. A process can have multiple threads that share the same memory space (heap), but each thread has its own stack.
* **Analogy**: A **process** is like a restaurant. A **thread** is a chef working in that restaurant's kitchen. Multiple chefs (threads) can work in the same kitchen (process), sharing utensils and ingredients (heap memory), but each chef has their own personal recipe book (thread stack).


### Java Memory Model (JMM)

The JMM defines the rules for how threads interact with memory, ensuring visibility and ordering of variable access across threads.

* **Main Memory (Heap)**: Shared by all threads.
* **Thread-local Memory (Cache)**: Each thread has its own local cache for performance. Changes made in a local cache are not immediately visible to other threads.
* **Problem**: This can lead to **visibility** issues, where one thread doesn't see the latest value written by another.
* **Analogy**: The **Main Memory** is a central library. Each **thread** is a researcher who borrows a book and makes notes on a personal notepad (local cache). Without a proper protocol, one researcher won't see the notes another has made until the notes are officially added back to the library's master copy. `volatile` and `synchronized` are protocols to ensure notes are read from and written back to the central library.


### Thread Creation, Lifecycle, and Communication

* **Creation**:

1. **Implement `Runnable`**: The preferred approach. Promotes composition.

```java
Runnable task = () -> System.out.println("Running task!");
Thread thread = new Thread(task);
thread.start();
```

2. **Extend `Thread`**: Less flexible as it prevents extending other classes.
* **Lifecycle**: A thread goes through several states:
    * `NEW`: The thread has been created but not yet started.
    * `RUNNABLE`: The thread is ready to run and waiting for CPU time.
    * `BLOCKED`: The thread is waiting to acquire a monitor lock (enter a `synchronized` block).
    * `WAITING`: The thread is waiting indefinitely for another thread to perform an action (e.g., calling `object.wait()` or `thread.join()`).
    * `TIMED_WAITING`: Waiting for a specified amount of time (e.g., `Thread.sleep()`).
    * `TERMINATED`: The thread has completed its execution.
* **Inter-thread Communication**: `wait()`, `notify()`, and `notifyAll()` are methods on the `Object` class used for coordination. They must be called from within a `synchronized` block.


### Thread Joining, Daemon Threads, and Priority

* **`join()`**: Causes the current thread to wait until the thread it's joining on is terminated.
* **Daemon Thread**: A low-priority thread that runs in the background. The JVM will exit without waiting for daemon threads to complete.
    * `thread.setDaemon(true);`
    * **Use Case**: Background tasks like garbage collection or monitoring.
* **Thread Priority**: A hint to the scheduler (`1` to `10`). **Best Practice**: Avoid relying on thread priority for correctness, as its behavior is platform-dependent.


### Locks and Synchronization

Locks are used to prevent race conditions by ensuring that only one thread can access a shared resource at a time.


| Mechanism | `synchronized` Keyword | `java.util.concurrent.locks.Lock` Interface |
| :-- | :-- | :-- |
| **Usage** | A language keyword applied to methods or blocks. | An API with `lock()` and `unlock()` methods. |
| **Locking** | Acquires and releases the lock automatically (block-structured). | Requires manual unlocking, typically in a `finally` block. |
| **Flexibility** | Basic. Blocking and cannot be interrupted. | Advanced. Offers timed waits, interruptible locks, and fairness policies. |
| **Example** | `synchronized(this) { ... }` | `lock.lock(); try { ... } finally { lock.unlock(); }` |

* **`ReentrantLock`**: A re-entrant lock, meaning a thread can acquire the same lock multiple times without deadlocking. It's the most common `Lock` implementation.
* **`ReadWriteLock`**: Allows multiple threads to read a resource concurrently but requires exclusive access for writing. Excellent for read-heavy data structures.
* **`StampedLock` (Java 8)**: An advanced lock with support for optimistic reads, which can offer better performance than `ReadWriteLock` under certain conditions.


### Concurrency Utilities

* **`Semaphore`**: Limits the number of threads that can access a specific resource.
    * **Analogy**: A semaphore with a permit count of 5 is like a restaurant with only 5 tables. The 6th customer must wait until a table is free.
* **`volatile`**: Guarantees that reads and writes to a variable are flushed to/from main memory, ensuring **visibility**. It also prevents certain instruction reordering. It does **not** provide atomicity.
* **Atomic Variables (`AtomicInteger`, `AtomicBoolean`, etc.)**: Provide lock-free, thread-safe operations on single variables using **Compare-And-Swap (CAS)** hardware instructions.


### Executor Framework and Thread Pools

Creating threads is expensive. Thread pools manage a set of worker threads to execute tasks, reducing overhead.

* **`ExecutorService`**: The primary interface for managing thread pools.
* **`Executors` Factory Class**: Provides convenient factory methods.
    * `newFixedThreadPool(int n)`: A pool with a fixed number of threads.
    * `newCachedThreadPool()`: A pool that grows and shrinks dynamically.
    * `newSingleThreadExecutor()`: A pool with only one thread, guaranteeing sequential execution of tasks.
    * `newScheduledThreadPool(int corePoolSize)`: For scheduling tasks to run after a delay or periodically.
* **Shutdown**:
    * `shutdown()`: Initiates a graceful shutdown. No new tasks are accepted, but running tasks will complete.
    * `awaitTermination(...)`: Blocks until all tasks have completed after a `shutdown` request.
* **Common Pitfall**: Not shutting down an `ExecutorService`. The application may not terminate because the threads in the pool are still alive.


### Asynchronous Programming

* **`Callable<V>` and `Future<V>`**:
    * `Callable`: Similar to `Runnable`, but can return a result and throw a checked exception.
    * `Future`: Represents the result of an asynchronous computation. `future.get()` blocks until the result is available.
* **`CompletableFuture<T>` (Java 8)**: A huge improvement over `Future`. It allows for building non-blocking, composable pipelines of asynchronous tasks (e.g., using `thenApply`, `thenCompose`, `allOf`).

```java
CompletableFuture.supplyAsync(() -> fetchOrder(orderId))
    .thenApply(order -> enrichOrder(order))
    .thenAccept(enrichedOrder -> processOrder(enrichedOrder))
    .exceptionally(ex -> { log.error(ex); return null; });
```


### `ThreadLocal`

Provides thread-scoped variables. Each thread that accesses a `ThreadLocal` variable gets its own independent copy.

* **Use Case**: Storing per-thread context, like a user's session ID or a transaction ID, without passing it through every method call.
* **Common Pitfall**: In application servers that use thread pools, `ThreadLocal` variables must be cleaned up (`remove()`) at the end of a request. Otherwise, the value may "leak" to the next request handled by the same thread.


### Virtual Threads vs. Platform Threads (Java 21)

| Feature | Platform (Normal) Threads | Virtual Threads (Project Loom) |
| :-- | :-- | :-- |
| **Nature** | Heavyweight OS threads. A scarce resource. | Lightweight threads managed by the JVM. A plentiful resource. |
| **Mapping** | 1:1 mapping to an OS thread. | M:N mapping. Many virtual threads run on a few platform threads. |
| **Creation Cost** | High. | Very low. |
| **Blocking** | Blocking a platform thread is expensive; it holds onto the OS thread. | Blocking is cheap. The virtual thread unmounts from its carrier platform thread, freeing it to run another virtual thread. |
| **Best For** | CPU-bound tasks. | I/O-bound tasks (e.g., waiting for network or database responses). |

* **Best Practice**: Use `Executors.newVirtualThreadPerTaskExecutor()` to easily leverage virtual threads for I/O-bound tasks.

***

## JVM Internals \& Performance

Understanding the Java Virtual Machine (JVM) is key to writing high-performance, robust applications and diagnosing complex issues like memory leaks and latency problems.

### JVM Architecture

The JVM is an abstract computing machine that enables a computer to run a Java program. Its main components are:

* **Class Loader Subsystem**: Responsible for loading, linking, and initializing class files.
* **Runtime Data Areas**: The memory areas used by the JVM during program execution.
* **Execution Engine**: Executes the bytecode. It includes the Interpreter, JIT Compiler, and Garbage Collector.


### Class Loaders

The JVM uses a delegation model for loading classes, which ensures that core Java classes are never accidentally replaced.

1. **Bootstrap Class Loader**: The root loader. It loads core Java APIs from `rt.jar` (or the `java.base` module in Java 9+). It is written in native code.
2. **Extension / Platform Class Loader**: Loads classes from the JDK's extension directories.
3. **Application / System Class Loader**: Loads classes from the application's classpath.

* **Delegation Process**: When asked to load a class, a class loader first delegates the request to its parent. Only if the parent cannot find the class does the current class loader attempt to load it.
* **Analogy**: Imagine a junior employee (Application loader) is asked for a company document. They first ask their manager (Extension loader). The manager, in turn, first asks the CEO (Bootstrap loader). The document is provided by the first person who finds it, starting from the top. This prevents the junior employee from providing a fake "company policy" document.


### Runtime Data Areas

These are the memory sections the JVM manages.


| Memory Area | Scope | Purpose |
| :-- | :-- | :-- |
| **Stack** | Per-Thread | Stores local variables, method call frames, and partial results. LIFO structure. |
| **PC Registers** | Per-Thread | Holds the address of the currently executing JVM instruction. |
| **Heap** | Shared | Stores all class instances and arrays (objects). Managed by the Garbage Collector. |
| **Method Area** | Shared | Stores per-class structures like runtime constant pool, field/method data, and method code. |
| **Metaspace (Java 8+)** | Shared | The implementation of the Method Area. It's allocated in **native memory**, not the heap. |
| **Runtime Constant Pool** | Per-Class (in Method Area) | A runtime representation of the constant pool table in a class file. |

* **Analogy (JVM Memory)**: A large workshop.
    * The **Heap** is the main factory floor where all products (objects) are assembled and stored.
    * Each worker (thread) has their own **Stack**, which is their personal workbench with instructions for the current task and temporary parts (local variables).
    * The **Method Area/Metaspace** is the central design library, holding all the blueprints (class metadata) for all products.


### Garbage Collection (GC)

GC is the process of automatically reclaiming heap memory occupied by objects that are no longer referenced by the application.

* **Core Idea**: An object is eligible for garbage collection if it is no longer reachable from any "GC Root" (e.g., local variables on a thread's stack, static variables).
* **Phases**: GC algorithms typically involve phases like:
    * **Mark**: Identify and mark all reachable objects.
    * **Sweep**: Remove all unreachable objects.
    * **Compact**: Move reachable objects together to reduce fragmentation.
* **Modern GC Algorithms**:
    * **G1 GC (Garbage-First)**: The default since Java 9. Divides the heap into regions and prioritizes collecting regions with the most garbage. Aims for a balance of throughput and latency.
    * **ZGC \& Shenandoah**: Ultra-low-latency collectors designed for applications with very large heaps and strict pause time requirements (often sub-millisecond).


### Just-In-Time (JIT) Compiler

Java code is first interpreted, which is slow. The JIT compiler improves performance by compiling "hot" (frequently executed) bytecode into native machine code at runtime.

* **Tiered Compilation**: The JVM uses both an interpreter and multiple levels of JIT compilation. Methods start by being interpreted, then get compiled by a "C1" compiler for quick optimization. If a method becomes very hot, it is re-compiled by the more aggressive "C2" compiler for maximum performance.
* **Analogy**: You hire a translator for a foreign speech.
    * **Interpreter**: Translates line-by-line, every time. Slow but starts immediately.
    * **JIT Compiler**: The translator notices the speaker repeats a certain paragraph often. They pre-translate this "hot" paragraph and just read from their notes when it comes up, which is much faster.


### Java Memory Model (JMM)

Defines the rules for how changes to variables made by one thread become visible to other threads. Keywords like `volatile` and `synchronized` are used to enforce these rules and prevent memory consistency errors.

### Profiling Tools

Tools used to monitor and diagnose JVM applications.

* `jconsole`, `jvisualvm`: GUI tools for monitoring CPU, memory, threads, and GC activity.
* `jcmd`: A command-line tool to send diagnostic commands to a running JVM.
* `jmap`: Creates heap dumps to analyze memory usage and find leaks.
* `jstack`: Generates thread dumps to diagnose deadlocks and thread issues.


### Common Performance Topics

* **Memory Leak Patterns**: In Java, a memory leak is when objects are no longer needed but are still reachable, preventing the GC from collecting them. Common causes include:
    * Growing `static` collections that are never cleared.
    * Un-removed listeners or callbacks.
    * Improperly closed resources (pre-Java 7).
* **Reference Types**: Allow you to interact with the GC.
    * `SoftReference`: Objects are garbage collected only when the JVM is low on memory. Good for caches.
    * `WeakReference`: Objects are garbage collected as soon as they are no longer strongly referenced. Used in `WeakHashMap` to hold metadata about objects without preventing their collection.
    * `PhantomReference`: Objects are enqueued for processing *after* they have been finalized. Used for scheduling pre-mortem cleanup actions.
* **Escape Analysis**: A JVM optimization where an object's scope of use is analyzed. If an object does not "escape" its method (i.e., it's not returned or assigned to a field), the JVM can allocate it on the **stack** instead of the heap. This is much faster and avoids GC overhead.

***

## File I/O and NIO

Java provides two main APIs for file and network I/O. The original `java.io` (blocking I/O) and the more modern `java.nio` (non-blocking I/O).

* **Analogy**:
    * **Blocking I/O (`java.io`)** is like making a phone call. You dial, wait for the person to pick up, talk, and hang up. You are "blocked" and can't do anything else until the call is finished.
    * **Non-blocking I/O (`java.nio`)** is like sending a text message. You send it and are immediately free to do other things. You can check your phone later (poll the selector) to see if you have received a reply.


### Legacy I/O (`java.io`)

This API, present since Java 1.0, is stream-based and works with blocking operations.

* **Stream-Based**: Data is read or written sequentially, one byte at a time.
* **Key Classes**:
    * **Byte Streams**: For binary data.
        * `InputStream` / `OutputStream`: The abstract base classes.
        * `FileInputStream` / `FileOutputStream`: For reading from and writing to files.
    * **Character Streams**: For text data (handles character encoding).
        * `Reader` / `Writer`: The abstract base classes.
        * `FileReader` / `FileWriter`: For reading from and writing to files.
* **Decorator Pattern**: `java.io` makes heavy use of wrappers to add functionality.
    * `BufferedInputStream` / `BufferedReader`: Adds buffering to improve performance by reading data in larger chunks.
    * `ObjectInputStream` / `ObjectOutputStream`: For serializing and deserializing objects.
    * `DataInputStream` / `DataOutputStream`: For reading and writing primitive Java data types.

```java
// Common pattern: wrapping streams
try (FileOutputStream fos = new FileOutputStream("data.bin");
     BufferedOutputStream bos = new BufferedOutputStream(fos);
     DataOutputStream dos = new DataOutputStream(bos)) {
    dos.writeInt(123);
    dos.writeDouble(45.67);
} catch (IOException e) {
    e.printStackTrace();
}
```

* **`Scanner`**: A high-level utility for parsing primitive types and strings from an `InputStream` or `Reader`.
* **`PrintWriter`**: A high-level `Writer` with convenient methods like `println()`.


### NIO (`java.nio`) - Non-blocking I/O

Introduced in Java 1.4, NIO provides a more modern, high-performance I/O API. It is buffer-oriented and supports non-blocking operations.

* **Core Components**:

1. **Channels**: A connection to an I/O entity like a file or a socket. Data is read from a channel into a buffer, or written from a buffer to a channel. Examples: `FileChannel`, `SocketChannel`.
2. **Buffers**: A fixed-size block of memory into which data is read or from which data is written. You interact with the buffer, not directly with the channel. The most common is `ByteBuffer`.
        * **Key properties**: `capacity`, `position`, `limit`. You `flip()` a buffer to switch from writing mode to reading mode.
3. **Selectors**: Allows a single thread to manage multiple channels. A thread can register channels with a selector and then ask the selector which channels are ready for I/O (e.g., ready to be read from or written to). This is the foundation of non-blocking I/O in server applications.
* **Memory-mapped files (`MappedByteBuffer`)**: A powerful feature of NIO that maps a region of a file directly into memory. This allows you to access or modify file content as if it were an in-memory array, which can be much faster than traditional stream-based I/O.


### NIO.2 (`java.nio.file`) - The Modern File API

Introduced in Java 7, NIO.2 provides a comprehensive and user-friendly API for working with files and directories, largely replacing the old `java.io.File` class.

* **Key Classes**:
    * **`Path`**: An object representing the path to a file or directory. It is OS-independent. `Paths.get("path/to/file")` is the standard way to create one.
    * **`Files`**: A utility class with numerous static methods for common file operations.
        * `Files.createFile(path)`, `Files.delete(path)`
        * `Files.copy(source, target)`, `Files.move(source, target)`
        * `Files.readAllBytes(path)`, `Files.readAllLines(path)`
        * `Files.write(path, bytes)`
        * `Files.exists(path)`, `Files.isDirectory(path)`
* **Directory Walking**: `Files.walkFileTree()` provides a powerful mechanism for recursively visiting all files and directories starting from a given path, using a `FileVisitor`.

```java
Path start = Paths.get(".");
try {
    Files.walkFileTree(start, new SimpleFileVisitor<Path>() {
        @Override
        public FileVisitResult visitFile(Path file, BasicFileAttributes attrs) {
            System.out.println("Found file: " + file.getFileName());
            return FileVisitResult.CONTINUE;
        }
    });
} catch (IOException e) {
    e.printStackTrace();
}
```

* **`WatchService`**: Allows you to watch a directory for changes (creation, deletion, or modification of files).


### Comparison: `java.io` vs `java.nio`

| Feature | `java.io` (Legacy IO) | `java.nio` (New IO) |
| :-- | :-- | :-- |
| **Orientation** | Stream-oriented (reads/writes one byte at a time). | Buffer-oriented (reads/writes data in blocks/buffers). |
| **Direction** | Streams are one-way (either `InputStream` or `OutputStream`). | Channels are two-way (can read and write). |
| **Blocking Mode** | Blocking. A thread is blocked until the I/O operation is complete. | Supports both blocking and non-blocking modes. |
| **Use Case** | Simple, sequential I/O. Good for small files or basic console I/O. | High-performance I/O, especially for network servers that need to handle many concurrent connections with a few threads. |

* **Best Practice**: For modern file operations, **always prefer the NIO.2 API (`Path`, `Files`)** over the old `java.io.File`. For networking, use NIO for high-concurrency servers.

***

## Reflection \& Annotations

Reflection and Annotations are advanced features that enable meta-programming in Java. They are the backbone of many modern frameworks like Spring, Hibernate, and JUnit.

* **Analogy**:
    * **Reflection** is like having a set of universal tools (a multimeter, a scope, and robotic arms) that can open up any electronic device (an object), inspect its circuit board (class structure), read the values of its components (fields), and even manually trigger its functions (invoke methods), all without a manual.
    * **Annotations** are like **labels** or Post-it notes you stick on the device's components. A `@Test` label tells a testing machine, "This button should be pressed during the quality check." The label itself does nothing, but the machine (the processing tool) understands it and acts accordingly.


### Reflection API

The Reflection API allows a program to inspect and manipulate itself at runtime. It can examine classes, interfaces, fields, and methods, and even create objects and invoke methods dynamically.

#### Core Classes

The main entry point is the `java.lang.Class` object.

* **`Class`**: Represents a class or interface. You can get a `Class` object in three ways:

1. `MyClass.class` (at compile time)
2. `myObject.getClass()` (from an instance)
3. `Class.forName("com.mypackage.MyClass")` (using the fully qualified name)
* **`Field`**: Represents a field of a class.
* **`Method`**: Represents a method of a class.
* **`Constructor`**: Represents a constructor of a class.


#### Example: Inspecting and Modifying an Object

```java
class User {
    private String name = "Default User";
    private void printHello() {
        System.out.println("Hello, " + name);
    }
}

public class ReflectionDemo {
    public static void main(String[] args) throws Exception {
        User user = new User();

        // --- Inspect and modify a private field ---
        Field privateField = User.class.getDeclaredField("name");
        privateField.setAccessible(true); // Break encapsulation!
        privateField.set(user, "John Doe"); // Change the value

        // --- Invoke a private method ---
        Method privateMethod = User.class.getDeclaredMethod("printHello");
        privateMethod.setAccessible(true); // Break encapsulation!
        privateMethod.invoke(user); // Output: Hello, John Doe
    }
}
```


#### Pitfalls and Best Practices

* **Performance Overhead**: Reflection is significantly slower than direct method calls because the JVM cannot perform its usual optimizations.
* **Security Risk**: `setAccessible(true)` breaks encapsulation, allowing access to private members. This can lead to fragile and insecure code.
* **Maintainability Issues**: Code using reflection is hard to refactor. A simple rename of a method or field can break the application at runtime because the names are often hardcoded as strings.
* **Best Practice**: Avoid reflection in general application code. Its use is justified in frameworks, serializers, and testing tools where dynamic behavior is essential.


### Annotations

Annotations provide metadata about the program. They have no direct effect on the operation of the code they annotate, but they can be read by other tools at compile time or runtime.

#### Built-in Annotations

* `@Override`: Tells the compiler that the method is intended to override a method in a superclass.
* `@Deprecated`: Marks a method or class as obsolete. The compiler generates a warning if it's used.
* `@SuppressWarnings`: Instructs the compiler to suppress specific warnings.
* `@FunctionalInterface` (Java 8): Indicates that an interface is intended to be a functional interface.


#### Meta-Annotations

These are annotations that are applied to other annotations.

* **`@Retention`**: Specifies how long the annotation should be retained.
    * `RetentionPolicy.SOURCE`: Discarded by the compiler.
    * `RetentionPolicy.CLASS`: Stored in the `.class` file but not available at runtime (default).
    * `RetentionPolicy.RUNTIME`: Available at runtime via reflection. **This is required for reflection-based processing.**
* **`@Target`**: Specifies the kinds of program elements to which an annotation can be applied (e.g., `TYPE`, `METHOD`, `FIELD`, `PARAMETER`).
* **`@Inherited`**: Indicates that the annotation should be inherited by subclasses.
* **`@Documented`**: Indicates that the annotation should be included in the Javadoc.


#### Custom Annotations and Processing

You can create your own annotations to drive framework logic.

**Step 1: Create a custom annotation**

```java
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

// This annotation will be available at runtime and can be applied to fields.
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.FIELD)
public @interface JsonField {
    public String value() default ""; // A member to hold a custom JSON key name
}
```

**Step 2: Apply the annotation**

```java
class Product {
    @JsonField("product_name")
    private String name;

    private double price;

    public Product(String name, double price) {
        this.name = name;
        this.price = price;
    }
}
```

**Step 3: Process the annotation using reflection**
This is how a JSON serialization library might work.

```java
public class JsonSerializer {
    public String serialize(Object object) throws IllegalAccessException {
        StringBuilder sb = new StringBuilder("{");
        Class<?> clazz = object.getClass();
        for (Field field : clazz.getDeclaredFields()) {
            field.setAccessible(true);
            if (field.isAnnotationPresent(JsonField.class)) {
                JsonField annotation = field.getAnnotation(JsonField.class);
                String key = annotation.value().isEmpty() ? field.getName() : annotation.value();
                sb.append("\"").append(key).append("\": \"").append(field.get(object)).append("\", ");
            }
        }
        // Remove trailing comma and space, add closing brace
        return sb.substring(0, sb.length() - 2) + "}";
    }
}

// Usage
Product p = new Product("Laptop", 1200.00);
JsonSerializer serializer = new JsonSerializer();
String json = serializer.serialize(p); // json will be: {"product_name": "Laptop"}
```

This example shows the powerful synergy between annotations (providing the metadata) and reflection (reading that metadata at runtime to alter behavior).

***

## JDBC \& Database Access

JDBC (Java Database Connectivity) is the standard Java API that allows Java applications to connect and interact with relational databases.

* **Analogy**: JDBC is like a universal adapter for power outlets. Your application is a device (e.g., a laptop), and the database is a foreign wall socket (e.g., European, UK, US). The **JDBC Driver** is the specific plug adapter for that country's socket. The **JDBC API** is the standard interface on the adapter that your laptop's plug always fits into. You only need to change the plug adapter (driver) to connect to a different wall socket (database), but your device's code doesn't change.


### JDBC Architecture and API

The architecture consists of two main layers:

1. **JDBC API**: Provides the interfaces (`Connection`, `Statement`, `ResultSet`, etc.) that your application code uses.
2. **JDBC Driver**: A vendor-specific implementation of the JDBC API that knows how to communicate with a particular database (e.g., MySQL Driver, PostgreSQL Driver).

### Steps to Connect to a Database

The classic workflow for a JDBC operation involves these steps:

1. **Load the Driver**: In modern JDBC (4.0+), this is usually automatic as long as the driver's JAR is on the classpath.
2. **Get a Connection**: Use `DriverManager.getConnection()` with the database URL, username, and password.
3. **Create a Statement**: Obtain a `Statement` or `PreparedStatement` object from the `Connection`.
4. **Execute the Query**: Run the SQL query using methods like `executeQuery()` (for `SELECT`) or `executeUpdate()` (for `INSERT`, `UPDATE`, `DELETE`).
5. **Process the `ResultSet`**: If it's a `SELECT` query, iterate through the `ResultSet` object to retrieve the data.
6. **Close Resources**: **Crucially**, close the `ResultSet`, `Statement`, and `Connection` in a `finally` block or, preferably, use a `try-with-resources` statement to ensure they are always closed.
```java
// Best practice: using try-with-resources for automatic closing
String url = "jdbc:mysql://localhost:3306/mydatabase";
String user = "user";
String pass = "password";
String sql = "SELECT id, name FROM employees WHERE id = ?";

try (Connection conn = DriverManager.getConnection(url, user, pass);
     PreparedStatement ps = conn.prepareStatement(sql)) {

    ps.setInt(1, 101); // Set the parameter for the '?'
    try (ResultSet rs = ps.executeQuery()) {
        if (rs.next()) {
            String name = rs.getString("name");
            System.out.println("Employee Name: " + name);
        }
    }
} catch (SQLException e) {
    e.printStackTrace();
}
```


### Statement vs. PreparedStatement vs. CallableStatement

This is a critical distinction for performance and security.


| Type | `Statement` | `PreparedStatement` | `CallableStatement` |
| :-- | :-- | :-- | :-- |
| **SQL Type** | Static SQL statements. | Parameterized SQL statements. | Stored Procedures. |
| **Compilation** | Compiled by the database every time it's executed. | **Pre-compiled** and cached by the database, leading to better performance for repeated execution. | Pre-compiled. |
| **Security** | **Vulnerable to SQL Injection** if used with string concatenation. | **Prevents SQL Injection** by design. | Prevents SQL Injection. |
| **Usage** | `conn.createStatement()` | `conn.prepareStatement("... WHERE id = ?")` | `conn.prepareCall("{call my_procedure(?) }")` |
| **Best Practice** | Avoid for dynamic queries. Only for truly static SQL. | **Always prefer `PreparedStatement`** for dynamic queries. | Use when you need to execute stored procedures. |

### SQL Injection Awareness

* **Common Pitfall**: Building queries by concatenating user input. This is a massive security vulnerability.
    * **Vulnerable Code**: `String sql = "SELECT * FROM users WHERE username = '" + userInput + "'";`
    * If a user enters `' OR '1'='1`, the query becomes `SELECT * FROM users WHERE username = '' OR '1'='1'`, which returns all users.
* **Solution**: Always use `PreparedStatement` with `?` placeholders. The driver correctly escapes the input, treating it as data, not as executable SQL.


### Batch Processing

To improve performance, you can send multiple SQL statements to the database in a single "batch." This reduces network round-trips.

```java
conn.setAutoCommit(false); // Recommended for batch operations
try (PreparedStatement ps = conn.prepareStatement("INSERT INTO products VALUES (?, ?)")) {
    ps.setString(1, "Laptop");
    ps.setDouble(2, 1200.00);
    ps.addBatch(); // Add statement to the batch

    ps.setString(1, "Mouse");
    ps.setDouble(2, 25.00);
    ps.addBatch();

    int[] updateCounts = ps.executeBatch(); // Execute all statements in the batch
    conn.commit(); // Commit the transaction
}
```


### Transactions and Rollback

A transaction is a sequence of operations performed as a single logical unit of work. They follow ACID properties.

* By default, JDBC is in `auto-commit` mode (each statement is its own transaction).
* **Best Practice**: For multi-step operations, disable auto-commit to manage the transaction manually.
    * `connection.setAutoCommit(false);`
    * If all steps succeed, call `connection.commit();`
    * If any step fails, call `connection.rollback();` in a `catch` block.


### Connection Pooling

* **Problem**: Establishing a database connection is a very slow and resource-intensive operation.
* **Solution**: A **Connection Pool** is a cache of database connections maintained so that they can be reused. When an application needs a connection, it borrows one from the pool. When it's done, it "closes" it, which actually just returns it to the pool.
* **Best Practice**: In any real-world application, **always use a connection pool**. Popular implementations include **HikariCP** (default in Spring Boot 2+), c3p0, and Apache DBCP.


### ORM vs. JDBC

* **JDBC**: Provides low-level control, requires writing SQL manually, and involves boilerplate code to map `ResultSet` data to Java objects.
* **ORM (Object-Relational Mapping)**: Frameworks like Hibernate/JPA provide a high-level abstraction. They map Java objects directly to database tables, generate SQL automatically, and manage sessions. This reduces boilerplate but can hide performance issues if not used carefully.

***

## Generics

Introduced in Java 5, generics provide compile-time type safety by allowing you to create classes, interfaces, and methods that operate on types as parameters.

* **Problem Solved**: Generics prevent `ClassCastException` at runtime by catching type mismatches at compile time.
* **Analogy**: Think of a non-generic `ArrayList` as a general-purpose cardboard box. You can put anything in it—books, apples, tools. But when you take something out, you have to inspect it to figure out what it is and be careful not to mistake an apple for a book. A generic `ArrayList<String>` is like a box clearly labeled "Strings Only." The compiler ensures only strings go in, so you can be confident that whatever you take out is a string, no inspection (`cast`) needed.


### Generic Classes and Interfaces

You can create your own classes and interfaces that are parameterized with a type.

```java
// A generic Box class that can hold any type T
public class Box<T> {
    private T content;

    public void set(T content) {
        this.content = content;
    }

    public T get() {
        return content;
    }
}

// Usage
Box<Integer> integerBox = new Box<>();
integerBox.set(10);
int num = integerBox.get(); // No cast needed

Box<String> stringBox = new Box<>();
stringBox.set("Hello");
// integerBox.set("World"); // Compile-time error!
```


### Generic Methods

You can also have methods with their own type parameters, independent of the class's type parameters.

```java
public class Util {
    // A generic method to print array elements
    public static <E> void printArray(E[] inputArray) {
        for (E element : inputArray) {
            System.out.printf("%s ", element);
        }
        System.out.println();
    }
}

// Usage
Integer[] intArray = { 1, 2, 3 };
String[] stringArray = { "A", "B", "C" };
Util.printArray(intArray);
Util.printArray(stringArray);
```


### Bounded Type Parameters

Sometimes you want to restrict the types that can be used as arguments. This is done using an **upper bound** with the `extends` keyword.

```java
// This Box can only hold types that are subtypes of Number (e.g., Integer, Double)
public class NumberBox<T extends Number> {
    private T number;

    public double doubleValue() {
        return number.doubleValue(); // We can call Number methods because T is a Number
    }
    // ...
}
```


### Wildcards (`?`)

Wildcards represent an unknown type and are used to increase the flexibility of methods that accept generic types as parameters.


| Wildcard Type | Syntax | Description |
| :-- | :-- | :-- |
| **Unbounded Wildcard** | `List<?>` | Represents a list of an unknown type. You can read from it (`Object`), but you cannot safely write to it (except `null`). |
| **Upper Bounded Wildcard** | `List<? extends Type>` | Represents a list of `Type` or any of its subtypes. **Covariant**. |
| **Lower Bounded Wildcard** | `List<? super Type>` | Represents a list of `Type` or any of its supertypes. **Contravariant**. |

### PECS: Producer Extends, Consumer Super

This is a fundamental mnemonic for deciding whether to use `extends` or `super`.

* **"Producer `extends`"**: If a generic structure is a **producer** (you only read items *from* it), use `? extends T`.
    * **Example**: You have a `List<? extends Number>`. You can safely get a `Number` from it because whatever the unknown type is, it's guaranteed to be a `Number`. But you can't add an `Integer` because the list might be a `List<Double>`.
* **"Consumer `super`"**: If a generic structure is a **consumer** (you only write items *to* it), use `? super T`.
    * **Example**: You have a `List<? super Integer>`. You can safely add an `Integer` to it because the list holds either `Integer`, `Number`, or `Object`. But when you read from it, you can only be sure you're getting an `Object`.

**The canonical example is copying a list:**

```java
public static <T> void copy(List<? extends T> src, List<? super T> dest) {
    // 'src' is a producer, so we use 'extends'.
    // 'dest' is a consumer, so we use 'super'.
    for (T item : src) {
        dest.add(item);
    }
}
```


### Type Erasure

* **How it Works**: To maintain backward compatibility, the Java compiler implements generics through a process called **type erasure**.

1. It replaces all generic type parameters with their bounds, or with `Object` if they are unbounded. So `List<String>` becomes `List`, and `T extends Number` becomes `Number`.
2. It inserts type casts where necessary to maintain type safety.
* **Consequence**: Generic type information is not available at runtime.
* **Analogy**: Type erasure is like using a stencil to paint a letter. You use the stencil (`<String>`) to ensure you paint a perfect "S". After you're done, you remove the stencil. The "S" is there (the code is type-safe), but the information about the stencil itself (`<String>`) is gone at runtime.


### Limitations of Generics

Due to type erasure, generics have some limitations:

* **Cannot use primitive types**: You must use wrapper classes (e.g., `List<Integer>`, not `List<int>`).
* **Cannot create instances of a type parameter**: You can't do `new T()`.
* **Cannot create arrays of a generic type**: `T[] array = new T;` is illegal. The runtime would not know what type of array to create.
* **Cannot declare static fields of a type parameter**: A static field is shared by all instances, so it cannot be specific to a type `T`.
* **Cannot use `instanceof` with a parameterized type**: `if (myList instanceof ArrayList<String>)` is not allowed because `String` is erased at runtime. You can only do `if (myList instanceof ArrayList)`.

***

## Serialization \& Deserialization

Serialization is the process of converting a Java object's state into a byte stream. Deserialization is the reverse process: rebuilding the object from that byte stream. This is used for persisting objects to disk, sending them over a network, or storing them in a database.

* **Analogy**: Serialization is like carefully disassembling a complex Lego model, putting all the pieces and the instruction manual into a box (the byte stream). Deserialization is when someone else receives the box and uses the instructions to perfectly reassemble the model.


### `Serializable` vs. `Externalizable`

To be serializable, a class must implement either the `Serializable` or `Externalizable` interface.


| Feature | `Serializable` | `Externalizable` |
| :-- | :-- | :-- |
| **Type** | A marker interface (no methods to implement). | An interface with two methods: `writeExternal()` and `readExternal()`. |
| **Control** | The JVM handles the entire process automatically (default serialization). | You have **full manual control** over what is written and how it's read. |
| **Implementation** | Very easy. Just add `implements Serializable`. | Requires you to implement the logic for reading/writing every field. |
| **Constructor** | The constructor is **not** called during deserialization. | A **`public` no-arg constructor** is required and is called during deserialization before `readExternal()` is invoked. |
| **`transient` keyword** | Obeys the `transient` keyword to skip fields. | The `transient` keyword is ignored; it's up to you what you write in `writeExternal()`. |
| **Use Case** | Simple, quick serialization where default behavior is sufficient. | When you need a specific format, performance optimization, or want to handle the serialization of non-serializable fields manually. |

### Custom Serialization with `writeObject()` and `readObject()`

Even when using `Serializable`, you can hook into the process to add custom logic by providing these special private methods. This is useful for encrypting fields, handling fields that aren't serializable, or adding versioning logic.

```java
class User implements Serializable {
    private String username;
    private transient String password; // Don't serialize the raw password

    private void writeObject(ObjectOutputStream oos) throws IOException {
        oos.defaultWriteObject(); // Performs default serialization first
        // Manually encrypt and write the password
        oos.writeObject(encrypt(this.password));
    }

    private void readObject(ObjectInputStream ois) throws IOException, ClassNotFoundException {
        ois.defaultReadObject(); // Performs default deserialization first
        // Manually read and decrypt the password
        this.password = decrypt((String) ois.readObject());
    }
    // ... encrypt/decrypt methods
}
```


### `serialVersionUID`

* This is a version control ID for a serializable class. It's a `private static final long`.
* During deserialization, the JVM checks if the `serialVersionUID` of the class on the receiving end matches the `serialVersionUID` from the serialized object. If they don't match, an `InvalidClassException` is thrown.
* **Best Practice**: **Always explicitly declare `serialVersionUID`**. If you don't, the compiler will generate one based on the class structure. Any minor change to the class (like adding a field) can cause the generated ID to change, breaking deserialization compatibility.


### `transient` Keyword and `static` Fields

* **`transient`**: An instance variable marked as `transient` will be **skipped** during default serialization. Its value will be `null` or the default for its type (e.g., `0`, `false`) after deserialization.
    * **Analogy**: Marking a field `transient` is like putting a "Do Not Pack" sticker on an item when moving house.
* **`static`**: Static fields belong to the class, not the object instance. Therefore, they are **never serialized**.


### Security Vulnerabilities in Deserialization

* **Critical Security Pitfall**: Deserialization of untrusted data is one of the most dangerous vulnerabilities in Java (often in the OWASP Top 10).
* **The Danger**: If an attacker can control the byte stream being deserialized, they can potentially craft a malicious object. When this object is deserialized, its `readObject()` method (or methods of objects it contains, known as a "gadget chain") can execute arbitrary code on the server, leading to a full system compromise.
* **Best Practice**:

1. **Never deserialize untrusted data.**
2. If you must, use a look-ahead deserialization pattern to validate the classes in the stream before they are instantiated.
3. **Prefer safer, explicit formats like JSON over native Java serialization** for communication with external clients.


### `readResolve()` and `writeReplace()`

These methods provide powerful hooks to replace the object being serialized or deserialized.

* `writeReplace()`: If this method exists, it is called during serialization. The object it returns will be serialized **instead of** the original object.
* `readResolve()`: If this method exists, it is called after deserialization. The object it returns will be the final object returned to the caller, **replacing** the newly created deserialized object.
* **Primary Use Case**: Enforcing singletons. The `readResolve()` method can discard the newly created instance and return the single, static instance of the class.


### Serialization Proxy Pattern

This is an advanced but highly recommended pattern for creating robust and secure serializable classes.

1. The main class is **not** `Serializable`.
2. You create a `private static` nested class (the "proxy") that **is** `Serializable`. This proxy class has fields to store the state of the outer class.
3. The outer class implements a `writeReplace()` method that returns a new instance of the proxy.
4. The proxy class implements a `readResolve()` method that uses the proxy's state to create and return a new instance of the outer class.

* **Benefits**: This decouples the serialized form from the class's implementation, making it much easier to maintain and evolve the class without breaking serialization compatibility. It also provides a single point of control (`readResolve`) to validate data during deserialization, improving security.

***

## Java APIs \& Utilities

This section covers a collection of fundamental classes from the standard library that are used in virtually every Java application.

### `java.lang`: Core Language Classes

This package is automatically imported into every Java source file.

#### `String`, `StringBuilder`, and `StringBuffer`

This is a classic and critical topic. All are used for handling character strings.


| Feature | `String` | `StringBuilder` | `StringBuffer` |
| :-- | :-- | :-- | :-- |
| **Mutability** | **Immutable**. Any modification creates a new object. | **Mutable**. Can be modified in place. | **Mutable**. |
| **Thread Safety** | Inherently thread-safe due to immutability. | **Not thread-safe**. | **Thread-safe**. Methods are `synchronized`. |
| **Performance** | Slower for frequent modifications due to object creation. | **Fastest** for string manipulation in a single thread. | Slower than `StringBuilder` due to synchronization overhead. |
| **Best Use Case** | When a string value will not change. Default choice for strings. | When you need to build or modify a string in a single-threaded environment (e.g., in a loop). | In multi-threaded environments where a shared string needs to be modified (rare). |

* **Common Pitfall**: Using the `+` operator to concatenate strings inside a loop.
    * `String result = ""; for (String s : list) { result += s; }`
    * This creates a new `String` object in every iteration, which is very inefficient. The modern JDK often optimizes this to use `StringBuilder` behind the scenes, but explicitly using `StringBuilder` is clearer and guaranteed to be performant.


#### Wrapper Classes \& Autoboxing

* As covered in Core Fundamentals, these classes (`Integer`, `Double`, `Boolean`, etc.) wrap primitive types into objects.
* **Autoboxing/Unboxing**: The automatic conversion between primitives and their wrapper types.
* **Key Use Cases**: Required for generics (`List<Integer>`) and to represent nullable values (`Integer` can be `null`, `int` cannot).


### `java.util`: The Utility Package

This package contains the collections framework and other useful utility classes.

#### `Objects`

A utility class introduced in Java 7 with `static` helper methods for operating on objects.

* **Best Practices**: Prefer these methods over manual checks.
* `Objects.requireNonNull(obj, "Message")`: Checks if an object is `null` and throws a `NullPointerException` with a custom message if it is. Excellent for validating parameters in constructors and methods.
* `Objects.equals(a, b)`: Compares two objects for equality in a null-safe way.
* `Objects.hash(values...)`: A convenient way to generate a hash code from multiple fields, useful for implementing `hashCode()`.
* `Objects.isNull(obj)`, `Objects.nonNull(obj)`: Clear, readable null checks.


#### `Arrays`

A utility class for common operations on arrays.

* `Arrays.sort(array)`: Sorts an array.
* `Arrays.binarySearch(array, key)`: Searches a sorted array.
* `Arrays.equals(arr1, arr2)`: Checks if two arrays are equal (content-wise).
* `Arrays.toString(array)`: Returns a string representation of an array's contents.
* `Arrays.asList(elements...)`: Returns a fixed-size `List` backed by an array.
    * **Common Pitfall**: The list returned by `Arrays.asList` is **not** a `java.util.ArrayList`. You cannot add or remove elements from it.
* `Arrays.stream(array)`: Creates a `Stream` from an array (Java 8+).


#### `Collections`

A utility class for operations on collections (covered in the Collections section). Provides sorting, searching, shuffling, and wrapper methods (`synchronized`, `unmodifiable`).

### Other Useful Utilities

* **`UUID`**: `UUID.randomUUID()` generates a unique 128-bit value, commonly used for generating unique IDs for database records, transactions, etc.
* **`Random` and `SecureRandom`**:
    * `Random`: Generates pseudo-random numbers. Fast but not suitable for security purposes.
    * `SecureRandom`: A cryptographically strong random number generator. Slower, but essential for security-sensitive applications like generating session tokens, salts, or cryptographic keys.
* **Regex (`java.util.regex`)**:
    * **`Pattern`**: Represents a compiled regular expression. Compiling a pattern is expensive, so it's best to create it once and reuse it.
    * **`Matcher`**: The engine that performs matching operations on a character sequence by interpreting a `Pattern`.


### `java.math`: For High-Precision Arithmetic

* **`BigDecimal`**: For arbitrary-precision signed decimal numbers.
    * **Crucial Best Practice**: **Never use `float` or `double` for financial calculations** due to floating-point inaccuracies. Always use `BigDecimal`.
    * **Common Pitfall**: Creating a `BigDecimal` from a `double` using the constructor (`new BigDecimal(0.1)`) can be inaccurate. Use the `String` constructor (`new BigDecimal("0.1")`) or the static factory method (`BigDecimal.valueOf(0.1)`) for predictable results.
* **`BigInteger`**: For arbitrary-precision integers, representing numbers larger than `Long.MAX_VALUE`.


### Formatting and Internationalization

* **`Formatter`**: Provides C-style `printf()` formatting capabilities.
* **`Locale`**: Represents a specific geographical, political, or cultural region. Used to tailor formatted output (like dates, currencies, and numbers) to the user's conventions.
* **`NumberFormat`, `DecimalFormat`, `DateTimeFormatter`**: Classes used for converting numbers and dates to and from locale-sensitive string representations.
