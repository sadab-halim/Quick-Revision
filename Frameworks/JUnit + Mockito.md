<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# You are a JUnit expert and mentor.

Your task is to generate a structured **quick revision notes for interview preparation** on JUnit, broken into sections.  
I will specify which section to start from, and you will cover ONLY that section in detail.  
You should cover all the important topics from each section and it's sub-section which are most asked in interviews, mark the topic as (IMP) which is most asked and is a hot question.

### Output Rules:

- Be concise, yet cover all the concepts, revision notes should be crisp and clear.
- Use headings, bullet points, tables, and short code snippets.
- Highlight **common pitfalls**, **best practices**, and **JUnit version differences** (JUnit 4 vs JUnit 5).
- Use comparison tables when useful (e.g., Assertions vs Matchers, JUnit 4 vs 5 annotations).
- Include **short examples** for each feature (@Test, @ParameterizedTest, etc.).
- For complex or abstract topics (e.g., mocking, CI/CD, TDD, system testing), use **real-life analogies** to simplify learning.
- End each section by asking if I want to continue with the next one.


### Sections:

1. Fundamentals of Unit Testing
What is a Unit Test?
Unit vs Integration vs System Tests
AAA (Arrange–Act–Assert) Pattern
Testing Pyramid \& Best Practices
Maven/Gradle setup for JUnit \& Mockito
2. JUnit Basics
Test Lifecycle: @BeforeEach, @AfterEach, @BeforeAll, @AfterAll
Basic Annotations: @Test, @Disabled, @DisplayName
Assertions:
assertEquals, assertNotEquals
assertTrue, assertFalse
assertNull, assertNotNull
assertThrows (exception testing)
Assumptions: assumeTrue, assumeFalse
3. Parameterized \& Repeated Tests
@ParameterizedTest with value sources (@ValueSource, @CsvSource, @MethodSource)
Custom argument providers
@RepeatedTest for repeated execution
4. Tagging, Filtering \& Conditional Tests
@Tag, @IncludeTags, @ExcludeTags
Conditional execution (@EnabledOnOs, @EnabledOnJre, etc.)
JUnit Extensions \& @ExtendWith
5. Advanced Assertions \& Matchers
Hamcrest Matchers (assertThat, is, containsString, etc.)
AssertJ fluent assertions
Combining multiple assertions
Soft assertions
6. Exception \& Timeout Testing
Testing expected exceptions (assertThrows)
JUnit 5 assertTimeout \& assertTimeoutPreemptively
Fail fast vs non-preemptive timeout handling
7. Mockito Fundamentals
What is Mockito \& why mocking?
Mocks vs Stubs vs Spies vs Fakes
Creating mocks:
@Mock annotation
Mockito.mock(Class.class)
Injecting mocks with @InjectMocks
Lifecycle: MockitoAnnotations.openMocks(this)
8. Stubbing Behavior
when(...).thenReturn(...)
when(...).thenThrow(...)
doNothing().when(mock).method()
doThrow(...).when(mock).method()
Returning multiple values (thenReturn(a, b, c))
Answering with lambdas (thenAnswer(...))
9. Verifying Behavior
verify(mock).method()
Verifying call counts: times(n), never(), atLeastOnce(), atMost(n)
verifyNoMoreInteractions()
Order verification with InOrder
10. Argument Captors \& Matchers
Built-in matchers: any(), eq(), anyString(), anyInt()
Mixing matchers \& exact values (pitfalls)
Capturing arguments: ArgumentCaptor
Custom matchers
11. Spies vs Mocks
Mockito.spy() for partial mocking
Difference between mock() and spy()
Stubbing real objects with spies
12. Advanced Mockito Usage
Mocking final classes \& static methods (Mockito 3+)
Deep stubs (RETURNS_DEEP_STUBS)
Mocking private methods (via PowerMock or delegation)
Mocking constructors (advanced case)
13. Mocking in Spring Context
@MockBean \& @SpyBean in Spring Boot tests
Testing with Spring profiles \& properties
Overriding @Value or @ConfigurationProperties in tests
Mocking external services (REST, DB, Kafka, etc.) in Spring Boot
14. TDD (Test-Driven Development)
Writing tests before implementation
Red → Green → Refactor cycle
Example: designing APIs with TDD
Common pitfalls in TDD
15. Coverage \& Quality
Measuring coverage with JaCoCo, IntelliJ coverage tool
Mutation testing (PIT, Stryker)
Flaky test detection \& elimination
16. CI/CD \& Test Reports
Running tests in pipelines (GitHub Actions, GitLab, Jenkins)
Generating reports (JUnit XML, HTML)
Parallel test execution in CI
Test caching \& optimizations
17. Integration \& System Testing with JUnit
@SpringBootTest for integration tests
@DataJpaTest, @WebMvcTest
Testcontainers for DB, Kafka, RabbitMQ integration
WireMock for mocking REST APIs
End-to-end tests with JUnit
18. Best Practices \& Patterns
Writing deterministic tests
Avoiding over-mocking
Test data builders \& factories
Given–When–Then test structure
Organizing test packages \& naming conventions
Layered test strategy (unit → integration → system → e2e)

### Instruction:

When I say **"Start from Section X"**, generate the revision guide for that section only.  
When done, ask me if I want to continue with the next section.  
Always maintain the same style so the entire revision guide feels consistent.

As your JUnit mentor, I am ready to generate the structured quick revision notes for your interview preparation. I will adhere to all the specific formatting and content guidelines you've outlined to ensure the guide is consistent and helpful.

Please let me know which section you would like to begin with.

---

# Start from Section: 1

A unit test is a piece of code written by a developer to verify that a small, isolated piece of an application's source code, the "unit," behaves exactly as expected. This process ensures code quality and correctness at the most granular level.

### What is a Unit Test?

A unit test focuses on the smallest testable part of an application, typically a single method or class. Its core purpose is to validate that the logic of that unit works correctly in isolation, without depending on external systems like databases, filesystems, or network services.

* **Isolation (IMP)**: The most crucial characteristic. Dependencies are replaced with "test doubles" like mocks or stubs to ensure the test is predictable and fast.
* **Speed**: Unit tests should run extremely fast (milliseconds). A large suite of thousands of unit tests should complete in minutes.
* **Automation**: They are fully automated and can be run with a single command, making them ideal for continuous integration.


### Unit vs. Integration vs. System Tests

Understanding the difference is a frequent interview topic. Imagine building a car: a unit test checks if the engine works on its own, an integration test checks if the engine and transmission work together, and a system test involves driving the fully assembled car.


| Feature | Unit Test | Integration Test | System Test |
| :-- | :-- | :-- | :-- |
| **Scope** | A single method or class in isolation. | Two or more interacting components (e.g., service and repository). | The entire application, end-to-end. |
| **Dependencies** | Mocked (e.g., using Mockito). | Real or in-memory (e.g., H2 database, Testcontainers). | Live or production-like (real DB, external APIs). |
| **Speed** | Very Fast (ms) | Slow (seconds) | Very Slow (minutes) |
| **Analogy** | Testing a single car engine on a stand. | Testing the engine connected to the transmission. | Taking the fully assembled car for a test drive. |

### AAA (Arrange–Act–Assert) Pattern (IMP)

The AAA pattern provides a clear and readable structure for writing unit tests. It separates the test into three distinct parts.

* **Arrange**: Set up the test. This includes initializing objects, preparing mock dependencies, and defining input data.
* **Act**: Execute the unit under test. This is typically a single method call on the object you are testing.
* **Assert**: Verify the outcome. Check if the method call produced the expected result, changed the state of the object correctly, or called its dependencies as expected.

```java
// Example of AAA Pattern
@Test
void testAdd_shouldReturnSumOfTwoNumbers() {
    // 1. Arrange
    Calculator calculator = new Calculator();
    int a = 10;
    int b = 5;
    int expectedResult = 15;

    // 2. Act
    int actualResult = calculator.add(a, b);

    // 3. Assert
    assertEquals(expectedResult, actualResult, "The sum should be correct");
}
```


### Testing Pyramid \& Best Practices

The Testing Pyramid is a model that guides how to balance different types of tests in your suite.

* **Base (Unit Tests)**: The largest part of the pyramid. Write many fast, simple unit tests.
* **Middle (Integration Tests)**: Fewer than unit tests. They verify interactions between components.
* **Top (End-to-End/UI Tests)**: The smallest part. These are slow, brittle, and expensive. Use them sparingly for critical user workflows.

**Best Practices**:

* Tests should be independent and repeatable.
* One test should verify one logical outcome.
* Name tests clearly to describe what they are testing (e.g., `methodName_shouldDoSomething_whenCondition`).
* Follow the **FIRST** principles: Fast, Independent, Repeatable, Self-Validating, Timely.


### Maven/Gradle setup for JUnit \& Mockito

You need to add JUnit 5 and Mockito dependencies to your build file with the `test` scope.

#### Maven (`pom.xml`)

```xml
<dependencies>
    <!-- JUnit 5 Jupiter API for writing tests -->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.10.0</version>
        <scope>test</scope>
    </dependency>
    <!-- JUnit 5 Jupiter Engine for running tests -->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-engine</artifactId>
        <version>5.10.0</version>
        <scope>test</scope>
    </dependency>
    <!-- Mockito Core for mocking -->
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-core</artifactId>
        <version>5.5.0</version>
        <scope>test</scope>
    </dependency>
    <!-- Mockito JUnit 5 integration -->
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-junit-jupiter</artifactId>
        <version>5.5.0</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```


#### Gradle (`build.gradle.kts`)

```kotlin
tasks.test {
    useJUnitPlatform()
}

dependencies {
    // JUnit 5 and Mockito
    testImplementation("org.junit.jupiter:junit-jupiter-api:5.10.0")
    testRuntimeOnly("org.junit.jupiter:junit-jupiter-engine:5.10.0")
    testImplementation("org.mockito:mockito-core:5.5.0")
    testImplementation("org.mockito:mockito-junit-jupiter:5.5.0")
}
```


***
Would you like to continue with Section 2: JUnit Basics?

---

# yes

Of course. Here is the quick revision guide for Section 2.

### Section 2: JUnit Basics

This section covers the fundamental annotations and assertions that form the core of writing tests in JUnit 5.

### Test Lifecycle (IMP)

JUnit 5 provides annotations to manage the lifecycle of a test class, allowing for setup and teardown logic to be executed before and after tests.


| Annotation | JUnit 4 Equivalent | Scope | Use Case |
| :-- | :-- | :-- | :-- |
| `@BeforeAll` | `@BeforeClass` | Static (runs once per class) | Initializing shared, expensive resources (e.g., database connections, starting a server). |
| `@AfterAll` | `@AfterClass` | Static (runs once per class) | Cleaning up shared resources created in `@BeforeAll`. |
| `@BeforeEach` | `@Before` | Instance (runs before each `@Test`) | Resetting state before every test to ensure isolation (e.g., re-initializing a mock object). |
| `@AfterEach` | `@After` | Instance (runs after each `@Test`) | Cleaning up resources used by a single test (e.g., deleting a temporary file). |

**Execution Order**: `@BeforeAll` → `@BeforeEach` → `@Test` → `@AfterEach` → `@AfterAll`

```java
// Example of Test Lifecycle
@DisplayName("A sample test class demonstrating lifecycle methods")
class LifecycleDemoTest {

    @BeforeAll
    static void setupAll() {
        System.out.println("Connecting to the database...");
    }

    @BeforeEach
    void setup() {
        System.out.println("  Loading test data...");
    }

    @Test
    void testOne() {
        System.out.println("    Executing testOne()");
        assertTrue(true);
    }

    @Test
    void testTwo() {
        System.out.println("    Executing testTwo()");
        assertTrue(true);
    }

    @AfterEach
    void teardown() {
        System.out.println("  Clearing test data...");
    }

    @AfterAll
    static void teardownAll() {
        System.out.println("Disconnecting from the database.");
    }
}
```

**Common Pitfall**: Forgetting to make `@BeforeAll` and `@AfterAll` methods **static**. JUnit 5 requires this because they run before the test class instance is created.

### Basic Annotations

| Annotation | Purpose | Example |
| :-- | :-- | :-- |
| `@Test` | Marks a method as a test method. This is the primary annotation for writing tests. | `@Test void myFirstTest() { /* ... */ }` |
| `@DisplayName` | Provides a custom, human-readable name for a test class or method. It supports spaces and emojis. (IMP) | `@DisplayName("✅ Should return true for a valid user")` |
| `@Disabled` | Disables a test method or class. It's good practice to include a reason. | `@Disabled("Ticket-123: This feature is currently under rework")` |

### Assertions (IMP)

