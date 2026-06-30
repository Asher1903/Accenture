# Python Interview Preparation Guide (Accenture)

This guide covers the 13 intermediate and advanced Python interview topics at Accenture. Each topic is structured to give you a clear definition, simple code examples, and a **"How to explain to the interviewer"** section with key talking points.

---

## 1. Python Data Types

### Definition
Python is a dynamically-typed language, meaning you don't need to declare variable types explicitly. Python's data types can be classified into:

| Category | Data Types | Description | Mutability |
| :--- | :--- | :--- | :--- |
| **Numeric** | `int`, `float`, `complex` | Whole numbers, decimals, and complex numbers | **Immutable** |
| **Sequence** | `str`, `list`, `tuple`, `range` | Ordered collections of items | `str`, `tuple`: **Immutable** <br> `list`: **Mutable** |
| **Mapping** | `dict` | Key-value pairs | **Mutable** |
| **Set** | `set`, `frozenset` | Unordered collections of unique elements | `set`: **Mutable** <br> `frozenset`: **Immutable** |
| **Boolean** | `bool` | `True` or `False` values | **Immutable** |
| **None Type** | `NoneType` | Represents the absence of a value (`None`) | **Immutable** |

### Code Example
```python
# Mutable example
my_list = [1, 2, 3]
my_list[0] = 99  # Allowed

# Immutable example
my_tuple = (1, 2, 3)
# my_tuple[0] = 99  # Raises TypeError
```

> [!TIP]
> **How to explain to the interviewer:**
> 1. **Classification:** Start by grouping them (Numeric, Sequence, Mapping, Set, Boolean).
> 2. **Mutability Concept:** Emphasize the difference between **Mutable** (can be changed after creation, like `list`, `dict`, `set`) and **Immutable** (cannot be changed, like `int`, `float`, `str`, `tuple`). Explain that modifying an immutable object creates a new object in memory.

---

## 2. Difference Between List and Tuple

### Quick Comparison

| Feature | List | Tuple |
| :--- | :--- | :--- |
| **Syntax** | Square brackets `[1, 2]` | Parentheses `(1, 2)` |
| **Mutability** | **Mutable** (can add, remove, modify elements) | **Immutable** (cannot change after creation) |
| **Memory** | Consumes more memory (allocated extra space for dynamic growth) | Consumes less memory (fixed size) |
| **Performance** | Slower iterations and allocation | Faster iterations and allocation |
| **Hashability** | Non-hashable (cannot be used as dict keys or set elements) | Hashable (if all elements inside are immutable; can be used as keys) |

### Code Example
```python
# List is mutable
colors_list = ["red", "blue"]
colors_list.append("green")  # Works!

# Tuple is immutable
colors_tuple = ("red", "blue")
# colors_tuple.append("green")  # AttributeError
```

> [!TIP]
> **How to explain to the interviewer:**
> *"The main difference is mutability. Lists are mutable and suitable for collections of data that will change dynamically during runtime. Tuples are immutable and are used for read-only write-protected data (like database credentials or geographic coordinates). Because tuples are immutable, they are faster, use less memory, and can be used as dictionary keys."*

---

## 3. Difference Between Set and Dictionary

### Quick Comparison

| Feature | Set | Dictionary |
| :--- | :--- | :--- |
| **Syntax** | `{1, 2, 3}` or `set()` | `{"key": "value"}` |
| **Structure** | Collection of unique elements | Collection of key-value pairs |
| **Keys/Values** | Only values (no duplicates allowed) | Keys must be unique and immutable; values can be duplicates |
| **Ordering** | Unordered | Insertion order is preserved (Python 3.7+) |
| **Primary Use** | Mathematical operations (union, intersection) & removing duplicates | Storing structured data for quick key-based lookups |

### Code Example
```python
# Set
unique_numbers = {1, 2, 2, 3}  # Results in {1, 2, 3}

# Dictionary
user_info = {"name": "Amit", "role": "Developer"}
```

> [!TIP]
> **How to explain to the interviewer:**
> *"Both sets and dictionaries use hash tables under the hood for \(O(1)\) lookup time complexity. However, a Set is a collection of unique, unordered elements (useful for deduplication and mathematical operations like intersection), whereas a Dictionary stores key-value pairs where keys must be unique and immutable (useful for rapid lookups and representing structured data)."*

---

## 4. Explain `*args` and `**kwargs`

### Definition
*   `*args` allows a function to accept any number of **positional arguments**. Inside the function, `args` is received as a **Tuple**.
*   `**kwargs` allows a function to accept any number of **keyword (named) arguments**. Inside the function, `kwargs` is received as a **Dictionary**.
*   The actual names `args` and `kwargs` are conventions; the unpacking operators `*` and `**` are what matter.

### Code Example
```python
def print_details(*args, **kwargs):
    print("args (tuple):", args)
    print("kwargs (dict):", kwargs)

print_details(1, 2, 3, name="Amit", age=25)
# Output:
# args (tuple): (1, 2, 3)
# kwargs (dict): {'name': 'Amit', 'age': 25}
```

