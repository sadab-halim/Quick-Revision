<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# You are a Python expert and mentor.

Your task is to generate a structured **quick revision notes for interview preparation** on Python, broken into sections.  
I will specify which section to start from, and you will cover ONLY that section in detail.  
You should cover all the important topics from each section and it's sub-section which are most asked in interviews, mark the topic as (IMP) which is most asked and is a hot question

### Output Rules:

- Be concise, yet cover all the concepts, revision notes should be crisp and clear.
- Use headings, bullet points, tables, and short code snippets.
- Highlight **common pitfalls**, **best practices**, and **Python version notes** (2 vs 3, 3.10 pattern matching, 3.12 features, etc.).
- Use comparison tables when explaining differences (e.g., list vs tuple, sync vs async).
- Include **short examples** to illustrate key points.
- For complex or abstract topics (e.g., coroutines, GIL, metaclasses), use **real-life analogies** to simplify learning.
- End each section by asking if I want to continue with the next one.


### Sections:

1. Python Fundamentals
Python history, philosophy (PEP 20 – Zen of Python)
Installing and managing Python (pyenv, conda, venv)
Python execution model (script mode, interactive mode, REPL, Jupyter)
Syntax basics: indentation, comments, docstrings
Data types overview: int, float, bool, str, bytes, NoneType
Variable assignment and naming conventions
Dynamic typing and duck typing
Boolean context \& truthiness rules (__bool__, __len__)
help(), dir(), id(), type(), isinstance()
2. Numbers, Strings, and Collections
Numeric types: int, float, complex, Decimal, Fraction
Operators: arithmetic, comparison, logical, bitwise, identity, membership
Augmented assignments (__iadd__, etc.)
Strings: indexing, slicing, immutability, f-strings, .format()
String methods: search, replace, split, join, case transformations
Bytes vs strings, encoding/decoding
Sequence unpacking \& starred expressions (a, *rest, b = seq)
Lists: creation, methods, comprehensions
Tuples: immutability, namedtuple, unpacking
Sets \& frozenset: set operations, comprehensions
Dictionaries: creation, methods, dict comprehensions
OrderedDict, defaultdict, Counter from collections
3. Control Flow \& Iteration
if, elif, else
for and while loops
break, continue, else on loops
pass, del
Comprehensions: list/dict/set/generator expressions
Comprehension scoping rules
enumerate, zip, range, map, filter
any(), all()
Pattern matching (match / case, 3.10+)
Pattern matching exhaustiveness (3.11+)
while True patterns, sentinel loops
4. Functions
Defining functions, parameters, return values
Positional-only (/) and keyword-only (*) parameters
Default arguments \& pitfalls (mutable defaults)
Arbitrary arguments (*args, **kwargs)
Extended unpacking in calls (func(*args, **kwargs))
Lambda functions and limitations
Higher-order functions
Function annotations \& typing hints
functools utilities (partial, lru_cache, cache)
Closures and variable scope (LEGB rule)
global and nonlocal
__call__ for callable objects
Decorators (function \& class decorators)
Parametrized decorators
5. Modules \& Packages
Import mechanics, absolute vs relative imports
__name__ == "__main__" idiom
Module search path (sys.path)
Packages, __init__.py behavior
Built-in modules overview (math, os, sys, itertools, functools, pathlib)
Namespaces and importlib
Packaging projects (pyproject.toml, setuptools, poetry, flit)
6. Object-Oriented Programming
Classes, instances, attributes, methods
__init__, __new__, __del__
Instance vs class vs static methods
Class attributes vs instance attributes
Inheritance, method resolution order (MRO)
Multiple inheritance and super()
Special methods for operators (__add__, __eq__, __lt__, etc.)
__hash__ \& equality contract
Truthiness with __bool__
__str__ vs __repr__
Abstract base classes (abc module)
Data classes (dataclasses.dataclass)
attrs library overview
__slots__ for memory optimization
7. Exceptions \& Error Handling
try, except, else, finally
Catching specific exceptions vs generic Exception
Raising exceptions (raise)
Exception chaining (raise from)
Custom exceptions
Built-in exception hierarchy
Context managers (with), __enter__ / __exit__
contextlib utilities (closing, suppress, ContextDecorator)
Async context managers (async with)
Exception groups \& except* (Python 3.11)
8. Iterators, Generators, and Coroutines
Iteration protocol (__iter__, __next__)
Generator functions \& yield
send(), throw() in generators
Generator expressions vs comprehensions
itertools module advanced functions
Async iteration (async for)
Coroutines with async def
Awaitables \& Tasks
9. Concurrency \& Parallelism
Threading basics (threading module)
Thread pools (concurrent.futures.ThreadPoolExecutor)
Multiprocessing basics and pools
Shared memory (multiprocessing.shared_memory)
Locks, Events, Conditions, Semaphores
Asyncio: event loop, tasks, task groups (3.11+)
Structured concurrency concepts in Python
Queues: queue.Queue, asyncio.Queue, multiprocessing.Queue
GIL and its implications
Subinterpreters (PEP 554 proposal awareness)
10. File I/O and OS Interaction
Reading/writing text and binary files
File modes and buffering
Context managers for files
os, shutil, glob, fnmatch
Path handling with pathlib
Temporary files (tempfile)
Memory-mapped files (mmap)
Environment variables (os.environ)
11. Networking \& IPC
TCP/UDP sockets (socket module)
selectors for multiplexing
HTTP requests (urllib, httpx, requests)
REST APIs with http.server
WebSockets (websockets lib)
Inter-process communication (pipes, queues)
xmlrpc and gRPC basics
12. Data Formats \& Parsing
JSON (json module), YAML (PyYAML), TOML (tomllib)
CSV, TSV parsing (csv module, pandas awareness)
XML parsing (xml.etree.ElementTree, lxml)
HTML parsing (html.parser, BeautifulSoup)
Regex (re module)
struct and binary parsing
13. Testing \& Quality
unittest, pytest frameworks
Fixtures and parametrization
Mocking (unittest.mock)
Code coverage (coverage.py)
Static analysis: pylint, flake8, bandit
Type checking: mypy, pyright
Property-based testing (hypothesis)
Pre-commit hooks
14. Standard Library Mastery
functools, itertools, collections, statistics
datetime, zoneinfo, calendar
decimal, fractions
weakref
copy (shallow vs deep copy)
logging advanced configs
argparse for CLI parsing
configparser, dataclasses, typing
15. Python Internals
CPython execution model (bytecode, interpreter loop)
dis module for disassembly
Python object model (PyObject, reference counting)
Garbage collection \& gc module
Memory management, interning
Buffer protocol (memoryview)
C API basics for extensions (ctypes, cffi)
Building Python from source
PyPy, MicroPython, Nuitka, Cython overview
16. Packaging, Distribution \& Deployment
pip, pipx, editable installs
setuptools, wheel, twine
pyproject.toml builds (PEP 517/518)
Virtual environments vs Conda
Dockerizing Python apps
Publishing to PyPI
17. Domain-Specific Python
Web development (Flask, Django, FastAPI)
Data science (numpy, pandas, matplotlib, seaborn, polars)
Machine learning (scikit-learn, PyTorch, TensorFlow)
Automation (Selenium, Playwright, PyAutoGUI)
GUI (Tkinter, PyQt, Kivy)
Game development (pygame, pyglet)
Robotics/IoT (MicroPython, CircuitPython)
18. Advanced Typing \& Code Design
typing module: List, Dict, Union, Optional, Literal
Protocols, TypedDict, Self, TypeVarTuple, Unpack
Generics in Python
Final, ClassVar
Design patterns in Python (singleton, factory, observer, strategy)
Functional programming style (map/filter/reduce, composition)

### Instruction:

When I say **"Start from Section X"**, generate the revision guide for that section only.  
When done, ask me if I want to continue with the next section.  
Always maintain the same style so the entire revision guide feels consistent.

I am ready to be your Python mentor and generate the revision notes according to your specifications. Please let me know which section you would like to start with by saying **"Start from Section X"**.

---

# Start from Section 1

Here are the revision notes for Section 1: Python Fundamentals.

### Python History \& Philosophy

- Created by **Guido van Rossum** and first released in 1991.
- Its philosophy emphasizes code readability and simplicity.
- The core principles are captured in **PEP 20 – The Zen of Python**. You can view them by running `import this` in a Python interpreter.
- Key tenets include: "Beautiful is better than ugly," "Explicit is better than implicit," and "Readability counts."


### Python Installation \& Environment Management (IMP)

Managing Python versions and project dependencies is a crucial skill. The standard is to use one virtual environment per project.


| Tool | Purpose | Use Case | Best Practice |
| :-- | :-- | :-- | :-- |
| **`venv`** | Creates lightweight, isolated virtual environments. | The default choice for application development. It keeps project dependencies separate. | Always create a `venv` for a new project. `python3 -m venv .venv` |
| **`pyenv`** | Manages multiple Python versions on a single machine. | When you need to switch between Python 3.8, 3.10, and 3.12 for different projects. | Use it to install specific Python versions, then use `venv` within a project. |
| **`conda`** | Manages environments and packages (Python and non-Python). | Ideal for data science, as it handles complex binary dependencies like NumPy and SciPy efficiently. | Use when your project depends on C/Fortran libraries or other non-Python tools. |

- **Common Pitfall**: Installing packages directly into the global Python installation. This leads to dependency conflicts between projects. Always use a virtual environment.


### Python Execution Model

- **Script Mode**: The standard way to run a program. The interpreter executes the code in a `.py` file from top to bottom.

```bash
python my_app.py
```

- **Interactive Mode (REPL)**: Started by typing `python` in your terminal. It provides a Read-Eval-Print Loop for running commands one by one, which is great for quick tests and exploration.
- **Jupyter Notebooks**: A web-based interactive environment that presents code in cells. It allows mixing code, text, and visualizations, making it popular for data analysis and prototyping.


### Syntax Basics (IMP)

- **Indentation**: Python uses whitespace (typically 4 spaces) to define code blocks (loops, functions, classes, etc.). This is a strict syntactical rule, not just a style preference.
- **Comments**: Begin with a hash (`#`). They are ignored by the interpreter.
- **Docstrings**: A string literal (`"""..."""` or `'''...'''`) that appears as the first statement in a module, function, class, or method definition. They are stored in the `__doc__` attribute and used by tools like `help()` to generate documentation.

```python
def calculate_sum(a, b):
    """This function returns the sum of two numbers."""
    return a + b

print(calculate_sum.__doc__)
# Output: This function returns the sum of two numbers.
```


### Data Types Overview

- **`int`**: Arbitrary-precision integers.
- **`float`**: 64-bit double-precision floating-point numbers.
- **`bool`**: Represents `True` or `False`. It is a subclass of `int` where `True` == `1` and `False` == `0`.
- **`str`**: Immutable sequence of Unicode characters.
- **`bytes`**: Immutable sequence of bytes (numbers from 0-255).
- **`NoneType`**: The type for the `None` object, which represents the absence of a value.
- **Python Version Note**: Python 3 unified `int` and `long` from Python 2 into a single `int` type that can grow to any size.


### Variable Assignment and Naming

- **Assignment**: `name = object`. A name is a reference to an object in memory.
- **PEP 8 Naming Conventions**:
    - `snake_case` for functions and variables (`my_variable`).
    - `PascalCase` for classes (`MyClass`).
    - `_leading_underscore`: A hint for internal use, not enforced.
    - `__double_leading_underscore`: Triggers name mangling in a class context.


### Dynamic Typing and Duck Typing (IMP)

- **Dynamic Typing**: Variable types are determined and checked at **runtime**. A variable can hold an integer and later be reassigned a string.

```python
x = 10      # x is an int
x = "hello" # Now x is a str
```

- **Duck Typing**: An object's suitability is determined by its methods and properties, not its explicit type. "If it walks like a duck and quacks like a duck, it is a duck."
- **Analogy**: Imagine a universal charging port (USB-C). You can plug in a phone, a laptop, or headphones. The port doesn't care *what* the device is (`type`); it only cares if the device can *handle charging* (has the right method/protocol). Python operates similarly; the `len()` function doesn't care if an object is a `list` or `str`, only that it implements the `__len__()` method.


### Boolean Context \& Truthiness (IMP)

An object's truth value is used in conditions like `if` or `while`.

- **Falsy Values**:
    - `None`
    - `False`
    - Zero of any numeric type: `0`, `0.0`, `0j`
    - Any empty sequence or collection: `''`, `()`, `[]`, `{}`
    - Objects from user-defined classes that have a `__bool__()` method returning `False` or a `__len__()` method returning `0`.
- **Truthy Values**: All other objects are considered `True`.
- **Evaluation Order**: For a custom object, Python first looks for a `__bool__()` method. If not found, it looks for `__len__()`. If neither exists, the object is always considered `True`.


