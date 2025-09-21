# JUnit

## Fundamentals

This guide covers the fundamentals of unit testing, including its core concepts, types, and setup. It explains the "what" and "why" of unit testing before diving into the specifics of JUnit.

### What is a Unit Test?

A unit test is a piece of code written to verify the behavior of a small, isolated piece of your application, known as a "unit." The goal is to test that the unit works as expected in isolation, without depending on external systems like databases, networks, or other parts of the application.

* **Analogy:** Think of testing a single Lego brick to ensure it has the right shape and size before using it to build a complex model.


### Unit vs. Integration vs. Functional Tests

Understanding the distinction between different test types is crucial for building a robust testing strategy.


| Test Type | Scope | Speed \& Cost | Analogy |
| :-- | :-- | :-- | :-- |
| **Unit Test** | A single class or method in isolation. | Very Fast / Low Cost | Testing the engine of a car by itself. |
| **Integration Test** | Two or more units interacting together (e.g., service to repository). | Slow / Medium Cost | Testing if the engine, transmission, and wheels work together. |
| **Functional/E2E Test** | The entire application flow from a user's perspective (e.g., UI to database). | Very Slow / High Cost | A test driver taking the fully assembled car for a drive. |

### The Test Pyramid

The Test Pyramid is a model that guides how to balance different types of tests in your application. It recommends having a large base of fast unit tests, a smaller layer of integration tests, and a very small number of slow end-to-end tests at the top.

* **Base (Unit Tests):** Forms the strong foundation. They are fast, reliable, and pinpoint failures accurately.
* **Middle (Integration Tests):** Ensures that different components collaborate correctly.
* **Top (End-to-End Tests):** Verifies the entire system flow but is slow and brittle. A failure here could be due to an issue in any underlying component.


### The AAA Pattern (Arrange–Act–Assert)

This pattern provides a clear structure for writing tests, making them readable and maintainable.

* **Arrange:** Set up the test. This involves creating objects, preparing inputs, and configuring mocks.
* **Act:** Execute the method being tested with the arranged parameters.
* **Assert:** Verify that the outcome of the action is what you expected.

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}

class CalculatorTest {
    @Test
    void testAddition() {
        // Arrange: Create the calculator instance and define inputs
        Calculator calculator = new Calculator();
        int a = 5;
        int b = 10;

        // Act: Call the method to be tested
        int result = calculator.add(a, b);

        // Assert: Check if the result is the expected value
        assertEquals(15, result, "5 + 10 should equal 15");
    }
}
```


### Setting Up JUnit

JUnit 5 requires the `junit-jupiter` dependency. This is different from JUnit 4, which used a single `junit` dependency.

### Maven

Add the following to your `pom.xml`. The `maven-surefire-plugin` is essential for running tests during the Maven build lifecycle.

```xml
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.10.2</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-engine</artifactId>
        <version>5.10.2</version>
        <scope>test</scope>
    </dependency>
</dependencies>

<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>3.2.5</version>
        </plugin>
    </plugins>
</build>
```


### Gradle

Add the following to your `build.gradle` file. The `testImplementation` configuration ensures JUnit is only available for tests.

```groovy
dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter-api:5.10.2'
    testRuntimeOnly 'org.junit.jupiter:junit-jupiter-engine:5.10.2'
}

test {
    useJUnitPlatform()
}
```


### IDE Integration

Modern IDEs like IntelliJ IDEA, Eclipse, and VS Code have excellent built-in support for JUnit.

* They automatically detect test classes and methods annotated with `@Test`.
* You can run tests directly from the editor using a "play" button next to the class or method.
* Test results are displayed in a dedicated panel, showing which tests passed or failed with detailed stack traces.
* **Best Practice:** Leverage your IDE's features to run single tests or entire test suites quickly, which speeds up the development feedback loop.

***

Would you like to continue with Section 2: JUnit Basics?

---

# yes

This section covers the foundational annotations and assertions that form the backbone of JUnit tests. Understanding the test lifecycle and how to make assertions is the first step toward writing effective tests.

### Test Lifecycle in JUnit

JUnit tests follow a specific execution order controlled by annotations. This lifecycle ensures that tests are run in a predictable and isolated manner.

1. **`@BeforeAll`**: A method annotated with this runs **once** before any tests in the class. It must be `static`. Use it for expensive, shared setup like database connections or starting a server.
2. **`@BeforeEach`**: Runs **before each** `@Test` method. Use it to reset the state and prepare the test environment for each individual test.
3. **`@Test`**: The actual test method.
4. **`@AfterEach`**: Runs **after each** `@Test` method. Use it for cleanup, such as deleting temporary files or releasing resources.
5. **`@AfterAll`**: Runs **once** after all tests in the class have completed. It must also be `static`. Use it to tear down the shared setup from `@BeforeAll`.

### Core Annotations (JUnit 5 vs. JUnit 4)

JUnit 5 (Jupiter) introduced a new set of annotations, which are more clearly named than their JUnit 4 counterparts.


| JUnit 5 | JUnit 4 | Purpose |
| :-- | :-- | :-- |
| `@BeforeAll` | `@BeforeClass` | Executes once before all tests in the class. |
| `@AfterAll` | `@AfterClass` | Executes once after all tests in the class. |
| `@BeforeEach` | `@Before` | Executes before each test method. |
| `@AfterEach` | `@After` | Executes after each test method. |
| `@Test` | `@Test` | Marks a method as a test. |
| `@Disabled` | `@Ignore` | Disables a test method or class. |
| `@DisplayName` | N/A | Provides a custom, human-readable name for tests. |
| `@Tag` | `@Category` | Tags tests for filtering and grouping. |

#### Example of Core Annotations

```java
import org.junit.jupiter.api.*;
import static org.junit.jupiter.api.Assertions.assertTrue;

@DisplayName("A demo test class for core annotations")
class CoreAnnotationsTest {

    @BeforeAll
    static void setupAll() {
        System.out.println("Runs once before all tests...");
    }

    @BeforeEach
    void setup() {
        System.out.println("Runs before each test...");
    }

    @Test
    @DisplayName("✅ A successful test case")
    void firstTest() {
        assertTrue(true);
        System.out.println("Executing the first test...");
    }

    @Test
    @DisplayName("Another test")
    void secondTest() {
        assertTrue(true);
        System.out.println("Executing the second test...");
    }

    @Test
    @Disabled("This test is disabled for demonstration purposes")
    void skippedTest() {
        // This test will not run
    }

    @AfterEach
    void tearDown() {
        System.out.println("Runs after each test...");
    }

