# Creational

<details>
  <summary>01 : Singleton</summary>

### Definition
Restricts the instantiation of a class to a single object. This is useful when exactly one object is needed to coordinate actions across the system.

### Intent / Purpose
A class has only one instance and to provide a single, global point of access to that instance.

### Problem
The Singleton pattern solves two problems at the same time, violating the **Single Responsibility Principle**:
1. Ensure that a class has just a single instance
2. Provide a global access point to that instance

### Solution
- Make the default constructor private, to prevent other objects
  from using the `new` operator with the Singleton class.
- Create a static creation method that acts as a constructor.
  Under the hood, this method calls the private constructor to create an object and saves it in a static field. All following calls to this method return the cached object

### Key Characteristics
- Single Instance
- Global Access
- Controlled Lifecycle

### UML Representation
```
+---------------------------+
|         Singleton         |
+---------------------------+
|   -instance: Singleton    |  <-- private static instance
+---------------------------+
| -Singleton()              |  <-- private constructor
| +getInstance(): Singleton |  <-- public static method
+---------------------------+
              ^
              |
              | .getInstance()
              |
          +--------+
          | Client |
          +--------+
```

### Real-World Analogy
**Central Government of a Country**: A country can have only one official government at a time. Regardless of where you are in the country, when you refer to "the government," you are referring to that single, unique entity. It serves as a global point of access for governance, law-making, and administration.

### Java Implementation

#### Basic Lazy Initialization

This approach creates the instance only when the `getInstance()` method is called for the first time. It is **NOT thread-safe**.

```java
public class LazySingleton {
    // The single instance, not initialized until first use.
    private static LazySingleton instance;

    // Private constructor to prevent instantiation from outside.
    private LazySingleton() {}

    // Public static method to get the instance.
    public static LazySingleton getInstance() {
        // Create the instance if it doesn't exist yet.
        if (instance == null) {
            instance = new LazySingleton();
        }
        return instance;
    }
}
```

#### Thread-Safe Synchronized Version

This version adds the `synchronized` keyword to the `getInstance()` method to make it **thread-safe**. However, _synchronization adds performance overhead_.

```java
public class ThreadSafeSingleton {
    private static ThreadSafeSingleton instance;

    private ThreadSafeSingleton() {}

    // The synchronized keyword ensures only one thread can execute this method at a time.
    public static synchronized ThreadSafeSingleton getInstance() {
        if (instance == null) {
            instance = new ThreadSafeSingleton();
        }
        return instance;
    }
}
```

#### Double-Checked Locking

This method _reduces the performance overhead of synchronization_ by **locking** only when the instance is null. The `volatile` keyword is crucial to prevent memory visibility issues.

```java
public class DoubleCheckedLockingSingleton {
    // 'volatile' ensures that multiple threads handle the instance variable correctly.
    private static volatile DoubleCheckedLockingSingleton instance;

    private DoubleCheckedLockingSingleton() {}

    public static DoubleCheckedLockingSingleton getInstance() {
        // First check (not synchronized) to avoid locking every time.
        if (instance == null) {
            // Synchronize on the class object.
            synchronized (DoubleCheckedLockingSingleton.class) {
                // Second check (synchronized) to ensure instance is created only once.
                if (instance == null) {
                    instance = new DoubleCheckedLockingSingleton();
                }
            }
        }
        return instance;
    }
}
```

#### Bill Pugh Inner Static Helper Class

This is a _widely recommended approach_ for its simplicity and **thread-safety** _without explicit synchronization_. The JVM handles the locking during class loading.

```java
public class BillPughSingleton {
    private BillPughSingleton() {}

    // A private static inner class to hold the singleton instance.
    // It's not loaded into memory until getInstance() is called.
    private static class SingletonHelper {
        private static final BillPughSingleton INSTANCE = new BillPughSingleton();
    }

    public static BillPughSingleton getInstance() {
        return SingletonHelper.INSTANCE;
    }
}
```

#### Enum-Based Singleton

Considered the most robust and simplest way to implement a Singleton in Java. It provides implicit thread safety and serialization guarantees.