### Built-in Introspection Functions (IMP)

These functions are essential for debugging and understanding your code.

- **`id(obj)`**: Returns the memory address of an object. Useful for checking if two variables point to the exact same object.

```python
a = [1, 2]
b = a
c = [1, 2]
print(id(a) == id(b)) # True, b is another name for a
print(id(a) == id(c)) # False, c is a different object with the same content
```

- **`type(obj)`**: Returns the type of an object.
- **`isinstance(obj, classinfo)`**: Returns `True` if `obj` is an instance of `classinfo` or any of its subclasses.
- **Best Practice**: Prefer `isinstance()` over `type()` for type checking, as it correctly handles inheritance.

```python
class MyInt(int): pass
x = MyInt(5)

print(type(x) == int)         # False
print(isinstance(x, int))   # True
```

- **`dir(obj)`**: Lists the attributes and methods of an object. Very useful for interactive exploration.
- **`help(obj)`**: Displays the documentation (docstring) and signature of an object, function, or module.

***
Would you like to continue with Section 2: Numbers, Strings, and Collections?

---

# yes

Of course. Here are the revision notes for Section 2: Numbers, Strings, and Collections.

### Numeric Types

Python offers several numeric types to suit different needs.


| Type | Description | Use Case | Example |
| :-- | :-- | :-- | :-- |
| **`int`** | Arbitrary-precision integers. | General-purpose whole number calculations. | `x = 1_000_000` |
| **`float`** | 64-bit floating-point numbers. | Scientific and engineering calculations where precision loss is acceptable. | `pi = 3.14159` |
| **`complex`** | Numbers with a real and imaginary part. | Electrical engineering, physics simulations. | `c = 2 + 3j` |
| **`Decimal`** | User-settable precision decimal numbers. From the `decimal` module. | **Financial calculations (IMP)**. Avoids floating-point inaccuracies. | `from decimal import Decimal; Decimal('10.1') + Decimal('20.2')` |
| **`Fraction`** | Rational numbers (numerator/denominator). From the `fractions` module. | When you need to represent exact ratios. | `from fractions import Fraction; Fraction(1, 3)` |

- **Common Pitfall**: Using `float` for money. Floating-point arithmetic can lead to rounding errors. Always use `Decimal` for financial applications.

```python
# Floating-point inaccuracy
print(0.1 + 0.2)  # Output: 0.30000000000000004

# Correct way with Decimal
from decimal import Decimal
print(Decimal('0.1') + Decimal('0.2')) # Output: Decimal('0.3')
```


### Operators

- **Arithmetic**: `+`, `-`, `*`, `/` (float division), `//` (integer division), `%` (modulo), `**` (exponent).
- **Comparison**: `==`, `!=`, `>`, `<`, `>=`, `<=`.
- **Logical**: `and`, `or`, `not`.
- **Bitwise**: `&` (AND), `|` (OR), `^` (XOR), `~` (NOT), `<<` (left shift), `>>` (right shift).
- **Identity**: `is`, `is not`. Checks if two variables point to the **same object in memory (IMP)**.
- **Membership**: `in`, `not in`. Checks for presence in a sequence.


### Augmented Assignments

These are shorthand operators (`+=`, `-=`, `*=`, etc.) that combine an operation with an assignment. For mutable types like lists, they often modify the object **in-place**.

```python
x = 10
x += 2  # Same as x = x + 2

my_list = [1, 2]
original_id = id(my_list)
my_list += [3, 4]  # In-place modification (__iadd__)
print(id(my_list) == original_id) # True
```


### Strings

- **Immutability (IMP)**: Once a string is created, it cannot be changed. Methods like `replace()` or `upper()` return a **new** string.
- **Indexing \& Slicing**: Access characters with `s[i]` and subsequences with `s[start:stop:step]`.
- **String Formatting (IMP)**:
    - **f-strings (Python 3.6+)**: The modern, preferred way. They are readable and fast.

```python
name = "Alice"
age = 30
print(f"User: {name}, Age: {age}")
```

    - **`.format()` method**: More verbose but more powerful for complex cases.

```python
print("User: {}, Age: {}".format(name, age))
```

- **Common String Methods**:
    - `.strip()`, `.lstrip()`, `.rstrip()`: Remove whitespace.
    - `.split(delimiter)`: Creates a list of substrings.
    - `delimiter.join(iterable)`: Joins elements of an iterable into a single string.
    - `.find()`, `.index()`: Find a substring (`.find()` returns -1 on failure, `.index()` raises `ValueError`).
    - `.replace(old, new)`: Returns a new string with replacements.
    - `.upper()`, `.lower()`, `.capitalize()`: Case transformations.
- **Bytes vs. Strings (IMP)**: This is a critical concept, especially for I/O and networking.
    - **Analogy**: A `str` is like a sheet of music—it's the abstract idea of the melody and notes. A `bytes` object is like the actual audio recording of that music in a specific format (like MP3 or WAV). You can't listen to sheet music directly; you must first *perform* (encode) it.
    - **`str`**: A sequence of **Unicode characters** for representing text.
    - **`bytes`**: A sequence of **raw bytes** (0-255) for representing binary data (files, network packets).
    - **`encode()`**: Converts `str` to `bytes`. `text.encode('utf-8')`.
    - **`decode()`**: Converts `bytes` to `str`. `data.decode('utf-8')`.
- **Python Version Note**: Python 3 made a strict distinction between `str` (Unicode) and `bytes`, resolving a major source of bugs in Python 2.


### Sequence Unpacking \& Starred Expressions (IMP)

- You can assign elements of a sequence to multiple variables.

```python
# Basic unpacking
p = (4, 5)
x, y = p # x=4, y=5

# Extended unpacking (Python 3+)
numbers = [1, 2, 3, 4, 5]
first, *middle, last = numbers
# first = 1
# middle = [2, 3, 4]
# last = 5
```


### Collections

| Collection | Key Characteristics | When to Use |
| :-- | :-- | :-- |
| **`list`** | Mutable, ordered, allows duplicates. | A general-purpose collection of items that you may need to change. |
| **`tuple`** | **Immutable**, ordered, allows duplicates. | Protecting data from changes; using as a dictionary key; returning multiple values from a function. |
| **`set`** | Mutable, **unordered**, **no duplicates**. | Removing duplicates; fast membership testing (`x in my_set`); mathematical set operations (union, intersection). |
| **`dict`** | Mutable, **ordered (Python 3.7+)**, stores key-value pairs. | Associating data; fast lookups by key. |

- **Comprehensions (IMP)**: A concise and readable way to create lists, sets, and dictionaries.

```python
# List comprehension
squares = [x**2 for x in range(10) if x % 2 == 0] # [0, 4, 16, 36, 64]

# Dict comprehension
square_map = {x: x**2 for x in range(5)} # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```


### Specialized Collections (`collections` module)

- **`collections.namedtuple`**: A factory function for creating tuple subclasses with named fields. Improves code readability.

```python
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(10, 20)
print(p.x + p.y) # 30
```

- **`collections.defaultdict` (IMP)**: A `dict` subclass that calls a factory function to supply missing values. Great for grouping or counting items.

```python
from collections import defaultdict

s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4)]
d = defaultdict(list)
for k, v in s:
    d[k].append(v)
# d is now defaultdict(<class 'list'>, {'yellow': [1, 3], 'blue': [2, 4]})
```

- **`collections.Counter`**: A `dict` subclass for counting hashable objects.

```python
from collections import Counter
c = Counter('abracadabra')
# c is Counter({'a': 5, 'b': 2, 'r': 2, 'c': 1, 'd': 1})
```

- **Python Version Note**: Dictionaries became insertion-ordered by default in Python 3.7. Before that, if you needed to preserve order, you had to use `collections.OrderedDict`. `OrderedDict` is still useful for its `move_to_end()` method and because its equality check considers order.

***
Would you like to continue with Section 3: Control Flow \& Iteration?

---

# yes

Excellent. Here are the revision notes for Section 3: Control Flow \& Iteration.

### `if`, `elif`, `else`

This is the standard conditional statement for executing code based on a condition's truthiness.

```python
score = 85
if score >= 90:
    grade = 'A'
elif score >= 80:
    grade = 'B'
else:
    grade = 'C'
print(grade) # Output: B
```


### Loops: `for` and `while`

- **`for` loop**: Iterates over the items of any sequence or iterable (`list`, `tuple`, `str`, `dict`, `range`).

```python
for char in "hello":
    print(char)
```

- **`while` loop**: Repeats as long as a condition is `True`.

```python
count = 3
while count > 0:
    print(count)
    count -= 1
```


### Loop Control: `break`, `continue`, and `else` (IMP)

- **`break`**: Immediately terminates the innermost loop.
- **`continue`**: Skips the rest of the current iteration and proceeds to the next one.
- **`else` on loops**: A special block that runs **only if the loop completes normally** (i.e., not terminated by a `break` statement). This is a frequent interview question.

**Use Case**: Searching for an item. The `else` block can handle the "not found" case gracefully.

```python
items = [1, 2, 3, 4]
for item in items:
    if item == 5:
        print("Found it!")
        break
else:
    # This runs because the loop finished without a 'break'.
    print("Item not found.") 
```


### `pass` and `del`

- **`pass`**: A null statement. It does nothing and is used as a placeholder where syntax requires a statement, but no code needs to be executed.

```python
def my_future_function():
    pass # Avoids an IndentationError
```

- **`del`**: Removes a name from a namespace or an item from a collection.

```python
x = 10
del x # 'x' is no longer defined

my_list = [10, 20, 30]
del my_list[1] # my_list is now [10, 30]
```


### Comprehensions (IMP)

A concise, "Pythonic" way to create collections. They are often faster and more readable than equivalent `for` loops.


| Type | Syntax | Example |
| :-- | :-- | :-- |
| **List Comprehension** | `[expr for item in iterable if cond]` | `[x*x for x in range(5)]` |
| **Set Comprehension** | `{expr for item in iterable if cond}` | `{s.lower() for s in ['A','b','A']}` |
| **Dict Comprehension** | `{key:val for item in iterable if cond}` | `{i: str(i) for i in range(3)}` |
| **Generator Expression** | `(expr for item in iterable if cond)` | `(n*n for n in range(1000))` |

- **Generator Expressions**: These look like list comprehensions but use parentheses. They create a **generator object** that yields items one by one (`lazy evaluation`), making them highly memory-efficient for large sequences.
- **Scoping Rule (Python 3)**: Comprehensions have their own local scope. Variables created inside a comprehension do not "leak" into the surrounding scope.


### Iteration Helpers (IMP)

- **`range(start, stop, step)`**: Generates a sequence of numbers. It's memory-efficient as it only stores the start, stop, and step values.
- **`enumerate(iterable, start=0)`**: Yields pairs of `(index, value)` during iteration. The preferred way to get an index in a loop.

```python
for i, fruit in enumerate(['apple', 'banana']):
    print(i, fruit) # 0 apple, 1 banana
```

- **`zip(*iterables)`**: Combines multiple iterables, yielding tuples of corresponding elements. It stops when the shortest iterable is exhausted.

```python
names = ['Alice', 'Bob']
ages = [30, 25]
for name, age in zip(names, ages):
    print(f"{name} is {age} years old.")
```

- **`map(function, iterable)`**: Applies a function to every item of an iterable, returning a map object (an iterator).
- **`filter(function, iterable)`**: Constructs an iterator from elements of an iterable for which a function returns `True`.
- **Best Practice**: For simple `map` and `filter` operations, comprehensions are often more readable. `[f(x) for x in iterable]` is usually preferred over `map(f, iterable)`.


### `any()` and `all()`

- **`all(iterable)`**: Returns `True` if all elements in the iterable are truthy.
- **`any(iterable)`**: Returns `True` if at least one element in the iterable is truthy.
- Both functions perform **short-circuiting**: they stop as soon as the result is known.


### Pattern Matching (`match` / `case`, Python 3.10+) (IMP)

A powerful control flow structure that checks a value against a series of patterns. It's like a supercharged `switch` statement.

- **Analogy**: Think of a mail sorter in a post office. The `match` statement is the sorter, and the value is the letter. Each `case` is a different mail slot (`case 'local'`), a type of mail (`case InternationalPackage()`), or a catch-all bin (`case _`).
- **Syntax**:

```python
def http_status(status):
    match status:
        case 200:
            return "OK"
        case 404:
            return "Not Found"
        case 418:
            return "I'm a teapot"
        case code if 500 <= code < 600: # Guard condition
            return f"Server Error: {code}"
        case _: # Wildcard - catches anything else
            return "Unknown status"

print(http_status(404)) # Not Found
print(http_status(503)) # Server Error: 503
```

