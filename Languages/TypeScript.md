<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# You are a TypeScript expert and mentor.

Your task is to generate a structured **quick revision notes for interview preparation** on TypeScript, broken into sections.  
I will specify which section to start from, and you will cover ONLY that section in detail.  
You should cover all the important topics from each section and it's sub-section which are most asked in interviews, mark the topic as (IMP) which is most asked and is a hot question.

### Output Rules:

- Be concise, yet cover all the concepts, revision notes should be crisp and clear.
- Use headings, bullet points, tables, and short code snippets.
- Highlight **common pitfalls**, **best practices**, and **TypeScript version notes**.
- Use comparison tables where useful (e.g., type vs interface, union vs intersection, any vs unknown).
- Include **short real-world examples** (functions, classes, generics, decorators).
- For complex or abstract topics (e.g., generics, advanced types, decorators), use **real-life analogies** to simplify learning.
- End each section by asking if I want to continue with the next one.


### Sections:

1. Introduction to TypeScript (what, why, benefits over JavaScript)
2. Basic Types (string, number, boolean, null, undefined, void, any, unknown, never)
3. Type Inference and Annotations (implicit vs explicit typing, best practices)
4. Functions (params, return types, optional/default/rest params, overloading)
5. Objects and Type Aliases (structural typing, custom types, reusability)
6. Interfaces (definition, extension, vs type aliases, readonly \& optional)
7. Union and Intersection Types (flexibility, composability, pitfalls)
8. Type Narrowing (type guards, `in`, `typeof`, `instanceof`, discriminated unions)
9. Enums (numeric, string, const enums, use cases, pitfalls)
10. Generics (functions, classes, constraints, default types, utility with collections)
11. Type Utilities (Partial, Pick, Omit, Readonly, Record, ReturnType, etc.)
12. Advanced Types (mapped types, conditional types, infer, template literal types)
13. Modules and Namespaces (import/export, ES modules, legacy namespaces)
14. Classes and Object-Oriented TypeScript (constructors, inheritance, access modifiers, abstract classes)
15. Decorators (class, method, property, parameter decorators, metadata reflection)
16. Working with JavaScript Code (interop, declaration files, DefinitelyTyped)
17. Error Handling and Strict Mode (`strictNullChecks`, `noImplicitAny`, exhaustiveness checks)
18. Configuration and Tooling (tsconfig.json, compiler options, build tools)
19. Testing with TypeScript (Jest, Mocha, ts-jest, type-safe mocks)
20. TypeScript in Real-World Applications (React, Angular, Node.js usage)
21. Design Patterns in TypeScript (Singleton, Factory, Observer, Strategy, Decorator)
22. Performance \& Optimization (compilation speed, bundle size, incremental builds)
23. Working with External Types (d.ts files, ambient declarations, extending types)
24. Miscellaneous \& Advanced (mixins, declaration merging, const assertions, satisfies operator)

### Instruction:

When I say **"Start from Section X"**, generate the revision guide for that section only.  
When done, ask me if I want to continue with the next section.  
Always maintain the same style so the entire revision guide feels consistent.

Understood. I am ready to begin generating your TypeScript quick revision guide. Please let me know which section you would like to start with.

---

# Start from Section: 1

TypeScript is an open-source, strongly typed programming language that builds on JavaScript by adding static type definitions. It helps developers write more robust, scalable, and maintainable code by catching errors during development rather than at runtime.

### What is TypeScript?

* TypeScript is a **superset of JavaScript**, meaning any valid JavaScript code is also valid TypeScript code.
* It is developed and maintained by Microsoft.
* The TypeScript compiler (`tsc`) transpiles TS code into plain, compatible JavaScript that can run in any browser or Node.js environment.
* Its core purpose is to add optional static typing to JavaScript, which is a dynamically typed language.


### Why Use TypeScript? (IMP)

This is a frequent interview question focused on understanding the value proposition of TypeScript.

* **Static Type Checking:** The primary benefit is catching type-related errors at compile time, long before the code is executed. This prevents a whole class of runtime errors (e.g., `TypeError: undefined is not a function`).
* **Improved Developer Experience (DX):** Static types enable powerful IDE features like intelligent code completion (IntelliSense), safe refactoring, and easier code navigation.
* **Enhanced Code Quality and Maintainability:** Types serve as a form of documentation, making the code easier to understand, reason about, and modify. This is especially crucial for large-scale applications and collaborative team environments.
* **Scalability:** It provides structures like interfaces, enums, and generics that help build and manage complex applications without losing control over the codebase.


### TypeScript vs. JavaScript

| Feature | JavaScript (ES6+) | TypeScript |
| :-- | :-- | :-- |
| **Typing System** | Dynamic | Static (optional) |
| **Error Detection** | Primarily at runtime. | Primarily at compile-time. |
| **Code Readability** | Relies on JSDoc and conventions. | High, as types are part of the syntax. |
| **Tooling \& IDE Support** | Good, but relies on linters/inference. | Excellent, with rich autocompletion \& refactoring. |
| **Object-Oriented** | Supports OOP via prototypes and classes. | Enhanced OOP with interfaces, access modifiers. |

### Real-World Analogy

Think of JavaScript as cooking without a recipe. You might mix ingredients that don't go well together and only find out when you taste the final dish (a **runtime error**).

TypeScript is like cooking with a detailed recipe. The recipe tells you exactly what ingredients (types) to use and in what amounts. If you try to add salt instead of sugar, the recipe warns you immediately (a **compile-time error**).

### Code Example: Spotting Errors Early

**JavaScript (Potential Runtime Error)**

```javascript
// This function expects a user object with a name property.
function getUsername(user) {
  return user.name.toUpperCase();
}

// This will crash the program at runtime because `null` has no 'name' property.
const user = null;
getUsername(user); // TypeError: Cannot read properties of null (reading 'name')
```

**TypeScript (Compile-Time Error)**

```typescript
interface User {
  name: string;
}

// The function signature clearly defines the expected type.
function getUsername(user: User) {
  return user.name.toUpperCase();
}

// The TypeScript compiler flags this error before you even run the code.
const user = null;
getUsername(user); // Error: Argument of type 'null' is not assignable to parameter of type 'User'.
```


### Best Practices \& Common Pitfalls

* **Best Practice:** Always enable `strict` mode in your `tsconfig.json` file. It activates a suite of type-checking rules (like `strictNullChecks`) that help you write safer code.
* **Common Pitfall:** Overusing the `any` type. Using `any` effectively disables type checking for a variable, which defeats the purpose of TypeScript. It should be used as an escape hatch only when necessary.

***
Would you like to proceed to Section 2: Basic Types?

---

# yes

Of course. Here is the revision guide for Section 2.

### `Section 2: Basic Types`

TypeScript extends JavaScript's primitive types with additional ones to create a more expressive and safe typing system. Understanding these basic types is fundamental.

#### Primitive Types

These are the most basic data types available.

* **`string`**: Represents text data.

```typescript
let name: string = "Alice";
```

* **`number`**: Represents both integer and floating-point numbers.

```typescript
let age: number = 30;
let price: number = 19.99;
```

* **`boolean`**: Represents `true` or `false` values.

```typescript
let isLoggedIn: boolean = true;
```

* **`null` \& `undefined`**: Each has a type of its own. By default, they are subtypes of all other types, but with `strictNullChecks` enabled (a best practice), they can only be assigned to variables of type `any`, `unknown`, or their respective types.

```typescript
let nothing: null = null;
let notAssigned: undefined = undefined;
```

    * **Best Practice**: Enable `strictNullChecks: true` in `tsconfig.json` to avoid unexpected `null` or `undefined` errors.


#### Special Types

These types serve specific purposes in TypeScript's type system.

* **`void`**: Used as the return type for functions that do not return a value.

```typescript
function logMessage(message: string): void {
  console.log(message);
}
```

* **`any` (IMP)**: The "escape hatch." It opts out of type checking. A variable of type `any` can be assigned any value, and you can access any of its properties without compiler checks.
    * **Use Case**: Migrating JavaScript code or working with third-party libraries without type definitions.
    * **Pitfall**: Defeats the purpose of TypeScript. Its use should be minimized.
* **`unknown` (IMP)**: A type-safe alternative to `any`. You can assign any value to a variable of type `unknown`, but you cannot perform any operations on it without first asserting or narrowing its type.
    * **Analogy**: `any` is like a "trust me" pass, letting you do anything. `unknown` is like a locked box; you can hold it, but you must check what's inside (narrow the type) before you can use its contents.
* **`never`**: Represents a value that will never occur. It's used for functions that always throw an error or have an infinite loop.

```typescript
// This function never returns a value
function throwError(message: string): never {
  throw new Error(message);
}
```


### Comparison: `any` vs. `unknown` (IMP)

This is a critical comparison often asked in interviews to test your understanding of type safety.


| Feature | `any` | `unknown` |
| :-- | :-- | :-- |
| **Type Safety** | **Not type-safe**. Disables all compiler checks. | **Type-safe**. Requires type checking before use. |
| **Assignment** | You can assign an `any` variable to a variable of any other type. | You can **only** assign an `unknown` variable to another `unknown` or `any` variable. |
| **Property Access** | Allowed. No checks are performed. | **Not allowed**. The compiler will throw an error until you narrow the type. |

#### Real-World Example: `any` vs. `unknown`

Imagine fetching data from an API where the response structure is unpredictable.

**Using `any` (Unsafe)**

```typescript
async function fetchDataAny(): Promise<any> {
    const response = await fetch('/api/data');
    return response.json();
}

const dataAny = await fetchDataAny();
// This compiles, but will crash at runtime if `dataAny` isn't what we expect.
console.log(dataAny.name.toUpperCase()); // Potential TypeError!
```

**Using `unknown` (Safe)**

```typescript
async function fetchDataUnknown(): Promise<unknown> {
    const response = await fetch('/api/data');
    return response.json();
}

const dataUnknown = await fetchDataUnknown();

// This will NOT compile, forcing us to check the type first.
// console.log(dataUnknown.name.toUpperCase()); // Error: Object is of type 'unknown'.

if (typeof dataUnknown === 'object' && dataUnknown && 'name' in dataUnknown && typeof (dataUnknown as any).name === 'string') {
    // Safe to use now
    console.log((dataUnknown as { name: string }).name.toUpperCase());
}
```


### Best Practices \& Pitfalls

* **Best Practice**: Prefer `unknown` over `any` whenever you need to represent a value of an unknown type. It forces you to write safer, more deliberate code.
* **Common Pitfall**: Forgetting that `void` as a return type means the function's return value is meant to be ignored, even if it technically returns something (like `undefined`).

***
Would you like to proceed to Section 3: Type Inference and Annotations?

---

# yes

Excellent. Let's dive into Section 3.

### `Section 3: Type Inference and Annotations`

TypeScript's ability to understand types, either by deduction or explicit declaration, is a core feature. Knowing when to rely on inference versus when to use annotations is key to writing clean and effective TypeScript.

#### Type Inference (Implicit Typing)

Type inference is when TypeScript automatically deduces the type of a variable based on its assigned value.

* If you initialize a variable with a value, TypeScript will "infer" its type.
* This makes your code less verbose while maintaining type safety.

```typescript
// TypeScript infers 'name' is of type 'string'
let name = "Bob";

// TypeScript infers 'age' is of type 'number'
let age = 30;

// This would cause an error because 'name' is inferred as a string
// name = 123; // Error: Type 'number' is not assignable to type 'string'.
```


#### Type Annotation (Explicit Typing)

Type annotation is when you explicitly tell TypeScript the type of a variable, function parameter, or function return value.

* You use annotations when a variable's type isn't obvious from its initial value or when it's not initialized at all.
* It serves as documentation and ensures the variable can only hold values of the specified type.

```typescript
// Explicitly annotating the type as 'string'
let name: string = "Bob";

// Annotating a variable that will be initialized later
let user: { name: string; id: number };

// Function parameter and return type annotations
function greet(name: string): string {
    return `Hello, ${name}`;
}
```


### When to Use Which? (IMP)

This is a common discussion point in interviews, focusing on code style and best practices.


| Scenario | Recommendation | Rationale |
| :-- | :-- | :-- |
| **Simple variable initializations** | Use **Inference** | The type is obvious from the value (`let x = 10;`). Annotating (`let x: number = 10;`) is redundant. |
| **Function return types** | Use **Annotation** | Acts as documentation, prevents accidental return of wrong types, and helps TypeScript spot bugs inside the function. |
| **Variables without initialization** | Use **Annotation** | TypeScript cannot infer the type, so you must annotate it. |
| **Function parameters** | Use **Annotation** | Parameters have no initial value, so their types must always be annotated. |
| **Complex objects or arrays** | Use **Annotation** | Improves readability and ensures the object has the correct shape, especially if the object is large or its type isn't immediately clear. |