    @AfterAll
    static void tearDownAll() {
        System.out.println("Runs once after all tests...");
    }
}
```


### Assertions

Assertions are static methods used to check if a certain condition is met. In JUnit 5, they are located in the `org.junit.jupiter.api.Assertions` class.


| Assertion Method | Description |
| :-- | :-- |
| `assertEquals(expected, actual)` | Fails if the two values are not equal. |
| `assertNotEquals(unexpected, actual)` | Fails if the two values are equal. |
| `assertTrue(condition)` | Fails if the condition is false. |
| `assertFalse(condition)` | Fails if the condition is true. |
| `assertNull(object)` | Fails if the object is not null. |
| `assertNotNull(object)` | Fails if the object is null. |
| `assertSame(expected, actual)` | Fails if the two objects do not refer to the exact same instance. |
| `assertNotSame(unexpected, actual)` | Fails if the two objects refer to the same instance. |

**Best Practice:** Always include a message in your assertions (`assertEquals(expected, actual, "Helpful message here")`). This message is displayed when the test fails, making it much easier to diagnose the problem.

#### `assertThrows` \& `assertDoesNotThrow`

Used to verify that a piece of code either throws a specific exception or doesn't throw one at all.

```java
@Test
@DisplayName("Ensure division by zero throws ArithmeticException")
void testExceptionThrowing() {
    // Arrange
    Calculator calculator = new Calculator();

    // Act & Assert
    assertThrows(ArithmeticException.class, () -> {
        calculator.divide(1, 0);
    }, "Dividing by zero should throw ArithmeticException");
}
```


#### Grouped Assertions with `assertAll`

`assertAll` allows you to group multiple assertions. Unlike individual assertions, which stop at the first failure, `assertAll` runs every assertion in the group and reports all failures together. This is extremely useful for validating multiple properties of an object.

```java
@Test
@DisplayName("Validate multiple properties of a user object")
void groupedAssertions() {
    // Arrange
    User user = new User("testuser", "Test", "User");

    // Act & Assert
    assertAll("user properties",
        () -> assertEquals("testuser", user.getUsername(), "Username should match"),
        () -> assertEquals("Test", user.getFirstName(), "First name should match"),
        () -> assertEquals("User", user.getLastName(), "Last name should match")
    );
}
```


***
Would you like to continue with Section 3: Parameterized \& Repeated Tests?

---

# yes

Of course. This section explores how to run the same test logic with different inputs using parameterized tests and how to repeat tests for stability checks.

### `@ParameterizedTest` for Data-Driven Testing

Parameterized tests allow you to run a single test method multiple times with different arguments. This is a powerful feature for reducing code duplication and testing a wide range of inputs with minimal effort. Instead of writing a separate test for each input, you write one test and provide the data.

To create a parameterized test, you replace the `@Test` annotation with `@ParameterizedTest` and provide a source of arguments using one of the source annotations.

#### `@ValueSource`

The simplest argument source. It provides an array of literal values (shorts, bytes, ints, longs, floats, doubles, chars, booleans, strings, or classes). It can only provide a single argument per invocation.

```java
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.ValueSource;
import static org.junit.jupiter.api.Assertions.assertTrue;

class StringUtils {
    public static boolean isBlank(String input) {
        return input == null || input.trim().isEmpty();
    }
}

class StringUtilsTest {
    @ParameterizedTest
    @ValueSource(strings = {"", "  ", "\t", "\n"})
    void testIsBlankWithBlankStrings(String input) {
        assertTrue(StringUtils.isBlank(input));
    }
}
```


#### `@EnumSource`

Provides enum constants as arguments. You can specify which constants to include or exclude.

```java
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.EnumSource;
import static org.junit.jupiter.api.Assertions.assertNotNull;

enum TimeUnit {
    SECONDS, MINUTES, HOURS
}

class EnumSourceTest {
    @ParameterizedTest
    @EnumSource(TimeUnit.class)
    void testAllTimeUnitsAreNotNull(TimeUnit unit) {
        assertNotNull(unit);
    }
}
```


#### `@CsvSource`

Provides arguments from comma-separated values (CSV) literal strings. Each string represents one invocation, and the values are mapped to the test method's parameters. This is one of the most common sources for providing multiple arguments.

```java
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.CsvSource;
import static org.junit.jupiter.api.Assertions.assertEquals;

class CsvSourceTest {
    @ParameterizedTest
    @CsvSource({
        "5, 5, 10",
        "10, -5, 5",
        "0, 0, 0"
    })
    void testAddition(int a, int b, int expectedResult) {
        Calculator calculator = new Calculator();
        assertEquals(expectedResult, calculator.add(a, b));
    }
}
```


#### `@CsvFileSource`

Similar to `@CsvSource`, but it reads the arguments from a CSV file located in the test resources (`src/test/resources`). This is ideal for separating large test datasets from the test code.

**`src/test/resources/addition-data.csv`:**

```csv
5, 5, 10
10, -5, 5
0, 0, 0
```

**Test Class:**

```java
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.CsvFileSource;
import static org.junit.jupiter.api.Assertions.assertEquals;

class CsvFileSourceTest {
    @ParameterizedTest
    @CsvFileSource(resources = "/addition-data.csv", numLinesToSkip = 0)
    void testAdditionFromFile(int a, int b, int expectedResult) {
        Calculator calculator = new Calculator();
        assertEquals(expectedResult, calculator.add(a, b));
    }
}
```


### Argument Converters

JUnit Jupiter performs automatic type conversion for many common types. For more complex conversions (e.g., a string "dd-MM-yyyy" to a `LocalDate` object), you can create a custom `ArgumentConverter`.

### Custom `ArgumentsProvider`

For scenarios where test data is complex or needs to be generated dynamically, you can create a custom provider by implementing the `ArgumentsProvider` interface. This gives you full programmatic control over the data supplied to your tests.

### `@RepeatedTest` for Stability Checks

A repeated test is run a specified number of times. It's marked with the `@RepeatedTest(n)` annotation. This is particularly useful for uncovering flaky tests or race conditions that might not appear in a single run.

You can access information about the current repetition by injecting a `RepetitionInfo` object into your test method.

```java
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.RepeatedTest;
import org.junit.jupiter.api.RepetitionInfo;
import static org.junit.jupiter.api.Assertions.assertTrue;

class RepeatedTestExample {
    @RepeatedTest(5)
    @DisplayName("Repeated test for stability")
    void stabilityTest(RepetitionInfo repetitionInfo) {
        System.out.println("Executing repetition " + repetitionInfo.getCurrentRepetition() +
                           " of " + repetitionInfo.getTotalRepetitions());
        // A real test would check a non-deterministic or concurrent behavior here
        assertTrue(true);
    }
}
```


***
Would you like to continue with Section 4: Tagging, Filtering \& Conditional Tests?

---

# yes

Of course. This section covers how to organize, filter, and conditionally execute your tests, giving you fine-grained control over which tests run and when.

### `@Tag` and Filtering Test Groups

Tags are used to categorize or group tests. You can apply the **`@Tag`** annotation to a test method or an entire class. This is the JUnit 5 equivalent of JUnit 4's **`@Category`**. Common use cases include tagging tests as "fast", "slow", "smoke", or "regression".

```java
import org.junit.jupiter.api.Tag;
import org.junit.jupiter.api.Test;

@Tag("smoke-tests")
class AuthenticationTest {

    @Test
    @Tag("fast")
    void testSuccessfulLogin() {
        // ... test logic
    }

    @Test
    @Tag("slow")
    @Tag("regression")
    void testLoginWithLargeDataSet() {
        // ... more complex test logic
    }
}
```

Once tagged, you can filter which tests to run using your build tool.

#### Filtering in Maven

You configure the `maven-surefire-plugin` in your `pom.xml` to include or exclude tags.

```xml
<build>
    <plugins>
        <plugin>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>3.2.5</version>
            <configuration>
                <!-- Run only tests tagged with 'fast' or 'smoke-tests' -->
                <groups>fast | smoke-tests</groups>
                <!-- Exclude any tests tagged with 'slow' -->
                <excludedGroups>slow</excludedGroups>
            </configuration>
        </plugin>
    </plugins>
</build>
```


#### Filtering in Gradle

In `build.gradle`, you configure the `test` task.

```groovy
test {
    useJUnitPlatform {
        // Run only tests tagged with 'fast'
        includeTags 'fast'
        
        // Exclude tests tagged with 'slow'
        excludeTags 'slow'
    }
}
```


### Conditional Execution

JUnit 5 provides a powerful set of annotations to enable or disable tests based on specific conditions. This is useful for tests that are only relevant in certain environments.

* **`@EnabledOnOs` / `@DisabledOnOs`**: Execute a test only on specific operating systems.
* **`@EnabledOnJre` / `@DisabledOnJre`**: Execute a test only on specific Java Runtime Environment versions.
* **`@EnabledIf` / `@DisabledIf`**: A generic annotation to enable/disable a test based on the result of a custom condition method.


#### Example: OS and JRE Conditions

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.condition.EnabledOnJre;
import org.junit.jupiter.api.condition.EnabledOnOs;
import org.junit.jupiter.api.condition.JRE;
import org.junit.jupiter.api.condition.OS;

class ConditionalTests {

    @Test
    @EnabledOnOs(OS.WINDOWS)
    void testOnlyOnWindows() {
        // This test runs only on Windows systems
    }

    @Test
    @EnabledOnOs({OS.LINUX, OS.MAC})
    void testOnlyOnLinuxOrMac() {
        // This test runs on Linux or macOS
    }

    @Test
    @EnabledOnJre(JRE.JAVA_17)
    void testOnlyOnJava17() {
        // This test runs only if the JRE is Java 17
    }

    @Test
    @EnabledOnJre(min = JRE.JAVA_11, max = JRE.JAVA_17)
    void testOnJava11To17() {
        // This test runs on any JRE from version 11 to 17
    }
}
```


