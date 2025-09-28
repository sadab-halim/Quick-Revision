# Object Oriented Programming

<details>
  <summary>01: Fundamentals</summary>

### Java Basics

Java is a class-based, object-oriented language. Understanding the distinction between primitive types (like `int`, `char`, `boolean`) which hold values, and reference types (like objects, arrays, strings) which hold memory addresses, is crucial for grasping OOP concepts. In OOP, we primarily work with reference types, which are instances of classes.

### What is OOP?

Object-Oriented Programming (OOP) is a programming paradigm based on the concept of "objects," which can contain data in the form of attributes (or fields) and code in the form of methods. The primary goal of OOP is to model real-world entities into software components, making code more modular, reusable, and easier to maintain.

* **Real-world Analogy:** Think of building with LEGO blocks. Each block is an object with its own properties (color, size) and potential connections (behavior). You combine these blocks to build a complex structure, just as you combine objects to build a software application.
* The main pillars of OOP are **Encapsulation**, **Inheritance**, **Polymorphism**, and **Abstraction**.


### Classes and Objects (IMP)

This is the most fundamental concept and a very common interview question.

* A **Class** is a blueprint or template for creating objects. It defines a set of attributes and methods that the created objects will have.
* An **Object** is an instance of a class. It is a concrete entity that has its own state (values for its attributes) and behavior (its methods).

| Concept | Analogy: Car Design | Real-World Example: Banking System |
| :-- | :-- | :-- |
| **Class** | The blueprint for a `Car`, defining that it will have a color, model, and engine. | The `BankAccount` class defining attributes like `accountNumber`, `balance` and methods like `deposit()`, `withdraw()`. |
| **Object** | A specific red Toyota Camry with VIN \#123. | A specific account object for John Doe with `accountNumber` "98765" and `balance` of \$5000. |

```java
// Class (Blueprint)
class Dog {
    // Attributes
    String breed;
    String name;

    // Method
    void bark() {
        System.out.println("Woof!");
    }
}

// Creating Objects (Instances)
Dog myDog = new Dog(); // myDog is an object of the Dog class
myDog.name = "Buddy";
```

* **Best Practice:** Class names should always be in **PascalCase** (e.g., `MyClass`).
* **Common Pitfall:** Confusing a class with an object. A class does not occupy memory for its data members until an object is created.


### Attributes and Methods

* **Attributes (Fields/Properties):** These are variables defined within a class that represent the state of an object. Each object of the class has its own copy of these attributes.
* **Methods (Functions/Behaviors):** These are functions defined within a class that operate on the object's data (attributes) and define its behavior.

```java
class Student {
    // Attributes
    int studentId;
    String name;

    // Method
    void displayDetails() {
        System.out.println("ID: " + studentId + ", Name: " + name);
    }
}
```

* **Best Practice:** Method names and variable names should be in **camelCase** (e.g., `myVariable`, `doSomething()`).


### Constructors (IMP)

A constructor is a special type of method that is used to initialize an object when it is created. It is called automatically at the time of object creation.

* It must have the same name as the class.
* It does not have a return type, not even `void`.
* If you do not define a constructor, the compiler provides a **default constructor** with no arguments.

```java
class Car {
    String model;

    // Default (No-Arg) Constructor
    public Car() {
        this.model = "Unknown";
    }

    // Parameterized Constructor
    public Car(String model) {
        this.model = model; // 'this' keyword refers to the current object
    }
}

// Usage
Car defaultCar = new Car(); // Calls the no-arg constructor -> model is "Unknown"
Car sportsCar = new Car("Ferrari"); // Calls the parameterized constructor -> model is "Ferrari"
```

* **Constructor Overloading (IMP):** A class can have multiple constructors as long as they have different parameter lists (different number of parameters or different types of parameters). This is a form of polymorphism.
* **Common Pitfall:** Assuming the default constructor is always available. If you define *any* parameterized constructor, the compiler will *not* provide a default constructor automatically. You must define it yourself if needed.
* **Language-Specific Note:** In C++, classes also have **destructors** (`~ClassName()`) for cleanup. In Python, the constructor is named `__init__()`. Java handles memory deallocation automatically via the Garbage Collector, so it does not have destructors.


</details>

---

<details>
  <summary>2: Core Principles of OOPs</summary>

### Encapsulation (IMP)