### Real-World Analogy

* **Type Inference**: It's like guessing someone's job from their uniform. If they're wearing a white coat and have a stethoscope, you infer they're a doctor. It's usually correct and efficient.
* **Type Annotation**: It's like that person wearing a name badge that says "Dr. Smith, Cardiologist." It's explicit, leaves no room for doubt, and is the most reliable source of information.


### Best Practices \& Common Pitfalls

* **Best Practice (Readability)**: Don't add annotations where they are redundant. The goal is code that is both safe and easy to read.

```typescript
// Good: Inference is clear
const year = 2025;

// Bad: Redundant and noisy
const year: number = 2025;
```

* **Best Practice (Safety)**: Always annotate function return types and object types that are not immediately obvious. This helps prevent bugs.

```typescript
// Good: Return type is explicitly 'Promise<User>'
interface User { name: string; }
async function getUser(id: number): Promise<User> {
    const response = await fetch(`/api/users/${id}`);
    const data = await response.json();
    return data; // TS ensures the returned 'data' matches 'User'
}
```

* **Common Pitfall (`noImplicitAny`)**: If a variable has no annotation and no initial value, TypeScript may infer its type as `any`. This is dangerous. The `noImplicitAny` compiler option (part of `strict` mode) flags these cases as errors, forcing you to be explicit.

***
Would you like to proceed to Section 4: Functions?

---

# yes

Of course. Here is the detailed guide for Section 4.

### `Section 4: Functions`

Typing functions is one of the most powerful features of TypeScript. It ensures that functions are called with the correct arguments and that their return values are handled properly.

#### Parameter and Return Types

* **Parameter Types**: All function parameters should be annotated with a type. This is mandatory under `noImplicitAny` because their values aren't known until the function is called.
* **Return Types**: It is a strong best practice to annotate the return type. This provides clear documentation and helps TypeScript validate that the function body actually returns the correct type of value.

```typescript
// Parameters 'a' and 'b' are typed as 'number'.
// The return value is explicitly typed as 'number'.
function add(a: number, b: number): number {
    return a + b;
}
```


#### Special Parameter Types (IMP)

This area is frequently tested in interviews to check your understanding of function signatures.

* **Optional Parameters (`?`)**: A parameter that may or may not be provided by the caller. It's marked with a `?` after the parameter name. Inside the function, its type is a union with `undefined`.
    * **Rule**: Optional parameters must appear after all required parameters.

```typescript
function greet(name: string, title?: string): string {
    return `Hello, ${title ? title + ' ' : ''}${name}`;
}
greet("Arya"); // Works
greet("Sansa", "Lady"); // Works
```

* **Default Parameters**: A parameter that is assigned a default value if no argument is passed. The type is inferred from the default value.
    * **Benefit**: They do not need to be at the end of the parameter list.

```typescript
function create_user(username: string, role: "admin" | "user" = "user") {
    console.log(`Created ${username} with role ${role}`);
}
create_user("JonSnow"); // role defaults to "user"
create_user("Daenerys", "admin");
```

* **Rest Parameters (`...`)**: Allows a function to accept an indefinite number of arguments as an array.
    * **Rule**: The rest parameter must be the last parameter in a function's signature.

```typescript
function sum(...numbers: number[]): number {
    return numbers.reduce((total, num) => total + num, 0);
}
sum(1, 2, 3); // Returns 6
sum(10, 20);  // Returns 30
```


#### Function Overloading (IMP)

Function overloading allows you to define multiple signatures for a single function, enabling it to be called with different argument types or counts.

1. **Overload Signatures**: Define the different ways the function can be called. These have no implementation (no `{...}`).
2. **Implementation Signature**: A single, more general signature with the actual function body. This signature is not visible to callers. Its purpose is to implement the logic for all the overloads.

**Real-World Analogy**: Think of a vending machine that accepts coins or a credit card.

* `pay(coin: Coin)` and `pay(card: CreditCard)` are the **overload signatures**—the public-facing slots.
* `pay(paymentMethod: Coin | CreditCard)` is the **implementation signature**—the internal mechanism that handles both payment types.

**Example**: A function that can combine two numbers or two strings.

```typescript
// 1. Overload signatures (what the caller sees)
function combine(a: number, b: number): number;
function combine(a: string, b: string): string;

// 2. Implementation signature (with the logic, not visible to caller)
function combine(a: number | string, b: number | string): number | string {
    // Type guard is necessary to handle the different types
    if (typeof a === 'number' && typeof b === 'number') {
        return a + b;
    }
    if (typeof a === 'string' && typeof b === 'string') {
        return a + b;
    }
    throw new Error("Invalid arguments. Both must be numbers or strings.");
}

const numResult = combine(10, 20); // numResult is inferred as 'number'
const strResult = combine("hello", "world"); // strResult is inferred as 'string'
// const error = combine(10, "world"); // Error: No overload matches this call.
```


### Best Practices \& Common Pitfalls

* **Best Practice**: Always annotate function return types, especially for complex functions or functions returning `Promise`. It prevents bugs and improves readability.
* **Common Pitfall**: The signature of the implementation function for overloads is not directly callable. TypeScript only allows you to call the function using one of the defined overload signatures.
* **Common Pitfall**: Forgetting to handle all cases within an overloaded function's implementation, which can lead to runtime errors even if the code compiles.

***
Would you like to proceed to Section 5: Objects and Type Aliases?

---

# yes

Understood. Let's move on to Section 5.

### `Section 5: Objects and Type Aliases`

TypeScript enhances JavaScript objects by allowing you to define their "shape" or structure, ensuring they have the properties you expect. Type aliases are a primary tool for creating reusable shape definitions.

#### Structural Typing (IMP)

This is a fundamental concept in TypeScript, often contrasted with nominal typing found in languages like Java or C\#.

* TypeScript's type system is **structural**, not nominal.
* This means if two objects have the **same shape** (the same properties with the same types), they are considered to be of the same type, regardless of what they are named.
* It's often called **"duck typing"**: "If it walks like a duck and it quacks like a duck, then it must be a duck."

**Real-World Analogy**:
Imagine you need a charger with a USB-C port. You don't care if it's made by Apple, Samsung, or another brand (**nominal** name). As long as it has a USB-C port (**structural** shape), it will work for your purpose. TypeScript thinks this way about types.

**Code Example**:

```typescript
type Person = {
    name: string;
    age: number;
};

type Employee = {
    name: string;
    age: number;
    employeeId: number;
};

function greet(person: Person) {
    console.log(`Hello, ${person.name}`);
}

const p: Person = { name: "John", age: 30 };
const e: Employee = { name: "Jane", age: 28, employeeId: 123 };

greet(p); // Works, shape matches exactly.
greet(e); // Also works! 'e' has 'name' and 'age', so it satisfies the 'Person' shape.
          // The extra 'employeeId' property is ignored.
```


#### Type Aliases (`type`)

A type alias allows you to create a new name for a type. It doesn't create a new type; it just creates a synonym.

* **Purpose**: To improve readability and reusability by giving a descriptive name to a complex type definition.
* They are incredibly versatile and can be used for primitives, unions, intersections, and object shapes.

**Syntax**:

```typescript
type AliasName = TypeDefinition;
```

**Real-World Examples**:

1. **Defining an object shape**:

```typescript
type User = {
    id: string;
    username: string;
    isActive: boolean;
};

function deactivateUser(user: User): User {
    user.isActive = false;
    return user;
}
```

2. **Aliasing a union type**:

```typescript
type Status = "pending" | "success" | "error";

let currentStatus: Status = "pending";
// currentStatus = "failed"; // Error: Type '"failed"' is not assignable to type 'Status'.
```

3. **Aliasing a primitive for clarity**:

```typescript
type UserID = string;

function fetchUserData(id: UserID) {
    // ...
}
```


### Best Practices \& Common Pitfalls