#### Example: `@EnabledIf` Custom Condition

`@EnabledIf` provides maximum flexibility. You provide the name of a method within the test class that returns `true` or `false`. The method must be `static` if used on a `@BeforeAll` or `@AfterAll` method.

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.condition.EnabledIf;

class EnabledIfTest {

    // Condition method
    boolean isCiEnvironment() {
        return "true".equalsIgnoreCase(System.getenv("CI"));
    }

    @Test
    @EnabledIf("isCiEnvironment")
    void testOnlyOnCiServer() {
        // This test will only run if the environment variable 'CI' is set to 'true'
    }
}
```

**Common Pitfall:** Forgetting to configure your build tool (Maven/Gradle) to recognize tags. The tags in your code do nothing on their own; they must be activated by the test runner configuration.

### Custom Conditions

For more complex or reusable logic, you can create your own condition by implementing the `ExecutionCondition` interface and applying it with `@ExtendWith`. This is an advanced feature for creating highly specific, reusable conditions across your test suite.

***
Would you like to continue with Section 5: Advanced Assertions \& Matchers?

---

# yes

Excellent. This section introduces powerful third-party libraries—AssertJ and Hamcrest—that dramatically improve the readability and expressiveness of your assertions, making tests easier to write and understand.

### Why Use Advanced Assertion Libraries?

While JUnit's built-in assertions (`assertEquals`, `assertTrue`, etc.) are functional, they can sometimes lead to verbose and less intuitive test code. Libraries like AssertJ and Hamcrest offer a more "fluent" and human-readable syntax.


| Feature | Standard JUnit 5 | AssertJ | Hamcrest |
| :-- | :-- | :-- | :-- |
| **Syntax** | `assertEquals(expected, actual)` | `assertThat(actual).isEqualTo(expected)` | `assertThat(actual, is(equalTo(expected)))` |
| **Readability** | Good | Excellent (reads like a sentence) | Very Good (highly descriptive) |
| **Chaining** | No | Yes (e.g., `hasSize(5).contains("x")`) | Limited |
| **Error Messages** | Good | Excellent (very detailed and clear) | Very Good (descriptive failure) |
| **Extensibility** | Limited | Excellent (easy to create custom assertions) | Excellent (easy to create custom matchers) |

### Using AssertJ for Fluent Assertions

AssertJ is the most popular assertion library for Java. Its "fluent" API allows you to chain multiple assertions together, making your tests read like natural language.

**Setup (Maven):**

```xml
<dependency>
    <groupId>org.assertj</groupId>
    <artifactId>assertj-core</artifactId>
    <version>3.25.3</version>
    <scope>test</scope>
</dependency>
```

**Fluent Assertion Examples:**
The entry point is the static method `assertThat()`. Your IDE's autocomplete will then guide you to the available assertions based on the object's type.

```java
import static org.assertj.core.api.Assertions.assertThat;
import org.junit.jupiter.api.Test;
import java.util.List;

class AssertJShowcaseTest {

    @Test
    void testStringAssertions() {
        String name = "Frodo Baggins";
        
        assertThat(name)
            .isNotNull()
            .startsWith("Frodo")
            .contains("Baggins")
            .endsWith("s")
            .doesNotContain("Samwise")
            .hasSize(13);
    }
    
    @Test
    void testListAssertions() {
        List<String> fellowship = List.of("Frodo", "Sam", "Gandalf");
        
        assertThat(fellowship)
            .hasSize(3)
            .contains("Sam", "Frodo")
            .doesNotContain("Sauron")
            .allMatch(s -> s.length() > 2)
            .last().isEqualTo("Gandalf");
    }
}
```


### Using Hamcrest for Matcher-Based Testing

Hamcrest provides a library of "matcher" objects that you can combine to create flexible assertion rules. The syntax follows the pattern `assertThat(actual, is(someMatcher(...)))`. It is the assertion library that JUnit 4 was originally built on.

**Setup (Maven):**

```xml
<dependency>
    <groupId>org.hamcrest</groupId>
    <artifactId>hamcrest</artifactId>
    <version>2.2</version>
    <scope>test</scope>
</dependency>
```

**Matcher Examples:**
Hamcrest's power lies in its composable matchers.

```java
import static org.hamcrest.MatcherAssert.assertThat;
import static org.hamcrest.Matchers.*;
import org.junit.jupiter.api.Test;
import java.util.List;
import java.util.Map;

class HamcrestShowcaseTest {

    @Test
    void testBasicMatchers() {
        String name = "Bilbo";
        assertThat(name, is(equalTo("Bilbo")));
        assertThat(name, not(equalTo("Frodo")));
    }
    
    @Test
    void testCollectionMatchers() {
        List<String> hobbits = List.of("Frodo", "Sam", "Pippin");
        
        assertThat(hobbits, hasSize(3));
        assertThat(hobbits, hasItem("Sam"));
        assertThat(hobbits, containsInAnyOrder("Sam", "Pippin", "Frodo"));
        assertThat(hobbits, not(hasItem("Gollum")));
    }
    
    @Test
    void testObjectMatchers() {
        // Assume a User class with getName() and getAge()
        User user = new User("test", 30);
        
        assertThat(user, allOf(
            hasProperty("name", is("test")),
            hasProperty("age", greaterThan(25))
        ));
    }
}
```


### Soft Assertions (AssertJ)

Normally, a test stops at the first failed assertion. **Soft assertions** allow you to run all assertions and report all failures together at the end. This is similar to JUnit 5's `assertAll`, but with AssertJ's fluent style.

* **Analogy:** Imagine a building inspector checking a house. A standard assertion is like the inspector stopping and filing a report the moment they find the first problem (e.g., a faulty wire). A soft assertion is like the inspector checking the entire house (wiring, plumbing, foundation) and then providing a single, comprehensive report listing all the problems found.

```java
import org.assertj.core.api.SoftAssertions;
import org.junit.jupiter.api.Test;

class SoftAssertionsTest {
    