Assertions are static methods within the `org.junit.jupiter.api.Assertions` class used to check if a condition is met. A failed assertion will cause the test to fail.


| Assertion | Description | Example |
| :-- | :-- | :-- |
| `assertEquals(expected, actual)` | Fails if the expected and actual values are not equal. | `assertEquals(4, calculator.add(2, 2));` |
| `assertNotEquals(unexpected, actual)` | Fails if the unexpected and actual values are equal. | `assertNotEquals(5, calculator.add(2, 2));` |
| `assertTrue(condition)` | Fails if the supplied boolean condition is false. | `assertTrue(list.isEmpty());` |
| `assertFalse(condition)` | Fails if the supplied boolean condition is true. | `assertFalse(list.contains(newItem));` |
| `assertNull(object)` | Fails if the provided object reference is not null. | `assertNull(userService.findUser("unknown"));` |
| `assertNotNull(object)` | Fails if the provided object reference is null. | `assertNotNull(userService.findUser("admin"));` |
| `assertThrows(exception, executable)` | Fails if the executable code block does not throw the expected exception type. (IMP) | `assertThrows(IllegalArgumentException.class, () -> user.setAge(-1));` |

**Best Practice**: Always provide an optional message in assertions (`assertEquals(expected, actual, "Helpful failure message")`). It makes debugging failed tests much easier.

### Assumptions

Assumptions, found in `org.junit.jupiter.api.Assumptions`, are used to control test execution based on external conditions. If an assumption fails, the test is **aborted** (skipped), not failed. This is useful for tests that should only run in specific environments.

* `assumeTrue(condition)`: The test proceeds only if the condition is true.
* `assumeFalse(condition)`: The test proceeds only if the condition is false.

```java
// Example of an Assumption
@Test
void testOnlyOnWindows() {
    // This test will be skipped on any OS other than Windows
    assumeTrue(System.getProperty("os.name").toLowerCase().contains("win"));
    
    // ... test logic specific to Windows ...
    System.out.println("Running Windows-specific test.");
}
```

**Analogy**: Think of an **assertion** as a final exam question: if you get it wrong, you fail. Think of an **assumption** as a prerequisite check: if you haven't taken the required course, you are simply not allowed to take the exam (the test is skipped).

***
Would you like to continue with Section 3: Parameterized \& Repeated Tests?

---

# yes

Of course. Here is the quick revision guide for Section 3.

### Section 3: Parameterized \& Repeated Tests

These JUnit 5 features allow you to run a test multiple times with different inputs or for a specified number of repetitions, which significantly reduces boilerplate code.

### @ParameterizedTest (IMP)

A `@ParameterizedTest` runs a test method multiple times with different arguments. It is a powerful replacement for writing many similar tests with slightly different inputs and expected outputs.

**Best Practice**: This is ideal for testing boundary conditions, edge cases, and various valid inputs for a single piece of logic without duplicating test code.

#### Value Sources

To use a parameterized test, you must declare at least one "source" that provides the arguments for each invocation.

* `@ValueSource`: The simplest source. It provides an array of literal values (shorts, bytes, ints, longs, floats, doubles, chars, booleans, strings, or classes). It can only provide a single argument per invocation.

```java
// Example with @ValueSource
@ParameterizedTest
@ValueSource(strings = {"racecar", "madam", "level"})
void testIsPalindrome_shouldReturnTrueForPalindromes(String input) {
    assertTrue(StringUtils.isPalindrome(input));
}
```

* `@CsvSource`: Allows you to express argument lists as comma-separated values (CSV). Each string in the `@CsvSource` represents one invocation and can supply multiple arguments.

```java
// Example with @CsvSource
@ParameterizedTest
@CsvSource({
    "5, 5, 10",    // a, b, expectedSum
    "10, -2, 8",
    "0, 0, 0"
})
void testAdd_shouldReturnCorrectSum(int a, int b, int expectedSum) {
    Calculator calculator = new Calculator();
    assertEquals(expectedSum, calculator.add(a, b));
}
```

* `@MethodSource`: The most flexible source. It refers to a static factory method that provides the arguments. This method must return a `Stream`, `Iterable`, `Iterator`, or an array of arguments. This is especially useful for creating complex objects as inputs. (IMP)

```java
// Example with @MethodSource
class CalculatorTest {
    @ParameterizedTest
    @MethodSource("additionArgumentsProvider")
    void testAdd(int a, int b, int expected) {
        Calculator calculator = new Calculator();
        assertEquals(expected, calculator.add(a, b));
    }

    // Static factory method providing arguments
    private static Stream<Arguments> additionArgumentsProvider() {
        return Stream.of(
            Arguments.of(2, 3, 5),      // Arguments.of() creates a set of args
            Arguments.of(10, 10, 20),
            Arguments.of(-5, 5, 0)
        );
    }
}
```

**Common Pitfall**: The factory method for `@MethodSource` must be `static` and must not accept any parameters unless the test class is annotated with `@TestInstance(Lifecycle.PER_CLASS)`.

### Custom Argument Providers

For highly complex or reusable argument generation logic, you can create a custom `ArgumentsProvider` and reference it using the `@ArgumentsSource` annotation. This is an advanced feature for scenarios where the built-in sources are insufficient.

### @RepeatedTest

The `@RepeatedTest` annotation allows you to run a test a specified number of times. This is useful for tests that might fail intermittently (flaky tests) or when testing behavior that involves randomness.

* You can access metadata about the current repetition using the `RepetitionInfo` dependency.
* The display name for each repetition can be customized using patterns like `{displayName}`, `{currentRepetition}`, and `{totalRepetitions}`.

```java
// Example of @RepeatedTest
private Set<Integer> uniqueIds = new HashSet<>();

@RepeatedTest(value = 5, name = "Repetition {currentRepetition} of {totalRepetitions}")
@DisplayName("Generate Unique ID")
void testGenerateUniqueId_shouldBeUnique(RepetitionInfo repetitionInfo) {
    // Arrange
    IdGenerator generator = new IdGenerator();
    
    // Act
    int id = generator.generate();
    
    // Assert
    System.out.println("Repetition " + repetitionInfo.getCurrentRepetition() + ": Generated ID = " + id);
    assertTrue(uniqueIds.add(id), "Generated ID should be unique");
}
```

**Analogy**: A `@ParameterizedTest` is like a scientist testing a formula with different chemicals (inputs) to see if the outcome is as expected. A `@RepeatedTest` is like a scientist repeating the *same* experiment multiple times to ensure the result is consistent and not a fluke.

***
Would you like to continue with Section 4: Tagging, Filtering \& Conditional Tests?

---

# yes

Of course. Here is the quick revision guide for Section 4.

### Section 4: Tagging, Filtering \& Conditional Tests

This section covers JUnit 5 features that give you fine-grained control over which tests are executed and under what conditions, which is essential for managing large test suites and running specific tests in different environments (e.g., local vs. CI).

### Tagging \& Filtering (IMP)

Tagging allows you to categorize tests into groups. You can then use these tags to selectively run or exclude certain groups of tests. This is extremely useful for separating fast unit tests from slow integration tests.

* `@Tag("tag-name")`: This annotation is used to assign a tag (a simple string) to a test method or an entire test class.

**Best Practices**:

* Use tags like `"unit"`, `"integration"`, `"slow"`, or `"api"` to classify tests.
* A test or class can have multiple `@Tag` annotations.

```java
@Tag("unit")
@DisplayName("Tests for the Calculator Service")
class CalculatorServiceTest {

    @Test
    @Tag("fast")
    @DisplayName("Should perform simple addition")
    void testAddition() {
        // ...
    }

    @Test
    @Tag("slow")
    @DisplayName("Should perform complex calculation")
    void testComplexCalculation() {
        // ...
    }
}
```


#### Filtering in Build Tools

The primary way to use tags is by configuring your build tool to include or exclude them during the test execution phase. This is a hot topic for CI/CD pipeline configuration.

* **Maven (surefire-plugin)**:

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-surefire-plugin</artifactId>
    <version>3.1.2</version>
    <configuration>
        <groups>fast | unit</groups> <!-- Run tests tagged with 'fast' OR 'unit' -->
        <excludedGroups>slow</excludedGroups> <!-- Exclude tests tagged with 'slow' -->
    </configuration>
</plugin>
```

* **Gradle**:

```kotlin
tasks.test {
    useJUnitPlatform {
        includeTags("fast", "unit")
        excludeTags("slow")
    }
}
```


### Conditional Execution

JUnit 5 provides a rich set of annotations to enable or disable tests based on various conditions. This prevents tests from running in environments where they are not designed to run.


| Annotation | Description |
| :-- | :-- |
| `@EnabledOnOs(OS.WINDOWS)` | Enables the test only on specified operating systems. |
| `@DisabledOnOs(OS.LINUX)` | Disables the test on specified operating systems. |
| `@EnabledOnJre(JRE.JAVA_11)` | Enables the test only on a specific Java Runtime Environment version. |
| `@DisabledOnJre(JRE.JAVA_8)` | Disables the test on a specific JRE version. |
| `@EnabledIfSystemProperty` | Enables a test if a JVM system property matches a specific value. |
| `@EnabledIfEnvironmentVariable` | Enables a test if an environment variable matches a specific value. |

```java
// Example of Conditional Execution
class ConditionalTest {

    @Test
    @EnabledOnOs(OS.MAC)
    void testOnlyOnMac() {
        // This logic will only run on macOS
    }

    @Test
    @EnabledOnJre(JRE.JAVA_17)
    void testOnlyOnJava17() {
        // This test requires Java 17 features
    }

    @Test
    @EnabledIfEnvironmentVariable(named = "CI", matches = "true")
    void testOnlyInCiEnvironment() {
        // This test will only run when the environment variable CI is set to 'true'
    }
}
```


### JUnit Extensions \& @ExtendWith (IMP)

The JUnit 5 extension model is a core concept that replaces JUnit 4's `@RunWith` and `@Rule`. Extensions allow third-party libraries (like Mockito or Spring) to hook into the test lifecycle to perform setup, teardown, or other logic.

* `@ExtendWith(ExtensionName.class)`: This annotation is used to register one or more extensions on a test class or method.

**Analogy**: Think of the JUnit test runner as a basic gaming console. Extensions are like cartridges or DLCs you plug in to add new capabilities, characters, or levels (e.g., mocking, dependency injection).


| Feature | JUnit 4 | JUnit 5 |
| :-- | :-- | :-- |
| **Mechanism** | `@RunWith`, `@Rule`, `@ClassRule` | `@ExtendWith` |
| **Flexibility** | Limited, only one `@RunWith` allowed per class. | Highly flexible, multiple extensions can be composed. |
| **Example** | `@RunWith(MockitoJUnitRunner.class)` | `@ExtendWith(MockitoExtension.class)` |

The most common use case you will see is integrating Mockito:

```java
// JUnit 5 with Mockito Extension
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.junit.jupiter.MockitoExtension;

@ExtendWith(MockitoExtension.class) // Enables Mockito annotations like @Mock and @InjectMocks
class MyServiceTest {
    // ... tests using mocks
}
```


***
Would you like to continue with Section 5: Advanced Assertions \& Matchers?

---

# yes

Of course. Here is the quick revision guide for Section 5.

### Section 5: Advanced Assertions \& Matchers

While JUnit 5's built-in assertions are good for basic checks, libraries like **Hamcrest** and **AssertJ** provide more powerful, readable, and "fluent" ways to write assertions, making your tests more expressive and easier to debug.

### Hamcrest Matchers

Hamcrest provides a library of "matcher" objects that let you define rules for why a test should pass. It integrates with JUnit via the `assertThat()` method, which improves readability.

* **Syntax**: `assertThat(actualValue, is(equalTo(expectedValue)));`
* **Readability**: It reads like a natural sentence: "Assert that the actual value is equal to the expected value."

**JUnit 4 vs. JUnit 5**: Hamcrest was very popular with JUnit 4. While JUnit 5 has improved its own assertions, Hamcrest is still widely used. You need to add the `hamcrest` dependency to your project.


| Matcher | Description | Example |
| :-- | :-- | :-- |
| `is(T value)`, `equalTo(T value)` | Checks for equality. `is()` is just syntactic sugar. | `assertThat(name, is("Frodo"));` |
| `not(matcher)` | Negates another matcher's result. | `assertThat(name, is(not("Sauron")));` |
| `containsString(substring)` | Checks if a string contains a substring. | `assertThat(message, containsString("error"));` |
| `hasItem(item)`, `hasItems(item1, ...)` | Checks if a collection contains one or more items. | `assertThat(fellowship, hasItem("Gandalf"));` |
| `hasSize(size)` | Checks the size of a collection. | `assertThat(fellowship, hasSize(9));` |
| `greaterThan(value)` | Checks if a number is greater than a value. | `assertThat(age, greaterThan(50));` |

```java
// Example with Hamcrest Matchers
import static org.hamcrest.MatcherAssert.assertThat;
import static org.hamcrest.Matchers.*;