* **Best Practice (Naming)**: Always use **PascalCase** for type alias names (e.g., `MyType`, `UserProfile`). This is a strong convention that distinguishes types from variables.
* **Best Practice (Reusability)**: If you define an object shape more than once, create a type alias for it. This follows the DRY (Don't Repeat Yourself) principle.

```typescript
// Bad: Repetitive and hard to maintain
function process(data: { id: number, value: string }) { /* ... */ }
function log(data: { id: number, value: string }) { /* ... */ }

// Good: Reusable and easy to update
type DataPacket = { id: number, value: string };
function process(data: DataPacket) { /* ... */ }
function log(data: DataPacket) { /* ... */ }
```

* **Common Pitfall**: TypeScript objects are "open," not "sealed." This means you can pass an object with *more* properties than the type defines, and it will be accepted as long as it has all the *required* properties. This is a direct result of structural typing.

***
Would you like to proceed to Section 6: Interfaces?

---

# yes

Understood. Here is the guide for Section 6.

### `Section 6: Interfaces`

Interfaces are a core feature in TypeScript used to define the "contract" or shape that an object must adhere to. They are a powerful way to enforce structure on objects, classes, and function parameters.

#### Defining an Interface

An interface is a named definition for an object's shape.

* It can include properties and their types.
* It only exists at compile-time for type-checking and is erased from the final JavaScript output.

```typescript
interface User {
    readonly id: number; // Cannot be changed after initialization
    username: string;
    email?: string; // Optional property
}

const user: User = {
    id: 1,
    username: "drogon"
};

// user.id = 2; // Error: Cannot assign to 'id' because it is a read-only property.
```


#### Extending Interfaces

Interfaces can inherit from one or more other interfaces using the `extends` keyword. This helps create more complex types from simpler, reusable building blocks.

```typescript
interface Person {
    name: string;
    age: number;
}

// Admin inherits all properties from Person and adds its own.
interface Admin extends Person {
    role: "admin" | "superadmin";
}

const admin: Admin = {
    name: "Tyrion",
    age: 40,
    role: "admin"
};
```


### `interface` vs. `type` Alias (IMP)

This is one of the most common TypeScript interview questions. While they often can be used interchangeably for defining object shapes, they have key differences.


| Feature | `interface` | `type` Alias |
| :-- | :-- | :-- |
| **Primary Use** | Defining the shape of **objects** and contracts for classes. | Creating an alias for **any type**, including primitives, unions, intersections, tuples, and objects. |
| **Extensibility** | Can be extended using `extends`. | Cannot be extended with `extends`. Composition is achieved using intersections (`&`). |
| **Declaration Merging** | **Yes**. If you define the same interface multiple times, TypeScript merges them into a single definition. | **No**. You cannot declare the same type alias twice within the same scope. |

#### Declaration Merging (A Key `interface` Feature)

Declaration merging is the ability of the TypeScript compiler to merge two or more separate declarations with the same name into a single definition. This is exclusive to `interface`.

**Real-World Analogy**: Imagine you have two separate shopping lists for the same trip. One has "milk" and "bread." The other has "eggs." Declaration merging automatically combines them into one master list: "milk," "bread," and "eggs."

**Code Example**:

```typescript
// Initial definition (e.g., from a library)
interface Box {
    height: number;
    width: number;
}

// Your own code extends it by adding a new property
interface Box {
    scale: number;
}

// TypeScript merges them. The 'box' object must now have all three properties.
const box: Box = {
    height: 10,
    width: 12,
    scale: 1.5
};
```

This is extremely useful for augmenting types from external libraries.

### Best Practices \& Common Pitfalls

* **Best Practice (When to use which?)**:
    * Use **`interface`** when defining object shapes or contracts for classes, especially if you expect them to be extended.
    * Use **`type`** for defining union types, intersection types, tuples, or aliases for primitive types. It's more versatile for non-object shapes.
* **Consistency is Key**: The official TypeScript documentation notes that the choice can be a matter of personal preference. The most important thing is to be consistent within your codebase. Many teams default to `interface` for objects and `type` for everything else.
* **Common Pitfall**: Trying to create a union or intersection with an `interface`. This is not possible; you must use a `type` alias for that.

```typescript
// This is not valid syntax
// interface Status = "success" | "error";

// Correct way using type
type Status = "success" | "error";
```


***
Would you like to proceed to Section 7: Union and Intersection Types?

---

# yes

Great. Let's proceed with Section 7.

### `Section 7: Union and Intersection Types`

Union and intersection types are fundamental tools for creating flexible and composite types in TypeScript.

#### Union Types (`|`)

A union type allows a variable to be one of **several possible types**. It is formed using the pipe (`|`) character.

* **Meaning**: OR
* It provides flexibility by allowing a value to hold different kinds of data.

**Real-World Analogy**: A universal charger port that can accept a USB-C cable **OR** a Lightning cable. The variable can hold either type of value.

**Code Example**:

```typescript
// A function that accepts an ID which can be a number or a string.
function findUserById(id: string | number) {
    // Before we can use string-specific methods, we must check the type.
    if (typeof id === "string") {
        // Here, TypeScript knows 'id' is a string.
        console.log(`Searching for user with string ID: ${id.toUpperCase()}`);
    } else {
        // Here, TypeScript knows 'id' is a number.
        console.log(`Searching for user with numeric ID: ${id}`);
    }
}
```

* **Working with Unions (IMP)**: When you have a value of a union type, you can only access members that are common to **all** types in the union. To access type-specific members, you must first narrow the type (using a type guard like `typeof`), as shown above.


#### Intersection Types (`&`)

An intersection type combines **multiple types into one**. This new type has all the properties of all the types it combines. It is formed using the ampersand (`&`) character.

* **Meaning**: AND
* It is used to compose existing types to create a new, more complex type.

**Real-World Analogy**: A Swiss Army knife. It's a knife **AND** a screwdriver **AND** a bottle opener. The final tool has the capabilities of all its constituent parts.

**Code Example**:

```typescript
interface Draggable {
    drag: () => void;
}

interface Resizable {
    resize: () => void;
}

// MovableWidget has the properties of BOTH Draggable AND Resizable.
type MovableWidget = Draggable & Resizable;

let widget: MovableWidget = {
    drag: () => console.log("Dragging..."),
    resize: () => console.log("Resizing...")
};

widget.drag();
widget.resize();
```


### Union (`|`) vs. Intersection (`&`) (IMP)

This comparison is a frequent interview topic.


| Feature | Union Type (`|`) | Intersection Type (`&`) |
| :-- | :-- | :-- |
| **Keyword** | `|` (Pipe) | `&` (Ampersand) |
| **Logic** | **OR** — The value can be one of the specified types. | **AND** — The type must have all properties from all specified types. |
| **Use Case** | Modeling a value that can be one of several distinct types (e.g., `string | number`). | Composing types to create a single, combined type (e.g., `TypeA & TypeB`). |
| **Result** | More **flexible** and permissive. Allows different shapes. | More **strict** and specific. Requires all features to be present. |

### Common Pitfalls

* **Union Pitfall**: Trying to access a property that doesn't exist on all types in the union without a type guard.

```typescript
function printId(id: string | number) {
    // console.log(id.toUpperCase()); // Error: Property 'toUpperCase' does not exist on type 'number'.
}
```

* **Intersection Pitfall (with primitives)**: Intersecting primitive types that have no overlap results in the `never` type, because a value cannot be two different primitive types simultaneously.

```typescript
type Impossible = string & number; // Type is 'never'
// let x: Impossible; // 'x' can never have a value.
```

* **Intersection Pitfall (with conflicting properties)**: If two intersected types have a property with the same name but different types, the resulting property type will be an intersection of those types. If they are incompatible primitives, it becomes `never`.

```typescript
interface A { prop: string; }
interface B { prop: number; }
type C = A & B; // The type of 'prop' in C is 'string & number', which is 'never'.
```


***
Would you like to proceed to Section 8: Type Narrowing?

---

# yes

Of course. Let's cover type narrowing.

### `Section 8: Type Narrowing`

Type narrowing is the process by which TypeScript's compiler figures out a more specific type for a variable within a certain block of code than its declared type. This is essential when working with union types, as it allows you to safely access properties unique to one of the types in the union.

**Real-World Analogy**: You have a box labeled "Fruit" (`string | number`). You can't just bite into it. You first need to look inside and check: "Is this an apple or a banana?" (`typeof`). Once you know it's an apple, you can safely perform apple-specific actions, like slicing it. This check is type narrowing.

#### Type Guards (IMP)

Type guards are expressions that perform a runtime check, guaranteeing the type of a variable within a specific scope.

1. **`typeof` Guard**: Used for narrowing primitive types like `string`, `number`, `boolean`, `symbol`, `bigint`, `undefined`, and `function`.

```typescript
function padLeft(value: string, padding: string | number) {
    if (typeof padding === "number") {
        // Inside this block, 'padding' is known to be a 'number'.
        return Array(padding + 1).join(" ") + value;
    }
    // Inside this block, 'padding' is known to be a 'string'.
    return padding + value;
}
```

2. **`instanceof` Guard**: Used for narrowing object types created via a class constructor. It checks if an object is an instance of a specific class.

```typescript
class Fish { swim() { console.log("swimming..."); } }
class Bird { fly() { console.log("flying..."); } }

function move(animal: Fish | Bird) {
    if (animal instanceof Fish) {
        // 'animal' is narrowed to type 'Fish'.
        animal.swim();
    } else {
        // 'animal' is narrowed to type 'Bird'.
        animal.fly();
    }
}
```

3. **`in` Operator Guard**: Checks if an object has a specific property. This is useful for narrowing based on an object's shape.

```typescript
interface Car { drive: () => void; }
interface Bike { ride: () => void; }

function startVehicle(vehicle: Car | Bike) {
    if ("drive" in vehicle) {
        // 'vehicle' is narrowed to 'Car'.
        vehicle.drive();
    } else {
        // 'vehicle' is narrowed to 'Bike'.
        vehicle.ride();
    }
}
```


#### Discriminated Unions (Tagged Unions) (IMP)

This is a very powerful and common pattern in TypeScript for working with union types in a fully type-safe way. It involves three components:

1. **A common, literal property** (the "discriminant" or "tag") that is present on every type in the union.
2. A **type alias** for the union of those types.
3. A **type guard** (usually a `switch` statement) on the discriminant property to narrow the type.

**Example**: Modeling the state of an API request.

```typescript
// 1. The discriminant is the 'status' property.
interface LoadingState {
    status: "loading";
}
interface SuccessState {
    status: "success";
    data: string[];
}
interface ErrorState {
    status: "error";
    error: string;
}

// 2. The union of all possible states.
type ApiState = LoadingState | SuccessState | ErrorState;

// 3. The type guard using a switch statement.
function handleState(state: ApiState) {
    switch (state.status) {
        case "loading":
            console.log("Loading data...");
            break;
        case "success":
            // 'state' is narrowed to 'SuccessState'. We can safely access 'data'.
            console.log("Data received:", state.data);
            break;
        case "error":
            // 'state' is narrowed to 'ErrorState'. We can safely access 'error'.
            console.error("Error:", state.error);
            break;
    }
}
```


### Best Practices \& Common Pitfalls

* **Best Practice (Exhaustiveness Checking)**: When using a `switch` statement on a discriminated union, you can use a `default` case with the `never` type to ensure you've handled every possible variant. If you add a new type to the union later and forget to update the `switch`, TypeScript will throw an error. This is a huge safety feature.

```typescript
function assertUnreachable(x: never): never {
    throw new Error("Didn't expect to get here");
}

function handleStateWithExhaustiveness(state: ApiState) {
    switch (state.status) {
        // ... cases for 'loading', 'success', 'error'
        default:
            // If we add a new state to ApiState but forget a 'case',
            // 'state' will not be 'never' here, and TS will error.
            assertUnreachable(state);
    }
}
```

* **Common Pitfall**: Using `typeof` for objects. `typeof null` is `"object"`, and `typeof []` is also `"object"`. Be careful when checking for generic objects; often the `in` operator or `instanceof` is more appropriate.

***
Would you like to proceed to Section 9: Enums?

---

# yes

Understood. Here is the guide for Section 9.

### `Section 9: Enums`

Enums (enumerations) are a feature added to JavaScript by TypeScript that allows for the creation of a named set of constant values. They improve code readability by giving friendly names to a set of numeric or string values.

**Real-World Analogy**: Think of enums as labels for fixed choices. Instead of remembering that `1` means "Pending," `2` means "Shipped," and `3` means "Delivered," you can use an enum to refer to them as `OrderStatus.Pending`, `OrderStatus.Shipped`, and `OrderStatus.Delivered`.

#### Numeric Enums

By default, enums are numeric. The first member is initialized to `0`, and each subsequent member auto-increments by `1`.

```typescript
enum Direction {
    Up,    // 0
    Down,  // 1
    Left,  // 2
    Right  // 3
}

let move: Direction = Direction.Up;
console.log(move); // Outputs: 0
```

You can also set the starting value manually:

```typescript
enum OrderStatus {
    Pending = 1,
    Shipped,      // 2
    Delivered     // 3
}
```

* **Reverse Mapping (IMP)**: Numeric enums have a unique feature called reverse mapping. The generated JavaScript object allows you to get the name of a member from its numeric value.

```typescript
console.log(Direction[2]); // Outputs: "Left"
```


#### String Enums

In a string enum, each member must be explicitly initialized with a string literal.

* They offer better readability and debugging experience because the logged value is the string itself, not an arbitrary number.
* String enums **do not** have reverse mappings.

```typescript
enum LogLevel {
    Error = "ERROR",
    Warning = "WARN",
    Info = "INFO"
}

function log(message: string, level: LogLevel) {
    console.log(`[${level}]: ${message}`);
}

log("User not found", LogLevel.Warning); // Outputs: [WARN]: User not found
```


#### Const Enums

A `const enum` is a special type of enum that is completely erased during compilation. The compiler will inline the actual value wherever the enum member is used.

* **Benefit**: Results in more concise and performant JavaScript code as no extra enum object is generated.
* **Drawback**: You cannot access `const enum` members at runtime (e.g., no reverse mapping) because the enum object doesn't exist.

```typescript
const enum HttpMethod {
    Get = "GET",
    Post = "POST"
}

// In the compiled JavaScript, this becomes:
// const method = "GET";
const method = HttpMethod.Get;
```


### Enums vs. Union Types (IMP)

This is a hot topic. Many developers now prefer using union types of string literals over enums for simple cases.


| Feature | Enum | Union of String Literals |
| :-- | :-- | :-- |
| **Generated JS** | Creates a runtime object (unless `const`). | Completely erased. No runtime footprint. |
| **Extensibility** | Closed. You cannot add new members from outside the definition. | More flexible. Can be composed with other types. |
| **Usage** | `MyEnum.Member` | `"member1"` |
| **Simplicity** | Can be overkill for a simple set of strings. | Very lightweight and simple. |
| **IDE Support** | Good autocompletion. | Excellent autocompletion. |

**Example**:

```typescript
// Enum
enum RoleEnum { Admin = "ADMIN", User = "USER" }
let role1: RoleEnum = RoleEnum.Admin;

// Union Type (often preferred)
type RoleType = "ADMIN" | "USER";
let role2: RoleType = "ADMIN";
```


### Pitfalls and Best Practices

* **Best Practice**: Prefer **string enums** or **union types** over numeric enums. String values are more descriptive and easier to debug. Union types offer a zero-cost abstraction.
* **Common Pitfall (Numeric Enums)**: The reverse mapping feature of numeric enums can be a source of confusion. It adds unexpected keys to your object, which can cause issues if you iterate over the enum object (e.g., `Object.keys(Direction)`).
* **When to Use `const enum`**: Use `const enum` when you need the performance benefit of inlining and are sure you will not need to access the enum as an object at runtime.

***
Would you like to proceed to Section 10: Generics?

---

# yes

Excellent. Generics are a powerful and frequently tested topic. Let's break it down.

### `Section 10: Generics`

Generics enable you to create reusable components (functions, classes, or interfaces) that can work with a variety of types rather than a single one. This allows you to write flexible and type-safe code.

**Real-World Analogy**: Think of a **placeholder** in a template. You design a birthday card template with a placeholder for a name: `Happy Birthday, {NAME}!`. This template (`generic component`) is reusable. When you use it for "Alice," the placeholder is replaced by `Alice` (`specific type`), and for "Bob," it's replaced by `Bob`. The structure remains the same, but the content type is provided when you use it.

#### Generic Functions (IMP)

A generic function uses a type parameter, typically denoted by `<T>`, to capture the type of the arguments passed to it. This allows the function to use that type information to ensure consistency between inputs and outputs.

**Problem without Generics**:

```typescript
// This only works for numbers
function getFirstNumber(arr: number[]): number {
    return arr[0];
}

// Using 'any' loses type information
function getFirstAny(arr: any[]): any {
    return arr[0];
}
const first = getFirstAny(["a", "b", "c"]); // 'first' is 'any', we don't know it's a string
```

**Solution with Generics**:

```typescript
function getFirst<T>(arr: T[]): T {
    return arr[0];
}

// TypeScript infers the type of T from the argument
const firstString = getFirst(["a", "b", "c"]); // 'firstString' is inferred as 'string'
const firstNumber = getFirst([1, 2, 3]);       // 'firstNumber' is inferred as 'number'
```

Here, `<T>` is the type parameter. `T` captures the type of the elements in the array and ensures the function returns a value of that same type.

#### Generic Classes

Classes can also be generic, allowing their properties and methods to work with a specific type provided upon instantiation.

```typescript
class DataStorage<T> {
    private data: T[] = [];

    addItem(item: T): void {
        this.data.push(item);
    }

    getItems(): T[] {
        return this.data;
    }
}

// A storage for numbers
const numberStorage = new DataStorage<number>();
numberStorage.addItem(10);
// numberStorage.addItem("hello"); // Error: Argument of type 'string' is not assignable to parameter of type 'number'.

// A storage for strings
const stringStorage = new DataStorage<string>();
stringStorage.addItem("hello");
```


#### Generic Constraints (`extends`) (IMP)

Sometimes you want to ensure that a generic type parameter has certain properties or methods. You can do this with constraints using the `extends` keyword.

**Real-World Analogy**: You're designing a machine that can juice any fruit (`<T>`). But to be "juiceable," the item must be a fruit. So you add a constraint: `T extends Fruit`. Now your machine will only accept types that are compatible with `Fruit`.

**Code Example**: A function that logs the length of its argument.

```typescript
// Without a constraint, this fails because 'T' could be anything (e.g., a number)
// function logLength<T>(arg: T): void {
//     console.log(arg.length); // Error: Property 'length' does not exist on type 'T'.
// }

// With a constraint, we guarantee that 'T' will have a 'length' property.
interface HasLength {
    length: number;
}

function logLength<T extends HasLength>(arg: T): void {
    console.log(arg.length);
}

logLength("hello world"); // Works (string has a length property)
logLength([1, 2, 3]);     // Works (array has a length property)
// logLength(123);         // Error: Argument of type 'number' is not assignable to parameter of type 'HasLength'.
```


### Best Practices \& Common Pitfalls

* **Best Practice**: Use `extends` to constrain your generics whenever your generic code needs to access specific properties of the type parameter. This makes your generics safer and more explicit.
* **Best Practice**: Use descriptive names for type parameters if it improves clarity (e.g., `<TKey, TValue>`), but for simple, single-letter generics, `T`, `U`, `V` are standard conventions.
* **Common Pitfall**: Overusing generics. If a function can be implemented with a simple union type, it might be cleaner than a generic.

```typescript
// Simpler union type might be better here
function formatId(id: string | number) {
    // ...
}

// A generic is overkill if the type isn't used to link inputs and outputs
function formatIdGeneric<T extends string | number>(id: T) {
    // ...
}
```


***
Would you like to proceed to Section 11: Type Utilities?

---

# yes

Of course. Utility types are a critical part of advanced TypeScript and are very common in interviews.

### `Section 11: Type Utilities (IMP)`

TypeScript provides several built-in utility types that help with common type transformations. These are essentially generic types that take another type as input and produce a new, modified type as output. Using them helps keep your code DRY (Don't Repeat Yourself).

**Real-World Analogy**: Think of utility types as tools in a workshop. You start with a raw piece of wood (your original type). You can use a saw (`Omit`) to cut a piece off, a drill (`Pick`) to select specific parts, or sandpaper (`Partial`) to smooth all the edges.

Let's use a base interface for our examples:

```typescript
interface User {
    id: number;
    name: string;
    email: string;
    isActive: boolean;
}
```


***

#### Key Transformation Utilities

* **`Partial<Type>`**: Constructs a type with all properties of `Type` set to optional. This is useful for creating objects that represent an "update" where only some fields are provided.

```typescript
// All properties of User are now optional.
type UserUpdate = Partial<User>;

// This is valid, even though 'name' and 'email' are missing.
const userToUpdate: UserUpdate = {
    id: 1,
    isActive: false
};
```

* **`Readonly<Type>`**: Constructs a type with all properties of `Type` set to `readonly`, meaning they cannot be reassigned.

```typescript
const lockedUser: Readonly<User> = {
    id: 2,
    name: "Readonly User",
    email: "readonly@example.com",
    isActive: true
};
// lockedUser.name = "New Name"; // Error: Cannot assign to 'name' because it is a read-only property.
```

* **`Required<Type>`**: Constructs a type consisting of all properties of `Type` set to required. It's the opposite of `Partial`.

```typescript
interface UserWithOptional {
    id: number;
    name?: string;
}
// 'name' is now required.
type CompleteUser = Required<UserWithOptional>;
// const user: CompleteUser = { id: 1 }; // Error: Property 'name' is missing.
```


***

#### Key Sub-setting Utilities

* **`Pick<Type, Keys>`**: Constructs a type by picking a set of properties (`Keys`) from `Type`.

**Analogy**: Creating a "greatest hits" album by picking your favorite songs from an artist's full catalog.

```typescript
// Creates a new type with only the 'id' and 'name' properties from User.
type UserSummary = Pick<User, "id" | "name">;

const summary: UserSummary = {
    id: 3,
    name: "User Three"
};
```

* **`Omit<Type, Keys>`**: Constructs a type by picking all properties from `Type` and then removing `Keys`. It's the opposite of `Pick`.

**Analogy**: Creating a playlist by taking a full album and removing a few songs you don't like.

```typescript
// Creates a new type with all properties from User EXCEPT 'email'.
type UserWithoutEmail = Omit<User, "email">;

const privateUser: UserWithoutEmail = {
    id: 4,
    name: "User Four",
    isActive: true
};
```


***

#### Other Important Utilities

* **`Record<Keys, Type>`**: Constructs an object type with a set of properties `Keys` whose values are all of `Type`. This is perfect for creating dictionaries or maps.

```typescript
type Page = "home" | "about" | "contact";
interface PageInfo {
    title: string;
    path: string;
}

// Creates a type where keys are 'home', 'about', or 'contact'
// and values must match the PageInfo interface.
const siteMap: Record<Page, PageInfo> = {
    home: { title: "Home", path: "/" },
    about: { title: "About Us", path: "/about" },
    contact: { title: "Contact", path: "/contact" }
};
```

* **`ReturnType<Type>`**: Extracts the return type of a function type.

```typescript
function createUser(name: string) {
    return { id: Date.now(), name: name };
}

// UserType is inferred as { id: number, name: string }
type UserType = ReturnType<typeof createUser>;
```

* **`NonNullable<Type>`**: Constructs a type by excluding `null` and `undefined` from `Type`.

```typescript
type ID = string | number | null | undefined;
// ValidId will be 'string | number'
type ValidId = NonNullable<ID>;
```


### Best Practices \& Pitfalls

* **Best Practice**: Combine utility types to create complex types without defining them from scratch. For example: `Partial<Omit<User, 'id'>>` would represent a user update object where the `id` cannot be changed.
* **Common Pitfall**: Confusing `Pick` and `Omit`. Remember: **Pick** *selects* properties, **Omit** *removes* them.
* **TypeScript Version Note**: Many utility types are built-in, but some advanced ones are added in newer versions. Always be aware of the TS version you are targeting.

***
Would you like to proceed to Section 12: Advanced Types?

---

# yes

Of course. This section covers some of the most powerful and complex features of TypeScript's type system, often asked in senior-level interviews.

### `Section 12: Advanced Types`

Advanced types allow you to perform complex manipulations and create dynamic types based on other types. They are the building blocks for many of TypeScript's utility types.

#### Mapped Types

Mapped types let you create new types by transforming the properties of an existing type. The syntax is similar to a `for...in` loop but for types.

**Syntax**: `[Property in keyof Type]: NewType;`

**Real-World Analogy**: Imagine you have a blueprint for a car (`Type`). A mapped type is like a factory process that takes this blueprint and creates a new one where, for every part (`Property in keyof Type`), you apply a modification, like making it "unbreakable" (`readonly`) or "optional."

**Example**: Creating a type where all properties of an existing type become nullable.

```typescript
interface Person {
    name: string;
    age: number;
}

// For each property in Person, make its type `T | null`.
type Nullable<T> = {
    [P in keyof T]: T[P] | null;
};

// Result: { name: string | null; age: number | null; }
type NullablePerson = Nullable<Person>;
```

```
**Insight**: Many built-in utility types like `Partial<T>`, `Readonly<T>`, and `Record<K,T>` are implemented using mapped types.
```


#### Conditional Types

Conditional types allow you to choose one of two types based on a condition. The syntax is like a ternary operator (`? :`) for types.

**Syntax**: `T extends U ? X : Y` (If `T` is assignable to `U`, the type is `X`; otherwise, it's `Y`).

**Real-World Analogy**: A sorting machine at a post office. It checks each package (`T`). "Does this package fit in the small box slot (`extends U`)? If yes (`?`), send it to the local delivery route (`X`). If not (`:`), send it to the freight route (`Y`)."

**Example**: A type that checks if another type is a string.

```typescript
type IsString<T> = T extends string ? true : false;

type A = IsString<"hello">; // Type A is 'true'
type B = IsString<123>;     // Type B is 'false'
```

**Insight**: Utilities like `NonNullable<T>` and `Exclude<T, U>` are implemented using conditional types. `Exclude<"a" | "b", "a">` results in `"b"`.

#### The `infer` Keyword (IMP)

The `infer` keyword is used within the `extends` clause of a conditional type to declare a new generic type variable that captures a part of the type being checked.

**Real-World Analogy**: `infer` is like using a variable in a regular expression capture group. In the pattern `image-(\d+).jpg`, you are saying, "If the string matches this pattern, *infer* the digits and put them in a variable for me to use."

This is most famously used to implement `ReturnType<T>`.

**Example**: Implementing `ReturnType<T>`

```typescript
// If T is a function type that takes any arguments and returns some type R,
// then 'infer' R and return it. Otherwise, return 'any'.
type MyReturnType<T> = T extends (...args: any[]) => infer R ? R : any;

function createMessage(message: string) {
    return { timestamp: Date.now(), message };
}

// 'MyReturnType<typeof createMessage>' infers 'R' as '{ timestamp: number, message: string }'.
type Message = MyReturnType<typeof createMessage>;
```


#### Template Literal Types

Template literal types allow you to create new string literal types by combining existing ones, similar to JavaScript's template literals.

**Real-World Analogy**: It's a "Mad Libs" for types. You have a template like `"{event}:{action}"` and provide sets of allowed words for `{event}` (`"user" | "post"`) and `{action}` (`"create" | "delete"`). TypeScript generates all possible combinations.

**Example**: Creating a set of event names.

```typescript
type Entity = "user" | "product";
type Action = "create" | "update" | "delete";

// This creates a union of all 6 possible strings:
// "user:create" | "user:update" | "user:delete" |
// "product:create" | "product:update" | "product:delete"
type EventName = `${Entity}:${Action}`;

let event: EventName = "user:update";
// let invalidEvent: EventName = "order:create"; // Error: "order" is not a valid Entity.
```

This is extremely powerful for ensuring type safety with event systems, API routes, or CSS class names.

***
Would you like to proceed to Section 13: Modules and Namespaces?

---

# yes

Certainly. Let's cover modules and namespaces.

### `Section 13: Modules and Namespaces`

Both modules and namespaces are tools in TypeScript for organizing code, grouping related logic, and preventing naming conflicts in the global scope. However, they work differently, and the modern standard is to use modules.

#### Modules (ES Modules) - The Modern Standard (IMP)

In modern TypeScript and JavaScript, each file is its own module. Anything declared in a file is scoped to that file unless it is explicitly exported.

* **`export`**: Makes a variable, function, class, or type alias available to other files.
    * **Named Export**: Exports a specific member. A file can have multiple named exports.
    * **Default Export**: Exports a single "main" value from the file. A file can have only one default export.

```typescript
// file: math-utils.ts
export const PI = 3.14;

export function add(a: number, b: number): number {
    return a + b;
}

export default class Calculator {
    // ...
}
```

* **`import`**: Brings exported members from another file into the current file's scope.

```typescript
// file: main.ts
// Importing the default export and named exports
import Calculator, { PI, add } from './math-utils';

// Or import everything from a module into a single namespace variable
import * as MathUtils from './math-utils';

console.log(PI); // 3.14
console.log(MathUtils.add(2, 3)); // 5
const calc = new Calculator();
```


#### Namespaces - The Legacy Way

Before ES Modules were standardized, TypeScript used `namespace` to group related code and prevent polluting the global scope. A namespace is an object that contains a set of related functionality.

* They are declared with the `namespace` keyword.
* You must `export` members from a namespace to make them accessible outside of it.
* Namespaces can be split across multiple files, and TypeScript will merge them (declaration merging).

```typescript
// file: validators.ts
namespace Validation {
    export interface StringValidator {
        isValid(s: string): boolean;
    }

    export class ZipCodeValidator implements StringValidator {
        isValid(s: string) {
            return s.length === 5;
        }
    }
}

// Usage (assuming validators.ts is loaded)
let validator = new Validation.ZipCodeValidator();
console.log(validator.isValid("12345")); // true
```


### Modules vs. Namespaces (IMP)

This is a key interview question to test your understanding of modern JavaScript architecture.


| Feature | Modules (ES Modules) | Namespaces |
| :-- | :-- | :-- |
| **Scope** | **File-scoped**. Each file is its own isolated module. | **Global-scoped**. Creates a single global object. |
| **Dependencies** | Explicitly managed with `import` and `export`. | Implicit. Relies on the order of `<script>` tags in HTML or build tool configuration. |
| **Relationship** | One module per file. | A single namespace can be split across multiple files. |
| **Modern Usage** | **The standard**. Recommended for all new applications (web, Node.js). | **Legacy**. Generally avoid in new projects. |
| **Declaration Merging** | Does not apply to files. | Namespaces with the same name are automatically merged. |

### Best Practices \& Common Pitfalls

* **Best Practice**: **Always use ES Modules (`import`/`export`) for new projects.** They are the standard in the entire JavaScript ecosystem, supported by browsers and Node.js, and work seamlessly with modern bundlers like Vite and Webpack.
* **When to Use Namespaces?**: The primary modern use case for namespaces is to organize types within a large, global declaration file (`.d.ts`). This is often seen in libraries that need to provide types for non-modular JavaScript code.
* **Common Pitfall**: Mixing modules and namespaces can lead to a confusing codebase. Stick to the module system unless you have a specific, well-justified reason to use a namespace. TypeScript's original term for namespaces was "internal modules," which can cause confusion; today, "module" almost exclusively refers to ES modules.

***
Would you like to proceed to Section 14: Classes and Object-Oriented TypeScript?

---

# yes

Excellent. Let's explore how TypeScript enhances object-oriented programming.

### `Section 14: Classes and Object-Oriented TypeScript`

TypeScript strengthens JavaScript's class-based system by adding powerful OOP features like access modifiers, interfaces, and abstract classes. This enables more robust and scalable application architectures.

#### Basic Class and Constructor

A class is a blueprint for creating objects. The `constructor` is a special method for creating and initializing an object instance of that class.

```typescript
class Animal {
    // Properties with types
    name: string;

    constructor(name: string) {
        this.name = name;
    }

    // Method
    move(distance: number = 0) {
        console.log(`${this.name} moved ${distance}m.`);
    }
}

const cat = new Animal("Cat");
cat.move(10); // Outputs: Cat moved 10m.
```


#### Access Modifiers (IMP)

Access modifiers control the visibility of class members (properties and methods). This is a TypeScript-only feature that is erased at runtime (unlike JavaScript's `#private` fields).


| Modifier | Description | Accessibility |
| :-- | :-- | :-- |
| **`public`** | The default. Members are accessible from anywhere. | Inside the class, from subclasses, and from outside. |
| **`private`** | Members can only be accessed from within the class they are defined in. | Only inside the defining class. |
| **`protected`** | Members can be accessed from within the class and any class that inherits from it. | Inside the class and from subclasses. |

**Example**:

```typescript
class Person {
    public name: string;
    private age: number;
    protected ssn: string;

    constructor(name: string, age: number, ssn: string) {
        this.name = name;
        this.age = age;
        this.ssn = ssn;
    }

    public celebrateBirthday() {
        this.age += 1; // Can access private 'age'
    }
}

class Employee extends Person {
    public getEmployeeDetails() {
        // Can access public 'name' and protected 'ssn'
        return `Name: ${this.name}, SSN: ${this.ssn}`;
    }
}

const person = new Person("John", 30, "123");
console.log(person.name); // OK
// console.log(person.age); // Error: Property 'age' is private.
// console.log(person.ssn);  // Error: Property 'ssn' is protected.
```


#### Parameter Properties (Shorthand) (IMP)

This is a concise syntax for declaring and initializing a class member from a constructor parameter. By adding an access modifier (`public`, `private`, `protected`, or `readonly`) to a constructor parameter, TypeScript automatically creates a property with that name and assigns the value.

```typescript
// Longhand
class Car {
    private make: string;
    constructor(make: string) {
        this.make = make;
    }
}

// Shorthand using parameter properties
class Suv {
    constructor(private make: string) {
        // 'this.make = make' is done automatically.
    }
}
```


#### Inheritance (`extends` and `super`)

Classes can inherit properties and methods from a base (or parent) class using the `extends` keyword.

* The `super()` keyword is used in a subclass's constructor to call the constructor of its parent class. **It must be called before accessing `this`**.

```typescript
class Dog extends Animal {
    // The 'name' property and 'move' method are inherited.
    constructor(name: string) {
        super(name); // Call the constructor of the 'Animal' class.
    }

    bark() {
        console.log("Woof! Woof!");
    }
}

const dog = new Dog("Buddy");
dog.bark();
dog.move(5);
```


#### Abstract Classes (IMP)

An abstract class is a base class that cannot be instantiated on its own. It is meant to be inherited by other classes. It can contain abstract members (methods or properties) that have no implementation and **must** be implemented by the derived classes.

**Real-World Analogy**: An abstract class is like a car **blueprint** (`AbstractVehicle`). The blueprint states that every vehicle must have an `engineStart()` method, but it doesn't define *how* it starts. A `GasolineCar` and an `ElectricCar` are concrete classes that inherit this blueprint and provide their own specific implementations for `engineStart()`.

```typescript
abstract class Shape {
    // An abstract method has no implementation.
    abstract getArea(): number;

    printArea() {
        console.log(`The area is ${this.getArea()}`);
    }
}

// const shape = new Shape(); // Error: Cannot create an instance of an abstract class.

class Circle extends Shape {
    constructor(private radius: number) {
        super();
    }
    // The derived class MUST implement the abstract method.
    getArea(): number {
        return Math.PI * this.radius ** 2;
    }
}

const circle = new Circle(5);
circle.printArea();
```


### Best Practices \& Common Pitfalls

* **Best Practice**: Encapsulate internal state by marking properties as `private` and exposing functionality through `public` methods.
* **Best Practice**: Use `abstract` classes to define a common contract for a set of related subclasses.
* **TypeScript Version Note**: Be aware of the difference between TypeScript's `private` (a compile-time check) and JavaScript's native `#private` fields (a runtime check enforced by the JS engine). Modern TS supports both.
* **Common Pitfall**: Forgetting to call `super()` in the constructor of a derived class. This will result in a reference error at runtime.

***
Would you like to proceed to Section 15: Decorators?

---

# yes

Certainly. Decorators are an advanced topic often used in frameworks like Angular and NestJS.

### `Section 15: Decorators`

Decorators are a special kind of declaration that can be attached to a class, method, accessor, property, or parameter. They are functions that are called at declaration time and can be used to observe, modify, or replace a definition.

**Important Note**: Decorators are an **experimental feature** in TypeScript. You must enable the `experimentalDecorators` compiler option in your `tsconfig.json` to use them.

```json
{
  "compilerOptions": {
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true // Often used with decorators
  }
}
```

**Real-World Analogy**: Think of decorators as "decorators" for a plain cake. The cake is your class or method.

* A `@log` decorator is like adding sprinkles—it adds logging without changing the cake's flavor (the core logic).
* A `@deprecate` decorator is like putting a warning sign next to the cake, advising people not to eat it.
* An `@bind` decorator is like gluing the cake to the plate, ensuring its context (`this`) never changes.


#### Types of Decorators (IMP)

1. **Class Decorators**: Applied to a class constructor. They receive the constructor of the class as their only argument. They can be used to modify or even replace the class definition.

```typescript
function sealed(constructor: Function) {
    Object.seal(constructor);
    Object.seal(constructor.prototype);
}

@sealed
class Greeter {
    greeting: string;
    constructor(message: string) {
        this.greeting = message;
    }
}
// Now, new properties cannot be added to Greeter or its prototype.
```

2. **Method Decorators**: Applied to a method. They receive three arguments: the target (the class prototype), the property key (the method name), and the property descriptor. They can be used to observe, modify, or replace a method definition.

```typescript
function log(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    const originalMethod = descriptor.value;
    descriptor.value = function (...args: any[]) {
        console.log(`Calling "${propertyKey}" with arguments:`, args);
        return originalMethod.apply(this, args);
    };
}

class Calculator {
    @log
    add(a: number, b: number) {
        return a + b;
    }
}

new Calculator().add(2, 3); // Will log the call before executing.
```

3. **Property Decorators**: Applied to a class property. They receive two arguments: the target (the class prototype) and the property key (the property name).
    * **Limitation**: They cannot directly observe or modify the value of a property because they run when the class is defined, not when it is instantiated. They are mainly used for recording metadata.
4. **Parameter Decorators**: Applied to a parameter of a method or constructor. They receive three arguments: the target (the class prototype), the property key (the method name), and the parameter index.
    * **Use Case**: Often used with the `reflect-metadata` library to record information about parameter types, which is essential for Dependency Injection (DI) frameworks.

#### Decorator Composition \& Execution

* Decorators can be composed (stacked) on top of each other.
* **Execution Order (IMP)**: Decorators on a declaration are evaluated bottom-up. In the example below, `@second` will run before `@first`.

```typescript
@first
@second
function myMethod() { /* ... */ }
```


#### Metadata Reflection API

Decorators become extremely powerful when combined with a metadata API, like the `reflect-metadata` library. This allows decorators to attach hidden metadata to a class or its members. Other parts of the application (like a dependency injection container) can then read this metadata at runtime to make decisions.

**Example Use Case**: In a web framework, a `@Get('/users')` decorator on a method doesn't change the method itself. Instead, it attaches metadata (`path: '/users'`, `method: 'GET'`) to it. The framework's router later reads this metadata to map incoming requests to the correct method.

### Best Practices \& Pitfalls

* **Framework-Driven**: Decorators are most commonly used within frameworks like **Angular** (for components, services) and **NestJS** (for controllers, providers, modules). They are less common in general application code.
* **Keep them Simple**: Decorators can add "magic" to your code, making it harder to understand what's happening. Keep their logic focused and simple (e.g., logging, validation, metadata).
* **Experimental Nature**: The decorator proposal for JavaScript has evolved. TypeScript's implementation is based on an older version of the proposal. Be aware that the standard may differ from TypeScript's current implementation.

***
Would you like to proceed to Section 16: Working with JavaScript Code?

---

# yes

Absolutely. Here is the guide for Section 16, focusing on how TypeScript works with existing JavaScript code.

### `Section 16: Working with JavaScript Code`

A major strength of TypeScript is its seamless interoperability with JavaScript. You can gradually migrate a JavaScript codebase to TypeScript or use existing JavaScript libraries in a TypeScript project with full type safety.

#### Coexistence and Migration (IMP)

TypeScript is a superset of JavaScript, meaning you can have both `.js` and `.ts` files in the same project.

* **`allowJs` Compiler Option**: To enable this, you must set `"allowJs": true` in your `tsconfig.json`. This tells the TypeScript compiler to include `.js` files in the compilation process.
* **Gradual Migration**: This is the most common use case. You can start by adding types to your JavaScript files using JSDoc comments and then rename files from `.js` to `.ts` one by one, adding more robust TypeScript syntax.

The problem with using plain JavaScript is that TypeScript doesn't know the types of the values coming from `.js` files, so it often infers them as `any`, which sacrifices type safety. The solution is declaration files.

#### Declaration Files (`.d.ts`) (IMP)

A declaration file (with a `.d.ts` extension) provides type information for JavaScript code. It contains only type annotations and **no implementations**.

**Real-World Analogy**: A `.d.ts` file is like a **user manual** for a JavaScript library. The manual tells you what buttons (`functions`) exist and what they do (`parameter and return types`), but it's not the device itself (the actual JS implementation). TypeScript reads this manual to understand how to use the device safely.

* **`declare` Keyword**: Inside a `.d.ts` file, you use `declare` to tell TypeScript that a variable, function, or module exists in the JavaScript environment.

**Example**:
Let's say you have a simple JavaScript library `string-util.js`:

```javascript
// file: string-util.js
exports.capitalize = (str) => str.charAt(0).toUpperCase() + str.slice(1);
```

To use this safely in TypeScript, you would create a corresponding declaration file:

```typescript
// file: string-util.d.ts
// This file describes the shape of string-util.js
export function capitalize(str: string): string;
```

Now, when you import it in a TypeScript file, you get full type safety:

```typescript
// file: app.ts
import { capitalize } from './string-util';

const name = capitalize("arya"); // 'name' is correctly inferred as 'string'
// capitalize(123); // Error: Argument of type 'number' is not assignable to parameter of type 'string'.
```


#### DefinitelyTyped: The Global Type Repository (IMP)

Writing declaration files for every library you use would be tedious. Fortunately, the community maintains **DefinitelyTyped**, a massive repository of high-quality `.d.ts` files for thousands of JavaScript libraries.

* **`@types` Scope**: These declaration files are published on npm under the `@types` scope.
* **Installation**: To get types for a library (e.g., `lodash`), you just install its corresponding `@types` package as a development dependency.

```bash
# Install the library
npm install lodash

# Install the types for the library
npm install --save-dev @types/lodash
```

* **Automatic Discovery**: Once installed, the TypeScript compiler will automatically find and use these type definitions from your `node_modules/@types` folder. No additional configuration is required.


### Best Practices \& Common Pitfalls

* **Best Practice**: Before using a JavaScript library, always search for its `@types` package on npm. Most popular libraries have one.
* **Best Practice (Migration)**: When migrating a JS codebase, enable `"checkJs": true` in your `tsconfig.json`. This allows TypeScript to start analyzing your `.js` files and report potential errors based on JSDoc comments, giving you early feedback before converting to `.ts`.
* **Common Pitfall**: Mismatched versions between a library and its `@types` package can lead to type errors. For example, using `lodash@4.17.x` with `@types/lodash@3.x.x`. Always try to keep them in sync.
* **Common Pitfall**: If a library ships with its own `.d.ts` files, you do not need to install an `@types` package for it. This is becoming more common as library authors adopt TypeScript.

***
Would you like to proceed to Section 17: Error Handling and Strict Mode?

---

# yes

Of course. Let's cover the critical topic of strictness and error handling.

### `Section 17: Error Handling and Strict Mode`

TypeScript's strict mode options are designed to help you write more robust and bug-free code by enabling a higher degree of type-checking. Understanding these options is key to leveraging TypeScript's full potential.

#### The `strict` Compiler Option (IMP)

In `tsconfig.json`, setting `"strict": true` is the single most important configuration for ensuring code quality. It's a master switch that enables a bundle of stricter type-checking options.

**Best Practice**: **Always** start new projects with `"strict": true`. Retrofitting strictness into a large, existing codebase can be very challenging.

**Real-World Analogy**: Writing code without strict mode is like building a structure with a simple level tool. Writing with `strict: true` is like having a laser-guided system that checks every angle and connection for perfect alignment, preventing structural weaknesses before they are built.

Let's look at the most important flags enabled by `strict` mode.

***

#### Key Strict Mode Flags

1. **`strictNullChecks` (IMP)**
    * **What it does**: By default, `null` and `undefined` are assignable to any type (e.g., `let name: string = null;` is allowed). This is a major source of runtime errors (e.g., "Cannot read property 'toUpperCase' of null"). `strictNullChecks` disables this behavior.
    * **With the flag enabled**: `null` and `undefined` can only be assigned to variables of type `any`, `unknown`, or their own respective types. To allow `null` or `undefined`, you must explicitly include it in a union type.

**Example**:

```typescript
// "strictNullChecks": false (default without strict mode)
let name: string = null; // Allowed, but dangerous

// "strictNullChecks": true
let nameOrNull: string | null = "Alice";
nameOrNull = null; // Allowed, because it's explicitly in the type.

// let nameNotNull: string = null; // Error: Type 'null' is not assignable to type 'string'.
```

2. **`noImplicitAny` (IMP)**
    * **What it does**: Raises an error on variables, parameters, or return values that are implicitly inferred as type `any`. It forces you to be explicit about types.

**Example**:

```typescript
// "noImplicitAny": false
function log(data) { // 'data' is implicitly 'any'
    console.log(data);
}

// "noImplicitAny": true
function log(data: any) { // You must explicitly type it as 'any' (or something better)
    console.log(data);
}
```

This flag doesn't ban `any`, but it makes sure you use it deliberately.
3. **`strictFunctionTypes`**
    * **What it does**: Enforces stricter checking of function parameter types in assignments, using contravariance. In simple terms, it prevents you from assigning a function that accepts a narrow set of arguments to a variable expecting a function that handles a wider set.

**Example**:

```typescript
class Animal {}
class Dog extends Animal {}

let processAnimal: (animal: Animal) => void;
let processDog: (dog: Dog) => void;

// This is unsafe, because processAnimal might be called with a cat,
// but processDog only knows how to handle dogs. strictFunctionTypes prevents this.
// processAnimal = processDog; // Error with strictFunctionTypes
processDog = processAnimal; // This is safe
```


***

#### Type-Safe Error Handling: Exhaustiveness Checking (IMP)

This pattern ensures that you handle every possible case when working with union types, especially discriminated unions. If you add a new variant to the union and forget to handle it, TypeScript will give you a compile-time error.

This is achieved by using a `default` case in a `switch` statement that tries to assign the variable to a value of type `never`.

**Example**:

```typescript
type Result = { status: "success", data: string } | { status: "error", code: number };

function handleResult(result: Result) {
    switch (result.status) {
        case "success":
            console.log(result.data);
            break;
        case "error":
            console.log(result.code);
            break;
        default:
            // If we add a new status to 'Result' (e.g., { status: "pending" })
            // but forget to add a case for it, 'result' will not be 'never' here.
            // This line will then cause a compile-time error.
            const _exhaustiveCheck: never = result;
            return _exhaustiveCheck;
    }
}
```


### Common Pitfalls

* **Turning off strict mode**: When faced with a complex type error, it's tempting to disable a strict flag. This is almost always a mistake, as you are simply hiding a potential runtime bug. The correct approach is to understand and fix the type mismatch.
* **Assuming a type**: Without `strictNullChecks`, developers often assume a variable is not `null`/`undefined` and access its properties, leading to runtime crashes.

***
Would you like to proceed to Section 18: Configuration and Tooling?

---

# yes

Of course. Let's cover the essential tooling and configuration for a TypeScript project.

### `Section 18: Configuration and Tooling`

Proper configuration is crucial for managing a TypeScript project, controlling how your code is checked and compiled. The `tsconfig.json` file is the heart of this process.

#### `tsconfig.json`: The Project's Rulebook (IMP)

The `tsconfig.json` file, placed at the root of a project, tells the TypeScript compiler (`tsc`) how to compile the project. The presence of this file indicates that the directory is the root of a TypeScript project.

* **Creation**: You can generate a default `tsconfig.json` file with comments by running `tsc --init`.


#### Key `compilerOptions` (IMP)

This section within `tsconfig.json` is where you define the core compilation rules. Here are some of the most important options:


| Option | Description | Common Value(s) |
| :-- | :-- | :-- |
| **`target`** | Specifies the ECMAScript version to which the code will be transpiled. | `"ES2020"`, `"ESNext"`. Choose based on the JS engines you need to support. |
| **`module`** | Specifies the module system for the generated code. | `"ESNext"`, `"CommonJS"`. `"ESNext"` for modern front-end, `"CommonJS"` for Node.js. |
| **`strict`** | Enables all strict type-checking options. **Highly recommended**. | `true` |
| **`outDir`** | The directory where compiled `.js` files will be placed. | `"./dist"` |
| **`rootDir`** | Specifies the root directory of your source `.ts` files. | `"./src"` |
| **`esModuleInterop`** | Improves compatibility between CommonJS and ES Modules. | `true` (almost always recommended) |
| **`sourceMap`** | Generates `.map` files, which allow you to debug your original `.ts` code in the browser or Node.js. | `true` |
| **`noEmit`** | Do not emit output files. Use this to perform type-checking without generating JavaScript. | `true` (useful in CI/CD or when another tool handles transpilation) |

#### Other Important `tsconfig.json` Properties

* **`include`**: An array of file paths or glob patterns specifying which files to include in the compilation. If omitted, it defaults to all `.ts`, `.tsx`, and `.d.ts` files in the project.

```json
"include": ["src/**/*"]
```

* **`exclude`**: An array of patterns specifying which files to *exclude* from compilation. `node_modules` is excluded by default.

```json
"exclude": ["node_modules", "dist"]
```

* **`extends`**: A path to another configuration file to inherit settings from. This is very useful in monorepos for creating a base configuration.

```json
"extends": "../../tsconfig.base.json"
```


#### The TypeScript Compiler (`tsc`)

`tsc` is the command-line tool that reads `tsconfig.json` and transpiles your TypeScript code into JavaScript.

* `tsc`: Compiles the entire project found in the current directory.
* `tsc --init`: Creates a `tsconfig.json` file.
* `tsc --watch` or `tsc -w`: Enters "watch mode," where it continuously monitors files for changes and recompiles them automatically.
* `tsc --noEmit`: Runs the type checker on the entire project but does not generate any JavaScript files. This is great for CI pipelines to verify type safety.


#### Integration with Build Tools

In real-world applications, `tsc` is often part of a larger build pipeline.

* **Vite/esbuild**: Modern build tools like Vite use `esbuild` to transpile TypeScript. `esbuild` is extremely fast because it only strips out the types and does **not** perform type checking. Type checking is expected to be done separately (e.g., by running `tsc --noEmit` or through IDE integration).
* **Webpack**: A powerful bundler that uses a "loader" like `ts-loader` to process TypeScript files. `ts-loader` invokes `tsc` and both type-checks and transpiles.
* **Babel**: Can also transpile TypeScript using `@babel/preset-typescript`. Like `esbuild`, it only removes types and does not perform type checking.


### Best Practices \& Pitfalls

* **Best Practice**: Start every project with `tsc --init` and immediately set `"strict": true`.
* **Best Practice**: Separate your source code (`src`) from your compiled output (`dist`) using `rootDir` and `outDir`. This keeps your project clean.
* **Common Pitfall**: Believing that Babel or `esbuild` is enough. These tools only handle transpilation. You **must** also run `tsc --noEmit` somewhere in your workflow (e.g., a pre-commit hook or CI check) to actually get the benefits of TypeScript's type checking.
* **Common Pitfall**: Forgetting to add new directories to the `"include"` array if you're not using the default settings, which can lead to files being silently ignored by the compiler.

***
Would you like to proceed to Section 19: Testing with TypeScript?

---

# yes

Excellent. Let's cover how to effectively test TypeScript code.

### `Section 19: Testing with TypeScript`

Testing in TypeScript provides a significant advantage: your tests themselves are type-checked. This prevents a class of bugs where tests are written against an incorrect or outdated understanding of the code's API, leading to false positives.

#### Setting Up a Testing Environment (with Jest) (IMP)

**Jest** is the most popular testing framework for JavaScript and TypeScript. To make it work with TypeScript, you need a preprocessor to transpile your TS code before Jest runs it.

1. **Installation**: Install Jest and the necessary TypeScript-related packages.

```bash
npm install --save-dev jest typescript ts-jest @types/jest
```

2. **Configuration (`jest.config.js`)**: Create a Jest configuration file. The `ts-jest` preset handles most of the setup automatically.

```javascript
// jest.config.js
/** @type {import('ts-jest').JestConfigWithTsJest} */
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node', // or 'jsdom' for front-end code
};
```

3. **TypeScript Config (`tsconfig.json`)**: It's a good practice to ensure Jest types are available in your project.

```json
{
  "compilerOptions": {
    // ...
    "types": ["jest"]
  }
}
```


#### Writing Tests

Tests are typically written in `.test.ts` or `.spec.ts` files. The syntax is the same as Jest in JavaScript, but with all the benefits of TypeScript's type safety.

**Example**: A simple function and its test.

```typescript
// file: src/utils/math.ts
export function add(a: number, b: number): number {
    return a + b;
}
```

```typescript
// file: src/utils/math.test.ts
import { add } from './math';

describe('add function', () => {
    it('should correctly add two numbers', () => {
        expect(add(2, 3)).toBe(5);
    });

    it('should fail with incorrect types', () => {
        // This line would cause a TypeScript compile error before the test even runs!
        // expect(add('2', 3)).toBe(5);
        // Error: Argument of type 'string' is not assignable to parameter of type 'number'.
    });
});
```


#### Type-Safe Mocks (IMP)

Mocking is essential for isolating units of code during testing. However, a standard `jest.mock()` can create mocks typed as `any`, defeating type safety.

**Problem**: Mocks can become outdated. If you change a function's signature in the original module, a manually written mock will not automatically update, and your tests may still pass with an incorrect implementation.

**Solution**: Use utility types to ensure your mocks conform to the original module's type signature.

**Example**: Mocking a data service.

```typescript
// file: src/services/userService.ts
export const userService = {
    getUser: (id: number): { id: number; name: string } => {
        // ... fetches user from a database
        throw new Error("Not implemented for tests");
    }
};
```

```typescript
// file: src/services/userService.test.ts
import { userService } from './userService';
import { mocked } from 'ts-jest/utils'; // Legacy in ts-jest v29+, now built into jest

// Mock the entire module
jest.mock('./userService');

// Use Jest's built-in `jest.Mocked` utility type for type-safe mocking.
const mockedUserService = userService as jest.Mocked<typeof userService>;

describe('userService', () => {
    it('should return a mocked user', () => {
        // Now the mock is type-safe.
        const mockUser = { id: 1, name: "Mocked User" };
        mockedUserService.getUser.mockReturnValue(mockUser);

        const user = mockedUserService.getUser(1);
        expect(user).toEqual(mockUser);
        expect(mockedUserService.getUser).toHaveBeenCalledWith(1);

        // TypeScript will catch errors if the mock is wrong:
        // mockedUserService.getUser.mockReturnValue({ id: 1 }); // Error: Property 'name' is missing.
    });
});
```

**Note**: `ts-jest`'s `mocked` helper has been integrated into Jest itself via the `jest.Mocked<T>` utility type, which is the modern standard.

### Best Practices \& Pitfalls

* **Best Practice**: Always use type-safe mocking (`jest.Mocked<T>`) to ensure your mocks stay in sync with the real implementation's API.
* **Best Practice**: Keep your test configuration (`jest.config.js`) and TypeScript configuration (`tsconfig.json`) aligned to avoid module resolution issues.
* **Common Pitfall**: Not realizing that build tools like Vite/esbuild or Babel **do not** run type checks during tests by default. You rely on your IDE and a separate `tsc --noEmit` command for that. `ts-jest` is an exception that *does* type-check.
* **Common Pitfall**: Having mocks with incorrect shapes that lead to tests passing for the wrong reasons. Type safety in mocks directly prevents this.

***
Would you like to proceed to Section 20: TypeScript in Real-World Applications?

---

# yes

Of course. Let's explore how TypeScript is applied in major real-world frameworks.

### `Section 20: TypeScript in Real-World Applications`

TypeScript is not just a language; it's a foundational part of the modern development ecosystem. Its adoption in major frameworks has been a key driver of its success, making large-scale application development more robust and manageable.

#### TypeScript with React (IMP)

While React can be written in plain JavaScript, using TypeScript has become the de facto standard for professional projects.

* **Setup**: Modern tools like `create-react-app` and Vite offer TypeScript templates out of the box (`npx create-react-app my-app --template typescript` or `npm create vite@latest my-app -- --template react-ts`).
* **File Extension**: Files containing JSX syntax must use the `.tsx` extension.

**Key Concepts for Typing in React**:

1. **Component Props (`Props`)**: Define the shape of a component's props using an `interface` or `type`.

```tsx
interface UserCardProps {
    userId: number;
    name: string;
    isActive?: boolean;
}

// Use the type to annotate the component's props
const UserCard = ({ userId, name, isActive = false }: UserCardProps) => {
    return (
        <div>
            <h2>{name} (ID: {userId})</h2>
            <p>Status: {isActive ? "Active" : "Inactive"}</p>
        </div>
    );
};
```

2. **State (`useState`)**: The `useState` hook can infer the type from its initial value. For complex types or when the initial value is `null`, you can provide an explicit type.

```tsx
import { useState } from 'react';

// Type is inferred as 'number'
const [count, setCount] = useState(0);

// Explicitly type the state when it can be null or an object
type User = { name: string };
const [user, setUser] = useState<User | null>(null);
```

3. **Event Handling**: TypeScript provides types for DOM events, preventing errors when accessing event properties.

```tsx
import React from 'react';

function MyInput() {
    const handleChange = (event: React.ChangeEvent<HTMLInputElement>) => {
        // 'event.target.value' is known to be a string
        console.log(event.target.value);
    };

    return <input type="text" onChange={handleChange} />;
}
```


#### TypeScript with Angular

Angular is written entirely in TypeScript, and its use is **mandatory**. The framework is designed to leverage TypeScript's features to their fullest.

* **Decorators**: Angular's architecture is built on decorators: `@Component`, `@Injectable`, `@Input()`, etc. These decorators attach metadata to classes, which Angular uses for dependency injection, component rendering, and more.
* **Classes and Services**: Components and services are classes, making OOP patterns and dependency injection natural.
* **Interfaces**: Used extensively to define data models and contracts between different parts of the application.
* **Tooling**: The Angular CLI (`ng`) handles all TypeScript configuration and compilation seamlessly.

```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-greeter',
  template: `<h1>Hello, {{ name }}!</h1>`
})
export class GreeterComponent {
  // @Input decorator uses metadata to define a component property.
  @Input() name: string = '';
}
```


#### TypeScript with Node.js \& Backend Frameworks (e.g., Express)

TypeScript brings type safety to backend development, which is crucial for building reliable APIs and services.

* **Setup**: The common development workflow uses `ts-node` or `tsx` to run TS files directly without a manual compile step. For production, you compile the project to JS using `tsc` and then run the output with Node.
* **`tsconfig.json`**: Key options include `"module": "CommonJS"` (or `"NodeNext"` for modern ES Modules) and `"target"` set to a Node.js-supported ECMAScript version (e.g., `"ES2020"`).
* **Typing Libraries**: The `@types` ecosystem is essential for using JavaScript libraries like Express, Knex, etc.

**Example with Express**:

```typescript
import express, { Request, Response, NextFunction } from 'express';

const app = express();

// The 'Request' and 'Response' types come from '@types/express'
app.get('/users/:id', (req: Request, res: Response) => {
    // TypeScript knows 'req.params' exists and its values are strings.
    const userId = req.params.id;
    res.json({ id: userId, name: `User ${userId}` });
});

app.listen(3000, () => console.log('Server running on port 3000'));
```


### Best Practices \& Pitfalls

* **React Best Practice**: Avoid using `React.FC` for typing components. It has some historical baggage (like implicitly providing `children`) and a simple type annotation on props (`const C = (props: P) => ...`) is now preferred.
* **Node.js Pitfall**: Forgetting that `tsc` only transpiles the code. For a development server that automatically restarts on changes, you need tools like `nodemon` combined with `ts-node`, or a single tool like `ts-node-dev`.
* **General Pitfall**: Assuming a library "just works." Always check if a JavaScript library has a corresponding `@types` package or ships its own `.d.ts` files to get the full benefit of type safety.

***
Would you like to proceed to Section 21: Design Patterns in TypeScript?

---

# yes

Of course. Let's delve into how classical design patterns are implemented and enhanced with TypeScript.

### `Section 21: Design Patterns in TypeScript`

TypeScript's static typing and object-oriented features (like interfaces, abstract classes, and access modifiers) make implementing design patterns safer and more explicit than in plain JavaScript.

#### Singleton Pattern (IMP)

* **Purpose**: Ensures a class has only one instance and provides a single, global point of access to it.
* **TypeScript Enhancement**: The `private constructor` is the key feature. It prevents anyone from creating a new instance of the class using the `new` keyword from outside.

```typescript
class DatabaseConnection {
    private static instance: DatabaseConnection;

    // A private constructor ensures this class cannot be instantiated from outside.
    private constructor() {
        console.log("Connecting to the database...");
        // Initialization logic here
    }

    // The static method provides the single point of access.
    public static getInstance(): DatabaseConnection {
        if (!DatabaseConnection.instance) {
            DatabaseConnection.instance = new DatabaseConnection();
        }
        return DatabaseConnection.instance;
    }

    public query(sql: string) {
        console.log(`Executing query: ${sql}`);
    }
}

// const db1 = new DatabaseConnection(); // Error: Constructor of class 'DatabaseConnection' is private.
const db1 = DatabaseConnection.getInstance();
const db2 = DatabaseConnection.getInstance();

console.log(db1 === db2); // true. Both variables point to the same instance.
db1.query("SELECT * FROM users");
```


#### Factory Pattern (IMP)

* **Purpose**: Creates objects without exposing the instantiation logic to the client. A factory method returns one of several possible classes that share a common superclass or interface.
* **TypeScript Enhancement**: An `interface` or `abstract class` defines the contract for the objects being created, ensuring type safety.

```typescript
// The "Product" interface
interface INotification {
    send(message: string): void;
}

// Concrete Products
class EmailNotification implements INotification {
    send(message: string) { console.log(`Sending email: ${message}`); }
}
class SMSNotification implements INotification {
    send(message: string) { console.log(`Sending SMS: ${message}`); }
}

// The Factory
class NotificationFactory {
    public createNotification(type: "email" | "sms"): INotification {
        switch (type) {
            case "email":
                return new EmailNotification();
            case "sms":
                return new SMSNotification();
            default:
                throw new Error("Invalid notification type");
        }
    }
}

const factory = new NotificationFactory();
const emailNotifier = factory.createNotification("email");
emailNotifier.send("Hello World"); // Outputs: Sending email: Hello World
```


#### Observer Pattern

* **Purpose**: Defines a one-to-many dependency where an object (the subject) maintains a list of dependents (observers) and notifies them automatically of any state changes.
* **TypeScript Enhancement**: Interfaces for `Subject` and `Observer` create a clear and type-safe contract. `private` properties protect the list of observers.

```typescript
interface IObserver {
    update(data: any): void;
}

interface ISubject {
    attach(observer: IObserver): void;
    detach(observer: IObserver): void;
    notify(): void;
}

class WeatherStation implements ISubject {
    private observers: IObserver[] = [];
    private temperature: number = 0;

    attach(observer: IObserver): void { this.observers.push(observer); }
    detach(observer: IObserver): void { /* ... logic to remove observer ... */ }
    notify(): void {
        this.observers.forEach(observer => observer.update(this.temperature));
    }

    setTemperature(temp: number) {
        this.temperature = temp;
        console.log(`Weather station updated temperature to ${temp}°C.`);
        this.notify();
    }
}

class TemperatureDisplay implements IObserver {
    update(temperature: number) {
        console.log(`Display: Temperature is now ${temperature}°C.`);
    }
}

const station = new WeatherStation();
const display1 = new TemperatureDisplay();
station.attach(display1);
station.setTemperature(25); // Will notify display1
```


#### Strategy Pattern

* **Purpose**: Defines a family of interchangeable algorithms and encapsulates each one. This allows the algorithm to be selected at runtime.
* **TypeScript Enhancement**: An `interface` defines the shape of the "strategy," ensuring any provided strategy object has the required method.

```typescript
interface IShippingStrategy {
    calculate(weight: number): number;
}

class FedExStrategy implements IShippingStrategy {
    calculate(weight: number): number { return weight * 3.5; }
}

class UPSStrategy implements IShippingStrategy {
    calculate(weight: number): number { return weight * 2.8; }
}

class ShoppingCart {
    private strategy: IShippingStrategy;

    constructor(strategy: IShippingStrategy) {
        this.strategy = strategy;
    }

    setStrategy(strategy: IShippingStrategy) {
        this.strategy = strategy;
    }

    calculateShipping(weight: number): number {
        return this.strategy.calculate(weight);
    }
}

const cart = new ShoppingCart(new FedExStrategy());
console.log(cart.calculateShipping(10)); // 35

cart.setStrategy(new UPSStrategy());
console.log(cart.calculateShipping(10)); // 28
```


#### Decorator Pattern (Structural)

**Important**: This is a *structural design pattern*, distinct from TypeScript's *decorator language feature* (`@decorator`). This pattern is about wrapping objects to add new behavior.

* **Purpose**: Dynamically add new functionality to an object without altering its class.
* **TypeScript Enhancement**: `abstract` classes and `interface`s are used to define the core component and the decorator contract, ensuring compatibility.

```typescript
// The core component interface
interface ICoffee {
    getCost(): number;
    getDescription(): string;
}

// A concrete component
class SimpleCoffee implements ICoffee {
    getCost(): number { return 10; }
    getDescription(): string { return "Simple coffee"; }
}

// An abstract decorator class
abstract class CoffeeDecorator implements ICoffee {
    constructor(protected coffee: ICoffee) {}

    abstract getCost(): number;
    abstract getDescription(): string;
}

// Concrete decorators
class MilkDecorator extends CoffeeDecorator {
    getCost(): number { return this.coffee.getCost() + 2; }
    getDescription(): string { return `${this.coffee.getDescription()}, milk`; }
}

class SugarDecorator extends CoffeeDecorator {
    getCost(): number { return this.coffee.getCost() + 1; }
    getDescription(): string { return `${this.coffee.getDescription()}, sugar`; }
}

let coffee: ICoffee = new SimpleCoffee();
console.log(`${coffee.getDescription()} costs $${coffee.getCost()}`); // Simple coffee costs $10

coffee = new MilkDecorator(coffee);
console.log(`${coffee.getDescription()} costs $${coffee.getCost()}`); // Simple coffee, milk costs $12

coffee = new SugarDecorator(coffee);
console.log(`${coffee.getDescription()} costs $${coffee.getCost()}`); // Simple coffee, milk, sugar costs $13
```


***
Would you like to proceed to Section 22: Performance \& Optimization?

---

# yes

Certainly. Let's discuss performance and optimization strategies in a TypeScript project.

### `Section 22: Performance & Optimization`

Optimizing a TypeScript project involves improving three key areas: **compilation speed**, final **bundle size**, and the **runtime performance** of the generated JavaScript.

#### 1. Compilation Speed (Build Time)

This is about how quickly your TypeScript code is checked and transpiled. Slow build times can severely impact developer productivity.

* **Incremental Compilation (`--watch`)**: Running `tsc --watch` allows the compiler to keep running, watch for file changes, and recompile only the files that have been modified. This is significantly faster than a full re-compile every time.
* **Project References (`--build`) (IMP)**: For large monorepos, project references are the most effective tool. You can split your codebase into smaller, interdependent sub-projects, each with its own `tsconfig.json`. When you run `tsc --build`, TypeScript intelligently builds only the projects that have changed and their dependents, avoiding redundant work.
* **Separating Transpilation and Type-Checking (IMP)**: This is the standard approach in modern development.
    * **Transpilation**: Use a fast transpiler like **esbuild** (used by Vite), **swc** (used by Next.js), or **Babel**. These tools are incredibly fast because they *only* strip out TypeScript syntax and do **not** perform type-checking.
    * **Type-Checking**: Run `tsc --noEmit` in a separate process. This tells the compiler to perform a full type-check of the project but not to generate any JavaScript files.
    * **Workflow**: During development, the fast transpiler provides near-instant reloads. The type-checker runs in the background (or as a pre-commit hook) to catch type errors.
* **`skipLibCheck`**: Set `"skipLibCheck": true` in `tsconfig.json`. This tells `tsc` to skip type-checking of all declaration files (`.d.ts`), including those in `node_modules`. This can dramatically speed up compilation in projects with many dependencies.
    * **Trade-off**: You might miss type errors caused by inconsistencies in library type definitions.


#### 2. Bundle Size Optimization

This is critical for web applications, as smaller bundles lead to faster page loads.

* **Use `const enum`**: As mentioned previously, `const enum` members are inlined by the compiler, and the enum object is completely erased. This results in zero bundle size overhead, unlike regular enums which generate a JavaScript lookup object.
* **Enable Tree Shaking via ES Modules**: TypeScript's use of ES Modules (`import`/`export`) is what allows bundlers like Webpack, Rollup, and Vite to perform **tree-shaking**. This process analyzes your imports and exports to eliminate any code that is not actually being used, significantly reducing the final bundle size.
* **`importHelpers` and `tslib`**: When TypeScript transpiles modern features (like `async/await` or class inheritance) for older JavaScript targets (like `ES5`), it sometimes needs to inject helper functions (e.g., `__awaiter`, `__extends`). By default, these helpers are added to every file that needs them, causing code duplication.
    * **Solution**:

1. Set `"importHelpers": true` in your `tsconfig.json`.
2. Add `tslib` as a dependency: `npm install tslib`.
    * Now, `tsc` will import these helpers from the `tslib` library instead of inlining them, reducing code duplication and overall bundle size.


#### 3. Runtime Performance (Zero-Cost Abstractions) (IMP)

A common misconception is that TypeScript adds runtime overhead. For the most part, this is untrue.

* **Erased Features (Zero Runtime Cost)**: Most of what makes TypeScript special exists only at compile time. These features are completely **erased** during compilation and have **zero impact** on runtime performance. This includes:
    * Interfaces (`interface`)
    * Type Aliases (`type`)
    * Type annotations (e.g., `: string`)
    * Generics (`<T>`)
    * The `declare` keyword
* **Emitted Features (Runtime Cost)**: Some features have a direct JavaScript equivalent and therefore generate code that runs in the browser or Node.js.
    * `class`
    * `enum` (regular enums generate a lookup object)
    * `namespace`
    * Decorators (can add significant runtime logic)

**Takeaway**: You can use TypeScript's powerful type system (interfaces, generics, etc.) as much as you want without worrying about slowing down your application's execution speed.

### Best Practices \& Pitfalls

* **Best Practice**: For fast development, use a modern tool like Vite that leverages `esbuild` for transpilation and run `tsc --noEmit` separately for type safety.
* **Best Practice**: In production builds for the web, always use `importHelpers` with `tslib` to minimize bundle size.
* **Common Pitfall**: Confusing build-time performance with runtime performance. TypeScript adds overhead to your build process, but it does so to *prevent* runtime errors and has a minimal-to-zero effect on the final code's execution speed.

***
Would you like to proceed to Section 23: Working with External Types?

---

# yes

Of course. This section is key for integrating TypeScript with the wider JavaScript ecosystem.

### `Section 23: Working with External Types`

This topic covers how to provide type information for code that exists outside your TypeScript project, such as third-party JavaScript libraries or global variables provided by a browser or Node.js environment.

#### Ambient Declarations (`declare`) (IMP)

The `declare` keyword is used to tell the TypeScript compiler that a variable, function, or module exists at runtime, even though its source code is not visible to the compiler. This is done inside a declaration file (`.d.ts`).

**Real-World Analogy**: `declare` is like making a promise to the compiler. You're saying, "Don't worry about where this comes from. I promise that at runtime, there will be a thing with this name and this type."

1. **Declaring a Global Variable**: To type a global variable (e.g., one added by a `<script>` tag).

```typescript
// in a global.d.ts file
declare const myGlobalApi: {
  init: (config: object) => void;
};

// Now you can use it safely in your .ts files
myGlobalApi.init({ key: "123" });
```

2. **Declaring a Module (Shim)**: If you're using a JavaScript library that has no type definitions, the import will cause an error. You can create a "shim" declaration file to quickly resolve this.

```typescript
// in a shims.d.ts file
declare module 'untyped-javascript-library';

// in your app.ts
import * as lib from 'untyped-javascript-library'; // 'lib' will be of type 'any'
```

This silences the error but gives you no type safety. It's a quick fix, not a complete solution.

#### Declaration Merging: Extending External Types (IMP)

Often, you'll need to add properties to existing interfaces defined by TypeScript or another library. This is called **module augmentation** or **declaration merging**.

* **Requirement**: You must be in a module (a file with at least one `import` or `export`). To augment global types, you declare a `global` block.

**Example 1: Augmenting the global `Window` interface**

```typescript
// in a window.d.ts file
export {}; // Make this file a module

declare global {
  interface Window {
    // Add a custom property to the window object
    __MY_APP_DATA__: {
      user: string;
    };
  }
}
```

**Example 2: Augmenting Express's `Request` object**
This is a very common pattern in backend development to add custom properties (like a user object from authentication middleware).

```typescript
// in a express.d.ts file
import { User } from './models/user'; // Assume User model is defined

declare global {
  namespace Express {
    // Merge our 'user' property into the existing Request interface
    export interface Request {
      user?: User;
    }
  }
}
```


#### Creating Your Own `.d.ts` Files

When a library doesn't have an `@types` package, you should create your own declaration file.

1. **Create a file**: Name it something like `my-library.d.ts` and place it in a `types` or `typings` directory at your project root.
2. **Ensure it's included**: Make sure your `tsconfig.json`'s `include` array covers this directory.

```json
{
  "include": ["src/**/*", "types/**/*"]
}
```

3. **Write the declarations**:

```typescript
// in types/my-library.d.ts
declare module 'my-library' {
  // Describe the shape of the module's exports
  export function doSomething(config: { a: number }): boolean;
  export const version: string;
}
```


### Best Practices \& Pitfalls

* **Best Practice**: Always check for an official `@types` package from DefinitelyTyped before writing your own declarations.
* **Best Practice**: Create a dedicated `types` or `typings` folder in your project for all custom `.d.ts` files to keep them organized.
* **Common Pitfall**: Trying to add implementation logic (e.g., `function myFunction() { ... }`) inside a `.d.ts` file. These files are for type definitions **only**.
* **Common Pitfall**: Modifying interfaces directly in `node_modules`. These changes will be lost on the next `npm install`. Always use module augmentation in your own project files.
* **Common Pitfall**: Creating a global declaration in a file that is already a module (i.e., has top-level `import`/`export`). To modify the global scope from within a module, you must wrap your declarations in a `declare global { ... }` block.

***
Would you like to proceed to Section 24: Miscellaneous \& Advanced?

---

# yes

Of course. Here is the final section of the revision guide, covering a range of advanced and modern TypeScript features.

### `Section 24: Miscellaneous & Advanced`

This section covers several powerful, modern, or niche features that demonstrate a deep understanding of TypeScript's capabilities.

#### `const` Assertions (`as const`) (IMP)

A `const` assertion tells TypeScript to infer the narrowest possible, immutable type for a literal expression.

**Real-World Analogy**: It's like flash-freezing an object. Once frozen (`as const`), its shape and values are locked in place, and TypeScript treats them as exact literals rather than general types.

It has three main effects:

1. **Literals become Literal Types**: `let x = "hello"` is type `string`. `let x = "hello" as const` is type `"hello"`.
2. **Object properties become `readonly`**:
3. **Arrays become `readonly` tuples**:

**Example**: Creating a fixed set of options without an enum.

```typescript
// Without 'as const'
export const routes = {
    home: '/',
    about: '/about',
};
// Type is { home: string; about: string; }

// With 'as const'
export const ROLES = {
    ADMIN: 'admin',
    USER: 'user',
} as const;
// Type is { readonly ADMIN: "admin"; readonly USER: "user"; }

// This allows us to create a union type of the values
type Role = typeof ROLES[keyof typeof ROLES]; // "admin" | "user"

function assignRole(role: Role) { /* ... */ }
assignRole(ROLES.ADMIN); // Works
// assignRole("editor"); // Error: "editor" is not assignable to type 'Role'
```

This pattern is often preferred over `enum` for its simplicity and zero runtime cost.

#### The `satisfies` Operator (TypeScript 4.9+) (IMP)

The `satisfies` operator allows you to validate that an expression conforms to a type **without changing the expression's own inferred type**. This solves the problem where annotating a variable with a broad type makes you lose the more specific information of its value.

**Problem without `satisfies`**:

```typescript
type Config = Record<string, string | number>;

const config: Config = { // Annotated with Config
    port: 8080,
    env: 'production'
};

// config.env.toUpperCase(); // Error: Property 'toUpperCase' does not exist on type 'string | number'.
// We lost the specific type information that 'env' is a string.
```

**Solution with `satisfies`**:

```typescript
type Config = Record<string, string | number>;

const config = {
    port: 8080,
    env: 'production'
} satisfies Config; // Validated against Config, but type is NOT changed.

// Now TypeScript remembers the specific types!
// 'config.env' is known to be 'string'.
config.env.toUpperCase(); // Works!
```

**Takeaway**: Use `satisfies` when you want to ensure an object matches a certain shape while preserving its specific literal types for later use.

#### Mixins

Since JavaScript classes can only extend a single superclass, mixins are a pattern used to compose functionality from multiple sources into a single class.

**Implementation**: This is a pattern, not a built-in feature. It's typically implemented with a helper function that merges the properties of multiple base classes into a target class.

```typescript
// A common mixin implementation helper
function applyMixins(derivedCtor: any, baseCtors: any[]) {
  baseCtors.forEach(baseCtor => {
    Object.getOwnPropertyNames(baseCtor.prototype).forEach(name => {
      Object.defineProperty(derivedCtor.prototype, name, Object.getOwnPropertyDescriptor(baseCtor.prototype, name)!);
    });
  });
}

// Reusable functionality in classes
class CanFly { fly() { console.log('Flying!'); } }
class CanSwim { swim() { console.log('Swimming!'); } }

// The target class
class SuperDuck implements CanFly, CanSwim {
    // These are required to satisfy the interface but will be implemented by the mixin.
    fly!: () => void;
    swim!: () => void;
}

// Mix in the functionality
applyMixins(SuperDuck, [CanFly, CanSwim]);

const duck = new SuperDuck();
duck.fly();   // "Flying!"
duck.swim();  // "Swimming!"
```


#### Declaration Merging (Recap)

As covered in Section 6, this is TypeScript's ability to merge multiple declarations with the same name into a single definition.

* It applies to `interface` and `namespace`.
* It **does not** apply to `type` aliases, `class`, or `function`.
* Its primary use cases are:
    * Augmenting interfaces from third-party libraries (module augmentation).
    * Splitting a large `namespace` across multiple files.

***

This concludes the TypeScript quick revision guide. You now have a comprehensive set of notes covering the most important concepts for interview preparation. Good luck