    @Test
    void testUserPropertiesWithSoftAssertions() {
        User user = new User("gandalf", "Olorin", 1000); // Assume age is wrong
        SoftAssertions soft = new SoftAssertions();
        
        soft.assertThat(user.getUsername()).isEqualTo("gandalf");
        soft.assertThat(user.getRealName()).isEqualTo("Gandalf the Grey"); // This will fail
        soft.assertThat(user.getAge()).isGreaterThan(2000); // This will also fail
        
        // Fails the test here and reports all collected errors
        soft.assertAll(); 
    }
}
```

**Best Practice:**

* For most cases, **AssertJ is the recommended choice** for modern Java projects due to its superior readability and IDE support.
* Use standard JUnit assertions for very simple checks, but switch to AssertJ or Hamcrest as soon as you need more expressive power.
* Use soft assertions when validating multiple independent properties of a single object to get a complete failure report in one go.

***
Would you like to continue with Section 6: Exception \& Timeout Testing?

---

# yes

Certainly. This section focuses on two critical aspects of robust testing: verifying that your code handles errors correctly by throwing exceptions, and ensuring it performs within acceptable time limits.

### Testing for Expected Exceptions

A key part of unit testing is ensuring that your code fails correctly when it receives invalid input or encounters an error state.

#### The JUnit 5 Way: `assertThrows`

The modern and recommended approach is using the `org.junit.jupiter.api.Assertions.assertThrows` method. It asserts that executing a given block of code (provided as a lambda) throws an exception of a specific type.

**Key Advantages:**

* **Precision:** It pinpoints the exact line of code that is expected to throw the exception.
* **Inspection:** It returns the thrown exception instance, allowing you to make further assertions on its properties, like the error message.

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertThrows;

class ExceptionTesting {

    public void processPayment(double amount) {
        if (amount <= 0) {
            throw new IllegalArgumentException("Amount must be positive");
        }
        // ... processing logic
    }

    @Test
    void testProcessPaymentThrowsExceptionForNegativeAmount() {
        // Arrange
        ExceptionTesting service = new ExceptionTesting();
        
        // Act & Assert
        IllegalArgumentException thrownException = assertThrows(
            IllegalArgumentException.class, 
            () -> service.processPayment(-50.0),
            "Expected processPayment to throw, but it didn't"
        );
        
        // Assert on the exception message
        assertEquals("Amount must be positive", thrownException.getMessage());
    }
}
```


#### JUnit 4 vs. JUnit 5 Exception Testing

| Method | JUnit 4 | JUnit 5 | Comments |
| :-- | :-- | :-- | :-- |
| **Simple Check** | `@Test(expected = IOException.class)` | `assertThrows(IOException.class, () -> {})` | The JUnit 4 way is less precise; the test passes if *any* line in the method throws the exception. |
| **Message Check** | `@Rule public ExpectedException thrown = ExpectedException.none();` | `assertThrows(...)` and `assertEquals(...)` | The JUnit 5 approach is cleaner and doesn't require a `@Rule`. |

**Common Pitfall (JUnit 4):** Using `@Test(expected=...)` is a common anti-pattern because it can't verify the exception's message and can produce false positives if the wrong line of code throws the expected exception. **Always prefer `assertThrows` in JUnit 5.**

### Testing with Timeouts

Timeout tests are essential for two reasons:

1. **Performance:** To ensure a method completes within a specific time budget.
2. **Stability:** To prevent tests from hanging indefinitely due to infinite loops or deadlocks.

JUnit 5 provides two assertions for this: `assertTimeout` and `assertTimeoutPreemptively`.

#### `assertTimeout` vs. `assertTimeoutPreemptively`

This is a critical distinction based on how the timeout is handled.

* **`assertTimeout`**: Executes the code in the **same thread**. It waits for the code to complete, and **only then** fails if the duration exceeded the timeout. The code itself is not interrupted.
    * **Analogy:** A stopwatch runner. You start the stopwatch, let the runner finish the race, and then check if their time was under the limit. The runner is never stopped mid-race.
    * **Use Case:** Safe for code that should not be interrupted, like database transactions.
* **`assertTimeoutPreemptively`**: Executes the code in a **different thread**. If the timeout is exceeded, the test fails immediately, and the main test thread stops waiting. The executed code is aborted via a `Thread.interrupt()`.
    * **Analogy:** A referee with an air horn. If the player doesn't complete the task in time, the horn blows, and the game stops right there.
    * **Use Case:** Best for catching infinite loops or truly hung processes.

**Best Practice:** Start with `assertTimeout` as it is safer. Only use `assertTimeoutPreemptively` if you are sure the code being tested is safe to be interrupted and you need to fail fast. Using it on non-thread-safe code can lead to unpredictable side effects.

```java
import org.junit.jupiter.api.Test;
import java.time.Duration;
import static org.junit.jupiter.api.Assertions.assertTimeout;
import static org.junit.jupiter.api.Assertions.assertTimeoutPreemptively;

class TimeoutTest {

    @Test
    void testCompletesWithinTimeout() {
        // This will pass because it completes before the 500ms timeout.
        assertTimeout(Duration.ofMillis(500), () -> {
            Thread.sleep(100); // Simulating work
        });
    }

    @Test
    void testFailsPreemptively() {
        // This test will fail after ~200ms without waiting for the full 500ms sleep to finish.
        assertTimeoutPreemptively(Duration.ofMillis(200), () -> {
            Thread.sleep(500); // This work takes too long
        });
    }
}
```


### Handling Flaky Tests with Timeouts

Flaky tests are tests that sometimes pass and sometimes fail without any code changes. Often, these are caused by timing issues or race conditions. While timeouts don't *fix* the root cause, they can make a flaky test fail consistently and predictably, which is the first step toward diagnosing and fixing it.

***
Would you like to continue with Section 7: Mocking \& Test Doubles?

---

# yes

Of course. This is one of the most critical sections for writing true unit tests. It explains how to isolate the code you are testing from its dependencies using mocks.

### What are Mocks and Test Doubles?

In unit testing, your goal is to test a single unit in **isolation**. However, most classes have dependencies (other classes they interact with). Mocks are "fake" objects that simulate the behavior of these real dependencies, allowing you to control their output and verify interactions.

* **Analogy:** A **mock** is like a **stunt double** in a movie. You're testing the lead actor's dramatic reaction (`UserService`). To do this, you don't need the real, unpredictable co-star (a live `DatabaseConnection`). Instead, you hire a stunt double (`Mock UserRepository`) who is programmed to do exactly what you need—for instance, pretend to fall over when the actor shouts. The mock lets you test your `UserService` logic without needing a real database.

Mockito is the most popular mocking framework for Java. It integrates seamlessly with JUnit.

### Mockito Core Concepts

**Setup (Maven):**

```xml
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <version>5.12.0</version>
    <scope>test</scope>
</dependency>
<!-- For JUnit 5 integration -->
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-junit-jupiter</artifactId>
    <version>5.12.0</version>
    <scope>test</scope>
</dependency>
```


#### Creating Mocks: `@Mock` and `@InjectMocks`

* **`@Mock`**: Creates a mock implementation for a class or interface.
* **`@InjectMocks`**: Creates an instance of the class under test and automatically injects the fields annotated with `@Mock` into it.

To enable these annotations, you need to initialize them in a `@BeforeEach` method.

```java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;

// Dependencies (real classes)
class UserRepository {
    public User findById(String id) { /* interacts with database */ return null; }
}
class EmailService {
    public void sendWelcomeEmail(String email) { /* sends real email */ }
}

// Class under test
class UserService {
    private final UserRepository userRepository;
    private final EmailService emailService;

    public UserService(UserRepository repo, EmailService service) {
        this.userRepository = repo;
        this.emailService = service;
    }

    public User registerUser(String id) {
        User user = userRepository.findById(id);
        if (user != null) {
            emailService.sendWelcomeEmail(user.getEmail());
        }
        return user;
    }
}

// Test class
class UserServiceTest {
    @Mock
    private UserRepository mockUserRepository; // The stunt double for the repository

    @Mock
    private EmailService mockEmailService; // The stunt double for the email service

    @InjectMocks
    private UserService userService; // The real actor whose logic we are testing

    @BeforeEach
    void setUp() {
        // Initializes mocks and injects them into userService
        MockitoAnnotations.openMocks(this);
    }

    @Test
    void testRegisterUser() {
        // Test logic will go here
    }
}
```


### Stubbing Behavior: Telling Mocks What to Do

Stubbing is the process of programming your mock object to return a specific value or perform a specific action when one of its methods is called.

* **`when(...).thenReturn(...)`**: For methods that return a value.