Encapsulation is the mechanism of bundling the data (attributes) and the code that operates on the data (methods) into a single unit, known as a class. It restricts direct access to an object's components, which is a key aspect of **data hiding**.[^3_1][^3_2][^3_3][^3_4]

* **Real-world Analogy:** Think of a capsule for medicine. The outer casing (the class) holds the various chemical ingredients (the data) together. You don't interact with the chemicals directly; you use the capsule as intended.
* **How to achieve it:**

1. Declare the class variables (attributes) as `private`.
2. Provide public `setter` and `getter` methods to access and modify the values of these private variables.[^3_2]


#### Advantages

* **Control:** You have precise control over the data. For example, a setter method can include validation logic.
* **Security:** It protects the object from unwanted access and modification from outside the class.[^3_2]
* **Maintainability:** The internal implementation can be changed without affecting outside code that uses the class's public methods.


#### Real-World Example: Banking System

A `BankAccount` class encapsulates the `balance`. The balance can only be changed through `deposit()` and `withdraw()` methods, not by directly setting it to a new value.

```java
public class BankAccount {
    private double balance; // Data is hidden

    // Public getter to view the balance
    public double getBalance() {
        return balance;
    }

    // Public setter (deposit method) to modify the balance
    public void deposit(double amount) {
        if (amount > 0) {
            this.balance += amount;
        }
    }
}
```


### Access Modifiers (IMP)

Access modifiers are keywords that set the accessibility or scope of a class, constructor, variable, method, or data member. They are crucial for implementing encapsulation.[^3_3][^3_5]


| Modifier | Class | Package | Subclass (Same Pkg) | Subclass (Diff Pkg) | World |
| :-- | :-- | :-- | :-- | :-- | :-- |
| **`public`** | Yes | Yes | Yes | Yes | Yes |
| **`protected`** | Yes | Yes | Yes | Yes | No |
| **`default`** | Yes | Yes | Yes | No | No |
| **`private`** | Yes | No | No | No | No |

* **`public`**: Accessible from everywhere.[^3_6]
* **`protected`**: Accessible within the same package and by subclasses in other packages.
* **`default` (no keyword)**: Accessible only within the same package.[^3_5]
* **`private`**: Accessible only within the same class.[^3_5]

**Best Practice:** Always keep attributes `private` and expose them only when necessary through `public` getters and setters. This is a core principle of robust design.

### Inheritance (IMP)

Inheritance is a mechanism where a new class (subclass or child class) derives attributes and methods from an existing class (superclass or parent class). It represents an **IS-A relationship** (e.g., a `Car` IS-A `Vehicle`).[^3_7]

* **Purpose:** The primary purpose is **code reusability**.[^3_3][^3_7]
* **Keyword:** In Java, inheritance is implemented using the `extends` keyword.


#### Example

```java
// Superclass
class Vehicle {
    void startEngine() {
        System.out.println("Engine started.");
    }
}

// Subclass
class Car extends Vehicle {
    void drive() {
        System.out.println("Car is driving.");
    }
}

// Usage
Car myCar = new Car();
myCar.startEngine(); // Inherited from Vehicle
myCar.drive();       // Own method
```


#### Types of Inheritance

* **Single Inheritance:** One class extends another class. (Supported by Java)
* **Multilevel Inheritance:** A class extends a class, which in turn extends another class (`C` -> `B` -> `A`). (Supported by Java)
* **Hierarchical Inheritance:** Multiple classes extend a single superclass. (Supported by Java)
* **Multiple Inheritance (IMP):** A class inheriting from more than one superclass. **Java does not support multiple inheritance with classes** to avoid the "Diamond Problem" (ambiguity when two parent classes have a method with the same name). It is achieved using interfaces.
* **Hybrid Inheritance:** A combination of two or more types of inheritance.

**Common Pitfall:** Inheritance leads to tight coupling between the superclass and subclass. Changes in the superclass can have unintended consequences for all subclasses.[^3_3]

### Polymorphism (IMP)

Polymorphism, meaning "many forms," is the ability of an object to take on many forms. In OOP, it allows a single action (like a method call) to be performed in different ways depending on the object it is being called on.[^3_8]

* **Real-world Analogy:** Your phone's "volume up" button. On the home screen, it increases ringer volume. In a music app, it increases media volume. In a call, it increases call volume. Same button, different behaviors based on the context.

There are two types of polymorphism in Java :[^3_8]

#### 1. Compile-Time Polymorphism (Static Binding)