```java
public enum EnumSingleton {
    // A single enum element defines the singleton instance.
    INSTANCE;

    // You can add methods to the enum as needed.
    public void doSomething() {
        // Business logic here.
    }
}
```

### Common Use Cases
- Logging
- Configuration Management
- Connection Pools
- Caching

### Advantages \& Benefits
- Controlled Access
- Resource Sharing
- Namespace Clarity

### Disadvantages \& Pitfalls
- Violates **Single Responsibility Principle** (SRP)
- Difficult to Test
- Hidden Dependencies
- Inflexibility

### Thread-Safety \& Concurrency Considerations
- Synchronization
- Volatile Keyword
- Memory Model

### Performance Implications
- Synchronization Overhead
- Optimization
- Eager vs Lazy

### Testing \& Mocking Strategies
- Refactor to Dependency Injection
- Wrapper Class
- Reflection

### Refactoring Alternatives
- Dependency Injection (DI)
- Factory Pattern
- Monostate Pattern

### Anti-Patterns \& Warnings
- Overuse
- Global State
- Hidden Coupling

</details>

---

<details>
    <summary>02 : Factory</summary>

### Definition
Factory Design Pattern encapsulates object instantiation logic, promoting loose coupling by separating the client from the concrete implementation of the objects it needs.

### Intent and Purpose
Solve the problem of creating objects without specifying the exact class of the object that will be created.

### Core Idea
Delegate the responsibility of object instantiation from the client to a dedicated "factory" method or class.

### Problem

### Solution

### Structure

### Real-World Analogy

Consider a car factory. When a customer orders a car, they don't build it themselves. They go to the dealership (the client) and specify a model (e.g., "Sedan" or "SUV"). The dealership sends this order to the factory (the `Creator`). The factory has different assembly lines (`ConcreteCreator` implementations), one for sedans and one for SUVs. Based on the order, the correct assembly line is used to produce the requested car (`ConcreteProduct`). The customer receives the final car without ever needing to know the complex details of its construction.

### When to Use It
- When a class cannot anticipate the class of objects it must create.
- When a class wants its subclasses to specify the objects it creates.
- When you want to provide users of your library or framework a way to extend its internal components.

### Variants \& Implementations in Java
There are three main variations, each solving the problem at a different level of abstraction.

#### Simple Factory (Static Factory Method)

This is not a "true" Gang of Four design pattern but a common programming idiom. It involves a single class with a method (often static) that creates and returns different types of objects based on an input parameter.

```java
// Product Interface
interface Notification {
    void notifyUser();
}

// Concrete Products
class EmailNotification implements Notification {
    @Override
    public void notifyUser() {
        System.out.println("Sending an Email notification");
    }
}

class SMSNotification implements Notification {
    @Override
    public void notifyUser() {
        System.out.println("Sending an SMS notification");
    }
}

// The Simple Factory
class NotificationFactory {
    // Factory method to create objects based on type
    public static Notification createNotification(String type) {
        if ("SMS".equalsIgnoreCase(type)) {
            return new SMSNotification();
        } else if ("EMAIL".equalsIgnoreCase(type)) {
            return new EmailNotification();
        }
        throw new IllegalArgumentException("Unknown notification type: " + type);
    }
}

// Client Code
class NotificationService {
    public static void main(String[] args) {
        Notification notification = NotificationFactory.createNotification("SMS");
        notification.notifyUser();
    }
}
```

#### Factory Method Pattern

This is the canonical Factory pattern. It uses inheritance and relies on a subclass to handle the instantiation of the desired concrete class. The superclass contains business logic that works with a generic product, while the `create` method is abstract.