```java
@Test
void testRegisterUser_sendsEmail_whenUserExists() {
    // Arrange: Program the mock's behavior
    User fakeUser = new User("123", "test@example.com");
    when(mockUserRepository.findById("123")).thenReturn(fakeUser);
    
    // Act: Run the method we are testing
    userService.registerUser("123");
    
    // Assert: We will verify this interaction in the next section
}
```

* **`when(...).thenThrow(...)`**: To make a mock method throw an exception.

```java
when(mockUserRepository.findById("invalid-id")).thenThrow(new RuntimeException("Database down"));
```

* **`doNothing()`, `doThrow()` for `void` methods**: Use this syntax when stubbing methods that return `void`.

```java
// Make the mock do nothing when sendWelcomeEmail is called
doNothing().when(mockEmailService).sendWelcomeEmail(anyString());

// Make a void method throw an exception
doThrow(new RuntimeException()).when(mockEmailService).sendWelcomeEmail("fail@example.com");
```


### Verifying Interactions: Checking if Mocks Were Called

Verification is checking *if* and *how* your class under test interacted with its dependencies (the mocks).

* **`verify(...)`**: Checks that a specific method on a mock was called.
* **Argument Matchers (`any()`, `eq()`, etc.)**: Used when you don't know or care about the exact argument value.
    * **Common Pitfall**: If you use an argument matcher for one argument, you **must** use them for all arguments (e.g., `verify(mock).someMethod(eq("known"), anyInt())`).

```java
@Test
void testRegisterUser_sendsEmail_whenUserExists() {
    // Arrange
    User fakeUser = new User("123", "test@example.com");
    when(mockUserRepository.findById("123")).thenReturn(fakeUser);
    
    // Act
    userService.registerUser("123");
    
    // Assert/Verify
    // Verify that findById was called exactly once with the argument "123"
    verify(mockUserRepository, times(1)).findById("123");
    
    // Verify that sendWelcomeEmail was called with the user's email
    verify(mockEmailService).sendWelcomeEmail("test@example.com");

    // Verify no other methods were called on this mock
    verifyNoMoreInteractions(mockEmailService);
}
```

**Common Verification Patterns:**

* `times(n)`: Verify exact number of calls.
* `never()`: Verify method was never called.
* `atLeastOnce()`: Verify it was called one or more times.
* `anyString()`, `anyInt()`, `any(User.class)`: Match any argument of that type.


### Spies vs. Mocks: Partial Mocking

| Feature | Mock (`Mockito.mock()`) | Spy (`Mockito.spy()`) |
| :-- | :-- | :-- |
| **Object Type** | A complete fake/dummy object. | A real object that is "wrapped" to be observed. |
| **Default Behavior** | Does nothing. Returns `null`, `0`, or empty collections. | **Calls the real methods of the object.** |
| **Purpose** | To isolate the class under test from its dependencies. | To partially mock a real object. You can stub *some* methods while letting others execute their real logic. |

* **Analogy for a Spy**: A spy is like the real actor performing most of their own stunts (real methods), but using a stunt double for just one specific, dangerous move (the stubbed method).

```java
@Test
void testSpy() {
    // Arrange
    List<String> realList = new ArrayList<>();
    List<String> spyList = Mockito.spy(realList);

    // Stubbing the spy: Use the doReturn/doAnswer syntax to avoid issues
    doReturn(100).when(spyList).size();

    // Act
    spyList.add("one"); // This calls the REAL add() method on the ArrayList
    spyList.add("two");

    // Assert
    // The stubbed size() method is called
    assertEquals(100, spyList.size());
    // The real add() method was called, so the list contains "one"
    assertTrue(spyList.contains("one"));
}
```

**Best Practice for Spies:** Always use the `doReturn(...).when(spy).methodCall()` syntax for stubbing spies. The alternative, `when(spy.methodCall()).thenReturn(...)`, can accidentally call the real method during the stubbing process, leading to unexpected behavior.

### Mocking `static` and `final` (Mockito-inline)

By default, Mockito cannot mock `static` methods, `final` classes, or `final` methods. Historically, this required a complex library called PowerMock. However, modern Mockito now includes this capability out-of-the-box with the **`mockito-inline`** engine. If you are using `mockito-core` version 2.1.0 or later, it is the default engine.

```java
// Mocking a static method
try (MockedStatic<MyStaticUtils> mocked = Mockito.mockStatic(MyStaticUtils.class)) {
    // Stub the static method call
    mocked.when(MyStaticUtils::getAppName).thenReturn("Mocked App");
    
    // Test your code that uses the static method
    assertEquals("Mocked App", new ClassUnderTest().getAppNameFromUtils());
}
```


***
Would you like to continue with Section 8: Testing in Spring Context?

---

# yes

Of course. Testing Spring applications requires special tools because components (beans) are managed by the Spring Application Context. This section explains how to leverage the `spring-boot-starter-test` module to test your application at different layers.

### `@SpringBootTest` vs. Test Slices (`@WebMvcTest`, `@DataJpaTest`)

Spring Boot provides "test slices" that load only a specific part of the application context, leading to much faster and more focused tests than loading the entire application.

* **Analogy:** Testing a car.
    * **`@SpringBootTest`** is like starting the **entire car**—engine, electronics, transmission, everything—just to check if the radio works. It's a full integration test.
    * **`@WebMvcTest`** is like testing the **dashboard and radio** in isolation, using simulators for the engine and wheels. It only loads the web layer.
    * **`@DataJpaTest`** is like testing the **transmission system** on a dedicated workbench, disconnected from the rest of the car. It only loads the persistence layer.

**Best Practice:** Always use the most specific test slice that fits your needs. Avoid `@SpringBootTest` for unit tests.


| Annotation | Scope | What it Loads | Use Case |
| :-- | :-- | :-- | :-- |
| **`@SpringBootTest`** | Full Application | The entire Spring Application Context. | Full integration tests, testing interactions between all layers. Very slow. |
| **`@WebMvcTest`** | Web Layer | Controllers, Filters, `JsonComponent`s, etc. | Testing controllers, request/response serialization, and validation. It does **not** load services or repositories. |
| **`@DataJpaTest`** | Persistence Layer | JPA Repositories, `EntityManager`. Uses an in-memory database (e.g., H2) by default. | Testing repository methods and custom JPQL queries. |

### Mocking Beans with `@MockBean` and `@SpyBean`

When using test slices, you must provide mock implementations for any beans that are not part of the slice.

* **`@MockBean`**: Replaces a bean in the Application Context with a Mockito mock. This is the Spring-aware equivalent of `@Mock`.
* **`@SpyBean`**: Wraps a real bean from the Application Context with a Mockito spy.

**Common Pitfall:** Forgetting to use `@MockBean` in a slice test. If you use `@WebMvcTest` for a `UserController` that depends on `UserService`, you **must** annotate `UserService` with `@MockBean`, otherwise Spring will fail to start the test context because it cannot find a `UserService` bean.

#### Example: `@WebMvcTest` with `@MockBean`

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.test.web.servlet.MockMvc;
import static org.mockito.Mockito.when;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.jsonPath;

// Assume UserController depends on UserService
@WebMvcTest(UserController.class)
class UserControllerTest {

    @Autowired
    private MockMvc mockMvc; // A utility to simulate HTTP requests

    @MockBean
    private UserService mockUserService; // Mock the service layer dependency

