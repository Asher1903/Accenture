# Python Basics & Functions Interview Guide

This guide covers core introductory concepts, syntax structures, and function mechanics in Python. Each topic contains clear definitions, simple code examples, and structured talking points to help you explain them in an interview.

---

## 1. Features of Python

### Key Features
*   **Easy to Learn and Read:** Simple syntax resembling natural English.
*   **Interpreted:** Executes code line-by-line, facilitating rapid debugging.
*   **Dynamically Typed:** Variable types are declared automatically at runtime.
*   **Object-Oriented & Multi-Paradigm:** Supports OOP, Procedural, and Functional programming.
*   **Platform Independent:** Write once, run anywhere.
*   **Large Standard Library:** Rich set of built-in functions and modules.

> [!TIP]
> **How to explain to the interviewer:**
> *"Python is a high-level, dynamically-typed, interpreted language. Its key selling point is developer productivity and code readability, allowing you to write complex programs with fewer lines of code compared to C++ or Java."*

---

## 2. Why is Python called an Interpreted Language?

### Definition
Instead of compiling the whole source code directly into machine-executable binary files (like C/C++ do), Python executes code dynamically at runtime.

### CPython Compilation Pipeline
1.  **Bytecode Generation:** Python compiles `.py` files into platform-independent intermediate **bytecode** (saved as `.pyc` files).
2.  **PVM execution:** The **Python Virtual Machine (PVM)** interprets the bytecode line-by-line into machine code for the target processor.

> [!TIP]
> **How to explain to the interviewer:**
> *"Python is described as an interpreted language because it translates and executes bytecode line-by-line at runtime. In reality, it is a hybrid: source code is first compiled into intermediate bytecode, which is then interpreted by the Python Virtual Machine (PVM)."*

---

## 3. Python Data Types

Python's built-in data types can be grouped as follows:
*   **Numeric:** `int`, `float`, `complex`
*   **Sequence:** `str`, `list`, `tuple`, `range`
*   **Mapping:** `dict`
*   **Set Types:** `set`, `frozenset`
*   **Boolean:** `bool` (`True`/`False`)
*   **Binary:** `bytes`, `bytearray`
*   **None Type:** `NoneType` (`None`)

---

## 4. Difference Between List, Tuple, Set, and Dictionary

| Data Structure | Syntax | Mutability | Ordering | Duplicate Values | Access Method |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **List** | `[1, 2, 3]` | **Mutable** | Ordered | Allowed | By Index (e.g., `l[0]`) |
| **Tuple** | `(1, 2, 3)` | **Immutable** | Ordered | Allowed | By Index (e.g., `t[0]`) |
| **Set** | `{1, 2, 3}` | **Mutable** | Unordered | Not Allowed | Checking membership (`in`) |
| **Dictionary** | `{"k": "v"}` | **Mutable** | Ordered (3.7+) | Unique Keys, duplicate values | By Key (e.g., `d["k"]`) |

---

## 5. Difference Between `==` and `is`

*   **`==` (Equality Operator):** Compares the **values** of two objects to see if they are equivalent.
*   **`is` (Identity Operator):** Compares the **memory addresses** of two objects to see if they point to the exact same object.

### Code Example
```python
a = [1, 2]
b = [1, 2]
print(a == b)  # True (same values)
print(a is b)  # False (different addresses in memory)
```

---

## 6. Mutable and Immutable Objects

*   **Mutable Objects:** Can change their state or content after creation without changing their memory address.
    *   *Examples:* `list`, `dict`, `set`.
*   **Immutable Objects:** Cannot be changed after creation. Any attempt to modify them results in the creation of a new object in memory.
    *   *Examples:* `int`, `float`, `str`, `tuple`, `bool`.

### Code Example
```python
# Strings are immutable
name = "Amit"
# name[0] = "O"  # TypeError

# Lists are mutable
items = [1, 2]
items[0] = 99  # Works!
```

---

## 7. Explain Indentation in Python

### Definition
Unlike languages that use curly braces `{}` to define code blocks, Python uses whitespaces/indentation to specify scope.
*   The recommended standard (PEP 8) is **4 spaces**.
*   Inconsistent indentation throws an `IndentationError`.

---

## 8. What are Keywords in Python?

### Definition
Keywords are **reserved words** that have a fixed, pre-defined meaning for the Python interpreter. They cannot be used as names for variables, functions, or classes.

*   *Examples:* `def`, `class`, `if`, `else`, `while`, `try`, `except`, `import`, `lambda`, `None`.
*   You can view them with:
    ```python
    import keyword
    print(keyword.kwlist)
    ```

---

## 9. What is a Function?

### Definition
A function is a block of organized, reusable code that performs a specific, isolated task. It helps partition code, makes it reusable, and supports the **DRY (Don't Repeat Yourself)** principle.

```python
def calculate_square(number):
    return number * number
```

---

## 10. Difference Between Parameters and Arguments

*   **Parameters:** The variable placeholders defined inside the function's declaration signature.
*   **Arguments:** The actual values passed to the function when it is invoked.

```python
# 'n' is a PARAMETER
def print_number(n):
    print(n)

# '42' is an ARGUMENT
print_number(42)
```

---

## 11. Explain `*args` and `**kwargs`

*   **`*args`:** Allows a function to take a variable number of positional arguments. Inside the function, they are gathered into a **Tuple**.
*   **`**kwargs`:** Allows a function to take a variable number of named/keyword arguments. Inside the function, they are gathered into a **Dictionary**.

```python
def example(*args, **kwargs):
    print(args)    # Tuple
    print(kwargs)  # Dictionary
```

---

## 12. What is Recursion?

### Definition
Recursion is when a function calls itself directly or indirectly to solve a problem by dividing it into smaller sub-problems.
*   **Base Case:** A stopping condition that returns a value directly (prevents infinite recursion).
*   **Recursive Case:** The step where the function calls itself with modified parameters.

```python
def sum_up_to(n):
    if n == 1:
        return 1  # Base Case
    return n + sum_up_to(n - 1)  # Recursive Case
```

---

## 13. What is a Lambda Function?

### Definition
A lambda function is an anonymous, single-expression function defined with the `lambda` keyword instead of `def`. It automatically returns the result of the expression without a `return` statement.

```python
multiply = lambda x, y: x * y
print(multiply(4, 5))  # Output: 20
```
