# Python Fundamentals Interview Preparation Guide

This guide covers the 16 core Python language topics from the **Round 1: Core Language** slide. Each topic is broken down into a **Core Concept**, **Example Code**, and an **Interview script** ("How to Say It").

---

## 1. Why is Python called an interpreted language?

### Core Concept
Python uses a hybrid compilation-interpretation model. When you run a Python script:
1. The **compiler** parses the source code (`.py`) and compiles it into intermediate bytecode (`.pyc`).
2. The **Python Virtual Machine (PVM)**—which is the interpreter—reads and executes this bytecode instruction by instruction on the target machine.

While it does undergo a compilation phase, Python is referred to as an "interpreted" language because the final step of translating code into machine instructions happens dynamically at runtime by the PVM, rather than beforehand into native machine code (like C/C++).

### Example Code
```python
import dis

def greet(name):
    return f"Hello, {name}!"

# dis.dis lets us view the compiled bytecode instructions that the PVM interprets
dis.dis(greet)
```

### How to Say It in an Interview
> *"Python is technically a hybrid compiled/interpreted language. When a script runs, Python first compiles the source code into an intermediate format called **bytecode**. This bytecode is then executed line-by-line by the **Python Virtual Machine (PVM)**, which is the interpreter. We call Python 'interpreted' because execution is performed by this virtual machine at runtime, providing platform independence at the cost of some execution speed compared to ahead-of-time compiled languages like C++."*

---

## 2. Mutable vs. Immutable Objects

### Core Concept
*   **Mutable Objects**: Can modify their content after creation without changing their identity (memory address, returned by `id()`).
*   **Immutable Objects**: Content cannot be modified. Any operation that appears to modify an immutable object actually creates a new object in memory with a new identity.

| Category | Data Types |
| :--- | :--- |
| **Mutable** | `list`, `dict`, `set`, `bytearray`, user-defined classes (by default) |
| **Immutable** | `int`, `float`, `complex`, `str`, `tuple`, `bool`, `frozenset`, `bytes` |

### Example Code
```python
# Mutable example
my_list = [1, 2]
print(id(my_list))  # E.g., 140231920803648
my_list.append(3)
print(id(my_list))  # Identity remains the SAME

# Immutable example
my_str = "hello"
print(id(my_str))   # E.g., 140231920822128
my_str += " world"
print(id(my_str))   # Identity is DIFFERENT (a new string was created)
```

### How to Say It in an Interview
> *"In Python, every variable points to an object. Objects are either mutable or immutable. **Mutable objects**, like lists, dicts, and sets, can be modified in-place without changing their memory address. **Immutable objects**, like strings, tuples, and numbers, cannot be changed. If you try to modify them, Python creates a new object in memory. A key practical difference is that immutable objects are **hashable** (if they contain only hashable values), meaning they can be used as dictionary keys or set elements, whereas mutable objects cannot."*

---

## 3. List vs. Tuple vs. Set vs. Dictionary

### Core Concept
*   **List**: Ordered, mutable sequence of elements. Allows duplicates.
*   **Tuple**: Ordered, immutable sequence. Allows duplicates. Faster and safer (read-only) than lists.
*   **Set**: Unordered collection of unique, hashable elements. Extremely fast membership testing (`O(1)`).
*   **Dictionary**: Collection of key-value pairs. Keys must be unique and hashable. Fast lookups and inserts (`O(1)`).

### Example Code
```python
# List: For sequential, modifiable data
users = ["Alice", "Bob"]

# Tuple: For fixed records or dictionary keys
location = (40.7128, -74.0060)

# Set: For membership tests and removing duplicates
unique_ids = {101, 102, 103}
print(104 in unique_ids)  # O(1) time complexity

# Dictionary: For key-value mapping
prices = {"apple": 1.5, "banana": 0.8}
```