    @Test
    void testGetUserById() throws Exception {
        // Arrange: Stub the mock bean
        User fakeUser = new User("1", "testuser");
        when(mockUserService.findById("1")).thenReturn(fakeUser);

        // Act & Assert
        mockMvc.perform(get("/users/1"))
               .andExpect(status().isOk())
               .andExpect(jsonPath("$.username").value("testuser"));
    }
}
```


### Mocking Configuration and Properties

Tests often need to run with different configuration properties than the main application.

* **`@TestPropertySource`**: A powerful annotation to override properties from `application.properties` for a single test class or hierarchy.
* **`@ActiveProfiles`**: Activates a specific Spring profile (e.g., "test") for a test, causing Spring to load configuration from `application-test.properties`.


#### Example: Overriding Properties for a Test

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.TestPropertySource;
import static org.assertj.core.api.Assertions.assertThat;

@SpringBootTest
// Overrides a property and adds a new one just for this test
@TestPropertySource(properties = {
    "feature.toggle.new-api=true",
    "external.service.url=http://localhost:9090/mock-service"
})
class MyServiceIntegrationTest {

    @Value("${feature.toggle.new-api}")
    private boolean isNewApiEnabled;

    @Test
    void testNewApiFeatureToggle() {
        assertThat(isNewApiEnabled).isTrue();
    }
}
```


### Testing the Data Layer with `@DataJpaTest`

`@DataJpaTest` configures an in-memory database and provides a `TestEntityManager`, a utility specifically for JPA tests to persist and find entities without relying on a full repository.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;
import org.springframework.boot.test.autoconfigure.orm.jpa.TestEntityManager;
import static org.assertj.core.api.Assertions.assertThat;

// Assume a 'Product' entity and 'ProductRepository'
@DataJpaTest
class ProductRepositoryTest {

    @Autowired
    private TestEntityManager entityManager; // Helper to manage entities for tests

    @Autowired
    private ProductRepository productRepository;

    @Test
    void testFindByCategory() {
        // Arrange
        Product electronicsProduct = new Product("Laptop", "Electronics");
        entityManager.persistAndFlush(electronicsProduct); // Save a product using the helper

        // Act
        List<Product> foundProducts = productRepository.findByCategory("Electronics");

        // Assert
        assertThat(foundProducts).hasSize(1)
                                 .first()
                                 .isEqualTo(electronicsProduct);
    }
}
```


***
Would you like to continue with Section 9: Test-Driven Development (TDD)?

---

# yes

Of course. This section explains Test-Driven Development (TDD), a software development methodology that inverts the traditional "code first, test later" approach.

### What is Test-Driven Development (TDD)?

Test-Driven Development is a process where you write a failing unit test **before** you write the production code that makes it pass. This is done in short, iterative cycles, ensuring that every piece of code is covered by a test from the moment it's created.

* **Analogy: Building with a Blueprint First.** TDD is like an architect creating a detailed blueprint (the test) that specifies exactly what a room should look like (e.g., "must have a window 2 meters wide"). Only after the blueprint is complete does the builder start putting up walls and cutting holes (writing code). The blueprint dictates the work, not the other way around.


### The Red-Green-Refactor Cycle

TDD follows a simple, repeatable rhythm:

1. **Red (Write a Failing Test):**
    * Think about a small piece of functionality you want to add.
    * Write a test that defines how that functionality should behave.
    * Run the test. It **must fail** because you haven't written the implementation code yet. If it passes, your test is likely flawed.
2. **Green (Write Code to Pass the Test):**
    * Write the **absolute minimum amount of code** necessary to make the failing test pass.
    * It's okay if the code is simple, "ugly," or inefficient at this stage. The goal is just to get a passing test bar.
    * **Common Practice:** It's even acceptable to hardcode a return value just to make the test pass and move to the next step.
3. **Refactor (Improve the Code):**
    * Now that you have a passing test as a safety net, you can clean up your implementation.
    * Improve the code's design, remove duplication, and enhance clarity without changing its external behavior.
    * Re-run the test to ensure it still passes after your refactoring.

This cycle is repeated for every small feature, building up the application piece by piece with a full suite of tests.

### TDD in Action: A Simple Example

Let's build a `PasswordValidator` that requires a password to be at least 8 characters long.

**Cycle 1: Password must be at least 8 characters.**

1. **Red:** Write a test for a password that is too short.

```java
@Test
void testPasswordIsInvalidIfShorterThan8Chars() {
    PasswordValidator validator = new PasswordValidator();
    assertFalse(validator.isValid("short")); // This will fail to compile
}
```

2. **Green:** Write the simplest code to make it pass.

```java
class PasswordValidator {
    public boolean isValid(String password) {
        return false; // The easiest way to make the test pass
    }
}
```

The test now passes, but the logic is wrong.
3. **Refactor:** Add a test for a *valid* password to force a better implementation.

**Cycle 2: A new test forces a refactor.**

1. **Red:** Add a test for a valid password.

```java
@Test
void testPasswordIsValidIf8CharsOrLonger() {
    PasswordValidator validator = new PasswordValidator();
    assertTrue(validator.isValid("longenough")); // This test will fail
}
```

2. **Green/Refactor:** Now we must write real logic to make *both* tests pass.

```java
class PasswordValidator {
    public boolean isValid(String password) {
        return password != null && password.length() >= 8;
    }
}
```

Now, both tests pass, and the code is correct and clean. The cycle can continue by adding more rules (e.g., must contain a number).

### Benefits \& Pitfalls of TDD

| Benefits | Pitfalls |
| :-- | :-- |
| **Safety Net for Refactoring** | **Steep Learning Curve:** Can feel slow and counter-intuitive at first. |
| **Drives Better Design:** Forces you to think about your code's API and usability from the start. | **Can be Difficult for Some Problems:** Less straightforward for UIs, complex integrations, or legacy code. |
| **Creates Living Documentation:** The tests serve as executable examples of how to use the code. | **Risk of Brittle Tests:** It's easy to accidentally test implementation details, making tests that break during refactoring. |
| **Guarantees High Test Coverage:** Coverage is a natural outcome, not an afterthought. | **Requires Discipline:** There's a temptation to skip steps (especially refactoring) under pressure. |


***
Would you like to continue with Section 10: Coverage \& Quality?

---

# yes

Of course. This section discusses how to measure the effectiveness of your tests using code coverage and how to go beyond basic metrics with mutation testing to ensure high-quality, meaningful tests.

### Test Coverage: What Is It?

Test coverage is a metric that measures the percentage of your production code that is executed by your automated tests. It helps identify which parts of your codebase are not being tested at all.

* **Analogy:** Think of test coverage as a map of a city showing all the streets you have driven down. A 90% coverage report means you've driven down 90% of the streets. It's a useful metric because it clearly shows the 10% of streets you've **never** visited. However, it **doesn't** tell you if you checked for potholes or verified the traffic lights on the streets you *did* visit.

**Common Pitfall:** High coverage does not guarantee high-quality tests. You can have 100% line coverage with tests that have no assertions. Coverage tells you what you've *executed*, not what you've *verified*.

### Test Coverage Tools

#### JaCoCo (Java Code Coverage)

JaCoCo is the standard code coverage tool in the Java ecosystem. It integrates directly with build tools like Maven and Gradle to generate detailed reports during your build process. The reports are typically generated in HTML, showing line-by-line and branch-by-branch coverage.

#### IntelliJ Built-in Coverage Runner

Most IDEs, like IntelliJ IDEA, have a built-in coverage runner. When you run tests with coverage enabled, it highlights lines in your source code with colors:

* **Green:** The line was fully executed by tests.
* **Yellow:** The line was partially executed (e.g., in an `if` statement, only one branch was taken).
* **Red:** The line was never executed by any test.

This is extremely useful for quick, local feedback while developing.

### Enforcing Minimum Coverage in Builds

You can configure your build to fail if test coverage drops below a certain threshold. This acts as a quality gate, preventing code with insufficient test coverage from being merged. A common and pragmatic target is **80% line coverage**.

#### Maven (with `jacoco-maven-plugin`)

In your `pom.xml`, configure the `check` goal.

```xml
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <version>0.8.12</version>
    <executions>
        <execution>
            <id>check</id>
            <goals>
                <goal>prepare-agent</goal>
                <goal>report</goal>
                <goal>check</goal>
            </goals>
            <configuration>
                <rules>
                    <rule>
                        <element>CLASS</element>
                        <limits>
                            <limit>
                                <counter>LINE</counter>
                                <value>COVERAGE</value>
                                <minimum>0.80</minimum> <!-- Fails build if line coverage is less than 80% -->
                            </limit>
                        </limits>
                    </rule>
                </rules>
            </configuration>
        </execution>
    </executions>