@Test
void testFellowshipMembers() {
    List<String> fellowship = Arrays.asList("Frodo", "Sam", "Gandalf");

    assertThat(fellowship, hasSize(3));
    assertThat(fellowship, hasItems("Frodo", "Sam"));
    assertThat(fellowship, not(hasItem("Sauron")));
}
```


### AssertJ Fluent Assertions (IMP)

AssertJ is a popular third-party library that provides "fluent" assertions. This means you can chain multiple checks together on the same object, leading to highly readable and maintainable tests.

* **Syntax**: `assertThat(actualValue).is...().is...()`
* **Key Benefits**:
    * **IDE Friendly**: Autocomplete reveals all possible assertions for an object's type (e.g., specific assertions for `List`, `String`, `Map`).
    * **Clarity**: Chained methods often read better than nested Hamcrest matchers.
    * **Rich Error Messages**: Provides very detailed messages on failure.

```java
// Example with AssertJ
import static org.assertj.core.api.Assertions.assertThat;

@Test
void testFellowshipMembersWithAssertJ() {
    List<String> fellowship = Arrays.asList("Frodo", "Sam", "Pippin", "Merry");

    // Chaining multiple assertions fluently
    assertThat(fellowship)
        .isNotNull()
        .hasSize(4)
        .contains("Frodo", "Sam")
        .doesNotContain("Sauron")
        .startsWith("Frodo"); // Checks the first element
}
```


### Combining Multiple Assertions with `assertAll()` (IMP)

A common pitfall in testing is that a test method stops at the **first failed assertion**. This forces you to fix issues one by one. JUnit 5's `assertAll()` solves this by executing all assertions within its block and then reporting all failures together.

**Analogy**: Traditional assertions are like a picky compiler that stops on the first error. `assertAll()` is like a modern linter that analyzes the whole file and gives you a complete list of issues at once.

```java
// Example of assertAll()
@Test
void testUserProperties() {
    User user = new User("Frodo", "Baggins", -50); // Invalid age

    // In a traditional test, only the first failure (lastName) would be reported.
    // assertEquals("Baggins", user.getLastName()); // Fails here, test stops.
    // assertEquals("Frodo", user.getFirstName());  // This line is never reached.
    // assertTrue(user.getAge() > 0);             // This line is never reached.

    // With assertAll(), all failures are reported.
    assertAll("User properties validation",
        () -> assertEquals("Baggins", user.getLastName(), "Last name is incorrect"),
        () -> assertEquals("Frodo", user.getFirstName(), "First name is incorrect"),
        () -> assertTrue(user.getAge() > 0, "Age must be positive")
    );
}
```


### Soft Assertions (AssertJ)

AssertJ provides a similar feature called "soft assertions". You collect all assertions, and then a final call checks them all. It's an alternative to `assertAll()` if you are already using AssertJ heavily.

```java
import org.assertj.core.api.SoftAssertions;

@Test
void testUserWithSoftAssertions() {
    User user = new User("Frod", "Baggins", -50);
    SoftAssertions softly = new SoftAssertions();
    
    softly.assertThat(user.getFirstName()).isEqualTo("Frodo");
    softly.assertThat(user.getAge()).isPositive();
    
    softly.assertAll(); // All failures are reported here
}
```


***
Would you like to continue with Section 6: Exception \& Timeout Testing?

---

# yes

Of course. Here is the quick revision guide for Section 6.

### Section 6: Exception \& Timeout Testing

This section focuses on how to verify that your code behaves correctly under exceptional circumstances and within expected performance limits.

### Testing Expected Exceptions (IMP)

A critical part of robust code is handling errors gracefully. Unit tests must verify that methods throw the correct exceptions under invalid conditions.

#### JUnit 5: `assertThrows()`

JUnit 5 provides the `assertThrows()` method, which is the modern and recommended way to test exceptions.

* **How it works**: It executes a provided code block (as a lambda) and asserts that it throws a specific type of exception.
* **Key Advantage**: It allows you to inspect the exception after it's caught. You can check its message, cause, or custom fields, which is a significant improvement over JUnit 4's `@Test(expected=...)`.

```java
// Example of assertThrows()
@Test
void testSetAge_shouldThrowExceptionForNegativeAge() {
    UserService userService = new UserService();
    
    // Define the action that should throw an exception
    Executable action = () -> userService.setAge(-10);
    
    // Assert that the action throws the expected exception
    IllegalArgumentException thrownException = assertThrows(
        IllegalArgumentException.class,
        action,
        "Should have thrown IllegalArgumentException for a negative age"
    );
    
    // (IMP) Optionally, assert properties of the thrown exception
    assertEquals("Age must be positive", thrownException.getMessage());
}
```

| Method | JUnit 4 | JUnit 5 |
| :-- | :-- | :-- |
| **Approach** | `@Test(expected = IllegalArgumentException.class)` annotation. | `assertThrows(IllegalArgumentException.class, executable)` method. |
| **Pros** | Simple for basic checks. | Can verify the exception's message and other properties. Test's intent is clearer. |
| **Cons** | Can't verify the exception message. Less precise, as any statement in the method can cause the test to pass. | Slightly more verbose. |

### Timeout Testing

Timeout tests ensure that a method completes its execution within a specified time limit. This is crucial for preventing performance regressions and detecting infinite loops.

#### `assertTimeout()` vs `assertTimeoutPreemptively()` (IMP)

JUnit 5 offers two ways to test timeouts, with a crucial difference in their behavior.


| Feature | `assertTimeout()` | `assertTimeoutPreemptively()` |
| :-- | :-- | :-- |
| **Execution** | Runs the code block in the **same thread**. | Runs the code block in a **different thread**. |
| **Behavior** | Waits for the code block to complete, then fails if the duration was exceeded. | Fails **immediately** as soon as the timeout is exceeded, interrupting the execution. |
| **Safety** | Safer. Recommended for code that is not thread-safe or has side effects. | Risky. Can lead to unpredictable behavior if the code is not designed for interruption. |
| **Analogy** | **Finish Line Timing**: A race official waits for a runner to cross the finish line and then checks their time. If it's too slow, the runner is disqualified *after finishing*. | **Whistle Stop**: A race official blows a whistle exactly at the time limit. The runner must stop immediately, wherever they are on the track. |

```java
// Example of timeout testing
@Test
void testLongRunningTaskWithTimeout() {
    // This will pass, as it's just under the 100ms limit.
    assertTimeout(Duration.ofMillis(100), () -> {
        Thread.sleep(90); // Simulates work
    });
}

@Test
void testLongRunningTaskWithPreemptiveTimeout() {
    // This test will fail because the task (120ms) exceeds the timeout (100ms)
    // and is stopped preemptively.
    assertTimeoutPreemptively(Duration.ofMillis(100), () -> {
        Thread.sleep(120); // Simulates work
    });
}
```

**Common Pitfall**: Using `assertTimeoutPreemptively` with code that modifies shared state or interacts with non-thread-safe resources. The abrupt termination can leave the system in an inconsistent state, causing other tests to fail unpredictably. Always prefer `assertTimeout` unless you have a specific need for preemption and understand the risks.

***
Would you like to continue with Section 7: Mockito Fundamentals?

---

# yes

Of course. Here is the quick revision guide for Section 7, which introduces the essential concepts of Mockito.

### Section 7: Mockito Fundamentals

This section covers the "what" and "why" of mocking and introduces Mockito, the most popular mocking framework for Java.

### What is Mockito \& Why Mocking? (IMP)

**Mockito** is a Java framework that lets you create "mock" objects in your tests.

**Why do we need mocking?**
The primary goal of a unit test is to test a single unit of code **in isolation**. However, most classes have dependencies on other classes (e.g., a `UserService` depends on a `UserRepository`). Calling a real `UserRepository` in a `UserService` test would mean you are no longer testing in isolation. The test could fail because of a bug in the repository, or it might require a database, making the test slow and complex.

**Mocking** solves this by replacing real dependencies with controllable, fake substitutes.

**Analogy: The Flight Simulator**

* **Real Object (Plane)**: A real Boeing 747. Flying it is expensive, risky, and depends on external factors like weather and air traffic control.
* **Mock Object (Flight Simulator)**: A fake cockpit that *simulates* the experience of flying. A pilot can practice landing in a storm (`when(weather).isStormy().thenReturn(true)`) or handling an engine failure (`doThrow(EngineFailureException.class).when(plane).engine(3)`) in a safe, controlled environment without needing a real plane.

In testing, Mockito is our flight simulator. It lets us simulate the behavior of dependencies so we can focus solely on the logic of the class we are testing.

### Mocks vs Stubs vs Spies vs Fakes (IMP)

This is a very common interview topic. These terms describe different types of "test doubles."


| Type | Description | Primary Use Case | Analogy |
| :-- | :-- | :-- | :-- |
| **Stub** | Provides pre-programmed, "canned" answers to method calls. It's used for **state verification**. | You need a dependency to return a specific value (e.g., `userRepository.findById(1)` should return a `User` object). | A movie extra who has one line: "He went that way!" They don't do anything else. |
| **Mock** | An object that you can set expectations on. It's used for **behavior verification**. | You need to check *if* a method was called, how many times, and with what arguments (e.g., `verify(emailService).sendWelcomeEmail("test@user.com")`). | A driving test examiner who doesn't drive but watches you and checks if you used your turn signals correctly. |
| **Spy** | A "partial mock." It is a wrapper around a **real object**. By default, it calls the real methods, but you can stub specific methods if needed. | You want to test most of a real object's behavior but need to override one or two methods (e.g., a method that makes a slow network call). | An undercover agent who is a real police officer but can lie about their identity (`spy.getName()`) when needed. |
| **Fake** | A full, working implementation, but simplified for testing. It's not a mock. | You need a dependency that behaves like the real thing but is too simple for production. | An in-memory database (like H2) that acts like a real database but is faster and simpler. |

**Note**: In practice, Mockito's "mocks" can act as both stubs (when you use `when().thenReturn()`) and mocks (when you use `verify()`).

### Creating Mocks

You can create mocks in two ways:

1. **Using the `@Mock` annotation (Recommended)**: This is the declarative and most common way.

```java
@ExtendWith(MockitoExtension.class)
class UserServiceTest {
    @Mock
    private UserRepository userRepository; // Creates a mock UserRepository
    
    // ... tests ...
}
```

2. **Using the `Mockito.mock()` method**: This is the programmatic way, useful when annotations aren't practical.

```java
class UserServiceTest {
    private UserRepository userRepository;

    @BeforeEach
    void setUp() {
        userRepository = Mockito.mock(UserRepository.class); // Programmatically create mock
    }
    
    // ... tests ...
}
```


### Injecting Mocks with `@InjectMocks` (IMP)

`@InjectMocks` creates an instance of your test subject and automatically injects fields annotated with `@Mock` into it. Mockito will try to inject dependencies via constructor, setter, or field injection (in that order).

**Common Pitfall**: `@InjectMocks` only works for mocks declared with `@Mock` in the same test class.

```java
@ExtendWith(MockitoExtension.class) // This extension enables both @Mock and @InjectMocks
class UserServiceTest {

    @Mock
    private UserRepository userRepository; // The mock dependency

    @Mock
    private EmailService emailService; // Another mock dependency

    @InjectMocks
    private UserService userService; // The real object we are testing. Mocks above are injected into it.

    @Test
    void testRegisterUser() {
        // Now you can write a test for userService, and it will use the mocked repository and email service.
    }
}
```


### Lifecycle: Initializing Mocks

Annotations like `@Mock` and `@InjectMocks` need to be processed. You have two main options:

1. **`@ExtendWith(MockitoExtension.class)` (Best Practice)**: Add this annotation to your test class. It integrates Mockito with the JUnit 5 lifecycle, automatically initializing mocks before each test.
2. **`MockitoAnnotations.openMocks(this)`**: If you can't use the extension, you can manually initialize mocks in a `@BeforeEach` method.

```java
class UserServiceTest {
    @Mock private UserRepository userRepository;
    @InjectMocks private UserService userService;

    private AutoCloseable closeable;

    @BeforeEach
    void setUp() {
        closeable = MockitoAnnotations.openMocks(this); // Initialize mocks
    }