### How to Say It in an Interview
> *"Choosing the right collection depends on ordering, mutability, and lookup speed:
> 1. Use a **List** when sequence order is important and the data needs to change.
> 2. Use a **Tuple** for structured, read-only data, which is more memory-efficient and can act as dict keys.
> 3. Use a **Set** for storing unique elements and performing fast $O(1)$ membership checks or set operations.
> 4. Use a **Dictionary** when you need to associate keys with values for $O(1)$ lookups."*

---

## 4. `append()` vs. `extend()` vs. `insert()`

### Core Concept
All three modify a list, but in different ways:
*   **`append(x)`**: Adds the object `x` as a single element to the end of the list. Time: `O(1)` (amortized).
*   **`extend(t)`**: Iterates through the collection `t` and adds each of its elements to the end of the list. Time: `O(k)` (where $k$ is the length of `t`).
*   **`insert(i, x)`**: Inserts element `x` at index `i`, shifting all subsequent elements right. Time: `O(n)`.

### Example Code
```python
# Starting list
a = [1, 2]
b = [1, 2]
c = [1, 2]

# append adds the argument as a single element
a.append([3, 4])
print(a)  # [1, 2, [3, 4]]

# extend flattens the input iterable
b.extend([3, 4])
print(b)  # [1, 2, 3, 4]

# insert adds at a specific index (shifts items)
c.insert(1, 99)
print(c)  # [1, 99, 2]
```

### How to Say It in an Interview
> *"**`append`** adds its argument to the end of the list as a single object. If you append a list, you get a nested list. **`extend`** iterates over its argument and adds each element individually, effectively merging the collections. **`insert`** places an element at a specific index. Performance-wise, `append` is very fast at $O(1)$ amortized time, whereas `insert` is $O(n)$ because it requires shifting all subsequent elements in memory."*

---

## 5. `remove()` vs. `pop()` vs. `del` vs. `clear()`

### Core Concept
These methods remove items from collections with distinct behaviors:
*   **`remove(val)`**: Deletes the **first occurrence** of `val`. Raises `ValueError` if the value is not present. Returns `None`. Time: `O(n)`.
*   **`pop(idx=-1)`**: Deletes and **returns** the item at index `idx` (defaults to the last item). Raises `IndexError` if the list is empty or index is out of bounds. Time: `O(1)` for the end, `O(n)` for any other index.
*   **`del`**: A Python keyword/statement used to delete an item at an index, slice, or delete the entire variable. Time: `O(n)` for shifts.
*   **`clear()`**: Empties the collection entirely. Time: `O(n)`.

### Example Code
```python
x = [10, 20, 30, 20, 40]

x.remove(20)  # Removes first '20'
print(x)      # [10, 30, 20, 40]

popped_item = x.pop(1)  # Pops item at index 1 (30)
print(popped_item)      # 30
print(x)                # [10, 20, 40]

del x[0]      # Deletes index 0
print(x)      # [20, 40]

x.clear()     # Removes everything
print(x)      # []
```

### How to Say It in an Interview
> *"The main differences lie in parameters, return values, and errors:
> * Use **`remove`** when you know the **value** you want to delete; it returns nothing and raises a `ValueError` if the value isn't there.
> * Use **`pop`** when you need the **index** and want to **retrieve** the removed value; it raises an `IndexError` on invalid indices.
> * **`del`** is a statement that deletes references (including slices) and doesn't return anything.
> * **`clear`** empties the entire list while maintaining the list reference."*

---

## 6. `is` vs. `==` (Identity vs. Equality)

### Core Concept
*   **`==` (Equality)**: Compares the **values** of two objects. It evaluates to `True` if the contents of the objects are equivalent (uses the `__eq__` method).
*   **`is` (Identity)**: Compares the **memory addresses** of two objects. It evaluates to `True` only if both variables point to the exact same object in memory (`id(a) == id(b)`).

### Example Code
```python
# Lists with identical content but different memory allocations
list_a = [1, 2, 3]
list_b = [1, 2, 3]

print(list_a == list_b)  # True (same values)
print(list_a is list_b)  # False (different objects in memory)

# Assigning reference
list_c = list_a
print(list_a is list_c)  # True (points to the same memory location)

# Note: Python caches small integers (-5 to 256) and short strings (interning)
x = 250
y = 250
print(x is y)  # True (due to CPython integer caching)
```