</plugin>
```


#### Gradle (with `jacoco` plugin)

In your `build.gradle`, configure the `jacocoTestCoverageVerification` task.

```groovy
jacocoTestCoverageVerification {
    violationRules {
        rule {
            element = 'CLASS'
            limit {
                counter = 'LINE'
                value = 'COVERAGE'
                minimum = 0.80 // Fails build if line coverage is less than 80%
            }
        }
    }
}
// Make the check run as part of the main build
check.dependsOn jacocoTestCoverageVerification
```


### Beyond Coverage: Mutation Testing with PIT

Since high coverage doesn't guarantee good tests, how do you measure test *quality*? The answer is **mutation testing**.

* **Analogy:** Mutation testing is like hiring a saboteur to check your security system. The saboteur (the tool) sneaks into your code and introduces small bugs ("mutations"), like changing `a > b` to `a >= b`, or `a + 1` to `a - 1`. It then runs your tests.
    * If your tests **fail**, you've "killed the mutant." This is good! It means your tests were strong enough to detect the bug.
    * If your tests **still pass**, the mutant "survived." This is bad. It reveals a weakness in your test suite—your tests didn't notice the bug.

**PIT (Pitest)** is the most popular mutation testing framework for Java. It modifies your compiled bytecode to introduce mutants and then runs your test suite against them, providing a "mutation score" which is a much more accurate measure of test quality than simple code coverage.

**Best Practice:** Aim for a high mutation score (>85%). A high score indicates that your tests are not just executing code, but are actually sensitive to changes in its behavior.

***
Would you like to continue with Section 11: CI/CD \& Test Reports?

---

# yes

Of course. This section explains how to integrate your JUnit tests into Continuous Integration/Continuous Deployment (CI/CD) pipelines to automate testing and how to generate human-readable reports from the results.

### The Role of Tests in CI/CD

CI/CD is an automated process that takes your code from a developer's machine to production. Automated tests are the most critical quality gate in this process. Every time new code is pushed, the CI server automatically builds the application and runs the entire test suite. If any test fails, the build is marked as "broken," and the new code is blocked from proceeding, providing instant feedback.

* **Analogy:** A CI/CD pipeline is like an automated bottling factory. Your code is the liquid. The test suite is the **quality control station** that automatically checks every single bottle for purity, fill level, and a proper seal. If a bad bottle is detected, the entire assembly line halts until the problem is fixed.


### Running JUnit Tests in CI Platforms

All major CI/CD platforms work by executing shell commands. To run your JUnit tests, you simply configure the pipeline to run your build tool's test command (e.g., `mvn test` or `./gradlew test`).

#### GitHub Actions

Create a `.yml` file in the `.github/workflows` directory of your repository.

```yaml
# .github/workflows/maven-ci.yml
name: Java CI with Maven

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up JDK 17
        uses: actions/setup-java@v4
        with:
          java-version: '17'
          distribution: 'temurin'
          cache: 'maven' # Caches Maven dependencies for faster builds

      - name: Build and run tests
        run: mvn -B package # The 'package' phase automatically runs 'test'
```


#### GitLab CI/CD

Create a `.gitlab-ci.yml` file in the root of your repository.

```yaml
# .gitlab-ci.yml
image: maven:3.9-eclipse-temurin-17 # Use a Docker image with Maven and Java pre-installed

stages:
  - test

test_job:
  stage: test
  script:
    - echo "Running tests..."
    - mvn test
```


#### Jenkins

Jenkins pipelines are typically defined in a `Jenkinsfile`.

```groovy
// Jenkinsfile (Declarative Pipeline)
pipeline {
    agent any // Specifies where the pipeline will run
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-repo/your-project.git'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test' // Execute the Maven test command
            }
        }
    }
}
```


### Generating Test Reports

The raw XML output from test runners is not easy to read. CI platforms can parse these files and display them in a user-friendly format. Advanced reporting tools like Allure can provide even richer insights.

#### Default Surefire Reports (Maven)

Maven's Surefire plugin automatically generates basic XML reports in `target/surefire-reports`. Most CI tools can parse these files out-of-the-box to display the number of passed, failed, and skipped tests.

#### Allure Framework for Advanced Reports

Allure is a powerful, open-source framework that creates interactive and comprehensive test reports.

* **Analogy:** A default Surefire report is like a plain text receipt from a cash register. An **Allure report** is like a detailed, interactive online dashboard for your finances, with historical trend charts, categorized spending, and downloadable statements.

**Key Features of Allure:**

* **Historical Trends:** Shows how test results have changed over time.
* **Categorization:** Groups failures by root cause (e.g., "Product Bug," "Test Bug").
* **Steps \& Attachments:** Allows you to log steps within a test and attach screenshots, logs, or other files to the report.
* **Environment Details:** Displays information about the test environment (e.g., browser version, OS, server URL).

You integrate Allure via a plugin for your build tool, which generates the report data. The CI server then uses the Allure command-line tool to render the HTML report.

### Parallel Test Execution in CI

As your test suite grows, it can become a bottleneck in the CI pipeline. Running tests in parallel can dramatically reduce execution time.

You can configure Maven's Surefire plugin to run tests in parallel by specifying a `forkCount`.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-surefire-plugin</artifactId>
    <version>3.2.5</version>
    <configuration>
        <!-- Run tests in parallel using 4 threads, one for each class -->
        <parallel>classes</parallel>
        <forkCount>4</forkCount>
        <reuseForks>true</reuseForks>
    </configuration>
</plugin>
```

**Common Pitfall: Test Independence.** For parallel execution to work, your tests **must be completely independent**. Tests that rely on shared, mutable state (like static variables, shared database records, or files on disk) will become "flaky"—they will randomly fail when run in parallel due to race conditions. This is a primary cause of unreliable CI builds.

***
Would you like to continue with Section 12: Integration \& System Testing with JUnit?

---

# yes

Excellent. This section moves beyond isolated unit tests to show how JUnit can be used as a foundation for writing powerful integration and system-level tests that verify how your application interacts with external dependencies like databases, APIs, and message brokers.

### JUnit as an Orchestrator

While JUnit is designed for unit tests, its lifecycle annotations (`@BeforeAll`, `@AfterAll`) and extension model make it a perfect orchestrator for managing the setup and teardown of complex test environments. For integration tests, we use JUnit to start and stop external services required for the test.

* **Analogy:** In an integration test, JUnit is the **stage manager** for a play. It doesn't act in the play itself, but it ensures the stage is set up correctly (`@BeforeAll` starts a database), the actors (your services) are in place, the scene runs, and everything is cleaned up afterward (`@AfterAll` stops the database).


### Integration with REST Assured for API Testing

**REST Assured** is a Java library that provides a fluent DSL (Domain-Specific Language) for testing REST APIs. It simplifies making HTTP requests and asserting on the responses. When combined with `@SpringBootTest`, you can write true end-to-end tests for your API endpoints.

```java
import io.restassured.RestAssured;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.web.server.LocalServerPort;
import static io.restassured.RestAssured.given;
import static org.hamcrest.Matchers.equalTo;

@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
class UserApiIntegrationTest {

    @LocalServerPort
    private int port; // Injects the random port the server started on

    @BeforeEach
    void setup() {
        RestAssured.port = port; // Configure REST Assured to use the correct port
    }

    @Test
    void testGetUserById_returnsUser() {
        // Assume the application is running and has a user with ID 1
        
        given()
            // No specific setup needed for a simple GET
        .when()
            .get("/api/users/1")
        .then()
            .statusCode(200)
            .body("username", equalTo("john_doe"))
            .body("id", equalTo("1"));
    }
}
```