Also known as **Method Overloading**. It is resolved at compile time.

* **Rule:** A class can have multiple methods with the **same name** but with **different parameters** (either different number, different type, or different order of parameters).

```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}

// Usage
Calculator calc = new Calculator();
calc.add(10, 20);      // Calls the first method
calc.add(10.5, 20.5);  // Calls the second method
```


#### 2. Runtime Polymorphism (Dynamic Binding)

Also known as **Method Overriding**. It is resolved at runtime.

* **Rule:** A subclass provides a specific implementation for a method that is already defined in its superclass. The method signature (name and parameters) must be the same.
* This is achieved through inheritance.[^3_8]

```java
class Shape {
    void draw() {
        System.out.println("Drawing a shape.");
    }
}

class Circle extends Shape {
    @Override // Annotation to indicate overriding
    void draw() {
        System.out.println("Drawing a circle.");
    }
}

class Square extends Shape {
    @Override
    void draw() {
        System.out.println("Drawing a square.");
    }
}

// Usage
Shape myShape = new Circle(); // Parent reference, child object
myShape.draw(); // Calls the Circle's draw() method at runtime. Output: "Drawing a circle."
```


</details>

---

<details>
  <summary>03: Relationships, and Object Behaviour</summary>

### Association, Aggregation, and Composition (IMP)

These three concepts describe the **HAS-A relationship** between objects. Understanding the difference is a common interview topic, as it demonstrates a deeper understanding of object modeling.

* **Real-world Analogy:** Think of a car. A car **has-a** driver (Association). It **has-a** music player (Aggregation). It **has-an** engine (Composition).

| Relationship | Description | Ownership | Lifespan of Part | Example |
| :-- | :-- | :-- | :-- | :-- |
| **Association** | A general "uses-a" or "has-a" relationship. Objects are independent. | No ownership. | Independent lifecycles. | A `Doctor` and a `Patient`. They are associated, but can exist independently. |
| **Aggregation** | A "has-a" relationship where one object (the whole) contains other objects (the parts), but the parts can exist independently. | Weak ownership. | Independent lifecycles. | A `Department` has `Professor`s. If the department closes, the professors still exist. |
| **Composition** | A strong "has-a" relationship. The part cannot exist without the whole. The whole object is responsible for creating and destroying its parts. | Strong ownership. | Part's lifecycle depends on the whole's. | A `House` has `Room`s. If the house is demolished, the rooms cease to exist. |

#### Code Examples

* **Association:** `Doctor` and `Patient` objects are created separately and then linked.

```java
class Patient { /* ... */ }
class Doctor {
    void assignPatient(Patient p) { /* ... */ }
}
```

* **Aggregation:** The `Department` holds references to `Professor` objects that are created outside of it.

```java
class Professor { /* ... */ }
class Department {
    private List<Professor> professors;
    // The list is populated with existing Professor objects
}
```

* **Composition (IMP):** The `House` creates its `Room` objects internally. When the `House` object is destroyed, the `Room` objects are also destroyed (by the Garbage Collector, as they are no longer reachable).

```java

class Room { /* ... */ }
class House {
    private Room livingRoom;
    public House() {
        // The House creates and "owns" the Room object
        this.livingRoom = new Room();
    }
}
```


**Best Practice:** Prefer Composition over Inheritance (often phrased as "Favor Composition over Inheritance"). Inheritance creates a rigid, tightly-coupled relationship (IS-A), whereas composition provides more flexibility (HAS-A).

### Object Cloning

Object cloning is the process of creating an exact copy of an object. The copy will have the same state as the original object. In Java, this is achieved by using the `clone()` method of the `Object` class.

To make a class cloneable, it must implement the `Cloneable` marker interface and override the `Object.clone()` method.

* **Marker Interface:** The `Cloneable` interface is a marker interface, meaning it has no methods. It just tells the JVM that objects of this class are permitted to be cloned.


#### Types of Cloning (IMP)

1. **Shallow Copy:** This is the default behavior of `clone()`. It creates a new instance and copies the values of all fields. If a field is a primitive type, its value is copied. If a field is a reference type (an object), the **reference is copied**, not the object it points to. Both the original and the clone will point to the same referenced object.
  * **Pitfall:** Modifying the referenced object through the cloned object will also affect the original object, which can lead to unexpected side effects.