### How to Say It in an Interview
> *"The **`==`** operator checks for **equality**, checking if the values or contents of two objects are the same. The **`is`** operator checks for **identity**, verifying if both variables point to the exact same object in memory. In practice, `is` should be used for comparing with singletons like `None` (e.g., `if val is None:`), while `==` should be used for comparing values."*

---

## 7. Deep Copy vs. Shallow Copy

### Core Concept
When copying compound objects (objects containing other objects, like nested lists):
*   **Shallow Copy**: Creates a new outer object, but inserts references to the original nested objects. Modifying nested mutable elements affects both copy and original.
*   **Deep Copy**: Creates a new outer object and recursively clones all nested objects. Fully independent.

### Example Code
```python
import copy

original = [[1, 2], [3, 4]]

# Shallow Copy
shallow = copy.copy(original)
# Deep Copy
deep = copy.deepcopy(original)

# Modify nested mutable element
original[0][0] = 99

print(original)  # [[99, 2], [3, 4]]
print(shallow)   # [[99, 2], [3, 4]] -> Impacted because it copied references
print(deep)      # [[1, 2], [3, 4]]  -> Unchanged because it copied values recursively
```

### How to Say It in an Interview
> *"A **shallow copy** constructs a new compound object but fills it with references to the nested objects inside the original. Therefore, changes to nested mutable elements are reflected in both copies. A **deep copy** recursively copies everything, constructing a completely independent object. We use the `copy` module in Python to achieve this, where `copy.copy()` is shallow and `copy.deepcopy()` is deep."*

---

## 8. Python Memory Management, Reference Counting, & Garbage Collection

### Core Concept
Python's memory management has three layers:
1.  **Memory Allocation**: PyMalloc manages the private heap, allocating memory for Python objects.
2.  **Reference Counting**: The primary memory management system. Each object tracks how many references point to it (`sys.getrefcount()`). When this count drops to 0, Python immediately deallocates the object.
3.  **Garbage Collector (GC)**: A secondary generational, cyclic garbage collector. Reference counting cannot detect **reference cycles** (e.g., Object A points to B, and B points to A, but both are unreachable by the main program). The GC periodically searches for and sweeps these cycles.

### Example Code
```python
import sys
import gc

class Node:
    pass

# Reference Counting
a = Node()
print(sys.getrefcount(a) - 1)  # Prints count (typically 1). Subtract 1 for temporary arg reference

# Reference Cycle (GC is needed here)
x = Node()
y = Node()
x.child = y
y.parent = x

del x
del y
# Memory isn't freed immediately because reference counts are still 1 (pointing to each other).
# The GC will eventually detect and collect this cycle.
gc.collect()  # Forces garbage collection run
```

### How to Say It in an Interview
> *"Python manages memory using a private heap. It relies primarily on **Reference Counting**, where every object tracks its references; once an object's reference count hits zero, it is instantly deallocated. However, reference counting fails to handle **reference cycles** (where objects reference each other but are unreachable). To solve this, Python has a built-in **Generational Garbage Collector** that runs periodically in the background, identifying cycles and cleaning up orphaned objects."*

---

## 9. `*args` and `**kwargs`

### Core Concept
*   **`*args`**: Allows a function to accept any number of positional arguments. Inside the function, `args` is received as a **tuple**.
*   **`**kwargs`**: Allows a function to accept any number of keyword arguments. Inside the function, `kwargs` is received as a **dictionary**.

The names `args` and `kwargs` are conventions; the actual operators are the single (`*`) and double (`**`) asterisks.