- **Pattern matching can**:
    - Match literals (numbers, strings).
    - Unpack sequences (`case [x, y]`).
    - Unpack mappings (`case {"name": name, "age": age}`).
    - Match against object types (`case int() as num`).
    - Use `if` guards for extra conditions.
- **Exhaustiveness (Python 3.11+)**: While not strictly enforced, linters can warn if your patterns don't cover all possibilities. The `case _:` wildcard is essential for handling all other cases.


### Looping Patterns

- **`while True` with `break`**: A common pattern for event loops or when the exit condition is complex and best checked inside the loop.
- **Sentinel Loop**: A loop that continues until a special "sentinel" value is detected. The two-argument `iter()` function is perfect for this.

```python
# Instead of this:
# while True:
#     line = input("Type 'quit' to exit: ")
#     if line == 'quit':
#         break
#     print("You typed:", line)

# Use a sentinel loop:
for line in iter(lambda: input("Type 'quit' to exit: "), 'quit'):
    print("You typed:", line)
```


***
Would you like to continue with Section 4: Functions?

---

# yes

Of course. Here are the revision notes for Section 4: Functions.

### Defining Functions

Functions are defined with the `def` keyword, followed by a name, parameters in parentheses, and a colon. The body is indented. The `return` statement exits a function, optionally passing back a value. A function without a `return` statement implicitly returns `None`.

```python
def add(a, b):
    """Returns the sum of two numbers."""
    return a + b
```


### Positional-Only and Keyword-Only Parameters (Python 3.8+) (IMP)

These provide more control over how arguments can be passed.

- **Positional-Only (`/`)**: Arguments before the `/` can *only* be passed by position.
- **Keyword-Only (`*`)**: Arguments after the `*` can *only* be passed by keyword.

```python
def my_func(pos_only, /, standard, *, kw_only):
    print(pos_only, standard, kw_only)

# Valid calls
my_func(1, 2, kw_only=3)
my_func(1, standard=2, kw_only=3)

# Invalid calls
# my_func(pos_only=1, standard=2, kw_only=3)  # TypeError: pos_only is positional-only
# my_func(1, 2, 3)                         # TypeError: kw_only must be a keyword
```

**Use Case**: Use `/` to prevent users from using keyword names for simple arguments (like in `len()`), making the API less brittle to future name changes. Use `*` to force clarity for arguments that have ambiguous meaning without their keyword.

### Default Arguments \& The Mutable Default Pitfall (VERY IMP)

Default values are evaluated **once** when the function is defined, not each time it's called. This creates a trap when using mutable objects like lists or dictionaries as defaults.

- **Common Pitfall**:

```python
def add_item(item, items=[]):
    items.append(item)
    return items

list1 = add_item(1) # [1]
list2 = add_item(2) # [1, 2] <- Unexpected! list1 is also [1, 2]
# Both calls modify the SAME list object created at function definition time.
```

- **Best Practice**: Use `None` as the default and create a new mutable object inside the function.

```python
def add_item_correct(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items
    
list1 = add_item_correct(1) # [1]
list2 = add_item_correct(2) # [2] <- Correct!
```


### Arbitrary Arguments (`*args`, `**kwargs`) (IMP)

- **`*args`**: Collects all extra positional arguments into a **tuple**.
- **`**kwargs`**: Collects all extra keyword arguments into a **dictionary**.

```python
def process_data(required_arg, *args, **kwargs):
    print(f"Required: {required_arg}")
    print(f"Extra positional args (tuple): {args}")
    print(f"Extra keyword args (dict): {kwargs}")

process_data("data", 1, 2, 3, user="admin", status="active")
# Required: data
# Extra positional args (tuple): (1, 2, 3)
# Extra keyword args (dict): {'user': 'admin', 'status': 'active'}
```

- **Extended Unpacking**: You can also use `*` and `**` to "unpack" iterables and dictionaries when *calling* a function.

```python
my_args = [1, 2, 3]
my_kwargs = {'user': 'admin', 'status': 'active'}
process_data("data", *my_args, **my_kwargs) # Same as the call above
```


### Lambda Functions

Anonymous, single-expression functions.

- **Syntax**: `lambda arguments: expression`
- **Limitations**: Can only contain a single expression, not statements like `if`, `for`, or `return`.
- **Use Case**: Ideal for short, disposable functions passed to higher-order functions like `sorted`, `map`, or `filter`.

```python
points = [(1, 2), (3, 1), (5, 4)]
# Sort points based on the second element (y-coordinate)
points.sort(key=lambda p: p[1])
# points is now [(3, 1), (1, 2), (5, 4)]
```


### Higher-Order Functions

A function that takes another function as an argument or returns a function. `sorted`, `map`, `filter`, and decorators are all examples.

### Closures and Scope (VERY IMP)

- **LEGB Rule**: Python resolves names by searching scopes in this order:

1. **L**ocal: Inside the current function.
2. **E**nclosing: In the scope of any enclosing functions (e.g., in a nested function).
3. **G**lobal: At the top level of the module.
4. **B**uilt-in: Names pre-assigned in Python (`len`, `print`, etc.).
- **Closure**: A function that "remembers" the environment in which it was created. It has access to variables from its enclosing (non-global) scope, even after the outer function has finished executing.
    - **Analogy**: Imagine a chef (`outer_func`) who creates a specific spice blend (`enclosing_variable`) for a recipe. He then gives that blend to a junior chef (`inner_func`). Even after the head chef goes home, the junior chef still has and can use that specific spice blend. The junior chef plus their blend is a closure.

```python
def make_multiplier(n):
    # n is the enclosing variable
    def multiplier(x):
        # This inner function is a closure
        return x * n
    return multiplier

times3 = make_multiplier(3) # times3 "remembers" that n is 3
times5 = make_multiplier(5) # times5 "remembers" that n is 5

print(times3(10)) # 30
print(times5(10)) # 50
```

- **`global` and `nonlocal`**:
    - `global x`: Declares that `x` refers to the global variable, allowing you to modify it.
    - `nonlocal x`: Declares that `x` refers to a variable in the nearest enclosing scope (but not global), allowing modification. This is essential for changing closure variables.


### Decorators (VERY IMP)

A decorator is a function that takes another function as input, adds some functionality, and returns another function. It's syntactic sugar for wrapping one function in another.

- **Analogy**: A decorator is like a manager (`decorator`) who oversees an employee (`original_function`). Before the employee does their job, the manager logs the start time. After the employee finishes, the manager logs the end time. The employee's core task remains unchanged, but the manager has added logging around it.
- **Syntax**:

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Something is happening before the function is called.")
        result = func(*args, **kwargs) # Call the original function
        print("Something is happening after the function is called.")
        return result
    return wrapper

@my_decorator
def say_whee():
    print("Whee!")

say_whee()
# The @my_decorator syntax is equivalent to:
# say_whee = my_decorator(say_whee)
```

- **`functools.wraps`**: When you decorate a function, you replace it with the wrapper. This loses the original function's metadata (`__name__`, `__doc__`). `functools.wraps` is a decorator that you apply to your wrapper function to copy this metadata over. **Always use it.**

```python
import functools

def my_decorator(func):
    @functools.wraps(func) # <-- This is crucial!
    def wrapper(*args, **kwargs):
        ...
    return wrapper
```

- **`functools.lru_cache` and `functools.cache`**: A powerful built-in decorator for **memoization**. It caches the results of function calls and returns the cached result when the same inputs occur again. Ideal for expensive, pure functions (functions that always return the same output for the same input). `cache` (Python 3.9+) is a simpler, faster version of `lru_cache`.

```python
import functools

@functools.cache
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n-1) + fibonacci(n-2)
# Subsequent calls to fibonacci(n) will be instantaneous.
```


***
Would you like to continue with Section 5: Modules \& Packages?

---

# yes

You got it. Here are the revision notes for Section 5: Modules \& Packages.

### Import Mechanics

A **module** is simply a Python file (`.py`) with code in it. A **package** is a directory of modules. The `import` system allows you to access code from other files.

- **`import module`**: Imports the entire module. You must prefix names with the module name (e.g., `math.pi`).
- **`from module import name`**: Imports a specific name (function, class, variable) directly into the current namespace.
- **`from module import name as alias`**: Imports a specific name with an alias to avoid naming conflicts.
- **`import module as alias`**: Imports the entire module with an alias (e.g., `import numpy as np`).
- **Common Pitfall**: Using `from module import *`. This is strongly discouraged because it pollutes the current namespace with unknown names, making code difficult to read and debug. It can also mask local variables or functions.


### Absolute vs. Relative Imports (IMP)

This defines how you specify the path to a module you are importing.


| Import Type | Description | Example | Best Practice |
| :-- | :-- | :-- | :-- |
| **Absolute** | Specifies the full path from the project's root directory. | `from my_app.utils import helper` | **Highly recommended (PEP 8)**. They are unambiguous and remain valid even if the current module's location changes. |
| **Relative** | Specifies the path relative to the current module's location. A single dot `.` means the current package; two dots `..` mean the parent package. | `from . import sibling_module`<br>`from ..parent_pkg import data` | Useful for reorganizing code within a large package, as internal paths don't need updating. However, they can make it unclear where a module is coming from. |

### The `__name__ == "__main__"` Idiom (VERY IMP)

This is a fundamental construct that allows a Python file to be used as both a reusable module and a standalone script.

- **How it works**:
    - Python automatically sets a special variable `__name__` for every module.
    - If you run a file directly (e.g., `python my_script.py`), Python sets `__name__` for that file to the string `"__main__"`.
    - If you import the file as a module into another script, `__name__` is set to the module's own name (e.g., `"my_script"`).
- **Analogy**: Think of a person's role. When they are the main character in their own life story (run directly), their role (`__name__`) is `"__main__"`. When they are a supporting character in someone else's story (imported), their role is just their name.
- **Use Case**: Place script-specific code (like running a demo, tests, or a main application loop) inside this block.

```python
# file: calculator.py

def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

# This code runs ONLY when the script is executed directly
if __name__ == "__main__":
    print("Running calculator as a standalone script.")
    result = add(5, 3)
    print(f"Test add(5, 3): {result}")

# When calculator.py is imported, the code above does NOT run.
```


### Module Search Path (`sys.path`)

When you `import my_module`, Python searches for `my_module.py` in a list of directories specified in `sys.path`. The search order is:

1. The directory of the script being run (or the current working directory for the interactive interpreter).
2. The directories listed in the `PYTHONPATH` environment variable (if set).
3. Standard library and site-packages directories where packages are installed by `pip`.

You can inspect this path: `import sys; print(sys.path)`.

### Packages and `__init__.py`

- A **package** is a directory containing Python modules and a special `__init__.py` file.
- **`__init__.py`**:
    - Its presence tells Python that the directory is a package.
    - The file can be empty.
    - It can contain initialization code that runs when the package is imported.
    - It can define `__all__`, a list of strings specifying which modules should be imported when a user does `from package import *`.
- **Python Version Note**: Since Python 3.3, directories without an `__init__.py` are considered "namespace packages," but using `__init__.py` for regular packages is still the standard and recommended practice for clarity.


### Built-in Modules Overview

- **`os`**: Interact with the operating system (e.g., `os.environ`, `os.getcwd()`).
- **`sys`**: Interact with the Python interpreter (e.g., `sys.argv`, `sys.exit()`, `sys.path`).
- **`pathlib` (Python 3.4+)**: An object-oriented way to handle filesystem paths.
    - **Best Practice**: Prefer `pathlib` over the older `os.path` module for path manipulation. It's more readable and less error-prone.

```python
from pathlib import Path
p = Path("/usr/local/bin")
new_file = p / "my_script.py" # Cleanly joins paths
print(new_file.name) # "my_script.py"
print(new_file.exists()) # False
```

- **`itertools`**: Functions for creating and working with iterators efficiently.
- **`functools`**: Higher-order functions and operations on callable objects (`wraps`, `cache`, `partial`).
- **`math`**: Common mathematical functions (`sin`, `cos`, `sqrt`).


### Packaging Projects (Modern Overview)

- **`pyproject.toml` (PEP 518)**: This is the modern, unified configuration file for Python projects. It specifies the build system and can also hold configuration for tools like `pytest`, `black`, and `mypy`.
- **Build Backends**: Tools that take your source code and create distributable packages (like wheels).
- **Project Management Tools**:
    - **`setuptools`**: The traditional and powerful build backend, often used directly or via other tools.
    - **`poetry` / `flit` / `pdm`**: Modern, all-in-one tools that manage dependencies, virtual environments, and the build process using `pyproject.toml`. They simplify project setup and dependency management significantly.

***
Would you like to continue with Section 6: Object-Oriented Programming?

---

# yes

Of course. This is a very important section for interviews. Here are the revision notes for Section 6: Object-Oriented Programming (OOP).

### Classes, Instances, Attributes, and Methods

- **Class**: A blueprint for creating objects. It defines a set of attributes and methods that the created objects will have.
- **Instance (or Object)**: A specific object created from a class.
- **Attribute**: A variable bound to an instance or a class (a piece of data).
- **Method**: A function bound to an instance or a class (an action).

```python
class Dog:
    # This is a class attribute
    species = "Canis familiaris"

    # The initializer method
    def __init__(self, name, age):
        # These are instance attributes
        self.name = name
        self.age = age

    # This is an instance method
    def bark(self):
        return f"{self.name} says woof!"