    @AfterEach
    void tearDown() throws Exception {
        closeable.close(); // Release mocks
    }
}
```


***
Would you like to continue with Section 8: Stubbing Behavior?

---

# yes

Of course. Here is the quick revision guide for Section 8.

### Section 8: Stubbing Behavior

"Stubbing" is the process of teaching your mock object how to behave when its methods are called. It's how you provide the "canned answers" or simulate the specific scenarios needed for your test. This is the core of **state verification**.

### `when(...).thenReturn(...)` (IMP)

This is the most fundamental stubbing technique. It tells a mock to return a specific value when a particular method is called with certain arguments.

* **Syntax**: `when(mockObject.method(arguments)).thenReturn(returnValue);`
* **BDD Style**: Mockito also offers a BDD-style alias, `given()`, which can improve readability: `given(mockObject.method(arguments)).willReturn(returnValue);`

```java
// Example with when(...).thenReturn(...)
@Test
void testFindUserById_shouldReturnUser() {
    // Arrange: Create a fake user to be returned by the mock
    User fakeUser = new User("testuser", "test@example.com");
    
    // Stubbing: Teach the mock to return the fakeUser when findById(1L) is called
    when(userRepository.findById(1L)).thenReturn(Optional.of(fakeUser));
    
    // Act
    Optional<User> foundUser = userService.findById(1L);
    
    // Assert
    assertTrue(foundUser.isPresent());
    assertEquals("testuser", foundUser.get().getUsername());
}
```


### `when(...).thenThrow(...)`

This is used to simulate error conditions by making a mock method throw an exception.

```java
// Example with when(...).thenThrow(...)
@Test
void testFindUserById_shouldThrowExceptionForInvalidId() {
    // Stubbing: Teach the mock to throw an exception for a specific ID
    when(userRepository.findById(99L)).thenThrow(new UserNotFoundException("User not found"));
    
    // Act & Assert
    assertThrows(UserNotFoundException.class, () -> {
        userService.findById(99L);
    });
}
```


### Stubbing Void Methods: The `do...()` Family (IMP)

What if you want to stub a method that returns `void`? You can't use `when(mock.voidMethod())` because the compiler expects a value inside `when()`. This is where the `do...()` family of methods is essential.

**Common Pitfall**: Trying to use `when()` for `void` methods is a classic beginner's mistake. The code won't compile. Always use a `do...()` method for `void`s.


| Method | Syntax | Use Case |
| :-- | :-- | :-- |
| **`doNothing()`** | `doNothing().when(mock).voidMethod();` | When you want a `void` method to do nothing at all (this is often the default behavior, but explicit stubbing can improve clarity). |
| **`doThrow()`** | `doThrow(new Exception()).when(mock).voidMethod();` | To make a `void` method throw an exception. |
| **`doAnswer()`** | `doAnswer(...).when(mock).voidMethod();` | For custom logic when a `void` method is called. |

```java
// Example with doThrow() for a void method
@Test
void testDeleteUser_shouldThrowExceptionIfUserHasActiveOrders() {
    // Stubbing: Teach the mock to throw an exception when trying to delete user 1L
    doThrow(new IllegalStateException("User has active orders"))
        .when(userRepository)
        .deleteById(1L);

    // Act & Assert
    assertThrows(IllegalStateException.class, () -> {
        userService.deleteUser(1L);
    });
}
```


### Returning Multiple Values

You can make a mock return different values on consecutive calls by chaining `thenReturn()`.

```java
// Example of returning multiple values
@Test
void testIterator() {
    Iterator<String> mockIterator = Mockito.mock(Iterator.class);
    
    // Stubbing: First call to next() returns "A", second "B", third "C"
    when(mockIterator.next()).thenReturn("A", "B", "C");

    assertEquals("A", mockIterator.next());
    assertEquals("B", mockIterator.next());
    assertEquals("C", mockIterator.next());
}
```


### Answering with Lambdas: `thenAnswer(...)`

For dynamic responses where the return value depends on the input arguments, `thenAnswer()` provides maximum flexibility.

**Analogy**: `thenReturn()` is like an actor reading a fixed script. `thenAnswer()` is like an improv comedian who creates a response on the spot based on the audience's suggestion (the input arguments).

```java
// Example with thenAnswer()
@Test
void testCreateUser_shouldReturnUserWithId() {
    // Stubbing: Use thenAnswer to dynamically handle the User object passed to save()
    when(userRepository.save(any(User.class))).thenAnswer(invocation -> {
        User userToSave = invocation.getArgument(0);
        userToSave.setId(1L); // Simulate the database assigning an ID
        return userToSave;
    });

    // Act
    User newUser = new User("newuser", "new@example.com");
    User savedUser = userService.registerUser(newUser);

    // Assert
    assertNotNull(savedUser.getId());
    assertEquals(1L, savedUser.getId());
}
```


***
Would you like to continue with Section 9: Verifying Behavior?

---

# yes

Of course. Here is the quick revision guide for Section 9.

### Section 9: Verifying Behavior

While stubbing is about setting up the state of your mocks (`when...then`), verification is about checking how your test subject interacted with its dependencies (`verify`). This is the core of **behavior verification** and is crucial for ensuring that your code not only produces the right result but also follows the correct process.

### `verify(mock).method()` (IMP)

This is the most basic verification. It checks if a specific method on a mock object was called at least once with the specified arguments. If the method was not called, the test fails.

```java
// Example with basic verify()
@Test
void testRegisterUser_shouldSendWelcomeEmail() {
    // Arrange
    User user = new User("testuser", "test@example.com");
    when(userRepository.save(any(User.class))).thenReturn(user);

    // Act
    userService.registerUser(user);

    // Assert (Behavior Verification)
    // Check that the sendWelcomeEmail method was called on the emailService mock
    // with the correct email address.
    verify(emailService).sendWelcomeEmail("test@example.com");
}
```


### Verifying Call Counts (IMP)

Often, just checking *if* a method was called isn't enough. You might need to ensure it was called a specific number of times, or not at all.


| Verification Mode | Description | Example |
| :-- | :-- | :-- |
| `times(n)` | Verifies the method was called exactly `n` times. | `verify(logger, times(2)).log("Event");` |
| `never()` | Verifies the method was **never** called. This is an alias for `times(0)`. | `verify(emailService, never()).sendPasswordResetEmail(anyString());` |
| `atLeastOnce()` | Verifies the method was called at least once. This is the default behavior of `verify()`. | `verify(cache, atLeastOnce()).put(any(), any());` |
| `atLeast(n)` | Verifies the method was called at least `n` times. | `verify(retryLogic, atLeast(3)).attemptConnection();` |
| `atMost(n)` | Verifies the method was called at most `n` times. | `verify(apiClient, atMost(5)).makeRequest();` |

```java
// Example with call count verification
@Test
void testProcessOrders_shouldNotNotifyAdminForSmallOrders() {
    // Arrange
    Order smallOrder = new Order(99.0); // An order below the notification threshold

    // Act
    orderProcessor.process(smallOrder);

    // Assert
    // Verify that the notificationService was never called for this small order
    verify(notificationService, never()).notifyAdmin(any(Order.class));
}
```


### `verifyNoMoreInteractions()`

This is a strict verification tool that fails the test if any interactions occurred with the given mock(s) that you haven't already explicitly verified.

* **Use Case**: To ensure that your code doesn't have any unexpected side effects or call dependencies when it shouldn't.
* **Common Pitfall**: Overusing `verifyNoMoreInteractions()` can make tests brittle. A small, harmless change in the implementation could break many tests. Use it judiciously, primarily when the absence of side effects is a critical requirement.

```java
@Test
void testSimpleQuery_shouldOnlyInteractWithRepository() {
    // Arrange & Act
    userService.findUserByUsername("test");

    // Assert
    verify(userRepository).findByUsername("test"); // Verify the expected interaction
    verifyNoMoreInteractions(userRepository);      // Ensure no other methods on the repo were called
    verifyNoInteractions(emailService);            // A stronger check that the mock was never touched at all
}
```


### Order Verification with `InOrder`

By default, `verify()` checks for interactions independently of their execution order. If the sequence of calls matters, you must use an `InOrder` verifier.

**Analogy**: A regular `verify()` is like a checklist: "Did you buy milk? Did you buy bread?". An `InOrder` verification is like a recipe: "Did you *first* mix the flour, and *then* add the eggs?".

```java
// Example with InOrder verification
@Test
void testSaveAndNotify_shouldSaveBeforeNotifying() {
    // Arrange
    User user = new User("test", "test@example.com");
    InOrder inOrder = Mockito.inOrder(userRepository, emailService); // Create an InOrder verifier for specific mocks

    // Act
    userService.registerUser(user);

    // Assert in order
    // 1. First, verify that save() was called on the repository.
    inOrder.verify(userRepository).save(user);
    // 2. Then, verify that sendWelcomeEmail() was called on the email service.
    inOrder.verify(emailService).sendWelcomeEmail("test@example.com");
}
```


***
Would you like to continue with Section 10: Argument Captors \& Matchers?

---

# yes

Of course. Here is the quick revision guide for Section 10.

### Section 10: Argument Captors \& Matchers

This section covers two powerful Mockito features that give you flexibility and precision when stubbing and verifying method calls.

### Built-in Argument Matchers (IMP)

Argument matchers allow you to stub or verify method calls without specifying the exact value of an argument. They provide flexibility by matching arguments based on type or other conditions. Matchers are used within `when()` and `verify()` calls.[^11_1]


| Matcher | Description | Example |
| :-- | :-- | :-- |
| `any()` | Matches any object, including null. For specific types, use `any(MyClass.class)`[^11_2]. | `when(mock.method(any(String.class))).thenReturn("result");` |
| `anyString()`, `anyInt()`, etc. | Type-safe matchers for common data types. They are slightly more efficient than `any(String.class)`[^11_2]. | `verify(mock).process(anyInt(), anyString());` |
| `eq(value)` | Matches a specific value. It is used to wrap a literal value so it can be used alongside other matchers[^11_3]. | `when(mock.method(anyString(), eq(100))).thenReturn("ok");` |
| `argThat(matcher)` | Matches an argument against a custom Hamcrest matcher or a lambda for complex validation. | `verify(mock).save(argThat(user -> user.isValid()));` |

#### Mixing Matchers \& Exact Values (A Critical Pitfall) (IMP)

Mockito requires that if you use an argument matcher for one argument in a method call, you **must use argument matchers for all arguments**. Mixing raw values with matchers will result in an `InvalidUseOfMatchersException`.[^11_3][^11_4]

* **Wrong**: `when(myMock.someMethod(anyString(), 5));`
    * This fails because `anyString()` is a matcher, but `5` is a raw value.
* **Correct**: `when(myMock.someMethod(anyString(), eq(5)));`
    * The `eq()` matcher wraps the raw value, satisfying Mockito's rule.[^11_3]


### Capturing Arguments: `ArgumentCaptor` (IMP)

Sometimes, you don't want to just match an argument; you want to **capture the actual object that was passed** to the mock so you can perform detailed assertions on it. This is the job of the `ArgumentCaptor`.[^11_5][^11_6]

**Analogy**: A matcher is like a bouncer checking IDs—they only care if you meet a general criterion (e.g., "over 21"). An `ArgumentCaptor` is like a security camera—it records the exact person who entered (`capture()`), so you can later review the footage (`getValue()`) to check specific details about them (e.g., what they were wearing).

#### How to Use `ArgumentCaptor`

Using an `ArgumentCaptor` is a three-step process:[^11_7]

1. **Create the Captor**: Instantiate an `ArgumentCaptor` for the type you want to capture.
2. **Capture the Argument**: Use the captor's `.capture()` method inside a `verify()` call.
3. **Assert the Captured Value**: Get the captured value using `.getValue()` and perform assertions on it.[^11_7]
```java
// Example of ArgumentCaptor
@Test
void testRegisterUser_shouldSaveUserWithCorrectDetails() {
    // 1. Create the captor for the User class
    ArgumentCaptor<User> userCaptor = ArgumentCaptor.forClass(User.class);
    
    // Act: Call the method under test
    userService.register("John Doe", "john.doe@example.com");
    
    // 2. Capture the argument passed to the repository's save method
    verify(userRepository).save(userCaptor.capture());
    
    // 3. Get the captured value and assert its properties
    User capturedUser = userCaptor.getValue();
    assertEquals("John Doe", capturedUser.getName());
    assertNotNull(capturedUser.getRegistrationTimestamp());
    assertTrue(capturedUser.isActive());
}
```


### Capturing Multiple Arguments

If a method is called multiple times, you can capture the argument for each call.

* Use `verify(mock, times(n)).method(captor.capture())` to capture arguments from multiple calls.
* Use `getAllValues()` to retrieve all captured arguments as a `List<T>`.[^11_6]

```java
// Example of capturing multiple values
@Test
void testAddMultipleProductsToCart() {
    // Arrange
    ArgumentCaptor<String> productCaptor = ArgumentCaptor.forClass(String.class);

    // Act
    cartService.addProduct("Apple");
    cartService.addProduct("Banana");

    // Capture arguments from two calls
    verify(cartRepository, times(2)).add(productCaptor.capture());

    // Assert all captured values
    List<String> capturedProducts = productCaptor.getAllValues();
    assertEquals(List.of("Apple", "Banana"), capturedProducts);
}
```


***
Would you like to continue with Section 11: Spies vs Mocks?
<span style="display:none">[^11_10][^11_11][^11_12][^11_13][^11_14][^11_15][^11_16][^11_17][^11_18][^11_19][^11_20][^11_21][^11_22][^11_23][^11_24][^11_25][^11_26][^11_8][^11_9]</span>

```
<div style="text-align: center">⁂</div>
```

[^11_1]: https://www.digitalocean.com/community/tutorials/mockito-argument-matchers-any-eq

[^11_2]: https://www.softwaretestinghelp.com/mockito-matchers/

[^11_3]: https://mangohost.net/blog/mockito-argument-matchers-any-eq/

[^11_4]: https://github.com/mockito/mockito/issues/1398

[^11_5]: https://www.baeldung.com/mockito-argumentcaptor

[^11_6]: https://www.digitalocean.com/community/tutorials/mockito-argumentcaptor-captor-annotation

[^11_7]: https://www.browserstack.com/guide/mockito-argumentcaptor

[^11_8]: https://stackoverflow.com/questions/36253040/example-of-mockitos-argumentcaptor

[^11_9]: https://www.browserstack.com/guide/how-to-use-argumentcaptor-in-mockito-for-effective-java-testing

[^11_10]: https://dev.to/pathus90/understanding-argumentcaptor-in-mockito-a-comprehensive-guide-2ehe

[^11_11]: https://site.mockito.org/javadoc/current/org/mockito/ArgumentCaptor.html

[^11_12]: https://www.baeldung.com/mockito-argument-matchers

[^11_13]: https://stackoverflow.com/questions/63481301/can-i-mix-one-matcher-and-1-exact-value-in-mockito-arguments

[^11_14]: https://davidvlijmincx.com/posts/mockito_argumentcaptor/

[^11_15]: https://site.mockito.org/javadoc/current/org/mockito/ArgumentMatchers.html

[^11_16]: https://www.toptal.com/java/a-guide-to-everyday-mockito

[^11_17]: https://www.appsdeveloperblog.com/mockito-argument-matchers-examples-and-usage/

[^11_18]: https://petertackage.com/posts/mockito-argument-matcher-pitfalls

[^11_19]: https://stackoverflow.com/questions/61165645/mockito-argument-matcher-for-java-8-functions

[^11_20]: https://moldstud.com/articles/p-enhance-your-java-test-cases-with-custom-matchers-in-mockito

[^11_21]: https://www.javacodegeeks.com/2024/11/mastering-mockito-argument-captors.html

[^11_22]: https://codemia.io/knowledge-hub/path/can_mockito_capture_arguments_of_a_method_called_multiple_times

[^11_23]: https://wesome.org/mockito-3-argument-captor

[^11_24]: https://stackoverflow.com/questions/7500312/mockito-match-any-class-argument

[^11_25]: https://codemia.io/knowledge-hub/path/mockito_match_any_class_argument

[^11_26]: https://www.javadoc.io/doc/org.mockito/mockito-core/4.9.0/org/mockito/ArgumentMatchers.html


---

# yes

Of course. Here is the quick revision guide for Section 11.

### Section 11: Spies vs. Mocks

Understanding the difference between a mock and a spy is a frequent and important interview topic. While both are "test doubles," they have fundamentally different behaviors and use cases.

### Difference Between `mock()` and `spy()` (IMP)

The core difference lies in their default behavior.


| Feature | `Mockito.mock(Class)` | `Mockito.spy(Object)` |
| :-- | :-- | :-- |
| **Nature** | **A complete fake.** It's a "hollow" shell of the class with no real logic[^12_1]. | **A wrapper around a real object.** It's the real instance with a "spying" layer on top[^12_2]. |
| **Default Behavior** | Methods do nothing and return default values (0, false, null) unless stubbed. | Methods execute the **actual code** from the real object unless stubbed[^12_2]. |
| **Creation** | `mock(List.class)` creates a new, fake `List`. | `spy(new ArrayList<>())` wraps an existing, real `ArrayList` instance[^12_2]. |
| **Use Case** | Isolate the class under test from its dependencies completely. | Test a class while still using most of its real logic, but overriding one or two specific methods[^12_3]. |

**Analogy: A Movie Stunt**

* **Mock**: A CGI character. It's created from scratch and has no connection to a real actor. You have to program every movement and expression (`when(...).thenReturn(...)`).
* **Spy**: The actual actor performing most of their own scenes. A stunt double (`doReturn(...)`) is only brought in for a single, dangerous scene (e.g., a method that calls an external API). The rest of the time, you're watching the real actor.


### `Mockito.spy()` for Partial Mocking

A "spy" allows for **partial mocking**, where you use a real object but override the behavior of only a few of its methods. This is useful for legacy code or when you want to avoid mocking a complex object entirely.[^12_3]

You can create a spy using `Mockito.spy(realObject)` or the `@Spy` annotation.

```java
// Example: Spying on a real ArrayList
@Test
void testSpyOnRealList() {
    // Arrange: Create a real list and wrap it in a spy
    List<String> realList = new ArrayList<>();
    List<String> spyList = Mockito.spy(realList);

    // Act: Call real methods on the spy
    spyList.add("one");
    spyList.add("two");

    // Assert: Verify real method calls
    verify(spyList).add("one");
    assertEquals(2, spyList.size()); // The real size() method is called

    // Stubbing a method on the spy
    // Now, when size() is called, it will return the stubbed value instead of the real one.
    when(spyList.size()).thenReturn(100);
    assertEquals(100, spyList.size());
}
```


### Stubbing Real Objects with Spies (A Critical Pitfall) (IMP)

When stubbing a spy, using `when(spy.method()).thenReturn()` can be dangerous because **it calls the real method first**. If the real method has side effects (like making a network call or throwing an exception), this will happen during the stubbing process itself.[^12_4]

**The Safe Way to Stub Spies**: Use the `doReturn(...).when(...)` syntax. This approach does **not** call the real method.

* **Risky**: `when(spy.get("key")).thenReturn("value");`
    * This calls the real `get("key")` method before stubbing it.
* **Safe**: `doReturn("value").when(spy).get("key");`
    * This bypasses the real method call entirely, safely replacing its behavior.

```java
// Example of the pitfall and the correct approach
@Test
void testSpyStubbing() {
    List<String> realList = new ArrayList<>();
    List<String> spyList = spy(realList);

    // Pitfall: This calls the real get(0) method, which throws an IndexOutOfBoundsException
    // because the list is empty.
    // assertThrows(IndexOutOfBoundsException.class, () -> {
    //     when(spyList.get(0)).thenReturn("stubbed value");
    // });

    // Correct Way: Use doReturn() to avoid calling the real method during stubbing.
    doReturn("stubbed value").when(spyList).get(0);
    
    // Now the stub works correctly.
    assertEquals("stubbed value", spyList.get(0));
}
```

**Best Practice**: Always use the `doReturn()`, `doThrow()`, or `doAnswer()` family of methods when stubbing spies to prevent unexpected side effects.

***
Would you like to continue with Section 12: Advanced Mockito Usage?
<span style="display:none">[^12_10][^12_11][^12_12][^12_13][^12_14][^12_15][^12_16][^12_17][^12_18][^12_5][^12_6][^12_7][^12_8][^12_9]</span>

```
<div style="text-align: center">⁂</div>
```

[^12_1]: https://intellipaat.com/blog/tutorial/mockito-tutorial/mockito-mock-vs-spy/

[^12_2]: https://www.browserstack.com/guide/mockito-spy-vs-mockito-mock

[^12_3]: https://www.testim.io/blog/mockito-spy/

[^12_4]: https://codemia.io/knowledge-hub/path/mockito_trying_to_spy_on_method_is_calling_the_original_method

[^12_5]: https://www.baeldung.com/mockito-spy

[^12_6]: https://stackoverflow.com/questions/11620103/mockito-trying-to-spy-on-method-is-calling-the-original-method

[^12_7]: https://stackoverflow.com/questions/15052984/what-is-the-difference-between-mocking-and-spying-when-using-mockito

[^12_8]: https://www.javacodegeeks.com/2015/11/mocks-spies-partial-mocks-and-stubbing.html

[^12_9]: https://site.mockito.org/javadoc/current/org/mockito/Spy.html

[^12_10]: https://stackoverflow.com/questions/28295625/mockito-spy-vs-mock

[^12_11]: https://www.j-labs.pl/en/tech-blog/mocks-stubs-and-spies-in-unit-testing-based-on-mockito/

[^12_12]: https://davidvlijmincx.com/posts/mockito-spy/

[^12_13]: https://stackoverflow.com/questions/12827580/mocking-vs-spying-in-mocking-frameworks

[^12_14]: https://labex.io/tutorials/java-spy-in-mockito-117989

[^12_15]: https://keploy.io/blog/community/mockito-spy-your-complete-guide-to-testing

[^12_16]: https://testrigor.com/blog/mocks-spies-and-stubs/

[^12_17]: https://www.baeldung.com/mockito-annotations

[^12_18]: https://www.youtube.com/watch?v=PJNcxY4I1F8


---

# yes

Of course. Here is the quick revision guide for Section 12.

### Section 12: Advanced Mockito Usage

This section covers powerful, but less common, Mockito features for handling difficult testing scenarios involving `final` classes, `static` methods, `private` methods, and constructors. These are often considered "code smells" in test design, but are sometimes necessary for legacy code.

### Mocking Final Classes \& Static Methods (IMP)

Historically, Mockito could not mock `final` classes or `static` methods, requiring the use of external tools like PowerMock. Modern versions of Mockito have largely eliminated this need.

* **Mocking `final` classes/methods**: Since Mockito 2.1.0, this is possible by using the "inline mock maker." You enable it by swapping the `mockito-core` dependency for `mockito-inline`. With Mockito 5.0 and newer, this is the default behavior.[^13_1][^13_2][^13_3]
* **Mocking `static` methods (Mockito 3.4.0+)**: Mockito can now mock static method calls directly using `Mockito.mockStatic()`. This creates a "scoped mock" that is active only within a `try-with-resources` block, ensuring that the static mock does not leak between tests.[^13_4]

```java
// Example of mocking a static method
@Test
void testStaticMethod() {
    // This will fail without mocking: assertEquals("real value", MyUtility.getStaticValue());

    // Create a scoped mock for all static methods in MyUtility class
    try (MockedStatic<MyUtility> mocked = Mockito.mockStatic(MyUtility.class)) {
        // Stub the static method
        mocked.when(MyUtility::getStaticValue).thenReturn("mocked value");

        // Assert the mocked behavior
        assertEquals("mocked value", MyUtility.getStaticValue());
        
        // You can also verify static calls
        mocked.verify(MyUtility::getStaticValue);
    }
    
    // Outside the try block, the static method has its original behavior again.
    assertEquals("real value", MyUtility.getStaticValue());
}
```


### Deep Stubs (`RETURNS_DEEP_STUBS`)

Deep stubs are a controversial feature used to simplify stubbing for fluent APIs where method calls are chained (e.g., a Builder pattern). Instead of manually mocking each object in the chain, `RETURNS_DEEP_STUBS` tells Mockito to automatically return a mock from each method call.[^13_5]

* **Use Case**: Testing code that uses a fluent API like `webClient.get().uri(...).retrieve().bodyToMono(...)`.[^13_5]
* **Warning (IMP)**: Overusing deep stubs is an anti-pattern. It makes tests extremely brittle and tightly coupled to the implementation. If a method in the chain changes, the test breaks. It's often called a "mocking hell". Only use it as a last resort.[^13_5]

```java
// Example of deep stubs
WebClient webClientMock = mock(WebClient.class, RETURNS_DEEP_STUBS);