### Example Code
```python
def print_details(*args, **kwargs):
    print("args:", args, type(args))
    print("kwargs:", kwargs, type(kwargs))

print_details(1, 2, "three", apple=1.5, banana=0.8)
# Output:
# args: (1, 2, 'three') <class 'tuple'>
# kwargs: {'apple': 1.5, 'banana': 0.8} <class 'dict'>

# Unpacking elements
nums = [1, 2, 3]
# Passing elements of lists as separate positional arguments
print(*nums) # Equivalent to print(1, 2, 3)
```

### How to Say It in an Interview
> *"The `*args` and `**kwargs` parameters make Python functions highly flexible by allowing them to accept a variable number of arguments. The single asterisk `*args` captures excess positional arguments into a **tuple**, while the double asterisk `**kwargs` captures excess keyword arguments into a **dictionary**. They are frequently used when writing decorators, or when inheriting classes where you want to forward arguments to the parent class constructor via `super()`."*

---

## 10. Lambda Functions, and `map()` / `filter()` / `reduce()`

### Core Concept
*   **Lambda Function**: A small, anonymous (unnamed) function restricted to a single expression. It implicitly returns the value of that expression.
*   **`map(func, iterable)`**: Applies `func` to all elements of the iterable and returns an iterator.
*   **`filter(func, iterable)`**: Evaluates `func(item)` for each item. Retains items where the result is truthy, returning an iterator.
*   **`reduce(func, iterable)`**: (From `functools`) Applies `func` cumulatively to items, reducing the sequence to a single value.

### Example Code
```python
from functools import reduce

nums = [1, 2, 3, 4, 5]

# Lambda for squaring
squared = list(map(lambda x: x**2, nums))
print(squared)  # [1, 4, 9, 16, 25]

# Lambda for filtering evens
evens = list(filter(lambda x: x % 2 == 0, nums))
print(evens)    # [2, 4]

# Reduce for summing all elements
total_sum = reduce(lambda x, y: x + y, nums)
print(total_sum)  # 15
```

### How to Say It in an Interview
> *"A **lambda** is a one-line anonymous function defined using the `lambda` keyword. It is useful for short, throwaway operations. **`map`** applies a function to every item in an iterable, **`filter`** filters elements based on a condition, and **`reduce`** collapses an iterable into a single cumulative value. 
> 
> *Note:* In modern Python, we often prefer **list comprehensions** over `map` and `filter` because they are generally more readable and performant."*

---

## 11. List Comprehensions vs. Generator Expressions

### Core Concept
*   **List Comprehensions**: Enclosed in square brackets `[...]`. They evaluate the entire loop immediately and load the resulting list fully into memory.
*   **Generator Expressions**: Enclosed in parentheses `(...)`. They return a generator object that evaluates lazily—meaning values are produced one-at-a-time on-demand (using `next()` or a loop) without holding the entire dataset in memory.

### Example Code
```python
import sys

# List Comprehension (Eager)
list_comp = [x**2 for x in range(10000)]
print(type(list_comp))         # <class 'list'>
print(sys.getsizeof(list_comp)) # E.g., ~85176 bytes

# Generator Expression (Lazy)
gen_exp = (x**2 for x in range(10000))
print(type(gen_exp))           # <class 'generator'>
print(sys.getsizeof(gen_exp))   # E.g., ~112 bytes (constant memory size)
```

### How to Say It in an Interview
> *"The primary difference is **memory efficiency** and **evaluation timing**. A **list comprehension** executes immediately and creates the entire list in memory, which is faster if you need to access all elements repeatedly. A **generator expression** evaluates lazily, generating items one at a time on demand. This consumes constant $O(1)$ memory regardless of dataset size, making generators ideal for processing extremely large datasets or infinite streams."*

---

## 12. Iterator vs. Generator, and the `yield` Keyword

### Core Concept
*   **Iterator**: An object that implements the **Iterator Protocol** by defining two methods:
    1.  `__iter__()` which returns the iterator object itself.
    2.  `__next__()` which returns the next element, raising `StopIteration` when elements are exhausted.