# Creating instances of the Dog class
my_dog = Dog("Fido", 5)
print(my_dog.bark()) # Output: Fido says woof!
```


### The Object Lifecycle: `__new__`, `__init__`, `__del__` (IMP)

- **`__new__(cls, ...)`**: A static method that is the **first step in object creation**. Its job is to create and return a new, empty instance of the class. You rarely need to override it, but it's crucial for subclassing immutable types like `str` or `tuple`.
- **`__init__(self, ...)`**: The **initializer**. It receives the newly created instance from `__new__` as `self`. Its job is to **initialize the attributes** of the instance. It does not return anything.
- **`__del__(self)`**: The **finalizer**. It's called just before the object is destroyed by the garbage collector. Its use is discouraged because the timing of garbage collection is unpredictable. Use context managers (`with` statement) for reliable cleanup.


### Instance, Class, and Static Methods (VERY IMP)

This is a frequent interview topic.


| Method Type | Decorator | First Argument | Purpose \& Analogy |
| :-- | :-- | :-- | :-- |
| **Instance Method** | (none) | `self` (the instance) | Operates on instance-specific data (`self.name`). **Analogy**: "What is *your* name?" - an action specific to one person. |
| **Class Method** | `@classmethod` | `cls` (the class) | Operates on the class itself. Often used as alternative constructors. **Analogy**: "How many people have been created?" - a question about the group, not an individual. |
| **Static Method** | `@staticmethod` | (none) | A regular function namespaced within the class. It has no access to the instance (`self`) or class (`cls`). **Analogy**: "What is the formula for calculating age from a birthdate?" - a utility related to the concept of a person, but not dependent on any specific person or the group. |

```python
class MyClass:
    def instance_method(self):
        print(f"Called from instance {self}")

    @classmethod
    def class_method(cls):
        print(f"Called from class {cls}")

    @staticmethod
    def static_method():
        print("Called from a static method")

obj = MyClass()
obj.instance_method()
MyClass.class_method() # Can also be called on an instance: obj.class_method()
MyClass.static_method()
```


### Class vs. Instance Attributes (IMP)

- **Class Attributes**: Shared by all instances of the class. They are defined directly under the class definition.
- **Instance Attributes**: Unique to each instance. They are typically defined inside `__init__` using `self`.
- **Common Pitfall**: Modifying a *mutable* class attribute from an instance can lead to surprising behavior.

```python
class Team:
    members = [] # Mutable class attribute

t1 = Team()
t2 = Team()

t1.members.append("Alice")

print(t1.members) # ['Alice']
print(t2.members) # ['Alice'] <- t2 is also affected!

# Best Practice: Use instance attributes for mutable state.
class TeamCorrect:
    def __init__(self):
        self.members = []
```


### Inheritance and `super()`

- **Inheritance**: Allows a class (child/subclass) to inherit attributes and methods from another class (parent/superclass).
- **Method Resolution Order (MRO)**: In multiple inheritance, Python determines the order in which to search parent classes for a method. You can inspect it with `ClassName.mro()`.
- **`super()` (IMP)**: A function that returns a proxy object, allowing you to call methods of a parent class. It works with the MRO to ensure that in a multiple inheritance hierarchy, each parent class method is called exactly once.

```python
class Parent:
    def speak(self):
        print("I am the parent")

class Child(Parent):
    def speak(self):
        super().speak() # Call the parent's speak method
        print("I am the child")

c = Child()
c.speak()
# Output:
# I am the parent
# I am the child
```


### Special (Dunder) Methods

- **`__str__` vs `__repr__` (VERY IMP)**:
    - **`__repr__(self)`**: Should return an **unambiguous, official** string representation of the object, ideally one that can be used to recreate the object (e.g., `eval(repr(obj)) == obj`). Target audience: **developers**. Called by `repr()`.
    - **`__str__(self)`**: Should return a **readable, user-friendly** string representation. Target audience: **end-users**. Called by `str()` and `print()`.
    - **Best Practice**: If you only define one, define `__repr__`. Python will use `__repr__` as a fallback for `__str__`.
- **Operators**: `__add__` (`+`), `__mul__` (`*`), `__eq__` (`==`), `__lt__` (`<`), etc.
- **`__hash__` and Equality**: If you implement a custom `__eq__`, Python makes your object unhashable by default. If you need it to be a dictionary key or in a set, you must also implement `__hash__` such that if `a == b`, then `hash(a) == hash(b)`.
- **Truthiness**: `__bool__(self)` should return `True` or `False`. If not defined, `__len__(self)` is used.


### Abstract Base Classes (`abc` module)

An ABC defines an **interface** that subclasses are expected to implement. You cannot instantiate an ABC directly.

```python
from abc import ABC, abstractmethod

class Shape(ABC): # Inherit from ABC
    @abstractmethod
    def area(self):
        pass

class Square(Shape):
    def __init__(self, side):
        self.side = side
    
    # Must implement the 'area' method
    def area(self):
        return self.side * self.side

# s = Shape() # TypeError: Can't instantiate abstract class
sq = Square(5)
print(sq.area()) # 25
```


### `dataclasses` (Python 3.7+)

A decorator that automatically generates special methods like `__init__`, `__repr__`, and `__eq__` for classes that are primarily used to store data.

```python
from dataclasses import dataclass

@dataclass(frozen=True) # frozen=True makes instances immutable
class Point:
    x: float
    y: float

p1 = Point(1.0, 2.0)
p2 = Point(1.0, 2.0)
print(p1)       # Point(x=1.0, y=2.0) <- Nice repr!
print(p1 == p2) # True <- __eq__ is implemented!
```

- The `attrs` library is a more powerful, third-party alternative that inspired `dataclasses`.


### `__slots__` for Memory Optimization (IMP)

By default, Python instances store their attributes in a dictionary called `__dict__`. This is flexible but uses memory.
`__slots__` is a class variable that pre-declares the instance attributes, telling Python *not* to use a `__dict__` and to allocate space for a fixed set of attributes directly.

- **Pros**:

1. Massive memory savings (can be 20-50%) when creating thousands or millions of small objects.
2. Slightly faster attribute access.
- **Cons**:

1. You cannot add new attributes to an instance at runtime.
2. Does not work well with multiple inheritance if parents have different slots.

```python
class PointWithSlots:
    __slots__ = ['x', 'y']
    def __init__(self, x, y):
        self.x = x
        self.y = y

p = PointWithSlots(1, 2)
# p.z = 3 # AttributeError: 'PointWithSlots' object has no attribute 'z'
```


***
Would you like to continue with Section 7: Exceptions \& Error Handling?

---

# yes

Of course. Handling errors gracefully is a mark of robust software. Here are the revision notes for Section 7: Exceptions \& Error Handling.

### `try`, `except`, `else`, `finally` (IMP)

This block provides a complete structure for handling exceptions.

- **`try`**: The block of code that might raise an exception.
- **`except`**: If an exception occurs in the `try` block, the matching `except` block is executed.
- **`else`**: If **no exceptions** are raised in the `try` block, the `else` block is executed. This is useful for code that should run only when the `try` part was successful.
- **`finally`**: This block is **always executed**, whether an exception occurred or not. It's used for cleanup actions like closing files or releasing resources.

```python
try:
    value = int(input("Enter a number: "))
except ValueError:
    print("That was not a valid number.")
else:
    # This runs only if int() was successful
    print(f"The square of your number is {value**2}")
finally:
    # This always runs
    print("Execution finished.")
```


### Catching Specific vs. Generic Exceptions (VERY IMP)

- **Best Practice**: Always catch the most specific exception possible.
- **Common Pitfall**: Using a bare `except:` or `except Exception:`. This is dangerous because it catches *everything*, including system-exiting exceptions (`SystemExit`), keyboard interrupts (`KeyboardInterrupt`), and assertion errors, which can hide bugs and make your program difficult to terminate.

```python
# Bad: Too broad, hides bugs
try:
    # some code
except Exception as e:
    print(f"An unknown error occurred: {e}")

# Good: Specific and clear
try:
    data = {"key": "value"}
    print(data["missing_key"])
except KeyError as e:
    print(f"Handled a missing key: {e}")

# Catching multiple specific exceptions
try:
    # some code
except (ValueError, TypeError) as e:
    print(f"Handled a value or type error: {e}")
```


### Raising Exceptions

- **`raise`**: You can trigger an exception manually using the `raise` keyword. This is useful for signaling errors in your own functions.

```python
def set_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative.")
    self.age = age
```

- **Exception Chaining (`raise from`) (IMP)**: When you catch an exception and raise a different one, you should link them using `raise ... from ...`. This preserves the original traceback, which is invaluable for debugging.

```python
def process_file(path):
    try:
        with open(path, 'r') as f:
            # process data
    except FileNotFoundError as e:
        # Wrap the original exception in a more semantic one
        raise ValueError(f"Configuration file not found at {path}") from e
```


### Custom Exceptions

Defining your own exceptions makes your code more readable and your error handling more precise. Create them by subclassing the built-in `Exception` class.

```python
class InsufficientFundsError(Exception):
    """Raised when a withdrawal exceeds the account balance."""
    pass

def withdraw(balance, amount):
    if amount > balance:
        raise InsufficientFundsError("Cannot withdraw more than the available balance.")
    return balance - amount
```


### Context Managers (`with`) (VERY IMP)

The `with` statement simplifies resource management (like files, network connections, or locks) by ensuring that cleanup logic is always executed.

- **Analogy**: A context manager is like a self-cleaning kitchen appliance. You turn it on (`__enter__`), use it (the `with` block), and it automatically runs its cleanup cycle (`__exit__`) when you're done, even if you make a mess (an exception).
- Any object that implements the **context management protocol** (the `__enter__` and `__exit__` methods) can be used with a `with` statement.
- **`__enter__(self)`**: Called when entering the `with` block. Its return value is bound to the variable after `as` (if present).
- **`__exit__(self, exc_type, exc_value, traceback)`**: Called when exiting the block.
    - If no exception occurred, all three arguments are `None`.
    - If an exception occurred, they are populated.
    - If `__exit__` returns `True`, the exception is **suppressed** (it won't be propagated).

```python
class MyFileHandler:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode

    def __enter__(self):
        print("Opening file...")
        self.file = open(self.filename, self.mode)
        return self.file

    def __exit__(self, exc_type, exc_value, traceback):
        print("Closing file...")
        self.file.close()
        # If we wanted to suppress exceptions, we would return True here.

with MyFileHandler('test.txt', 'w') as f:
    f.write('hello')
# Output:
# Opening file...
# Closing file...
```

- **`contextlib` module**: Provides utilities to easily create context managers, like `@contextmanager` decorator which turns a simple generator function into one.


### Exception Groups (`except*`, Python 3.11+) (IMP)

This is a modern feature for handling multiple, concurrent exceptions, which is common in asynchronous programming.

- **`ExceptionGroup`**: A new exception type that can wrap several unrelated exceptions.
- **`except*`**: A variant of `except` that can match and extract subgroups of exceptions from an `ExceptionGroup`.

```python
# This is a conceptual example. TaskGroup would create the ExceptionGroup.
try:
    # Imagine two concurrent tasks failing
    raise ExceptionGroup(
        "many errors",
        [ValueError("bad value"), TypeError("bad type")]
    )
except* ValueError as eg: # Match all ValueErrors in the group
    print(f"Handled ValueErrors: {eg.exceptions}")
except* TypeError as eg: # Match all TypeErrors
    print(f"Handled TypeErrors: {eg.exceptions}")

# Output:
# Handled ValueErrors: (ValueError('bad value'),)
# Handled TypeErrors: (TypeError('bad type'),)
```


***
Would you like to continue with Section 8: Iterators, Generators, and Coroutines?

---

# yes

Of course. This section covers some of Python's most powerful and memory-efficient features. Here are the revision notes for Section 8: Iterators, Generators, and Coroutines.

### The Iteration Protocol (IMP)

This is the mechanism that powers `for` loops in Python. An object is considered **iterable** if it knows how to produce an **iterator**.

- **Iterable**: An object that implements the `__iter__()` method, which must return an iterator. Examples: `list`, `str`, `dict`.
- **Iterator**: An object that implements both `__iter__()` (returning itself) and `__next__()`, which returns the next item or raises `StopIteration` when there are no more items.

**Analogy**: An **iterable** is like a book. An **iterator** is like a bookmark. The book itself isn't keeping track of your reading progress, but the bookmark is. You can have multiple bookmarks (iterators) for the same book (iterable).

```python
# How a 'for' loop really works:
my_list = [1, 2]