// Stub the end of the chain without mocking intermediate steps
when(webClientMock.get().uri("/api").retrieve()).thenReturn(someResponse);
```


### Mocking Private Methods

Mockito, by design, **cannot mock private methods**. This is intentional, as a unit test should focus on the public API of a class, treating its internal implementation as a black box. The need to mock a private method often indicates a design problem.

**Workarounds (to be used with caution)**:

1. **Refactor**: The best solution. If a private method contains complex logic, extract it into a new class with a public method. You can then mock this new dependency.
2. **Change Access Modifier \& Spy**: Change the method from `private` to package-private (default access) and use a `Mockito.spy()` to stub it. This is less intrusive than PowerMock but still modifies production code for testing purposes.[^13_6]
3. **PowerMock**: The traditional tool for this. It uses bytecode manipulation to mock private methods but adds complexity and can be fragile.[^13_7][^13_8]

### Mocking Constructors (Mockito 3.5.0+)

Sometimes, your class under test creates a `new` instance of an object inside a method (e.g., `new Date()` or `new HttpClient()`). Mockito's `mockConstruction()` allows you to intercept these constructor calls and return a mock instead.[^13_9]

* Like `mockStatic()`, this is a scoped feature used within a `try-with-resources` block.[^13_10]
* It is enabled by using the `mockito-inline` dependency.[^13_10]

```java
// Example of mocking a constructor
@Test
void testMethodThatCreatesObject() {
    // Within this block, any "new MyCollaborator()" will return a mock
    try (MockedConstruction<MyCollaborator> mocked = mockConstruction(MyCollaborator.class,
            (mock, context) -> {
                // Stub the methods of the mock that will be created
                when(mock.doWork()).thenReturn("mocked work");
            })) {
        
        MyService service = new MyService();
        
        // The service internally creates a MyCollaborator instance, but gets our mock instead.
        String result = service.businessLogic();
        
        assertEquals("mocked work", result);
    }
}
```


***
Would you like to continue with Section 13: Mocking in Spring Context?
<span style="display:none">[^13_11][^13_12][^13_13][^13_14][^13_15][^13_16][^13_17][^13_18][^13_19][^13_20]</span>

```
<div style="text-align: center">⁂</div>
```

[^13_1]: https://www.baeldung.com/mockito-final

[^13_2]: https://www.infoq.com/news/2023/01/mockito-5/

[^13_3]: https://davidvlijmincx.com/posts/mockito_mock_final_methods_and_classes/

[^13_4]: https://www.baeldung.com/mockito-mock-static-methods

[^13_5]: https://rieckpil.de/creating-deep-stubs-with-mockito-to-chain-method-stubbing/

[^13_6]: https://dzone.com/articles/mock-private-method

[^13_7]: https://www.softwaretestinghelp.com/mock-private-static-void-methods-mockito/

[^13_8]: https://www.baeldung.com/powermock-private-method

[^13_9]: https://www.browserstack.com/guide/mockito-mock-constructor

[^13_10]: https://docs.diffblue.com/features/cover-cli/project-configuration/mocking

[^13_11]: https://stackoverflow.com/questions/26700860/how-do-i-mock-a-static-method-in-final-class

[^13_12]: https://www.browserstack.com/guide/mockito-mock-static-method

[^13_13]: https://www.testim.io/blog/mocking-static-methods-mockito/

[^13_14]: https://www.baeldung.com/mockito-fluent-apis

[^13_15]: https://stackoverflow.com/questions/19963622/mockito-verify-mock-with-returns-deep-stubs-returns-more-calls-than-expecte

[^13_16]: https://stackoverflow.com/questions/8799439/testing-private-method-using-mockito

[^13_17]: https://www.baeldung.com/java-mockito-constructors-unit-testing

[^13_18]: https://www.youtube.com/watch?v=9Tj2Wpcnp9A

[^13_19]: https://github.com/mockito/mockito/issues/3378

[^13_20]: https://stackoverflow.com/questions/13364406/mock-a-constructor-with-parameter


---

# yes

Of course. Here is the quick revision guide for Section 13.

### Section 13: Mocking in Spring Context

When testing a Spring Boot application, you often need to mock beans within the Spring `ApplicationContext` itself. This is different from a plain unit test, as the mocks need to integrate with Spring's dependency injection framework.

### `@MockBean` \& `@SpyBean` (IMP)

Spring Boot provides two powerful annotations for this purpose. They replace a real bean in the application context with a mock or a spy for the duration of a single test class.[^14_1]


| Annotation | Description | Use Case |
| :-- | :-- | :-- |
| **`@MockBean`** | Replaces an existing bean in the context with a complete Mockito mock. If no bean of that type exists, it adds the mock to the context[^14_2]. | When you want to **completely isolate** your test subject from a dependency. For example, mocking an `EmailService` so no actual emails are sent[^14_3]. |
| **`@SpyBean`** | Wraps an existing real bean with a Mockito spy. The real bean must exist in the context[^14_4]. | When you want to use the **real behavior** of a bean but need to stub or verify a few of its methods. For example, using a real `PaymentService` but stubbing its external `validatePayment()` method[^14_1]. |

**Analogy**: `@MockBean` is like replacing a real actor with a CGI stand-in for the entire film shoot. `@SpyBean` is like keeping the real actor but using a stunt double for one specific scene.

```java
// Example using @MockBean and @SpyBean
@SpringBootTest
class UserServiceIntegrationTest {