```java
// Product Interface
interface Document {
    void open();
}

// Concrete Products
class WordDocument implements Document {
    @Override
    public void open() {
        System.out.println("Opening Word document...");
    }
}

class PdfDocument implements Document {
    @Override
    public void open() {
        System.out.println("Opening PDF document...");
    }
}

// Abstract Creator (The "Factory")
abstract class Application {
    // The factory method is abstract, forcing subclasses to implement it.
    public abstract Document createDocument();

    public void newDocument() {
        // The creator's business logic doesn't know the concrete product type.
        Document doc = createDocument();
        doc.open();
    }
}

// Concrete Creators
class WordApplication extends Application {
    @Override
    public Document createDocument() {
        // The subclass decides which concrete product to create.
        return new WordDocument();
    }
}

class PdfApplication extends Application {
    @Override
    public Document createDocument() {
        return new PdfDocument();
    }
}

// Client Code
class Client {
    public static void main(String[] args) {
        // Depending on configuration or environment, create a specific application.
        Application app = new WordApplication();
        app.newDocument(); // Uses the factory method to create a WordDocument.

        Application pdfApp = new PdfApplication();
        pdfApp.newDocument(); // Uses the factory method to create a PdfDocument.
    }
}
```

#### Abstract Factory Pattern

The Abstract Factory pattern provides an interface for creating *families* of related or dependent objects without specifying their concrete classes. It is a "factory of factories." While the Factory Method produces one product, the Abstract Factory produces a whole set of products.

```java
// Abstract Products for a family (e.g., UI elements for a theme)
interface Button { void paint(); }
interface Checkbox { void paint(); }

// Concrete Products for Theme 1 (e.g., Windows)
class WinButton implements Button { 
    public void paint() { 
        System.out.println("Painting a Windows button."); 
    } 
}

class WinCheckbox implements Checkbox { 
    public void paint() { 
        System.out.println("Painting a Windows checkbox."); 
    } 
}

// Concrete Products for Theme 2 (e.g., macOS)
class MacButton implements Button { 
    public void paint() { 
        System.out.println("Painting a macOS button."); 
    } 
}

class MacCheckbox implements Checkbox { 
    public void paint() { 
        System.out.println("Painting a macOS checkbox."); 
    } 
}

// The Abstract Factory interface
interface GUIFactory {
    Button createButton();
    Checkbox createCheckbox();
}

// Concrete Factories for each family
class WinFactory implements GUIFactory {
    public Button createButton() { return new WinButton(); }
    public Checkbox createCheckbox() { return new WinCheckbox(); }
}

class MacFactory implements GUIFactory {
    public Button createButton() { return new MacButton(); }
    public Checkbox createCheckbox() { return new MacCheckbox(); }
}

// Client Code
class ApplicationRunner {
    private final Button button;
    private final Checkbox checkbox;

    public ApplicationRunner(GUIFactory factory) {
        button = factory.createButton();
        checkbox = factory.createCheckbox();
    }

    public void run() {
        button.paint();
        checkbox.paint();
    }

    public static void main(String[] args) {
        // The client code can be configured with a specific factory
        // to change the entire look and feel of the application.
        GUIFactory factory = new MacFactory();
        ApplicationRunner app = new ApplicationRunner(factory);
        app.run();
    }
}
```

### Common Use Cases
- Logging Frameworks
- Database Connection
- GUI Components
- Parsers

### Advantages and Benefits
- Encapsulation of Creation Logic
- Decoupling
- Scalability

### Disadvantages and Pitfalls
- Over-abstraction
- Class Explosion
- Testing Difficulty

### Design Principles Applied
- Single Responsibility Principle (SRP)
- Open/Closed Principle (OCP)
- Dependency Inversion Principle (DIP)

</details>

---

<details>
    <summary>03: Abstract Factory</summary>

### Definition
Abstract Factory is a design pattern that defines an interface for creating a set of related products, but lets subclasses decide which concrete classes to instantiate.

### Intent / Purpose
Isolate a client from the concrete implementation details of a set of objects it needs to create. It solves the problem of creating different "families" of related objects, where the client code should not depend on which specific family is being used.

### Core Idea
The core idea is to abstract the creation of objects. Instead of the client instantiating concrete classes directly using `new`, it calls creation methods on an abstract factory object. This factory is responsible for creating a family of related objects. 