# 1. Get an iterator from the iterable
iterator = iter(my_list)  # Calls my_list.__iter__()

# 2. Repeatedly call next() on the iterator
print(next(iterator)) # 1
print(next(iterator)) # 2

# 3. The loop stops when StopIteration is raised
# next(iterator) -> raises StopIteration
```


### Generator Functions \& `yield` (VERY IMP)

A generator function is a simpler way to create an iterator. It's a function that uses the `yield` keyword instead of `return`.

- When a generator function is called, it returns a **generator object** (a type of iterator) but does not start execution.
- When `next()` is called on the generator object, the function executes until it hits a `yield` statement.
- The `yield` statement **pauses** the function, saves its state, and returns the yielded value.
- On the next `next()` call, the function **resumes** execution right after the `yield`.

**Analogy**: A generator is like a movie on a streaming service. You don't download the whole movie at once. You "yield" one frame at a time, and the player can pause and resume exactly where it left off, saving bandwidth and memory.

```python
def count_up_to(max_val):
    print("Generator started")
    count = 1
    while count <= max_val:
        yield count  # Pause and send 'count' back
        count += 1
    print("Generator finished")

counter = count_up_to(3) # No code inside the function has run yet
print(next(counter))     # Output: Generator started, then 1
print(next(counter))     # Output: 2
print(next(counter))     # Output: 3
# next(counter)          # Output: Generator finished, then raises StopIteration
```


### Advanced Generator Methods: `send()` and `throw()`

Generators can also receive data, making them a simple form of coroutine.

- **`gen.send(value)`**: Resumes the generator and sends a `value` *into* it. The `yield` expression itself evaluates to this sent value.
- **`gen.throw(exception)`**: Resumes the generator and raises an exception inside it at the `yield` point.

```python
def listener():
    print("Ready to listen...")
    while True:
        # The 'yield' expression receives the sent value
        message = yield
        print(f"Received: {message}")

l = listener()
next(l) # Prime the generator to the first yield
l.send("Hello") # Output: Received: Hello
l.send("World") # Output: Received: World
```


### Generator Expressions vs. List Comprehensions

- **Generator Expression**: `(x * x for x in range(1000))`
    - Creates a generator object.
    - **Lazy evaluation**: computes items one by one, on demand.
    - Memory efficient: uses constant, minimal memory regardless of the sequence size.
- **List Comprehension**: `[x * x for x in range(1000)]`
    - Creates a list in memory.
    - **Eager evaluation**: computes all items at once.
    - Uses memory proportional to the number of items.

**Best Practice**: Use generator expressions for large sequences or when you only need to iterate over the items once.

### `itertools` Module

This standard library module provides a collection of fast, memory-efficient tools for working with iterators. It offers advanced functions like `chain`, `cycle`, `permutations`, `combinations`, and more.

### Asynchronous Programming

Asynchronous code allows you to run multiple operations concurrently without using threads. It's ideal for I/O-bound tasks (like network requests or database queries) where the program would otherwise wait.

#### `async for` and Async Iteration

Just as `for` uses the iteration protocol, `async for` uses the **asynchronous iteration protocol**.

- **Async Iterable**: An object with an `__aiter__()` method that returns an async iterator.
- **Async Iterator**: An object with an `__anext__()` method that returns an **awaitable** which resolves to the next item or raises `StopAsyncIteration`.


#### Coroutines with `async def` (VERY IMP)

- A function defined with `async def` is a **coroutine**.
- When called, it returns a **coroutine object** but does not execute.
- To run it, you must either `await` it from another coroutine or schedule it on an **event loop** (like `asyncio.run()`).
- The `await` keyword pauses the execution of the current coroutine, allowing the event loop to run other tasks, until the awaited operation (e.g., a network request) is complete.

**Analogy**: A coroutine is like a chef in a kitchen (the event loop). The chef starts cooking a soup (`await cook_soup()`). While the soup is simmering (an I/O-bound task), the chef doesn't just stand there and wait. They move on to chopping vegetables for another dish. When the soup's timer goes off (the I/O completes), the chef can return to it. `await` is the point where the chef can switch tasks.

#### Awaitables \& Tasks

- An **awaitable** is anything you can use in an `await` expression. This includes coroutines and `Task` objects.
- An `asyncio.Task` is an object that wraps a coroutine and manages its execution on the event loop.

```python
import asyncio

async def fetch_data(url):
    print(f"Fetching {url}...")
    await asyncio.sleep(2) # Simulate a network request
    print(f"Done fetching {url}.")
    return {"data": "some data"}

async def main():
    # Create a task to run fetch_data concurrently
    task = asyncio.create_task(fetch_data("http://example.com"))
    
    # Do other work while the task is running
    print("Doing other work in main...")
    await asyncio.sleep(1)
    
    # Now, wait for the task to complete and get its result
    result = await task
    print(f"Received result: {result}")

# Run the main coroutine using the asyncio event loop
asyncio.run(main())
```


***
Would you like to continue with Section 9: Concurrency \& Parallelism?

---

# yes

Of course. Here are the revision notes for Section 9: Concurrency \& Parallelism. This section is critical for advanced and system design interviews, as it explores how Python handles doing multiple things at once.

### Concurrency vs. Parallelism (IMP)

This distinction is fundamental.


| Concept | Description | How it's achieved in Python | Best for | Analogy |
| :-- | :-- | :-- | :-- | :-- |
| **Concurrency** | **Managing** multiple tasks at once. The tasks can be interleaved on a single CPU core, giving the illusion of simultaneous execution. | `threading`, `asyncio` | **I/O-bound** tasks (waiting for network, disk, database). | A chef juggling multiple recipes. They switch between tasks (chopping, stirring, waiting for an oven) but are still just one person. |
| **Parallelism** | **Executing** multiple tasks simultaneously on multiple CPU cores. | `multiprocessing` | **CPU-bound** tasks (heavy calculations, data processing). | A kitchen with multiple chefs, each working on a different recipe at the same time on their own stove. |

### The Global Interpreter Lock (GIL) (VERY IMP)

- The **GIL** is a mutex (a type of lock) that protects access to Python objects, preventing multiple native threads from executing Python bytecode at the same time within a single process.
- **Implication**: Even on a multi-core machine, only **one thread** can execute Python code at a time. This means `threading` **does not achieve parallelism** for CPU-bound tasks in standard CPython.
- **Why it's useful for I/O-bound tasks**: When a thread is waiting for I/O (e.g., a network response), it releases the GIL, allowing another thread to run. This makes `threading` effective for concurrency.
- **How to bypass the GIL**: Use `multiprocessing`, which creates separate processes, each with its own Python interpreter and memory space (and thus, its own GIL).


### `threading` Module

- Used for creating and managing threads within a single process.
- **Use Case**: Running I/O-bound operations concurrently.

```python
import threading
import time

def io_task(name):
    print(f"Thread {name}: Starting I/O task...")
    time.sleep(2) # Simulate waiting for I/O
    print(f"Thread {name}: Finished.")

threads = [threading.Thread(target=io_task, args=(i,)) for i in range(3)]
for t in threads:
    t.start() # Start the threads
for t in threads:
    t.join()  # Wait for all threads to complete
```


### `multiprocessing` Module

- Used for creating and managing separate processes, bypassing the GIL to achieve true parallelism.
- **Use Case**: Running CPU-bound tasks in parallel on multi-core systems.
- **Challenge**: Processes have separate memory spaces. Communicating between them requires Inter-Process Communication (IPC) mechanisms like `multiprocessing.Queue` or `multiprocessing.Pipe`.

```python
import multiprocessing
import time

def cpu_task(n):
    print(f"Process {n}: Starting CPU task...")
    # Simulate heavy computation
    sum = 0
    for i in range(10**7):
        sum += i
    print(f"Process {n}: Finished.")

if __name__ == "__main__": # Important guard for multiprocessing
    processes = [multiprocessing.Process(target=cpu_task, args=(i,)) for i in range(3)]
    for p in processes:
        p.start()
    for p in processes:
        p.join()
```


### `concurrent.futures` (High-Level API) (IMP)

This module provides a high-level, easier-to-use interface for managing threads and processes through **thread/process pools**.

- **`ThreadPoolExecutor`**: Manages a pool of threads for concurrent I/O-bound tasks.
- **`ProcessPoolExecutor`**: Manages a pool of processes for parallel CPU-bound tasks.
- **`Future` Object**: When you submit a task to an executor, it returns a `Future` object, which is a placeholder for the result that will be available later.

```python
from concurrent.futures import ThreadPoolExecutor
import time

def task(name):
    time.sleep(2)
    return f"Task {name} complete"

with ThreadPoolExecutor(max_workers=3) as executor:
    # submit() schedules a single task and returns a future
    future1 = executor.submit(task, "A")
    
    # map() applies a function to an iterable, returning results as they complete
    results = executor.map(task, ["B", "C"])
    
    print(future1.result()) # Blocks until future1 is done
    for r in results:
        print(r)
```


### Synchronization Primitives

These tools are used to coordinate work and prevent race conditions when multiple threads/processes access shared resources.

- **`Lock`**: The simplest primitive. Only one thread can acquire the lock at a time.
- **`Event`**: A simple mechanism to signal between threads. One thread can `wait()` for an event, while another thread can `set()` it.
- **`Semaphore`**: Like a lock, but allows a fixed number of threads to acquire it simultaneously. Useful for controlling access to a resource with a limited capacity (e.g., a connection pool).
- **`Condition`**: A more advanced primitive that combines a lock with the ability for threads to `wait()` for a certain condition to become true and be `notify()`-ed by another thread.


### `asyncio`: Concurrency without Threads

- As discussed in Section 8, `asyncio` uses a single-threaded **event loop** to manage many concurrent tasks.
- It is highly efficient for I/O-bound workloads with thousands of connections, often outperforming `threading` due to lower memory overhead (no need to create separate OS threads).
- **Task Groups (Python 3.11+)**: A modern and safer way to manage concurrent tasks, implementing the principles of **structured concurrency**. It ensures that all tasks in a group are awaited before exiting.

```python
import asyncio

async def my_task(n):
    await asyncio.sleep(n)
    print(f"Task {n} finished.")

async def main():
    async with asyncio.TaskGroup() as tg:
        tg.create_task(my_task(1))
        tg.create_task(my_task(2))
    # The 'with' block will not exit until both tasks are complete.
    print("All tasks in the group are done.")

asyncio.run(main())
```


### Queues for Communication (IMP)

Queues are thread-safe/process-safe data structures essential for passing messages between concurrent units.


| Module | Queue Class | Use Case |
| :-- | :-- | :-- |
| `queue` | `queue.Queue` | Communication between threads (`threading`). |
| `asyncio` | `asyncio.Queue` | Communication between `asyncio` tasks. |
| `multiprocessing` | `multiprocessing.Queue` | Communication between processes (`multiprocessing`). |


***
Would you like to continue with Section 10: File I/O and OS Interaction?

---

# yes

Absolutely. Here are the revision notes for Section 10: File I/O and OS Interaction.

### Reading and Writing Files (IMP)

The primary function for file handling is `open()`. The recommended way to use it is with a `with` statement, which ensures the file is automatically closed even if errors occur.

- **Syntax**: `with open(filename, mode, encoding=None) as f:`
- **Modes**:
    - `'r'`: Read (default).
    - `'w'`: Write (truncates the file first).
    - `'a'`: Append (writes to the end of the file).
    - `'x'`: Exclusive creation (fails if the file already exists).
    - `'+'`: Update (reading and writing).
- **Text vs. Binary Mode (IMP)**:
    - **Text mode (`'t'`)**: Default. Data is decoded/encoded automatically using a specified `encoding` (or the system default). Handles universal newlines. Use for text files like `.txt`, `.csv`, `.json`.
    - **Binary mode (`'b'`)**: Appended to the mode string (e.g., `'rb'`, `'wb'`). Data is read/written as raw **bytes**. No encoding/decoding is performed. Use for non-text files like images, executables, or compressed data.

```python
# Best Practice: Always use 'with' and specify encoding for text files.

# Writing to a text file
with open('data.txt', 'w', encoding='utf-8') as f:
    f.write('Hello, world!\n')
    f.write('This is a test.\n')