    @Autowired
    private UserService userService; // The real service we are testing

    @MockBean
    private UserRepository userRepository; // Replaced with a complete mock

    @SpyBean
    private AuditService auditService; // The real bean is wrapped in a spy

    @Test
    void testRegisterUser_shouldSaveUserAndLogAudit() {
        // Arrange (Stubbing the mock)
        User user = new User("testuser");
        when(userRepository.save(any(User.class))).thenReturn(user);

        // Arrange (Stubbing a method on the spy)
        // We use doNothing() because logEvent is a void method
        doNothing().when(auditService).logEvent(anyString());

        // Act
        userService.register(user);

        // Assert
        verify(userRepository).save(user); // Verify interaction with the mock
        verify(auditService).logEvent("User testuser registered"); // Verify interaction with the spy
    }
}
```


### Testing with Spring Profiles \& Properties

**Spring Profiles** allow you to define different bean configurations for different environments (e.g., `dev`, `test`, `prod`). In tests, you can activate a specific profile using `@ActiveProfiles("test")` to load a test-specific configuration (e.g., an in-memory H2 database instead of a real one).[^14_5][^14_6]

**Overriding Properties in Tests (IMP)**
It's often necessary to override `application.properties` values in tests.


| Method | Description | Example |
| :-- | :-- | :-- |
| `@TestPropertySource` | An annotation that lets you specify properties directly or load them from a file for a test class. | `@TestPropertySource(properties = "feature.toggle=true")`[^14_7] |
| `@SpringBootTest(properties=...)` | Allows you to define properties directly on the `@SpringBootTest` annotation. | `@SpringBootTest(properties = "api.key=test-key")`[^14_8] |
| `application-test.properties` | Create a properties file in `src/test/resources`. If a "test" profile is active, Spring Boot will automatically load it. |  |

### Mocking External Services (REST, DB, etc.) in Spring Boot

In integration tests (`@SpringBootTest`), you don't want to make real network calls to external APIs or message queues.

1. **Mock the Client Bean (Most Common)**: Use `@MockBean` to replace the client that communicates with the external service (e.g., your `RestTemplate` wrapper or `KafkaProducer`). This is simple and effective for testing your service logic in isolation from the external system.[^14_3]
2. **Use a Mock Server (Higher Fidelity)**: For more realistic testing that includes HTTP serialization and network behavior, use tools like **WireMock** or **Testcontainers**.
    * **WireMock**: A library that runs a mock HTTP server. You can stub specific endpoints to return canned responses. You would then point your application to the WireMock server's URL using `@TestPropertySource`.[^14_7]
    * **Testcontainers**: A library that lets you run real services (like a database, Kafka, or a mock server) in Docker containers during your tests. This provides the highest level of confidence that your integration works correctly.

***
Would you like to continue with Section 14: TDD (Test-Driven Development)?
<span style="display:none">[^14_10][^14_11][^14_12][^14_13][^14_14][^14_15][^14_16][^14_17][^14_18][^14_19][^14_20][^14_9]</span>

```
<div style="text-align: center">⁂</div>
```

[^14_1]: https://scalablehuman.com/2023/11/16/advanced-mocking-techniques-with-spring-boot-mastering-spybean-and-mockbean/

[^14_2]: https://blog.stackademic.com/understanding-spybean-and-mockbean-in-spring-boot-testing-10f35c8ca283

[^14_3]: https://www.arhohuttunen.com/spring-boot-integration-testing/

[^14_4]: https://www.baeldung.com/spring-spy-vs-spybean

[^14_5]: https://dev.to/isaactony/how-to-use-spring-profiles-in-your-spring-boot-application-o18

[^14_6]: https://www.codingshuttle.com/spring-boot-handbook/spring-profiles

[^14_7]: https://www.browserstack.com/guide/java-mock-server-setup-tutorial

[^14_8]: https://www.baeldung.com/spring-tests-override-properties

[^14_9]: https://stackoverflow.com/questions/43999517/what-is-difference-between-spybean-and-mockbean-in-mockito

[^14_10]: https://docs.spring.io/spring-framework/reference/testing/annotations/integration-spring/annotation-mockitobean.html

[^14_11]: https://stackoverflow.com/questions/44639941/overriding-value-in-integration-test

[^14_12]: https://docs.openrewrite.org/recipes/java/spring/boot3/replacemockbeanandspybean

[^14_13]: http://www.everydayunittesting.com/2019/01/integration-testing-with-spring-profiles.html

[^14_14]: https://www.youtube.com/watch?v=286xwHGMRHg

[^14_15]: https://github.com/spring-projects/spring-boot/issues/34768

[^14_16]: https://www.diffblue.com/resources/guide-to-overriding-spring-boot-properties-for-testing/

[^14_17]: https://stackoverflow.com/questions/29550098/mock-external-server-during-integration-testing-with-spring

[^14_18]: https://alexis-segura.com/notes/spring-boot-mockbean-and-spybean-are-saying-goodbye/

[^14_19]: https://stackoverflow.com/questions/39690094/spring-boot-default-profile-for-integration-tests

[^14_20]: https://testcontainers.com/guides/testing-rest-api-integrations-using-mockserver/


---

# yes

Of course. Here is the quick revision guide for Section 14.

### Section 14: TDD (Test-Driven Development)

Test-Driven Development (TDD) is a software development methodology where you write tests *before* you write the production code. This "test-first" approach flips traditional development on its head and ties testing directly into the design process.[^15_1][^15_2]

**Analogy: Building with a Blueprint**

* **Traditional Development**: Like building a house without a detailed plan. You build a room, then check if it's the right size. It's easy to make mistakes that require costly rework.
* **TDD**: Like creating a detailed architectural blueprint first. You decide exactly where every door and window should go (`write the test`). Then, you build the walls to match the blueprint (`write the code`). The blueprint guides your construction and ensures you build exactly what you planned.


### Red → Green → Refactor Cycle (IMP)

TDD is defined by a simple, repetitive cycle with three phases:[^15_3]

1. **Red Phase**: **Write a failing test.**
    * Think about a small piece of functionality you need. Write a unit test that defines how that feature should work.
    * Run the test. It **must fail** because the implementation code doesn't exist yet. If it passes, your test is either wrong or testing something that already works. This step is crucial for verifying that your test is valid.[^15_4][^15_5]
2. **Green Phase**: **Write the simplest code to make the test pass.**
    * Write the absolute minimum amount of production code needed to satisfy the test.
    * Don't worry about elegance or efficiency at this stage. The goal is to get a "green" signal from your testing framework as quickly as possible.[^15_4]
3. **Refactor Phase**: **Clean up the code.**
    * Now that you have a passing test acting as a safety net, you can improve the code you just wrote.
    * Remove duplication, improve naming, and enhance the structure without changing its external behavior.[^15_6]
    * Rerun the test to ensure your refactoring didn't break anything. The test should still be green.

This cycle is repeated for every new piece of functionality, creating a robust, well-tested codebase incrementally.

### Example: Designing an API with TDD

Let's design a simple `Calculator.add(a, b)` method using TDD.

1. **Red**: Write a test for adding two positive numbers.

```java
@Test
void testAdd_shouldReturnSumOfTwoPositiveNumbers() {
    Calculator calculator = new Calculator();
    assertEquals(5, calculator.add(2, 3)); // Fails: The 'add' method doesn't exist yet.
}
```

2. **Green**: Write the simplest code to make it pass.

```java
public class Calculator {
    public int add(int a, int b) {
        return 5; // Good enough to make the test pass!
    }
}
```

3. **Refactor**: The code is simple, but it's wrong. Let's write another test to force a better implementation.

***

4. **Red**: Write a test for a different set of numbers.

```java
@Test
void testAdd_shouldHandleDifferentNumbers() {
    Calculator calculator = new Calculator();
    assertEquals(10, calculator.add(7, 3)); // Fails: The method currently always returns 5.
}
```

5. **Green**: Write the correct implementation.

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b; // Now this is the correct, simple implementation.
    }
}
```