*   **Generator**: A simpler way to create iterators. It is a function that contains one or more `yield` statements.
*   **`yield`**: Pauses the function, saves its entire state (local variables, execution line), and sends a value back to the caller. When `next()` is called again, execution resumes immediately after the `yield`.

### Example Code
```python
# Custom Iterator
class Counter:
    def __init__(self, limit):
        self.limit = limit
        self.current = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.current < self.limit:
            self.current += 1
            return self.current
            # StopIteration signals loop termination
        raise StopIteration

# Generator (Implements the iterator protocol automatically)
def gen_counter(limit):
    current = 1
    while current <= limit:
        yield current  # Execution pauses here
        current += 1

# Testing generator
g = gen_counter(3)
print(next(g))  # 1
print(next(g))  # 2
print(next(g))  # 3
# print(next(g)) -> Raises StopIteration
```

### How to Say It in an Interview
> *"All generators are iterators, but not all iterators are generators. An **iterator** is any object that conforms to the iterator protocol by implementing `__iter__` and `__next__`. Writing custom iterators requires boilerplate code.
> 
> A **generator** is a cleaner way to write iterators using functions and the **`yield`** keyword. When Python encounters `yield`, it pauses the function's stack frame, saves its state, and returns the yielded value. When called again, it resumes right where it left off. They are memory efficient because they compute values lazily, only when requested."*

---

## 13. Variable Scope and the LEGB Rule

### Core Concept
The **LEGB rule** defines the sequence in which Python searches for variables:
1.  **L (Local)**: Inside the current function (or lambda).
2.  **E (Enclosing)**: In any enclosing (outer) helper functions (from inside-out).
3.  **G (Global)**: At the module level (top-level of the `.py` file).
4.  **B (Built-in)**: Pre-loaded names (like `len`, `range`, `ValueError`).

If a variable is not found in any scope, Python raises a `NameError`.
Use `global` or `nonlocal` keywords to write to variables in outer scopes.

### Example Code
```python
x = "Global x"  # Global Scope

def outer_func():
    x = "Enclosing x"  # Enclosing Scope
    
    def inner_func():
        x = "Local x"  # Local Scope
        print(x)      # Looks at Local -> "Local x"
        print(len(x)) # Looks at Local -> Enclosing -> Global -> Built-in (len) -> 7
        
    inner_func()

outer_func()

# Writing to outer scopes
counter = 0

def increment():
    global counter
    counter += 1  # Modifies the global variable
```

### How to Say It in an Interview
> *"Python resolves variable names using the **LEGB rule**, which stands for **Local**, **Enclosing**, **Global**, and **Built-in**. When resolving a variable name, Python checks the scopes in that exact order. If you need to modify a variable in the global scope from within a function, you must declare it with the `global` keyword. If you need to modify a variable in a nested outer function, you use the `nonlocal` keyword."*

---

## 14. PEP 8, Keywords, Identifiers, and Core Data Types

### Core Concept
*   **PEP 8**: Python's style guide. Key rules:
    *   4-space indentation (no tabs).
    *   `snake_case` for functions/variables, `PascalCase` for classes, `UPPER_CASE` for constants.
    *   Line length limit of 79 characters.
    *   Imports at the top of the file, grouped (standard library, third-party, local).
*   **Keywords**: Reserved words (e.g., `def`, `class`, `import`, `with`, `yield`) that cannot be used as variable names.
*   **Identifiers**: Custom names given to variables, functions, classes, etc. Must start with a letter or underscore, and contain only alphanumeric characters and underscores.

### Example Code
```python
# PEP 8 Compliant Code
import os  # Standard library

CONSTANT_VAL = 42  # Constant

class DatabaseConnector:  # PascalCase class name
    def __init__(self, db_url):
        self.db_url = db_url  # snake_case attribute

    def connect_to_db(self):  # snake_case function
        pass
```