# Reading from a text file
with open('data.txt', 'r', encoding='utf-8') as f:
    content = f.read() # Reads the entire file
    # or
    lines = f.readlines() # Reads all lines into a list
    # or iterate line by line (memory efficient)
    for line in f:
        print(line.strip())

# Working with binary files
with open('image.jpg', 'rb') as f_in, open('image_copy.jpg', 'wb') as f_out:
    chunk_size = 4096
    while True:
        chunk = f_in.read(chunk_size)
        if not chunk:
            break
        f_out.write(chunk)
```

- **Buffering**: I/O is typically buffered. Data written may not be sent to the disk immediately. `f.flush()` forces it, and the file is automatically flushed and closed upon exiting the `with` block.


### `pathlib`: Modern Path Handling (VERY IMP)

The `pathlib` module (Python 3.4+) provides an object-oriented interface for filesystem paths. It is the modern, preferred alternative to the string-based `os.path`.

- **Analogy**: Using `os.path` is like giving directions with verbal instructions ("turn left at the big tree, then go 500 feet..."). Using `pathlib` is like using a GPS navigator object; it understands concepts like "parent directory" and "file extension" directly.

| Feature | `os.path` (Old Way) | `pathlib` (New Way) |
| :-- | :-- | :-- |
| **Path Creation** | `path = os.path.join('/etc', 'nginx', 'nginx.conf')` | `p = Path('/etc') / 'nginx' / 'nginx.conf'` |
| **Get Parent Dir** | `os.path.dirname(path)` | `p.parent` |
| **Get Filename** | `os.path.basename(path)` | `p.name` |
| **Get Extension** | `os.path.splitext(path)[1]` | `p.suffix` |
| **Check Existence** | `os.path.exists(path)` | `p.exists()` |
| **Check if File** | `os.path.isfile(path)` | `p.is_file()` |
| **Read/Write** | `with open(path, 'r') ...` | `text = p.read_text()` <br> `p.write_text("new content")` |

```python
from pathlib import Path

# Create a path object
config_path = Path.home() / '.config' / 'my_app'

# Create the directory if it doesn't exist
config_path.mkdir(parents=True, exist_ok=True)

# Create a file path
file_path = config_path / 'settings.conf'

# Write content easily
file_path.write_text('theme = dark\n')

# Read content easily
content = file_path.read_text()
print(content)
```


### OS Interaction Modules

- **`os`**: Provides a way of using operating system dependent functionality.
    - `os.getcwd()`: Get current working directory.
    - `os.chdir(path)`: Change directory.
    - `os.listdir(path)`: Get a list of directory entries.
    - `os.environ`: A dictionary-like object to access **environment variables**.
        - `api_key = os.environ.get('API_KEY')` (using `.get()` avoids a `KeyError`).
- **`shutil`**: High-level file and directory operations.
    - `shutil.copy(src, dst)`: Copies a file.
    - `shutil.copytree(src, dst)`: Recursively copies a directory.
    - `shutil.move(src, dst)`: Moves a file or directory.
    - `shutil.rmtree(path)`: Recursively deletes a directory (**Warning**: this is permanent).
- **`glob`**: Finds all pathnames matching a specified pattern according to Unix shell rules.
    - `glob.glob('*.txt')`: Find all files ending with `.txt`.
    - `glob.glob('**/*.py', recursive=True)`: Find all Python files in all subdirectories.
    - `pathlib` has this built-in: `for f in Path('.').glob('**/*.py'): ...`


### Temporary and Memory-Mapped Files

- **`tempfile`**: Securely create temporary files and directories. The OS takes care of cleaning them up.

```python
import tempfile

with tempfile.TemporaryDirectory() as temp_dir:
    print(f"Created temporary directory: {temp_dir}")
    # Use the directory...
# The directory and its contents are deleted upon exiting the 'with' block.
```

- **`mmap` (Memory-mapped files)**: An advanced module that maps a file into memory. Changes to the memory object are directly written back to the file. This can be more efficient than standard `read`/`write` calls for random-access modifications to a large file.

***
Would you like to continue with Section 11: Networking \& IPC?

---

# yes

Of course. Let's dive into Section 11: Networking \& Inter-Process Communication (IPC). This section covers how Python programs communicate with each other and with services across a network.

### TCP/UDP Sockets (`socket` module) (IMP)

The `socket` module provides low-level access to the operating system's network interface. It's the foundation for most network communication in Python.[^12_1][^12_2]

- **Analogy**: A socket is like a telephone. You need one to make a call (initiate a connection), and another person needs one to receive the call. The telephone number is the IP address and port.

| Protocol | `socket.SOCK_STREAM` (TCP) | `socket.SOCK_DGRAM` (UDP) |
| :-- | :-- | :-- |
| **Connection** | Connection-oriented: A stable connection must be established before data transfer (like a phone call)[^12_3]. | Connectionless: Packets are sent without establishing a connection (like sending postcards)[^12_3]. |
| **Reliability** | **Guaranteed delivery** and order. Packets are re-sent if lost[^12_3]. | **No guarantee** of delivery or order. Packets can be lost or arrive out of sequence[^12_4]. |
| **Speed** | Slower due to handshakes and error-checking overhead[^12_3]. | Faster due to lower overhead[^12_3][^12_5]. |
| **Use Case** | File transfers, web browsing, email—where data integrity is crucial[^12_3]. | Video streaming, online gaming, DNS—where speed is more important than perfect reliability[^12_3]. |

```python
# Simple TCP Server Example
import socket

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.bind(('127.0.0.1', 65432))
    s.listen()
    conn, addr = s.accept()
    with conn:
        print(f"Connected by {addr}")
        while True:
            data = conn.recv(1024)
            if not data:
                break
            conn.sendall(data) # Echo back the data
```


### `selectors` for I/O Multiplexing (IMP)

The `selectors` module provides high-level and efficient I/O multiplexing, allowing you to monitor multiple sockets for activity without using threads. It's a performant way to handle many connections concurrently in a single thread.[^12_6][^12_7]

- **Analogy**: `selectors` is like a receptionist at a large office. Instead of one employee constantly checking their personal mailbox (blocking I/O), the receptionist watches all mailboxes (`sel.select()`) and only notifies an employee (`callback`) when a new piece of mail has actually arrived (`EVENT_READ`).[^12_7]

```python
# Simplified echo server using selectors
import selectors
import socket

sel = selectors.DefaultSelector()

def accept_conn(sock):
    conn, addr = sock.accept()
    conn.setblocking(False)
    sel.register(conn, selectors.EVENT_READ, read_data)

def read_data(conn):
    data = conn.recv(1024)
    if data:
        conn.send(data)
    else:
        sel.unregister(conn)
        conn.close()

# Server setup
lsock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
lsock.bind(('localhost', 65432))
lsock.listen()
lsock.setblocking(False)
sel.register(lsock, selectors.EVENT_READ, accept_conn)

# Event loop
while True:
    events = sel.select() # Blocks until a socket is ready
    for key, mask in events:
        callback = key.data
        callback(key.fileobj)
```


### HTTP Requests (VERY IMP)

Making HTTP requests to APIs is a common task. Several libraries are available, each with its own strengths.[^12_8]


| Library | Key Features | Use Case |
| :-- | :-- | :-- |
| **`urllib`** | Part of the **standard library**. Lower-level, can be verbose[^12_9][^12_8]. | When you cannot have external dependencies or need fine-grained control[^12_9]. |
| **`requests`** | The de facto standard. **Simple, intuitive API**. Synchronous only[^12_8]. | The default choice for most synchronous applications. Excellent for beginners and experts alike[^12_8]. |
| **`httpx`** | The "next generation" client. API is very similar to `requests`. Supports **sync and async** (`await`) and **HTTP/2**[^12_8]. | For new projects, especially those using `asyncio`, or when HTTP/2 support is needed[^12_8]. |

```python
# Using requests (the most common choice)
import requests

try:
    response = requests.get('https://api.github.com/users/python')
    response.raise_for_status() # Raises an exception for bad status codes (4xx or 5xx)
    user_data = response.json() # Decodes JSON response into a dict
    print(user_data['name'])
except requests.exceptions.RequestException as e:
    print(f"An error occurred: {e}")
```


### REST APIs with `http.server`

The `http.server` module can be used to create a very basic web server for simple testing or demos. It's not suitable for production use. For real REST APIs, use a proper framework like **Flask**, **FastAPI**, or **Django**.[^12_10][^12_11]

### WebSockets (`websockets` library)

WebSockets provide a **full-duplex**, low-latency communication channel over a single TCP connection, perfect for real-time applications like chat apps or live dashboards. The `websockets` library is a popular choice that integrates with `asyncio`.[^12_12][^12_13]

```python
# Simple WebSocket echo server using the 'websockets' library
import asyncio
import websockets

async def echo(websocket):
    async for message in websocket:
        await websocket.send(f"Echo: {message}")

async def main():
    async with websockets.serve(echo, "localhost", 8765):
        await asyncio.Future()  # Run forever

asyncio.run(main())
```


### Inter-Process Communication (IPC) (IMP)

When using `multiprocessing`, processes have separate memory spaces and cannot share data directly. IPC mechanisms are required to communicate between them.[^12_14]

- **`Pipe`**: A two-way communication channel between **two** specific processes. `multiprocessing.Pipe()` returns a pair of connection objects.[^12_15]
- **`Queue`**: A multi-producer, multi-consumer queue. Any number of processes can put items in or get items from the queue, making it flexible for complex communication patterns.[^12_15]

```python
from multiprocessing import Process, Queue

def worker(q):
    """Worker process that puts a message on the queue."""
    q.put('Hello from the worker process!')

if __name__ == "__main__":
    q = Queue()
    p = Process(target=worker, args=(q,))
    p.start()
    
    print(q.get()) # Blocks until an item is available
    
    p.join()
```


### Remote Procedure Call (RPC): `xmlrpc` and `gRPC`

RPC frameworks allow a program to execute a function or procedure in another process (on the same or a different machine) as if it were a local call.

- **`xmlrpc`**:
    - Built into the Python standard library.[^12_16]
    - Simple to set up and use.[^12_17]
    - Uses XML for data encoding and HTTP for transport.
    - Slower and less feature-rich compared to modern alternatives.
- **`gRPC`**:
    - A high-performance, modern framework from Google.[^12_18]
    - Uses **Protocol Buffers (`.proto` files)** to define service interfaces and message structures.[^12_19]
    - Uses HTTP/2 for transport, enabling features like streaming.
    - Requires code generation steps before use but offers excellent performance and cross-language compatibility.[^12_19]

***
Would you like to continue with Section 12: Data Formats \& Parsing?
<span style="display:none">[^12_20]</span>

```
<div style="text-align: center">⁂</div>
```

[^12_1]: https://www.geeksforgeeks.org/python/sockets-python/

[^12_2]: https://realpython.com/python-sockets/

[^12_3]: https://www.digitalocean.com/community/tutorials/python-socket-programming-server-client

[^12_4]: https://wiki.python.org/moin/UdpCommunication

[^12_5]: https://www.youtube.com/watch?v=esLgiMLbRkI

[^12_6]: https://dev.to/hexshift/how-to-use-pythons-selectors-module-for-efficient-io-multiplexing-1dgf

[^12_7]: https://www.youtube.com/watch?v=TO5NRbdZi3A

[^12_8]: https://proxiesapi.com/articles/requests-vs-urllib-vs-httpx-vs-aiohttp

[^12_9]: https://realpython.com/urllib-request/

[^12_10]: https://www.xingyulei.com/post/py-http-server/index.html

[^12_11]: https://www.integrate.io/blog/an-introduction-to-rest-api-with-python/

[^12_12]: https://www.videosdk.live/developer-hub/websocket/python-websocket-library

[^12_13]: https://github.com/python-websockets/websockets

[^12_14]: https://www.c-sharpcorner.com/article/demystifying-inter-process-communication-ipc-in-python/

[^12_15]: https://www.geeksforgeeks.org/python/multiprocessing-python-set-2/

[^12_16]: https://docs.python.org/3/library/xmlrpc.server.html

[^12_17]: https://www.tutorialspoint.com/xmlrpc-server-and-client-modules-in-python

[^12_18]: https://grpc.io/docs/languages/python/basics/

[^12_19]: https://tyk.io/docs/5.2/plugins/supported-languages/rich-plugins/grpc/getting-started-python/

[^12_20]: https://stackoverflow.com/questions/27893804/udp-client-server-socket-in-python


---

# yes

Excellent. Parsing and manipulating data are core skills for any Python developer. Here are the revision notes for Section 12: Data Formats \& Parsing.

### Common Data Formats

| Format | Module(s) | Primary Use Case | Key Feature |
| :-- | :-- | :-- | :-- |
| **JSON** | `json` (standard library) | APIs, web communication, simple data storage[^13_1]. | Ubiquitous, language-agnostic, built-in support[^13_2]. |
| **YAML** | `PyYAML` (third-party) | Configuration files, human-written data[^13_3]. | Very human-readable, supports comments[^13_3][^13_4]. |
| **TOML** | `tomllib` (standard library, 3.11+) | Configuration files (e.g., `pyproject.toml`)[^13_5]. | Simple, unambiguous syntax[^13_5][^13_6]. |
| **CSV** | `csv` (standard library) | Tabular data, spreadsheets, data import/export[^13_7]. | Simple, widely supported by data tools[^13_8]. |

### JSON (`json` module) (VERY IMP)

JSON (JavaScript Object Notation) is the de facto standard for data exchange on the web. Python's `json` module provides a simple way to work with it.[^13_9][^13_10]

- **Serialization (Python to JSON)**:
    - `json.dumps(obj)`: Converts a Python object (like a `dict` or `list`) into a JSON formatted **string**.[^13_9]
    - `json.dump(obj, file_object)`: Writes the JSON string representation of `obj` to a file-like object.[^13_11]
- **Deserialization (JSON to Python)**:
    - `json.loads(json_string)`: Parses a JSON formatted **string** and converts it into a Python object.[^13_10]
    - `json.load(file_object)`: Reads from a file-like object, parses the JSON data, and returns a Python object.

```python
import json