### Database Integration Tests with Testcontainers

**Testcontainers** is a revolutionary library that allows you to run real external services (databases, message queues, web browsers) inside Docker containers that are managed by your JUnit tests. This provides high-fidelity testing against production-like dependencies without the hassle of manual setup.

* **Analogy:** Testcontainers gives you a **brand-new, disposable kitchen** for every recipe you test. You start with a clean PostgreSQL container (`@Container`), run your test against it, and then Testcontainers throws the entire container away. This guarantees that tests are isolated and don't interfere with each other by leaving behind data.

```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.DynamicPropertyRegistry;
import org.springframework.test.context.DynamicPropertySource;
import org.testcontainers.containers.PostgreSQLContainer;
import org.testcontainers.junit.jupiter.Container;
import org.testcontainers.junit.jupiter.Testcontainers;
import static org.assertj.core.api.Assertions.assertThat;

@Testcontainers // Enables Testcontainers support in JUnit 5
@SpringBootTest
class UserRepositoryTCIntegrationTest {

    @Container // Marks this as a container to be managed by JUnit
    private static final PostgreSQLContainer<?> postgres = new PostgreSQLContainer<>("postgres:15-alpine");

    @Autowired
    private UserRepository userRepository;

    // Dynamically set the database connection properties for Spring at runtime
    @DynamicPropertySource
    static void configureProperties(DynamicPropertyRegistry registry) {
        registry.add("spring.datasource.url", postgres::getJdbcUrl);
        registry.add("spring.datasource.username", postgres::getUsername);
        registry.add("spring.datasource.password", postgres::getPassword);
    }
    
    @Test
    void testSaveAndFindUser() {
        // Arrange
        User user = new User("test_user");
        
        // Act
        userRepository.save(user);
        
        // Assert
        User foundUser = userRepository.findById(user.getId()).orElse(null);
        assertThat(foundUser).isNotNull();
        assertThat(foundUser.getUsername()).isEqualTo("test_user");
    }
}
```


### Embedded Servers for Local Testing

Before Testcontainers became popular, the common approach was to use "embedded" or in-memory versions of external services. These are still useful for lightweight tests where 100% production fidelity is not required.


| Service | Embedded Tool | Comments |
| :-- | :-- | :-- |
| **Database** | **H2 Database** | An in-memory Java SQL database. It's very fast but can have subtle SQL dialect differences from production databases like PostgreSQL or MySQL. This is a **common pitfall**. |
| **Message Broker** | **Embedded Kafka** (`spring-kafka-test`) | Provides an in-memory Kafka broker that runs within the test's JVM. Excellent for testing Kafka producers and consumers without needing a Docker environment. |

**Best Practice:** Prefer **Testcontainers** over embedded servers for database testing, as it provides much higher confidence by running the exact same database engine you use in production. Use embedded servers for services like Kafka where the embedded version is well-supported and offers a good balance of speed and realism.

***
Would you like to continue with the final section, Section 13: Best Practices \& Patterns?

---

# yes

Excellent. This final section provides a collection of best practices, patterns, and conventions to help you write tests that are clean, maintainable, and valuable in the long run.

### Test Naming Conventions

The name of a test should clearly describe its purpose and context. A well-named test acts as a piece of documentation.

**Popular Conventions:**

1. **`methodName_should_expectedBehavior_when_stateUnderTest`**
    * This is highly descriptive and easy to read.
    * Example: `registerUser_should_throwException_when_emailIsInvalid()`
2. **`given_when_then`** (Behavior-Driven Development style)
    * Mirrors the structure of a BDD scenario.
    * Example: `givenUserExists_whenRegisteringWithSameEmail_thenThrowDuplicateUserException()`
3. **Using `@DisplayName`**
    * JUnit 5's `@DisplayName` allows you to use plain English sentences with spaces and special characters. This is often the most readable option.

```java
@Test
@DisplayName("should return an empty list when no products match the category")
void testFindByCategory_returnsEmptyList_forNoMatches() {
    // ...
}
```


**Best Practice:** Choose one convention and apply it consistently across your project. The goal is for another developer to understand the test's intent just by reading its name.

### Avoiding Brittle Tests

A **brittle test** is a test that fails due to small, unrelated changes in the production code, even when the overall behavior is still correct. They create noise and slow down development.

* **Analogy:** A brittle test is like a security guard who raises an alarm not only for intruders but also if the homeowner repaints their front door. A **robust test** is a guard who only cares about actual threats (changes in behavior).

**How to Avoid Brittle Tests:**

* **Test Behavior, Not Implementation:** Focus on the public API of a class. Don't test private methods directly. If a private method's logic is important, it should be covered by a test of the public method that calls it.
* **Don't Over-Mock:** Mock external dependencies (database, network, file system), but not every class. Mocking classes that are part of the same logical unit makes tests coupled to the implementation.
* **Use Specific Assertions:** Instead of asserting that two complex objects are identical (`assertEquals(obj1, obj2)`), assert only on the specific properties you care about. AssertJ is excellent for this (`assertThat(user.getName()).isEqualTo("test")`).


### Isolating External Dependencies

This reinforces a core principle of the Test Pyramid:

* **For Unit Tests:** Use mocks (Mockito) to simulate external systems. This keeps tests fast and focused on your business logic.
* **For Integration Tests:** Use real services, but in a controlled environment. **Testcontainers** is the gold standard for this, ensuring your tests run against a production-like database or message broker without affecting a shared development environment.

**Common Pitfall:** Running automated tests against a shared, persistent development database. This is a recipe for flaky tests, as one test can leave data that causes another test to fail. Always use ephemeral, in-memory databases or Testcontainers.

### Data-Driven Testing

As covered in Section 3, using parameterized tests (`@ParameterizedTest`) is a best practice for several reasons:

* It drastically reduces boilerplate code.
* It encourages testing of edge cases (e.g., empty strings, null values, zero, negative numbers).
* It makes it easy for other developers to add new test cases by simply adding a new row to a CSV source.


### Using Builders \& ObjectMothers for Test Data Setup

The "Arrange" block of a test can become very complex when you need to create intricate objects. The Object Mother and Builder patterns help manage this complexity.

#### The Object Mother Pattern

An Object Mother is a factory class that creates and provides pre-configured object instances for your tests.

* **Analogy:** An Object Mother is like a restaurant's prep station. Instead of making a "standard sandwich" from scratch in every test, you just ask the "prep station" for one.

```java
public class UserMother {
    public static User createDefaultUser() {
        return new User("123", "default_user", "default@test.com", true);
    }
    
    public static User createUnverifiedUser() {
        return new User("456", "unverified_user", "unverified@test.com", false);
    }
}

// In your test:
@Test
void testLoginWithUnverifiedUser() {
    // Arrange
    User user = UserMother.createUnverifiedUser();
    // ...
}
```


#### The Builder Pattern

The Builder pattern provides a fluent API to construct complex objects. It makes tests more readable by describing *what* is being set. It's often combined with the Object Mother pattern.

```java
// A builder for the User class
public class UserBuilder {
    private String id = "default-id";
    private String username = "default-user";
    
    public UserBuilder withId(String id) {
        this.id = id;
        return this;
    }
    
    public UserBuilder withUsername(String username) {
        this.username = username;
        return this;
    }
    
    public User build() {
        return new User(id, username);
    }
}

// In your test:
@Test
void testSomething() {
    // Arrange
    User adminUser = new UserBuilder()
                        .withId("admin-001")
                        .withUsername("admin")
                        .build();
    // ...
}
```

This concludes the JUnit quick revision guide. You now have a comprehensive overview from fundamentals to advanced patterns. Happy testing