6. **Refactor**: The code is clean and correct. No refactoring is needed. We can continue to add more tests for edge cases (e.g., negative numbers, zero).

### Common Pitfalls in TDD

* **Writing tests that are too large**: A TDD test should be small and focused on one specific behavior. Large tests make the Red-Green-Refactor cycle slow and difficult.
* **Forgetting to run the test and see it fail (Red phase)**: Skipping this step can lead to "false positives"—tests that pass for the wrong reasons, providing a false sense of security.[^15_5]
* **Skipping the Refactor phase**: Once the test is green, it's tempting to move on. Neglecting to refactor leads to technical debt and makes the code harder to maintain.[^15_5]
* **Writing production code during the Red phase**: The discipline of TDD requires you to only write code in response to a failing test.
* **Testing implementation details**: Tests should focus on public behavior, not the internal implementation. Tying tests to private methods makes refactoring difficult.

***
Would you like to continue with Section 15: Coverage \& Quality?
<span style="display:none">[^15_10][^15_11][^15_12][^15_13][^15_14][^15_15][^15_16][^15_17][^15_18][^15_19][^15_20][^15_7][^15_8][^15_9]</span>

```
<div style="text-align: center">⁂</div>
```

[^15_1]: https://developer.ibm.com/articles/5-steps-of-test-driven-development/

[^15_2]: https://www.browserstack.com/guide/what-is-test-driven-development

[^15_3]: https://www.qodo.ai/glossary/red-green-refactor/

[^15_4]: https://www.ranorex.com/blog/a-guide-to-test-driven-development-tdd/

[^15_5]: https://www.thesecretdeveloper.com/blog/the-most-common-mistakes-in-test-driven-development

[^15_6]: https://dev.to/mungaben/the-tdd-cycle-red-green-refactor-1aaf

[^15_7]: https://www.geeksforgeeks.org/software-engineering/test-driven-development-tdd/

[^15_8]: https://brainhub.eu/library/test-driven-development-tdd

[^15_9]: https://www.testrail.com/blog/test-driven-development/

[^15_10]: https://www.practitest.com/resource-center/article/tdd-guide/

[^15_11]: https://smartbear.com/blog/basics-of-test-driven-development-tdd/

[^15_12]: https://www.codecademy.com/article/tdd-red-green-refactor

[^15_13]: https://www.statsig.com/perspectives/tdd-principles-tools-pitfalls

[^15_14]: https://testdriven.io/test-driven-development/

[^15_15]: http://www.jamesshore.com/v2/blog/2005/red-green-refactor

[^15_16]: https://www.youtube.com/watch?v=1pPeV5Ik_30

[^15_17]: https://agilealliance.org/glossary/tdd/

[^15_18]: https://martinfowler.com/bliki/TestDrivenDevelopment.html

[^15_19]: https://www.pluralsight.com/resources/blog/software-development/test-driven-development-implementation

[^15_20]: https://www.youtube.com/watch?v=B1j6k2j2eJg


---

# yes

Of course. Here is the quick revision guide for Section 15.

### Section 15: Coverage \& Quality

Writing tests is only half the battle; you also need to measure their effectiveness. This section covers how to measure test coverage, assess test quality, and deal with unreliable tests.

### Measuring Coverage with JaCoCo (IMP)

**Code coverage** is a metric that measures what percentage of your production code is executed by your automated tests. It helps identify parts of your application that are not tested.[^16_1]

**JaCoCo (Java Code Coverage)** is the standard tool for measuring code coverage in the Java ecosystem. It integrates with build tools like Maven and Gradle to generate detailed HTML reports.[^16_2][^16_3]

**How to set up JaCoCo (with Maven)**:
Add the `jacoco-maven-plugin` to your `pom.xml`. The plugin will automatically attach to the `test` phase of your build.

```xml
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <version>0.8.11</version>
    <executions>
        <execution>
            <goals>
                <goal>prepare-agent</goal>
            </goals>
        </execution>
        <execution>
            <id>report</id>
            <phase>test</phase>
            <goals>
                <goal>report</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

After running `mvn clean install`, the report will be generated in `target/site/jacoco/index.html`.

**Common Pitfall**: Treating 100% coverage as the ultimate goal. High coverage is good, but it doesn't guarantee your tests are meaningful. A test can execute a line of code without actually asserting its behavior, giving a false sense of security.

### Mutation Testing (IMP)

While code coverage asks, "Is this line of code *executed*?", mutation testing asks, "If this line of code were to change, would any of my tests *fail*?". It is a much more powerful way to assess the quality of your tests.

**Analogy: The Sabotaged Component**

* **Code Coverage**: You test a car by turning it on to see if the engine runs. This "covers" the engine.
* **Mutation Testing**: An engineer secretly sabotages a tiny part of the engine (e.g., loosens a spark plug wire). You then run your tests again. If your tests still pass, it means they weren't thorough enough to detect the sabotage. If they fail, your tests are effective.

**How it works**:

1. A mutation testing tool takes your source code and creates many slightly modified versions, called "mutants." Each mutant has a small change (e.g., `a + b` becomes `a - b`, `if (x > y)` becomes `if (x >= y)`).
2. Your entire test suite is run against each mutant.
3. If a test fails, the mutant is considered "killed." If all tests pass, the mutant "survives."
4. The quality of your test suite is measured by the **mutation score**: `(Killed Mutants / Total Mutants) * 100`.

**Popular Tools**:

* **PIT (pitest)**: The most popular mutation testing tool for Java.[^16_4]
* **Stryker**: A popular tool for JavaScript, C\#, and Scala.[^16_5]


### Flaky Test Detection \& Elimination

A **flaky test** is a test that can both pass and fail without any changes to the code. Flaky tests are a major problem in CI/CD because they erode trust in the test suite and slow down development.[^16_6]

**Common Causes of Flakiness**:

* **Asynchronicity**: Tests that don't properly wait for asynchronous operations to complete (e.g., a `Future` or a message queue operation).
* **Order Dependency**: Tests that pass only when run in a specific order. Unit tests should always be independent.[^16_6]
* **External Dependencies**: Relying on unstable external services, networks, or databases that may be slow or temporarily unavailable.[^16_6]
* **Concurrency**: Issues like race conditions in code that uses multiple threads.
* **Randomness**: Using random data in tests can lead to unpredictable outcomes.

**How to Fix Flaky Tests**:

1. **Identify them**: Rerunning failed tests is the most common way to spot a flaky test. If it passes on the second run, it's likely flaky. Many CI tools can automate this detection.[^16_7]
2. **Isolate the cause**: Check for the common causes listed above.
3. **Make them deterministic**:
    * For async code, use libraries like Awaitility to wait for conditions instead of using `Thread.sleep()`.
    * Ensure each test cleans up after itself in `@AfterEach`.
    * Replace random values with fixed test data.

***
Would you like to continue with Section 16: CI/CD \& Test Reports?
<span style="display:none">[^16_10][^16_11][^16_12][^16_13][^16_14][^16_15][^16_16][^16_17][^16_18][^16_19][^16_20][^16_8][^16_9]</span>

```
<div style="text-align: center">⁂</div>
```

[^16_1]: https://www.baeldung.com/jacoco

[^16_2]: https://www.eclemma.org/jacoco/

[^16_3]: https://www.geeksforgeeks.org/java/how-to-generate-code-coverage-report-with-jacoco-in-java-application/

[^16_4]: https://www.browserstack.com/guide/mutation-analysis-in-software-testing

[^16_5]: https://stryker-mutator.io

[^16_6]: https://www.testrail.com/blog/flaky-tests/

[^16_7]: https://circleci.com/blog/reducing-flaky-test-failures/

[^16_8]: https://www.jacoco.org/jacoco/trunk/index.html

[^16_9]: https://www.youtube.com/watch?v=m57hpoXO6a4

[^16_10]: https://docs.gradle.org/current/userguide/jacoco_plugin.html

[^16_11]: https://www.weetechsolution.com/blog/best-tools-of-mutation-testing

[^16_12]: https://stackoverflow.com/questions/22836455/jacoco-report-generation-using-maven

[^16_13]: https://www.datadoghq.com/knowledge-center/flaky-tests/

[^16_14]: https://github.com/jacoco/jacoco

[^16_15]: https://stryker-mutator.io/docs/

[^16_16]: https://www.browserstack.com/test-reporting-and-analytics/features/test-reporting/what-is-flaky-test

[^16_17]: https://docs.gitlab.com/ci/testing/code_coverage/jacoco/

[^16_18]: https://learn.microsoft.com/en-us/dotnet/core/testing/mutation-testing

[^16_19]: https://testomat.io/blog/overcome-flaky-tests-straggle-flakiness-in-your-test-framework/

[^16_20]: https://github.com/stryker-mutator/stryker-net


---

# yes

Of course. Here is the quick revision guide for Section 16.

### Section 16: CI/CD \& Test Reports

Integrating automated tests into a Continuous Integration/Continuous Deployment (CI/CD) pipeline is the ultimate goal of test automation. This ensures that every code change is automatically built and verified, providing rapid feedback to developers.

### Running Tests in Pipelines

CI servers like **GitHub Actions**, GitLab CI, or Jenkins are configured to automatically execute your test suite whenever new code is pushed.

A typical workflow in **GitHub Actions** for a Maven project looks like this:

1. **Trigger**: The workflow runs on every `push` to the `main` branch or on a `pull_request`.
2. **Checkout**: The runner checks out the repository code.[^17_1]
3. **Set up JDK**: The correct Java version is installed on the runner.
4. **Run Tests**: The build tool is invoked to compile the code and run the tests (e.g., `mvn clean install`).[^17_2]

If any test fails, the command will exit with a non-zero status code, causing the pipeline step to fail and blocking the code from being merged or deployed.

```yaml
# Example GitHub Actions workflow for a Java project
name: Java CI with Maven

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Set up JDK 17
      uses: actions/setup-java@v3
      with:
        java-version: '17'
        distribution: 'temurin'
    - name: Build with Maven
      run: mvn -B package --file pom.xml