# Python dictionary
python_data = {
    "name": "Alice",
    "age": 30,
    "isStudent": False,
    "courses": ["History", "Math"]
}

# 1. Serialize to a JSON string
json_string = json.dumps(python_data, indent=4) # indent makes it readable
print(json_string)

# 2. Deserialize from a JSON string back to a Python object
reloaded_data = json.loads(json_string)
print(reloaded_data['name']) # Output: Alice
```


### YAML (`PyYAML` library)

YAML is a human-friendly data serialization format often used for configuration. It is a superset of JSON. It is not in the standard library; you need to install it: `pip install PyYAML`.[^13_3]

- **`yaml.safe_load(stream)`**: Parses a YAML stream and produces Python objects.
    - **Best Practice (VERY IMP)**: Always use `safe_load()` instead of `load()`. The standard `load()` is insecure as it can execute arbitrary Python code, making it dangerous to use with untrusted data.[^13_3]
- **`yaml.dump(data, stream)`**: Serializes a Python object into a YAML formatted stream.

```python
import yaml

# A YAML string
yaml_string = """
name: Bob
age: 42
roles:
  - admin
  - editor
"""

# Load YAML into a Python dictionary
data = yaml.safe_load(yaml_string)
print(data['roles']) # Output: ['admin', 'editor']
```


### TOML (`tomllib` module)

TOML (Tom's Obvious, Minimal Language) is a configuration file format designed to be easy to read. It is the format used for `pyproject.toml`. Support was added to the standard library in Python 3.11 with the `tomllib` module.[^13_5][^13_6]

- `tomllib.loads(toml_string)`: Parses a TOML string into a dictionary.
- `tomllib.load(file_object)`: Parses a TOML file (opened in binary mode, `rb`) into a dictionary.

```python
# Requires Python 3.11+
import tomllib

toml_string = """
[database]
server = "192.168.1.1"
ports = [ 8001, 8001, 8002 ]
"""

config = tomllib.loads(toml_string)
print(config['database']['server']) # Output: 192.168.1.1
```


### CSV (`csv` module) (IMP)

The `csv` module helps read and write tabular data from Comma Separated Values files.[^13_7][^13_8]

- `csv.reader(file_object)`: Reads a CSV file, returning a reader object that iterates over lines, with each row represented as a **list of strings**.[^13_7]
- `csv.DictReader(file_object)`: Similar to `reader`, but maps the information in each row to a `dict` whose keys are given by the first row (the header). This is often more convenient.[^13_8]

```python
import csv

# Using DictReader
with open('employees.csv', 'r', newline='') as csvfile:
    reader = csv.DictReader(csvfile)
    for row in reader:
        print(f"{row['name']} works in the {row['department']} department.")
```


### XML and HTML Parsing (IMP)

- **XML (`xml.etree.ElementTree`, `lxml`)**:
    - `xml.etree.ElementTree`: The built-in module for parsing and creating XML data. It's safe and reasonably efficient.
    - `lxml`: A powerful, fast, and feature-rich third-party library (`pip install lxml`). It's often the preferred tool for complex XML (and HTML) processing and supports XPath, XSLT, and more.[^13_12][^13_13]
- **HTML (`BeautifulSoup`)**:
    - HTML in the wild is often broken or malformed. Standard XML parsers will fail on it.
    - **BeautifulSoup** (`pip install beautifulsoup4`) is the go-to library for web scraping. It sits on top of a parser (like `html.parser` from the standard library or `lxml`) and provides a Pythonic, tag-based interface for navigating and searching a messy HTML document.[^13_14][^13_15]

```python
# BeautifulSoup example for web scraping
from bs4 import BeautifulSoup
import requests

html_doc = requests.get("http://example.com").text
soup = BeautifulSoup(html_doc, 'html.parser')

# Find the first <h1> tag
title = soup.find('h1').text
print(title) # Output: Example Domain
```


### Regular Expressions (`re` module) (VERY IMP)

Regex provides a powerful mini-language for finding and manipulating text patterns.[^13_16]

- **Best Practice**: Use raw strings (`r"..."`) for regex patterns to prevent backslashes from being interpreted as escape sequences.[^13_17]
- **Key Functions**:
    - `re.search(pattern, string)`: Scans through a string, looking for the **first** location where the pattern produces a match. Returns a match object, or `None`.[^13_17]
    - `re.findall(pattern, string)`: Finds **all** non-overlapping matches and returns them as a list of strings.
    - `re.sub(pattern, repl, string)`: Replaces occurrences of the pattern in a string with a replacement string (`repl`).[^13_17]
    - `re.compile(pattern)`: Compiles a regular expression pattern into a pattern object, which can be reused for more efficient matching.

```python
import re

text = "My email is alice@example.com and my friend's is bob.smith@work.co.uk"
# Find all email addresses in the text
emails = re.findall(r'[\w\.-]+@[\w\.-]+', text)
print(emails) # Output: ['alice@example.com', 'bob.smith@work.co.uk']
```


### Binary Parsing (`struct` module)

The `struct` module performs conversions between Python values and C structs represented as Python `bytes` objects. It is essential for working with binary file formats or network protocols.[^13_18][^13_19]

- `struct.pack(format, v1, v2, ...)`: Packs Python values into a `bytes` object according to the `format` string.
- `struct.unpack(format, buffer)`: Unpacks a `bytes` object into a tuple of Python values.

```python
import struct

# Pack an integer, a 2-char string, and a float into bytes
# 'i' = integer, '2s' = 2-char string, 'f' = float
packed_data = struct.pack('>i2sf', 1024, b'PY', 3.14)

# Unpack the bytes back into Python objects
unpacked_data = struct.unpack('>i2sf', packed_data)
print(unpacked_data) # Output: (1024, b'PY', 3.140000104904175)
```


***
Would you like to continue with Section 13: Testing \& Quality?
<span style="display:none">[^13_20]</span>

```
<div style="text-align: center">⁂</div>
```

[^13_1]: https://www.geeksforgeeks.org/python-json/

[^13_2]: https://docs.python.org/3/library/json.html

[^13_3]: https://python.land/data-processing/python-yaml

[^13_4]: https://www.geeksforgeeks.org/python/python-yaml-module/

[^13_5]: https://www.educative.io/answers/how-does-the-tomllib-library-work

[^13_6]: https://realpython.com/python311-tomllib/

[^13_7]: https://www.geeksforgeeks.org/python/working-csv-files-python/

[^13_8]: https://realpython.com/python-csv/

[^13_9]: https://www.w3schools.com/python/python_json.asp

[^13_10]: https://www.pythoncheatsheet.org/modules/json-module

[^13_11]: https://codeinstitute.net/global/blog/working-with-json-in-python/

[^13_12]: https://blog.apify.com/python-lxml-tutorial/

[^13_13]: https://lxml.de/parsing.html

[^13_14]: https://oxylabs.io/blog/beautiful-soup-parsing-tutorial

[^13_15]: https://www.crummy.com/software/BeautifulSoup/bs4/doc/

[^13_16]: https://www.geeksforgeeks.org/python/regular-expression-python-examples/

[^13_17]: https://mimo.org/glossary/python/regex-regular-expressions

[^13_18]: https://www.fluentpython.com/extra/parsing-binary-struct/

[^13_19]: https://parseltongue.co.in/understanding-the-struct-module-in-python/

[^13_20]: https://realpython.com/python-json/


---

# yes

Great, let's move on to ensuring code quality. Here are the revision notes for Section 13: Testing \& Quality.

### Testing Frameworks: `unittest` vs. `pytest` (VERY IMP)

Writing automated tests is crucial for maintaining code quality and preventing regressions. Python has a built-in framework, `unittest`, and a very popular third-party one, `pytest`.[^14_1]


| Feature | `unittest` | `pytest` |
| :-- | :-- | :-- |
| **Origin** | Part of the **standard library**[^14_2][^14_3]. | Third-party (`pip install pytest`). |
| **Boilerplate** | More verbose. Requires creating classes that inherit from `unittest.TestCase`[^14_4]. | More concise. Tests are simple functions. |
| **Assertions** | Uses specific assertion methods: `self.assertEqual()`, `self.assertTrue()`, `self.assertRaises()`[^14_1]. | Uses the standard Python `assert` statement, providing rich output on failure. |
| **Fixtures** | Setup/teardown is done via `setUp()` and `tearDown()` methods. | Has a powerful and flexible **fixture** system using decorators (`@pytest.fixture`)[^14_5]. |
| **Ecosystem** | Basic and self-contained. | Has a vast ecosystem of plugins for things like coverage, async, HTML reports, etc. |

**Best Practice**: While `unittest` is built-in, most of the community has embraced **`pytest`** for its simpler syntax, powerful features, and extensive plugin support.

### Fixtures and Parametrization (Pytest) (IMP)

- **Fixtures (`@pytest.fixture`)**: A function that provides a fixed baseline for tests. They are used for setup and teardown, such as creating a database connection, a temporary file, or a complex object. Pytest injects them into your test functions by name.
- **Parametrization (`@pytest.mark.parametrize`)**: A decorator that allows you to run a single test function multiple times with different arguments. This is highly effective for reducing code duplication.[^14_5][^14_6]

```python
import pytest

# A fixture that provides data for a test
@pytest.fixture
def sample_user():
    return {"name": "Alice", "email": "alice@example.com"}

# A test function that uses the fixture
def test_user_name(sample_user):
    assert sample_user["name"] == "Alice"

# A parametrized test
@pytest.mark.parametrize("a, b, expected", [
    (1, 2, 3),
    (-1, 1, 0),
    (5, 5, 10),
])
def test_add(a, b, expected):
    assert a + b == expected
```


### Mocking (`unittest.mock`) (VERY IMP)

Mocking is the practice of replacing parts of your system (like external APIs or complex objects) with controlled replacements that mimic their behavior. This allows you to test a unit of code in **isolation**. `unittest.mock` is part of the standard library.[^14_7][^14_8]

- **Analogy**: A mock object is like a **stunt double** in a movie. You use the stunt double (`Mock`) when the real actor (`requests.get`) would be too slow, expensive, or dangerous to use in a scene (the test).
- **`Mock`**: A flexible object that can pretend to be any other object. You can specify return values and check if methods were called.
- **`patch`**: A decorator or context manager that temporarily replaces an object in a module with a `Mock` for the duration of a test.[^14_7]

```python
import requests
from unittest.mock import patch

def get_github_user(username):
    response = requests.get(f"https://api.github.com/users/{username}")
    return response.json()

@patch('requests.get') # Replace requests.get with a mock
def test_get_github_user(mock_get):
    # Configure the mock's return value
    mock_response = mock_get.return_value
    mock_response.json.return_value = {"name": "Guido van Rossum"}
    
    # Call the function under test
    user = get_github_user("gvanrossum")
    
    # Assert that the function behaved as expected
    mock_get.assert_called_with("https://api.github.com/users/gvanrossum")
    assert user["name"] == "Guido van Rossum"