> [!TIP]
> **How to explain to the interviewer:**
> *"We use `*args` and `**kwargs` when we don't know beforehand how many arguments might be passed to a function. A classic use case is writing wrapper functions, decorators, or subclassing where we pass all arguments to the parent class constructor using `super().__init__(*args, **kwargs)`."*

---

## 5. What is a Lambda Function?

### Definition
A lambda function is an **anonymous (nameless) function** defined using the `lambda` keyword. It can take any number of arguments but can only have a **single expression** (the result of which is automatically returned without a `return` keyword).

### Code Example
```python
# Regular function
def square(x):
    return x * x

# Lambda equivalent
square_lambda = lambda x: x * x

# Common real-world usage: Sorting a list of tuples by the second element
points = [(1, 9), (2, 5), (3, 7)]
points.sort(key=lambda item: item[1])
print(points)  # Output: [(2, 5), (3, 7), (1, 9)]
```

> [!TIP]
> **How to explain to the interviewer:**
> *"Lambda functions are throwaway, inline functions. They are used when we need a simple function for a short period, typically as arguments to higher-order functions like `map()`, `filter()`, or `sorted()`. I should avoid using lambda functions for complex logic to maintain code readability."*

---

## 6. Difference Between `==` and `is`

### Definition
*   `==` is the **equality** operator. It compares the **values** of the two objects. (Under the hood, it calls the object's `__eq__` method).
*   `is` is the **identity** operator. It compares the **memory locations (IDs)** of the two objects. It returns `True` only if both variables point to the exact same object in memory.

### Code Example
```python
list_a = [1, 2, 3]
list_b = [1, 2, 3]

print(list_a == list_b)  # True (values are identical)
print(list_a is list_b)  # False (stored in different memory addresses)

list_c = list_a
print(list_a is list_c)  # True (both point to the same list object)
```

> [!IMPORTANT]
> **Interviewer Trap: Small Integer Interning**
> If you test `x = 10; y = 10; print(x is y)`, Python returns `True`. This is because Python caches (interns) small integers between `-5` and `256` in memory to optimize performance. Mentioning this will highly impress the interviewer!

---

## 7. What are Decorators?

### Definition
A decorator is a function that takes another function as an argument, extends its behavior without modifying its source code, and returns a new function. It is based on the concept that functions in Python are **first-class objects** (they can be passed around as arguments, assigned to variables, and returned).

### Code Example
```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Executing code BEFORE the actual function...")
        result = func(*args, **kwargs)
        print("Executing code AFTER the actual function...")
        return result
    return wrapper

@my_decorator
def greet(name):
    print(f"Hello, {name}!")

greet("Amit")
```

> [!TIP]
> **How to explain to the interviewer:**
> *"Decorators allow us to wrap another function to extend its behavior cleanly. Common real-world applications include logging, tracking execution time, caching/memoization, and checking user authentication/authorization in web frameworks like Flask and Django."*

---

## 8. What are Generators?

### Definition
Generators are functions that return an iterator using the `yield` keyword instead of `return`. 
*   Unlike `return`, which terminates the function completely, `yield` pauses the function's execution, saves its state, and returns the yielded value.
*   When called again (via a loop or `next()`), the generator resumes exactly where it left off.

### Code Example
```python
def fibonacci_generator(limit):
    a, b = 0, 1
    while a < limit:
        yield a
        a, b = b, a + b

# Using the generator
for num in fibonacci_generator(10):
    print(num, end=" ")  # Output: 0 1 1 2 3 5 8
```

> [!IMPORTANT]
> **Key Benefit: Memory Efficiency (Lazy Evaluation)**
> Generators do not store the entire sequence in memory. They generate one item at a time on demand. This makes them crucial when reading large log files (gigabytes of data) or infinite streams, preventing Out-Of-Memory (OOM) errors.

---

## 9. Explain Exception Handling

### Definition
Exception handling is a mechanism to handle runtime errors gracefully so that the application doesn't crash. In Python, it is implemented using the `try-except-else-finally` block:

1.  **`try`**: Code block that might raise an exception.
2.  **`except`**: Code block that runs if a specific exception is raised in `try`.
3.  **`else`**: Code block that runs **only if no exceptions** occurred in the `try` block.
4.  **`finally`**: Code block that **always runs**, regardless of whether an exception occurred. (Used for cleanup operations like closing database connections or files).

### Code Example
```python
try:
    file = open("data.txt", "r")
    content = file.read()
    result = 10 / len(content)
except FileNotFoundError:
    print("Error: The file was not found.")
except ZeroDivisionError:
    print("Error: Cannot divide by zero because the file is empty.")
else:
    print("File read successfully. Result:", result)
finally:
    try:
        file.close()
        print("File closed successfully.")
    except NameError:
        pass  # File variable was never created
```

> [!TIP]
> **How to explain to the interviewer:**
> *"Always catch specific exceptions (like `ValueError` or `KeyError`) instead of writing a generic `except Exception:`. Generic catches mask other errors and make debugging difficult. The `finally` block is essential because it guarantees resources are released safely even if the code crashes."*

---

## 10. What are Modules and Packages?

### Definition
*   **Module**: A module is a single Python file (with a `.py` extension) containing executable code, functions, classes, or variables.
*   **Package**: A package is a directory (folder) that contains multiple modules (files) and sub-packages. Traditionally, it contains a special file named `__init__.py` (which runs when the package is imported).

### Structure Example
```text
my_project/
│
└── payment_system/            <-- This is a Package
    ├── __init__.py            <-- Initializes the package
    ├── credit_card.py         <-- This is a Module
    └── upi.py                 <-- This is a Module
```

### Import Code
```python
# Importing a module from a package
from payment_system import credit_card

credit_card.process_payment(100)
```

> [!TIP]
> **How to explain to the interviewer:**
> *"Modules help in code reusability and separating concerns within a single file. Packages allow us to organize multiple related modules hierarchically in folders. This prevents naming conflicts and makes large-scale applications easier to manage."*

---

## 11. List Comprehension

### Definition
List comprehension offers a shorter, more readable syntax to create a new list based on the values of an existing iterable. It replaces verbose `for` loops and `if` conditions with a single line of code.

### Syntax
`new_list = [expression for item in iterable if condition]`

### Code Example
```python
# 1. Traditional approach (4 lines)
even_squares = []
for x in range(10):
    if x % 2 == 0:
        even_squares.append(x ** 2)

# 2. List comprehension approach (1 line)
even_squares = [x ** 2 for x in range(10) if x % 2 == 0]
```

> [!TIP]
> **How to explain to the interviewer:**
> *"List comprehension is a concise and pythonic way to create lists. In addition to being cleaner, list comprehensions are slightly faster than standard `for` loops because the looping operation is executed at C-level speed inside the interpreter rather than running step-by-step Python byte-code. However, we should avoid them if the expression becomes too nested or complex, as it compromises code readability."*

---

## 12. Context Managers (`with` statement)

### Definition
A **Context Manager** is a tool that automates the allocation and release of resources. It guarantees that setup actions (like opening a file or database connection) are matched with the correct teardown actions (like closing the file or connection), even if errors occur inside the block. 

### Analogy
Imagine borrowing a book from a study room. A context manager acts as an automated system that registers the book when you walk in and guarantees it is returned when you walk out, even if you trip and get hurt (raise an exception) inside the room.

### Code Example
```python
# Standard way (Using Context Manager)
with open("test.txt", "w") as file:
    file.write("Hello, World!")
# File is automatically closed here! Even if an exception occurred inside the block.

# Custom Context Manager using a Class
class CustomOpen:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode

    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file

    def __exit__(self, exc_type, exc_val, exc_tb):
        self.file.close()
```

> [!IMPORTANT]
> **Under the Hood: The Protocol**
> Explain to the interviewer that any class can become a context manager if it implements the **Context Manager Protocol**:
> 1.  `__enter__()`: Executed when entering the `with` block (handles setup).
> 2.  `__exit__()`: Executed when leaving the `with` block (handles cleanup/exception handling).

---

## 13. How Python Handles Memory

### Definition
Python utilizes automatic memory management. As a developer, you don't need to manually allocate or deallocate memory (unlike languages like C or C++). Memory management in Python consists of three main pillars:

### 1. The Private Heap Space
All Python objects, classes, and variables are stored in a **Private Heap**. Programmers do not have direct access to this heap; the Python interpreter (specifically the Python memory manager) handles memory allocation.

### 2. Reference Counting (Primary Garbage Collector)
Every object in Python has a reference count associated with it. 
*   When you create a reference to an object, its reference count increases by `1`.
*   When a reference goes out of scope or is deleted, the count decreases by `1`.
*   **Memory Release:** When an object's reference count drops to **`0`**, Python immediately reclaims its memory.

```python
x = [1, 2, 3]  # Reference count for list is 1
y = x          # Reference count for list is 2
del x          # Reference count for list is 1
del y          # Reference count for list is 0 -> Memory is instantly freed!
```

### 3. Generational Garbage Collector (Secondary GC)
*   **The Problem:** What if Object A references Object B, and Object B references Object A (a **Circular Reference**)? Even if they are disconnected from the rest of the code, their reference counts will remain `1`. They will leak memory.
*   **The Solution:** Python runs a cyclic garbage collector in the background. It groups objects into three generations (Gen 0, Gen 1, Gen 2) based on survival. It scans these generations periodically to detect circular reference cycles and delete unused objects.

> [!TIP]
> **How to explain to the interviewer:**
> *"Python manages memory automatically using a **Private Heap**. Its primary memory reclamation mechanism is **Reference Counting**, which immediately deallocates objects when their count hits 0. To handle circular references (which reference counting cannot resolve), Python uses a cyclic **Generational Garbage Collector** that scans objects in the background."*