2. **Deep Copy:** A deep copy creates a new instance and also creates copies of all objects that the original object refers to. The original and the clone are fully independent.
  * **How to achieve it:** You must manually override the `clone()` method to recursively clone all referenced objects.

#### Code Example

```java
class Address implements Cloneable {
    String city;
    public Address(String city) { this.city = city; }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}

class Employee implements Cloneable {
    String name;
    Address address; // Reference type

    public Employee(String name, Address address) {
        this.name = name;
        this.address = address;
    }

    // Shallow Copy implementation
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }

    /*
    // Deep Copy implementation
    @Override
    protected Object clone() throws CloneNotSupportedException {
        Employee cloned = (Employee) super.clone();
        cloned.address = (Address) this.address.clone(); // Manually clone the Address object
        return cloned;
    }
    */
}

// Usage
Address addr = new Address("New York");
Employee original = new Employee("John", addr);
Employee cloned = (Employee) original.clone();

cloned.address.city = "London"; // In a shallow copy, this changes the city for 'original' as well.
                                // In a deep copy, it does not.
```

</details>

---

<details>
  <summary>04: Advanced Programming in OOPs</summary>

### Abstraction (IMP)

Abstraction is the concept of hiding complex implementation details and showing only the essential features of the object. It helps in managing complexity by focusing on the "what" an object does, rather than the "how" it does it.

* **Real-world Analogy:** Driving a car. You know that pressing the accelerator makes the car go faster, but you don't need to know the complex mechanics of the engine, fuel injection, and transmission. The car's interface (pedals, steering wheel) is an abstraction.
* In Java, abstraction is primarily achieved using **Abstract Classes** and **Interfaces**.

| Abstraction | Encapsulation |
| :-- | :-- |
| **Focus:** Hides complexity at the design level. | **Focus:** Hides data at the implementation level. |
| **How:** Using abstract classes and interfaces. | **How:** Using access modifiers (`private`, `protected`). |
| **Purpose:** To provide a general structure or contract. | **Purpose:** To protect the internal state of an object. |

### Abstract Classes and Methods

An **abstract class** is a class that cannot be instantiated on its own and must be subclassed. It can contain both abstract methods (methods without a body) and concrete methods (methods with a body).

* Use the `abstract` keyword to declare a class or method as abstract.
* If a class has at least one abstract method, the class itself must be declared abstract.
* Any subclass of an abstract class must either implement all of its parent's abstract methods or be declared abstract itself.

```java
// Abstract Class
abstract class Shape {
    String color;

    // Concrete method
    public String getColor() {
        return color;
    }

    // Abstract method (no implementation)
    abstract double getArea();
}

// Concrete subclass
class Circle extends Shape {
    double radius;

    @Override
    double getArea() { // Provides implementation for the abstract method
        return Math.PI * radius * radius;
    }
}
```


### Interfaces (IMP)

An interface is a completely abstract "class" that is used to group related methods with empty bodies. It's a contract that a class can promise to adhere to.

* **Before Java 8:** Interfaces could only have abstract methods and `public static final` constants.
* **Java 8 onwards:** Interfaces can now also have `default` and `static` methods with implementations.

| Abstract Class | Interface |
| :-- | :-- |
| Can have both abstract and concrete methods. | Can have abstract methods. From Java 8+, can have `default` and `static` methods. |
| Supports single inheritance (a class can extend only one abstract class). | Supports multiple inheritance (a class can implement multiple interfaces). |
| Can have instance variables (`non-final`). | Can only have `public static final` constants. |
| **Use when:** You want to provide a common base with some default implementation. (IS-A relationship with shared state/behavior). | **Use when:** You want to define a contract for behavior that different classes can implement. (Defines a capability, e.g., `Runnable`, `Comparable`). |

### Static Keyword (IMP)

The `static` keyword is used for memory management. It indicates that a particular member (variable or method) belongs to the **class itself**, rather than to an **instance** (object) of the class.

* **Static Variable (Class Variable):** There is only one copy of a static variable, shared among all objects of the class.
  * **Use Case:** A counter for the number of objects created (`studentCount` in a `Student` class).
* **Static Method:** Can be called without creating an instance of the class.
  * **Restriction:** A static method cannot use non-static members (instance variables or methods) directly and cannot use the `this` keyword, because it is not associated with any specific object.
  * **Use Case:** Utility methods, like `Math.max()`.