```


### Code Coverage (`coverage.py`)

Code coverage measures the percentage of your code that is executed by your tests. It helps you identify parts of your application that are not being tested.[^14_9][^14_10]

- **Workflow**:

1. Run tests under coverage: `coverage run -m pytest`
2. View a report in the terminal: `coverage report`
3. Generate an interactive HTML report: `coverage html`


### Static Analysis (Linters) (IMP)

Static analysis tools inspect your code for errors, style violations, and potential bugs **without actually running it**.


| Tool | Focus | Description |
| :-- | :-- | :-- |
| **`flake8`** | **Speed \& Simplicity** | A popular wrapper around `PyFlakes` (error checking), `pycodestyle` (PEP 8 style), and `McCabe` (complexity). It's fast and easy to configure. |
| **`pylint`** | **Thoroughness** | Very thorough and highly configurable. It checks for style, errors, and "code smells" (patterns that suggest a deeper problem). Can be "noisy" if not configured[^14_11]. |
| **`bandit`** | **Security** | A static analysis tool specifically designed to find common security vulnerabilities in Python code[^14_12]. |

### Type Checking (`mypy`, `pyright`) (IMP)

Type checkers use the type hints in your code (e.g., `name: str`) to find a class of bugs related to incorrect types before you run the code.

- **`mypy`**: The original and most established type checker for Python.
- **`pyright`**: A newer type checker from Microsoft, known for its high performance. It is the engine behind the Pylance extension for VS Code. By default, `pyright` infers return types and checks unannotated code, while `mypy` requires explicit configuration to do so.[^14_13]


### Property-Based Testing (`hypothesis`)

This is a different approach to testing. Instead of writing tests for specific inputs, you define general **properties** that your code should satisfy for *any* valid input. The library then generates hundreds of diverse inputs (including edge cases) to try and find a counterexample that breaks your property.[^14_14][^14_15]

```python
from hypothesis import given, strategies as st

def my_sort(data: list) -> list:
    # A correct sorting function
    return sorted(data)

@given(st.lists(st.integers()))
def test_sort_is_idempotent(data):
    # A property of sorting is that sorting a sorted list doesn't change it.
    assert my_sort(my_sort(data)) == my_sort(data)
```

When `hypothesis` finds a failing example, it automatically simplifies it to the smallest possible case, which is a powerful debugging aid.[^14_14]

### Pre-commit Hooks (`pre-commit` framework)

The `pre-commit` framework allows you to identify simple issues before submission to code review. You define a list of checks (like formatters, linters, and type checkers) in a `.pre-commit-config.yaml` file. The framework runs these checks on your staged files every time you make a commit. This is an excellent way to enforce code quality standards automatically across a team.[^14_16][^14_17]

***
Would you like to continue with Section 14: Standard Library Mastery?
<span style="display:none">[^14_18][^14_19][^14_20]</span>

```
<div style="text-align: center">⁂</div>
```

[^14_1]: https://www.browserstack.com/guide/unit-testing-python

[^14_2]: https://docs.python.org/3/library/unittest.html

[^14_3]: https://realpython.com/python-unittest/

[^14_4]: https://www.geeksforgeeks.org/python/unit-testing-python-unittest/

[^14_5]: https://www.fiddler.ai/blog/advanced-pytest-patterns-harnessing-the-power-of-parametrization-and-factory-methods

[^14_6]: https://stackoverflow.com/questions/42228895/how-to-parametrize-a-pytest-fixture

[^14_7]: https://www.geeksforgeeks.org/python/python-mock-library/

[^14_8]: https://betterstack.com/community/guides/scaling-python/python-unittest-mock/

[^14_9]: https://github.com/nedbat/coveragepy

[^14_10]: https://coverage.readthedocs.io

[^14_11]: https://pycon.switowski.com/04-code-style/linters/

[^14_12]: https://github.com/stratis-storage/project/issues/64

[^14_13]: https://docs.basedpyright.com/v1.31.4/usage/mypy-comparison/

[^14_14]: https://pypi.org/project/hypothesis/

[^14_15]: https://semaphore.io/blog/property-based-testing-python-hypothesis-pytest

[^14_16]: https://ljvmiranda921.github.io/notebook/2018/06/21/precommits-using-black-and-flake8/

[^14_17]: https://pre-commit.com

[^14_18]: https://www.learnenough.com/blog/python-unit-testing-frameworks

[^14_19]: https://py-launch-blueprint.readthedocs.io/en/latest/tasks/type_checking_code.html

[^14_20]: https://www.dataquest.io/blog/unit-tests-python/


---

# yes

Of course. A deep understanding of the standard library separates proficient Python developers from the rest. Here are the revision notes for Section 14: Standard Library Mastery.

### Key Utility Modules

| Module | Purpose | Key Functions/Classes (IMP) |
| :-- | :-- | :-- |
| **`functools`** | Higher-order functions and operations on callables[^15_1][^15_2]. | `partial`, `lru_cache`, `cache`, `wraps`, `reduce`, `singledispatch`[^15_3]. |
| **`itertools`** | Fast, memory-efficient tools for creating and working with iterators[^15_4]. | `count`, `cycle`, `chain`, `accumulate`, `permutations`, `combinations`[^15_4][^15_5]. |
| **`collections`** | Specialized, high-performance container datatypes[^15_6][^15_7]. | `Counter`, `defaultdict`, `deque`, `namedtuple`, `ChainMap`[^15_6]. |
| **`statistics`** | Functions for basic mathematical statistics of numeric data. | `mean`, `median`, `mode`, `stdev`, `variance`[^15_8][^15_9]. |

### Date and Time: `datetime`, `zoneinfo` (IMP)

Handling dates and times is a common task, but time zones make it complex.

- **`datetime` module**: Provides classes for manipulating dates and times.
    - `datetime.datetime`: Represents a specific point in time (year, month, day, hour, minute, second).
    - `datetime.date`: Represents a date (year, month, day).
    - `datetime.timedelta`: Represents a duration or difference between two dates/times.
- **Aware vs. Naive Objects**:
    - **Naive**: Does not have time zone information.
    - **Aware**: Has time zone information via its `tzinfo` attribute.[^15_10]
- **`zoneinfo` module (Python 3.9+)**: The modern, standard way to handle IANA time zones. It eliminates the need for third-party libraries like `pytz` or `dateutil` for most common use cases.[^15_10]
- **Best Practice**: Perform all internal logic and storage using **aware `datetime` objects in UTC**. Only convert to a local time zone for display purposes when interacting with a user.

```python
from datetime import datetime
from zoneinfo import ZoneInfo

# Create a naive datetime
naive_dt = datetime(2025, 10, 26, 12, 0, 0)

# Make it an aware datetime in UTC
utc_dt = naive_dt.replace(tzinfo=ZoneInfo("UTC"))

# Convert it to another time zone for display
helsinki_tz = ZoneInfo("Europe/Helsinki")
local_dt = utc_dt.astimezone(helsinki_tz)

print(f"UTC Time: {utc_dt}")
print(f"Helsinki Time: {local_dt}")
```


### Precise Numerics: `decimal` and `fractions`

- **`decimal`**: As seen before, provides user-settable precision for decimal arithmetic, avoiding the rounding errors of `float`. **Crucial for financial applications**.
- **`fractions`**: Provides rational number arithmetic. It stores numbers as a numerator and a denominator, so it can represent any rational number with perfect precision.[^15_11]


### `weakref`: Non-Owning References (IMP)

The `weakref` module allows you to create references to objects that do not protect the object from being garbage collected.[^15_12]

- **Analogy**: A normal ("strong") reference is like a leash on a dog; as long as the leash is held, the dog won't run away (the object won't be garbage collected). A **weak reference** is like just looking at the dog; if everyone holding a leash lets go, the dog will run away, and you'll just be looking at an empty space.
- **Use Case**: Caching. You can store large objects in a cache using weak references. If the rest of the program stops using an object, the garbage collector can remove it, and the cache will automatically drop its reference, saving memory.[^15_13]
- `weakref.WeakValueDictionary` and `weakref.WeakKeyDictionary` are dictionary subclasses that use weak references for their values or keys, respectively.[^15_13]

```python
import weakref

class BigObject:
    pass

obj = BigObject()
weak_ref = weakref.ref(obj) # Create a weak reference

# You can access the object by calling the reference
print(weak_ref()) # <__main__.BigObject object at ...>

del obj # Delete the only strong reference

# The object is now gone, and the weak reference returns None
print(weak_ref()) # None
```


### `copy`: Shallow vs. Deep Copy (VERY IMP)

The `copy` module provides functions for duplicating objects. The distinction between shallow and deep copies is a frequent interview topic.[^15_14]


| Copy Type | `copy.copy(x)` (Shallow) | `copy.deepcopy(x)` (Deep) |
| :-- | :-- | :-- |
| **Action** | Creates a new **top-level** object but inserts **references** to the objects found in the original[^15_15]. | Creates a new top-level object and then **recursively** creates new copies of all objects found within the original[^15_14]. |
| **Result** | A new object that is independent at the top level, but shares all nested data[^15_15]. | A completely independent clone of the original object and all of its nested data[^15_14]. |
| **Analogy** | You **photocopy** a document binder. You get a new binder, but the pages inside are still just copies pointing to the original pages. | You **manually retype** every page in the binder into a brand new set of pages and put them in a new binder. |

```python
import copy

# A list containing a nested list
original_list = [1, 2, [3, 4]]

# Shallow copy
shallow = copy.copy(original_list)
# Deep copy
deep = copy.deepcopy(original_list)

# Modify the nested list in the original
original_list[^15_2][^15_0] = 'X'

print(f"Original: {original_list}") # [1, 2, ['X', 4]]
print(f"Shallow:  {shallow}")      # [1, 2, ['X', 4]] <-- Affected!
print(f"Deep:     {deep}")         # [1, 2, [3, 4]]  <-- Unaffected.
```


### `logging` Advanced Configuration

While `logging.basicConfig()` is fine for simple scripts, real applications require more robust configuration, typically done via a dictionary with `logging.config.dictConfig`. This allows you to define:

- **Loggers**: The entry points for logging (`logging.getLogger(__name__)`).
- **Handlers**: Where log messages are sent (e.g., `StreamHandler` for console, `FileHandler` for files).
- **Formatters**: How log messages are formatted (e.g., timestamp, log level, message).
- **Filters**: Rules to further control which log records are processed.


### `argparse` for CLI Parsing

The `argparse` module is the standard way to create user-friendly command-line interfaces. It automatically generates help messages and handles argument parsing and validation.

```python
import argparse

parser = argparse.ArgumentParser(description="A simple CLI tool.")
parser.add_argument("input_file", help="The file to process.")
parser.add_argument("-o", "--output", help="Output file name.", default="output.txt")
parser.add_argument("-v", "--verbose", action="store_true", help="Enable verbose output.")

args = parser.parse_args()

print(f"Input file: {args.input_file}")
print(f"Output file: {args.output}")
if args.verbose:
    print("Verbose mode enabled.")
```


### `configparser`, `dataclasses`, and `typing`

- **`configparser`**: For parsing classic INI-style configuration files.
- **`dataclasses`**: A decorator for creating classes that primarily store data, automatically generating methods like `__init__` and `__repr__`.
- **`typing`**: Provides the foundation for type hints, enabling static analysis and improving code clarity.

***
This concludes the structured revision guide. I have covered all the sections you requested. I am ready to assist you further.
<span style="display:none">[^15_16][^15_17][^15_18][^15_19][^15_20]</span>

```
<div style="text-align: center">⁂</div>
```

[^15_1]: https://docs.python.org/3/library/functools.html

[^15_2]: https://www.geeksforgeeks.org/python/functools-module-in-python/

[^15_3]: https://realpython.com/ref/stdlib/functools/

[^15_4]: https://www.pythoncheatsheet.org/modules/itertools-module

[^15_5]: https://www.cybrosys.com/blog/an-overview-of-itertools-in-python-and-its-functions-and-classes

[^15_6]: https://www.pickl.ai/blog/python-collections-module/

[^15_7]: https://www.geeksforgeeks.org/python/python-collections-module/

[^15_8]: https://www.w3schools.com/python/module_statistics.asp

[^15_9]: https://www.tutorialsteacher.com/python/statistics-module

[^15_10]: https://docs.djangoproject.com/en/5.2/topics/i18n/timezones/

[^15_11]: https://www.askpython.com/python-modules/python-fractions-module

[^15_12]: https://realpython.com/ref/stdlib/weakref/

[^15_13]: https://www.geeksforgeeks.org/python/weak-references-in-python/

[^15_14]: https://www.educative.io/answers/what-is-difference-between-shallow-copy-and-deep-copy-in-python

[^15_15]: https://www.linkedin.com/pulse/understanding-difference-between-shallow-copy-deep-python-torabi-nnh5e

[^15_16]: https://www.python-engineer.com/posts/functools-overview/

[^15_17]: https://www.tutorialspoint.com/python/python_functools_module.htm

[^15_18]: https://www.scaler.com/topics/python-functools/

[^15_19]: https://realpython.com/python-datetime/

[^15_20]: https://www.educative.io/answers/how-to-get-a-fraction-from-a-decimal-number-in-python