### How to Say It in an Interview
> *"**PEP 8** is Python's official style guide. Adhering to it ensures code consistency and readability. Key guidelines include using 4 spaces for indentation, naming functions in `snake_case` and classes in `PascalCase`, and keeping lines under 79 characters. **Keywords** are Python's reserved syntax words, while **identifiers** are user-defined names. Most production teams enforce PEP 8 using linters and formatters like `flake8` or `black` in their CI/CD pipelines."*

---

## 15. `sort()` vs. `sorted()`; Slicing & Negative Indexing

### Core Concept
*   **`list.sort()`**: Sorts the list **in-place** (mutates the original list). Returns `None`. It is a method exclusive to lists.
*   **`sorted(iterable)`**: Returns a **new** sorted list from any iterable (strings, tuples, sets, dict keys). The original collection is untouched.
*   *Algorithm*: Both use **Timsort** (an adaptive, stable sorting algorithm with time complexity $O(n \log n)$).
*   **Slicing**: Syntax is `sequence[start:stop:step]`.
*   **Negative Indexing**: Starts from the end: `-1` is the last item, `-2` is second to last.

### Example Code
```python
# sort vs sorted
nums1 = [3, 1, 2]
nums2 = [3, 1, 2]

print(sorted(nums2))  # Returns [1, 2, 3]
print(nums2)          # Original remains [3, 1, 2]

nums1.sort()
print(nums1)          # Original is now mutated to [1, 2, 3]

# Slicing and Negative Indexing
s = "Python"
print(s[-1])     # 'n' (last character)
print(s[0:4])    # 'Pyth' (indices 0, 1, 2, 3)
print(s[::-1])   # 'nohtyP' (reversed string using step=-1)
```

### How to Say It in an Interview
> *"The difference between `sort` and `sorted` is that **`sort()`** modifies a list in-place and returns `None`, whereas the built-in **`sorted()`** function accepts any iterable and returns a brand-new sorted list, preserving the original data. Both use **Timsort**, which is highly efficient. 
> 
> For **slicing**, Python uses the `[start:stop:step]` syntax. **Negative indexing** allows us to access elements relative to the end of a sequence (where `-1` represents the last item), which eliminates the need to calculate the sequence's length manually."*

---

## 16. Splitting Strings, Joining, `find()` vs. `index()`, `replace()` vs. `translate()`

### Core Concept
*   **`split(sep)`**: Splits a string into a list of substrings based on a delimiter.
*   **`join(iterable)`**: Concatenates a collection of strings using the base string as the delimiter. (Much faster than `+` operations due to string immutability).
*   **`find(sub)` vs. `index(sub)`**: Both search for a substring. If not found, `find` returns `-1`, whereas `index` raises a `ValueError`. (`find` only exists for strings; lists only support `index`).
*   **`replace(old, new)` vs. `translate(table)`**: `replace` swaps all occurrences of one string with another. `translate` executes multiple single-character replacements simultaneously using a translation mapping (created with `str.maketrans()`), which is faster for character-level transformations.

### Example Code
```python
# split and join
words = "apple,banana,cherry".split(",")
print(words)                  # ['apple', 'banana', 'cherry']
print("-".join(words))        # 'apple-banana-cherry'

# find vs index
text = "Hello World"
print(text.find("z"))         # -1
# print(text.index("z"))      # Raises ValueError

# replace vs translate
msg = "hello google"
print(msg.replace("g", "q"))  # "hello qooqle"

# translate (fast character swaps)
trans_table = str.maketrans("abc", "123")  # a->1, b->2, c->3
print("abc cab".translate(trans_table))     # "123 312"
```

### How to Say It in an Interview
> *"For string operations, **`split`** breaks strings apart, while **`join`** is the standard, memory-efficient way to merge an iterable of strings. 
> 
> When searching for substrings, **`find()`** returns `-1` on failure, which is safer for conditional statements, while **`index()`** raises a `ValueError` which is useful if you want to handle failures explicitly.
> 
> Finally, **`replace`** is used for substituting substrings, whereas **`translate`** is ideal for character-by-character replacements. `translate` is much faster when doing multiple character substitutions because it performs all mappings in a single pass using a translation table."*