* **Static Block:** A block of code that is executed once, when the class is first loaded into memory.
* **Static Nested Class:** A nested class that is declared `static`. It does not have access to the instance members of the outer class.


### Exception Handling (IMP)

Exception handling is a mechanism to handle runtime errors in a way that maintains the normal flow of the application.[^5_1]

* **Exception Hierarchy:** In Java, all exceptions are objects that inherit from the `Throwable` class. The main branches are `Error` (serious problems that applications shouldn't try to catch, like `OutOfMemoryError`) and `Exception` (conditions that applications might want to catch).[^5_1]
* **Checked vs. Unchecked Exceptions:**
  * **Checked Exceptions:** Exceptions that are checked at compile-time (e.g., `IOException`, `SQLException`). A method must either handle them with a `try-catch` block or declare them with the `throws` keyword.[^5_4]
  * **Unchecked Exceptions (Runtime Exceptions):** Exceptions that are not checked at compile-time (e.g., `NullPointerException`, `ArrayIndexOutOfBoundsException`). You are not required to handle or declare them, but it's good practice to avoid them through defensive coding.


#### Keywords

* **`try`**: The block of code to be monitored for exceptions.[^5_2]
* **`catch`**: Catches and handles the exception thrown by the `try` block.[^5_2]
* **`finally`**: This block is **always** executed, whether an exception is thrown or not. It's used for cleanup code (e.g., closing a file or a database connection).[^5_4]
* **`throw`**: Used to manually throw an exception.[^5_4]
* **`throws`**: Used in a method signature to declare the exceptions that the method might throw but does not handle itself.[^5_4]

```java
public void readFile(String fileName) throws IOException { // Declares that it might throw IOException
    FileReader reader = null;
    try {
        reader = new FileReader(fileName);
        // ... code to read file ...
    } catch (FileNotFoundException e) {
        // Handle a specific exception
        System.err.println("File not found: " + e.getMessage());
    } finally {
        // Cleanup code
        if (reader != null) {
            reader.close(); // This itself can throw an IOException
        }
    }
}
```

* **Try-with-Resources (Java 7+):** A cleaner way to handle resources that must be closed. The resource is automatically closed after the `try` block finishes.

```java
try (FileReader reader = new FileReader("file.txt")) {
    // ... code to read file ...
} catch (IOException e) {
    // ... handle exception ...
}
// 'reader' is automatically closed here.
```


### Other Topics

* **Inner Classes:** A class defined within another class. They can access all members (including private) of the outer class. Useful for logical grouping and increased encapsulation.
* **Generics (`<>`):** Provide compile-time type safety by allowing you to create classes, interfaces, and methods that operate on types as parameters. This avoids the need for explicit casting and prevents `ClassCastException` at runtime.
* **File Handling:** In an OOP context, file operations are often encapsulated within classes. For example, a `FileParser` class might handle reading and writing, using streams (`FileInputStream`, `FileOutputStream`) and readers/writers (`FileReader`, `BufferedWriter`).


</details>

---

<details>
  <summary>05: OOP Design & Lifecycle Management</summary>

### Design Principles (IMP)

While OOP provides the tools, design principles guide how to use them effectively. **SOLID** is a famous mnemonic for five of the most important principles.

* **S - Single Responsibility Principle (SRP):**
  * **Concept:** A class should have only one reason to change, meaning it should have only one job or responsibility.
  * **Real-world Example:** In a library system, a `Book` class should only hold data about the book (title, author). It should not be responsible for saving the book to a database or printing it. Those are separate responsibilities for a `BookRepository` or `BookPrinter` class.
* **O - Open/Closed Principle (OCP):**
  * **Concept:** Software entities (classes, modules) should be open for extension, but closed for modification.
  * **How:** Use abstraction (abstract classes, interfaces) and polymorphism. Instead of changing existing code, you create a new subclass or implementation to add new functionality.
  * **Real-world Example:** A `DiscountCalculator` class can calculate discounts. To add a new discount type (e.g., "Christmas Discount"), you shouldn't modify the `DiscountCalculator`. Instead, you create a new class `ChristmasDiscount` that implements a `Discount` interface, and the calculator can use it without any changes to its own code.
* **L - Liskov Substitution Principle (LSP):**
  * **Concept:** Objects of a superclass should be replaceable with objects of its subclasses without breaking the application. Essentially, a subclass must be a true substitute for its superclass.
  * **Classic Violation:** The "Rectangle-Square" problem. If a `Square` class inherits from a `Rectangle` class and you set its width, its height must also change to maintain the square's properties. This violates the behavior of a `Rectangle` (where width and height can change independently), making it a poor substitute.
* **I - Interface Segregation Principle (ISP):**
  * **Concept:** No client should be forced to depend on methods it does not use. It's better to have many small, specific interfaces than one large, general-purpose one.
  * **Real-world Example:** Don't create a single `Worker` interface with methods like `work()`, `eat()`, and `sleep()`. A `Robot` might implement `work()` but not the other two. It's better to have separate `Workable`, `Eatable`, and `Sleepable` interfaces.
* **D - Dependency Inversion Principle (DIP):**
  * **Concept:** High-level modules should not depend on low-level modules. Both should depend on abstractions (interfaces).
  * **How:** This is the core idea behind **Dependency Injection (DI)**. Instead of a class creating its own dependencies (e.g., `new DatabaseConnection()`), the dependencies are "injected" from an external source (e.g., passed into the constructor).
  * **Real-world Example:** A `NotificationService` (high-level) shouldn't depend directly on an `EmailSender` (low-level). Both should depend on a `MessageSender` interface. This allows you to easily switch from sending emails to sending SMS messages just by injecting a different implementation of the interface.


### Design Patterns (IMP)

Design patterns are reusable, proven solutions to commonly occurring problems in software design. They are not specific algorithms, but high-level recipes for structuring your code. They are typically categorized into three groups :[^6_6]

#### 1. Creational Patterns

These patterns deal with object creation mechanisms, trying to create objects in a manner suitable to the situation.

* **Singleton (IMP):** Ensures a class has only one instance and provides a global point of access to it. **Use Case:** Logging services, database connection pools, configuration managers.
* **Factory Method:** Defines an interface for creating an object, but lets subclasses decide which class to instantiate. **Use Case:** When a class cannot anticipate the class of objects it must create.
* **Builder:** Separates the construction of a complex object from its representation, so the same construction process can create different representations. **Use Case:** Building a complex `User` object with many optional fields.


#### 2. Structural Patterns

These patterns focus on how classes and objects are composed to form larger structures.

* **Adapter:** Allows objects with incompatible interfaces to work together. **Use Case:** Making a new third-party library work with an existing system without changing the system's code.
* **Decorator:** Adds new responsibilities to an object dynamically without altering its class. **Use Case:** Adding features like scrolling or a border to a window object.
* **Facade:** Provides a simplified, unified interface to a complex subsystem. **Use Case:** A single `OrderFulfillment` facade that simplifies interactions with inventory, billing, and shipping systems.[^6_6]


#### 3. Behavioral Patterns

These patterns are concerned with communication between objects.

* **Observer (IMP):** Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically. **Use Case:** Implementing "listeners" in user interfaces, where multiple UI elements need to update when data changes.
* **Strategy:** Defines a family of algorithms, encapsulates each one, and makes them interchangeable. **Use Case:** Allowing a user to choose between different sorting algorithms (`SortByPrice`, `SortByRating`) at runtime.
* **Template Method:** Defines the skeleton of an algorithm in a superclass but lets subclasses override specific steps of the algorithm without changing its structure. **Use Case:** A `DataParser` template method could define the steps `readData() -> processData() -> writeData()`, while subclasses implement the specifics for parsing XML vs. JSON.


### Object Lifecycle

The lifecycle of an object refers to the sequence of states an object goes through from its creation to its destruction.

1. **Creation:** An object is created using the `new` keyword, which allocates memory on the heap for the object. The appropriate constructor is then called to initialize its state.
2. **In Use (Reachable):** The object is in use as long as there is at least one active reference pointing to it. During this phase, its methods can be called and its state can be modified.
3. **Unreachable/Destruction:** An object becomes eligible for **Garbage Collection (GC)** when there are no more references pointing to it.
  * **Garbage Collection (IMP):** This is the automatic process in Java that reclaims memory occupied by unreachable objects. Developers do not need to manually deallocate memory, which prevents common errors like memory leaks.
  * **`finalize()` method:** This method is called by the garbage collector just before an object is destroyed. **Best Practice:** Avoid using `finalize()`. It is unreliable (you can't know when or even if it will be called) and has been deprecated since Java 9. Use `try-with-resources` or `finally` blocks for resource cleanup instead.


</details>

---