```


### Generating Reports (JUnit XML, HTML)

Test runners produce standardized reports that CI tools can parse to display results.

* **JUnit XML Format**: This is the de-facto standard. Tools like Maven Surefire generate an XML file for each test class, detailing successes, failures, and execution time. CI servers read these files to determine the status of the test run.[^17_3]
* **HTML Reports**: While XML is for machines, HTML is for humans. Plugins like the `maven-surefire-report-plugin` can convert the raw XML results into a user-friendly HTML site, making it easy to browse test results. Many CI platforms also have their own UI for displaying test results by parsing the XML files.[^17_2][^17_4][^17_3]


### Parallel Test Execution (IMP)

As a test suite grows, its execution time can become a bottleneck in the CI/CD pipeline. **Parallel testing** is the practice of running multiple tests simultaneously to reduce the overall execution time.[^17_5][^17_6]

* **How it works**: CI tools can split your test suite into multiple "slices" and distribute them across several runners or threads, which execute in parallel.[^17_5]
* **Prerequisites**: Tests must be **independent and stateless**. A test should not depend on the outcome or side effects of another test.[^17_7]
* **JUnit 5 Support**: JUnit 5 has built-in support for parallel execution. You can enable it via a properties file (`junit-platform.properties`) to run tests concurrently at the class or method level.


### Test Caching \& Optimizations

To further speed up CI pipelines, caching is essential.

* **Dependency Caching**: The first time a pipeline runs, it downloads all the project dependencies (e.g., from Maven Central). Caching stores these dependencies on the CI runner, so subsequent builds can reuse them instead of re-downloading, saving significant time.[^17_7]
* **Build Caching**: Tools like Gradle have sophisticated build caches that can skip tasks if the inputs haven't changed, including re-running tests for modules that were unaffected by a code change.

![Summary table of CI/CD testing aspects for JUnit integration, report generation, parallel execution, and caching.](https://ppl-ai-code-interpreter-files.s3.amazonaws.com/web/direct-files/54f761afadcd02bd02d45bdc351ab2d8/016549dd-f998-4c7c-94b7-979bd1097422/4a348686.png)

Summary table of CI/CD testing aspects for JUnit integration, report generation, parallel execution, and caching.

***
Would you like to continue with Section 17: Integration \& System Testing with JUnit?
<span style="display:none">[^17_10][^17_11][^17_12][^17_13][^17_14][^17_15][^17_16][^17_17][^17_18][^17_19][^17_20][^17_8][^17_9]</span>

```
<div style="text-align: center">⁂</div>
```

[^17_1]: https://support.testrail.com/hc/en-us/articles/7529728971924-Integrating-with-GitHub-Actions

[^17_2]: https://octopus.com/blog/githubactions-running-unit-tests

[^17_3]: https://www.digitalocean.com/community/tutorials/junit-html-report

[^17_4]: https://www.geeksforgeeks.org/software-testing/junit-5-test-reports-in-html/

[^17_5]: https://www.browserstack.com/guide/speed-up-ci-cd-pipelines-with-parallel-testing

[^17_6]: https://katalon.com/resources-center/blog/how-to-accelerate-your-ci-cd-pipeline-with-parallel-testing

[^17_7]: https://www.browserstack.com/guide/optimize-tests-for-continuous-integration

[^17_8]: https://docs.github.com/en/actions/tutorials/build-and-test-code

[^17_9]: https://www.youtube.com/watch?v=0lbDMomNt4A

[^17_10]: https://github.com/marketplace/actions/junit-test-dashboard

[^17_11]: https://atlasgo.io/guides/testing/github-actions

[^17_12]: https://www.youtube.com/watch?v=aOWWq70-z5o

[^17_13]: https://docs.gitlab.com/ci/caching/

[^17_14]: https://stackoverflow.com/questions/75494740/can-you-unit-test-pipeline-code-in-github-actions

[^17_15]: https://www.cloudbees.com/blog/what-is-parallel-testing

[^17_16]: https://sanitarium.se/blog/2025/07/07/working-with-gos-test-cache-on-ci/

[^17_17]: https://notes.kodekloud.com/docs/GitHub-Actions/Continuous-Integration-with-GitHub-Actions/Workflow-Configure-Unit-Testing

[^17_18]: https://stackoverflow.com/questions/2385553/how-can-i-generate-an-html-report-for-junit-results

[^17_19]: https://learn.microsoft.com/en-us/azure/devops/pipelines/test/parallel-testing-any-test-runner?view=azure-devops

[^17_20]: https://github.com/vllm-project/vllm/issues/25004


---

# yes

Of course. Here is the quick revision guide for Section 17.

### Section 17: Integration \& System Testing with JUnit

While JUnit is known for unit tests, the JUnit 5 framework is an excellent orchestrator for higher-level integration and system tests, especially within a Spring Boot ecosystem.

### `@SpringBootTest` for Integration Tests (IMP)

`@SpringBootTest` is the core annotation for Spring Boot integration testing. It bootstraps the entire application, loading the full `ApplicationContext` to create a test environment that closely mimics production[^18_1][^18_2].

* **When to Use**: Use it for tests that span multiple layers of your application (e.g., from a controller down to the database) to ensure all components are wired together correctly.
* **Web Environment**: By default, it uses a mock servlet environment. To start a real embedded server (like Tomcat) and make actual HTTP calls, use `@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)`. This will also inject a `TestRestTemplate` for you to use as an HTTP client.[^18_2]

```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
class UserRegistrationIntegrationTest {

    @Autowired
    private TestRestTemplate restTemplate;

    @Autowired
    private UserRepository userRepository;

    @Test
    void testRegisterUser_shouldCreateUserInDatabase() {
        // Arrange
        UserRegistrationRequest request = new UserRegistrationRequest("testuser", "password");
        
        // Act: Make a real HTTP call to the running application
        ResponseEntity<Void> response = restTemplate.postForEntity("/api/users/register", request, Void.class);
        
        // Assert
        assertEquals(HttpStatus.CREATED, response.getStatusCode());
        assertTrue(userRepository.findByUsername("testuser").isPresent());
    }
}
```


### `@DataJpaTest` vs. `@WebMvcTest`

These are "slice" annotations that load only a specific part of the application context, resulting in much faster tests than `@SpringBootTest`.[^18_3][^18_4]


| Annotation | Loads | Use Case |
| :-- | :-- | :-- |
| **`@DataJpaTest`** | The JPA persistence layer only (Repositories, `EntityManager`). Auto-configures an in-memory database (like H2) by default[^18_3]. | Test your Spring Data JPA repositories and custom queries without loading the whole application. |
| **`@WebMvcTest`** | The web layer only (Controllers, filters, security). Other layers like services and repositories are not loaded and must be mocked with `@MockBean`[^18_3]. | Test your controllers' request mappings, input validation, and serialization/deserialization. |

### Testcontainers for Real Dependencies (IMP)

In-memory databases like H2 are fast but may not support specific features of your production database (e.g., PostgreSQL-specific JSON functions). **Testcontainers** solves this by letting you programmatically start and stop real services in lightweight Docker containers for your tests.[^18_5][^18_6]

* **Analogy**: Using an in-memory database is like practicing for a driving test in a go-kart. Using Testcontainers is like practicing in the actual car model you'll be tested in.
* **Use Cases**: Provides throwaway instances of databases (Postgres, MySQL), message brokers (Kafka, RabbitMQ), or any other service that can run in a Docker container.[^18_7]

```java
// Example with Testcontainers and JUnit 5
@SpringBootTest
@Testcontainers
class UserRepositoryIntegrationTest {

    @Container
    static PostgreSQLContainer<?> postgres = new PostgreSQLContainer<>("postgres:15-alpine");

    @DynamicPropertySource
    static void setDatasourceProperties(DynamicPropertyRegistry registry) {
        registry.add("spring.datasource.url", postgres::getJdbcUrl);
        registry.add("spring.datasource.username", postgres::getUsername);
        registry.add("spring.datasource.password", postgres::getPassword);
    }

    @Autowired
    private UserRepository userRepository;
    
    // ... your tests will now run against a real PostgreSQL database
}
```


### WireMock for Mocking REST APIs

When your application depends on external REST APIs, you don't want your integration tests to make real network calls. **WireMock** runs a mock HTTP server that you can configure to return specific responses for certain requests.[^18_8][^18_9]

* **How it works**: You start a WireMock server, point your application's API client to it (using `@TestPropertySource`), and stub the endpoints you need.
* **Use Case**: Test how your application behaves with API success cases, error responses (4xx, 5xx), and network delays, all in a fast and deterministic way.[^18_8]


### End-to-End (E2E) Tests with JUnit

While tools like Cypress or Selenium are common for UI-based E2E testing, JUnit can be used to write API-level E2E tests. These tests validate a complete user workflow from the perspective of an external client.[^18_10]

* **Scope**: An E2E test for an e-commerce site might involve:

1. Calling the API to register a user.
2. Calling the API to log in and get a token.
3. Calling the API to add an item to the cart.
4. Calling the API to complete the checkout.
* **Strategy**: These tests should be used sparingly for critical business flows because they are slow and can be brittle. They run against a fully deployed application with live dependencies.[^18_11]

***
Would you like to continue with Section 18: Best Practices \& Patterns?
<span style="display:none">[^18_12][^18_13][^18_14][^18_15][^18_16][^18_17][^18_18][^18_19][^18_20]</span>

```
<div style="text-align: center">⁂</div>
```

[^18_1]: https://reflectoring.io/spring-boot-test/

[^18_2]: https://www.diffblue.com/resources/spring-boot-test-slices-overview-and-usage/

[^18_3]: https://javarevisited.blogspot.com/2021/09/difference-between-webmvctest-and-da.html

[^18_4]: https://engineering.zalando.com/posts/2023/11/mastering-testing-efficiency-in-spring-boot-optimization-strategies-and-best-practices.html

[^18_5]: https://java.testcontainers.org/modules/databases/

[^18_6]: https://testcontainers.com

[^18_7]: https://testcontainers.com/guides/getting-started-with-testcontainers-for-java/

[^18_8]: https://www.geeksforgeeks.org/software-testing/create-your-first-mocked-api-endpoint-with-wiremock/

[^18_9]: https://wiremock.org

[^18_10]: https://www.javacodegeeks.com/2023/06/tutorial-to-end-to-end-testing.html

[^18_11]: https://ramok.tech/2017/10/22/core-tests-types/

[^18_12]: https://spring.io/guides/gs/testing-web

[^18_13]: https://www.baeldung.com/spring-boot-testing

[^18_14]: https://www.javaguides.net/2022/03/springboottest-spring-boot-example.html

[^18_15]: https://docs.spring.io/spring-boot/reference/testing/spring-boot-applications.html

[^18_16]: https://stackoverflow.com/questions/59097035/springboottest-vs-webmvctest-datajpatest-service-unit-tests-what-is-the-b

[^18_17]: https://www.baeldung.com/spring-boot-testing-main-class

[^18_18]: https://docs.wiremock.io/samples/mock-rest-api

[^18_19]: https://bugbug.io/blog/software-testing/unit-testing-vs-end-to-end-testing/

[^18_20]: https://dzone.com/articles/integration-testing-in-spring-boot-1


---

# yes

Of course. Here is the final section of the quick revision guide.

### Section 18: Best Practices \& Patterns

This section covers essential principles and patterns for writing clean, effective, and maintainable tests. Adhering to these practices is a hallmark of a senior developer.

### Writing Deterministic Tests (IMP)

A deterministic test is one that produces the same result every single time it is run. Non-deterministic (flaky) tests are a major source of friction and should be avoided at all costs.

**Best Practices for Determinism**:

* **No External Dependencies**: Unit tests must not rely on networks, filesystems, or databases. Mock all external calls.
* **Control Time**: Don't use `new Date()` or `System.currentTimeMillis()` in tests. Inject a `java.time.Clock` into your services and use a fixed clock in your tests to control the "current" time.
* **Fixed Test Data**: Avoid using random data generators directly in tests. If you need random-like data, use a fixed seed so the data is the same for every test run.
* **Ensure Test Isolation**: Each test should be able't run independently and in any order. Use `@BeforeEach` and `@AfterEach` to reset state between tests.


### Avoiding Over-Mocking

Mocking is powerful, but overusing it can lead to brittle tests that are tightly coupled to the implementation.

* **The Problem**: If you mock every dependency of a class, your test might just be verifying that your code calls the mocks in a certain order. If you later refactor the internal implementation without changing the outcome, the test breaks.
* **When to Mock**: Mock external systems, slow dependencies, or components with non-deterministic behavior.
* **When Not to Mock**: Don't mock simple value objects or classes that are fast and deterministic. It's often better to use real instances of internal components if they don't have heavy dependencies of their own.


### Test Data Builders \& Object Mothers

Creating complex test objects inside every test method leads to code duplication and makes tests hard to read.

* **Test Data Builder Pattern**: A fluent API for creating test objects. It provides sensible defaults and allows you to override only the fields relevant to your test.

```java
// Usage of a builder
User user = new UserBuilder()
                .withUsername("testuser")
                .withRoles("ADMIN")
                .build();
```

* **Object Mother Pattern**: A factory class that provides pre-configured instances of objects for common scenarios.

```java
// Usage of an Object Mother
User adminUser = TestUsers.anAdminUser();
User standardUser = TestUsers.aStandardUser();
```


### Given–When–Then Test Structure (IMP)

This is a popular naming and structuring convention for tests, especially in Behavior-Driven Development (BDD). It makes the intent of the test crystal clear.

* **Given**: The setup or arrangement phase.
* **When**: The action or method call being tested.
* **Then**: The verification or assertion phase.

```java
@Test
void givenAdminUser_whenDeletingResource_thenShouldSucceed() {
    // Given: an admin user and a resource
    User admin = new UserBuilder().withRoles("ADMIN").build();
    Resource resource = new Resource();

    // When: the user tries to delete the resource
    boolean result = permissionService.canDelete(admin, resource);

    // Then: the action is permitted
    assertTrue(result);
}
```


### Organizing Test Packages \& Naming Conventions

* **Package Structure**: A standard Maven/Gradle convention is to mirror the production package structure in `src/test/java`. For a class `com.app.service.UserService`, the test should be `com.app.service.UserServiceTest`.
* **Naming Conventions**: Test method names should be descriptive and explain what is being tested.
    * **`methodName_shouldStateBehavior_whenCondition`**: `add_shouldReturnSum_whenBothNumbersArePositive()`
    * **`should_doSomething_when_somethingHappens`**: `should_throwException_when_userIsNotFound()`
    * **Given-When-Then**: `given_invalidInput_when_createUser_then_throwValidationException()`


### Layered Test Strategy

A healthy application relies on a balanced test portfolio, as described by the **Testing Pyramid**.

* **Unit Tests (Base)**: Thousands of fast tests forming the foundation. They test individual classes in isolation.
* **Integration Tests (Middle)**: Hundreds of tests verifying the interaction between components (e.g., service to repository, repository to a Testcontainer database).
* **End-to-End (E2E) Tests (Top)**: A few dozen slow tests that validate critical user workflows from end to end (e.g., API-level tests).

This layered strategy provides the best balance of feedback speed, reliability, and confidence.

***
This concludes the JUnit quick revision guide. I hope this structured format helps with your interview preparation