### UML Representation (ASCII)
```
+----------+       uses        +-------------------+
|  Client  |------------------>|  AbstractFactory  |
+----------+                   |-------------------|
                               | +createProductA() |
                               | +createProductB() |
                               +---------^---------+
                                         |
                 +-----------------------+---------------------+
                 |                                             |
+-----------------------+                       +-----------------------+
|   ConcreteFactory1    |                       |    ConcreteFactory2   |
|-----------------------|                       |-----------------------|
| +createProductA(): A1 |                       | +createProductA(): A2 |
| +createProductB(): B1 |                       | +createProductB(): B2 |
+-----------------------+                       +-----------------------+
       |       |                                     |       |
       | creates products                            | creates products
       |                                             |
+------v------+   +------v------+            +------v------+   +------v------+
|  ProductA1  |   |  ProductB1  |            |  ProductA2  |   |  ProductB2  |
+------^------+   +------^------+            +------^------+   +------^------+
       |               |                            |               |
       | implements    | implements                 | implements    | implements
       |               |                            |               |
+------------------+ +------------------+    +------------------+ +------------------+
| AbstractProductA | | AbstractProductB |    | AbstractProductA | | AbstractProductB |
+------------------+ +------------------+    +------------------+ +------------------+

```

### Real-World Analogy
A good analogy is a factory for manufacturing UI components for different operating systems like macOS and Windows.

* **AbstractFactory**: `GUIFactory` interface with methods like `createButton()` and `createCheckbox()`.
* **AbstractProduct**: `Button` and `Checkbox` interfaces.
* **ConcreteFactory**: `WindowsFactory` and `MacOSFactory` classes that implement `GUIFactory`.
* **ConcreteProduct**: `WindowsButton`, `WindowsCheckbox`, `MacOSButton`, and `MacOSCheckbox` classes.

### Java Implementation

This example implements the UI toolkit analogy.

```java
// === 1. Abstract Product Interfaces ===

// AbstractProductA
interface Button {
    void paint();
}

// AbstractProductB
interface Checkbox {
    void paint();
}

// === 2. Concrete Product Implementations ===

// ConcreteProductA1
class WindowsButton implements Button {
    @Override
    public void paint() {
        System.out.println("Rendering a button in Windows style.");
    }
}

// ConcreteProductB1
class WindowsCheckbox implements Checkbox {
    @Override
    public void paint() {
        System.out.println("Rendering a checkbox in Windows style.");
    }
}

// ConcreteProductA2
class MacOSButton implements Button {
    @Override
    public void paint() {
        System.out.println("Rendering a button in macOS style.");
    }
}

// ConcreteProductB2
class MacOSCheckbox implements Checkbox {
    @Override
    public void paint() {
        System.out.println("Rendering a checkbox in macOS style.");
    }
}

// === 3. Abstract Factory Interface ===

interface GUIFactory {
    Button createButton();
    Checkbox createCheckbox();
}

// === 4. Concrete Factory Implementations ===

// ConcreteFactory1
class WindowsFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new WindowsButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new WindowsCheckbox();
    }
}

// ConcreteFactory2
class MacOSFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new MacOSButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new MacOSCheckbox();
    }
}

// === 5. Client Code ===

// The client code works with factories and products only through abstract types.
class Application {
    private Button button;
    private Checkbox checkbox;

    public Application(GUIFactory factory) {
        button = factory.createButton();
        checkbox = factory.createCheckbox();
    }

    public void paintUI() {
        button.paint();
        checkbox.paint();
    }
}

// === 6. Demo: Configuring and Running the Application ===

public class ApplicationRunner {
    private static Application configureApplication() {
        GUIFactory factory;
        String osName = System.getProperty("os.name").toLowerCase();
        if (osName.contains("mac")) {
            factory = new MacOSFactory();
        } else {
            factory = new WindowsFactory();
        }
        return new Application(factory);
    }

    public static void main(String[] args) {
        // The application is configured at runtime based on the OS.
        Application app = configureApplication();
        app.paintUI();
    }
}
```

### Advantages / Benefits
- Isolates Concrete Classes
- Promotes Consistency
- Easy to Exchange Product Families
- Improved Scalability

### Disadvantages / Pitfalls
- Difficult to Add New Product Types
- Increased Complexity

### Design Principles Involved
- Dependency Inversion Principle (DIP)
- Open / Closed Principle (OCP)
- Encapsulation

</details>

---