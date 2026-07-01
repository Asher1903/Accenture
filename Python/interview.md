# Python Fundamentals: Interview Verbal Scripts

This document compiles optimized, professional verbal answers to each of the 16 core Python questions from the slide. Use these scripts to practice speaking clearly, structuring your answers logically, and using high-value technical terms.

---

## 1. Why is Python called an interpreted language?
> *"Python is technically a hybrid compiled/interpreted language. When a script runs, Python first compiles the source code into an intermediate format called **bytecode**. This bytecode is then executed line-by-line by the **Python Virtual Machine (PVM)**, which is the interpreter. We call Python 'interpreted' because execution is performed by this virtual machine at runtime, providing platform independence at the cost of some execution speed compared to ahead-of-time compiled languages like C++."*

---

## 2. Mutable vs. Immutable Objects
> *"In Python, every variable points to an object. Objects are either mutable or immutable. **Mutable objects**, like lists, dicts, and sets, can be modified in-place without changing their memory address. **Immutable objects**, like strings, tuples, and numbers, cannot be changed. If you try to modify them, Python creates a new object in memory. A key practical difference is that immutable objects are **hashable** (if they contain only hashable values), meaning they can be used as dictionary keys or set elements, whereas mutable objects cannot."*

---

## 3. List vs. Tuple vs. Set vs. Dictionary
> *"Choosing the right collection depends on ordering, mutability, and lookup speed:
> 1. Use a **List** when sequence order is important and the data needs to change.
> 2. Use a **Tuple** for structured, read-only data, which is more memory-efficient and can act as dict keys.
> 3. Use a **Set** for storing unique elements and performing fast $O(1)$ membership checks or set operations.
> 4. Use a **Dictionary** when you need to associate keys with values for $O(1)$ lookups."*

---

## 4. `append()` vs. `extend()` vs. `insert()`
> *"**`append`** adds its argument to the end of the list as a single object. If you append a list, you get a nested list. **`extend`** iterates over its argument and adds each element individually, effectively merging the collections. **`insert`** places an element at a specific index. Performance-wise, `append` is very fast at $O(1)$ amortized time, whereas `insert` is $O(n)$ because it requires shifting all subsequent elements in memory."*

---

## 5. `remove()` vs. `pop()` vs. `del` vs. `clear()`
> *"The main differences lie in parameters, return values, and errors:
> * Use **`remove`** when you know the **value** you want to delete; it returns nothing and raises a `ValueError` if the value isn't there.
> * Use **`pop`** when you need the **index** and want to **retrieve** the removed value; it raises an `IndexError` on invalid indices.
> * **`del`** is a statement that deletes references (including slices) and doesn't return anything.
> * **`clear`** empties the entire list while maintaining the list reference."*

---

## 6. `is` vs. `==` (Identity vs. Equality)
> *"The **`==`** operator checks for **equality**, checking if the values or contents of two objects are the same. The **`is`** operator checks for **identity**, verifying if both variables point to the exact same object in memory. In practice, `is` should be used for comparing with singletons like `None` (e.g., `if val is None:`), while `==` should be used for comparing values."*

---

## 7. Deep Copy vs. Shallow Copy
> *"A **shallow copy** constructs a new compound object but fills it with references to the nested objects inside the original. Therefore, changes to nested mutable elements are reflected in both copies. A **deep copy** recursively copies everything, constructing a completely independent object. We use the `copy` module in Python to achieve this, where `copy.copy()` is shallow and `copy.deepcopy()` is deep."*

---

## 8. Python Memory Management, Reference Counting, & Garbage Collection
> *"Python manages memory using a private heap. It relies primarily on **Reference Counting**, where every object tracks its references; once an object's reference count hits zero, it is instantly deallocated. However, reference counting fails to handle **reference cycles** (where objects reference each other but are unreachable). To solve this, Python has a built-in **Generational Garbage Collector** that runs periodically in the background, identifying cycles and cleaning up orphaned objects."*

---

## 9. `*args` and `**kwargs`
> *"The `*args` and `**kwargs` parameters make Python functions highly flexible by allowing them to accept a variable number of arguments. The single asterisk `*args` captures excess positional arguments into a **tuple**, while the double asterisk `**kwargs` captures excess keyword arguments into a **dictionary**. They are frequently used when writing decorators, or when inheriting classes where you want to forward arguments to the parent class constructor via `super()`."*

---

## 10. Lambda Functions, and `map()` / `filter()` / `reduce()`
> *"A **lambda** is a one-line anonymous function defined using the `lambda` keyword. It is useful for short, throwaway operations. **`map`** applies a function to every item in an iterable, **`filter`** filters elements based on a condition, and **`reduce`** collapses an iterable into a single cumulative value. 
> 
> *Note:* In modern Python, we often prefer **list comprehensions** over `map` and `filter` because they are generally more readable and performant."*

---

## 11. List Comprehensions vs. Generator Expressions
> *"The primary difference is **memory efficiency** and **evaluation timing**. A **list comprehension** executes immediately and creates the entire list in memory, which is faster if you need to access all elements repeatedly. A **generator expression** evaluates lazily, generating items one at a time on demand. This consumes constant $O(1)$ memory regardless of dataset size, making generators ideal for processing extremely large datasets or infinite streams."*

---

## 12. Iterator vs. Generator, and the `yield` Keyword
> *"All generators are iterators, but not all iterators are generators. An **iterator** is any object that conforms to the iterator protocol by implementing `__iter__` and `__next__`. Writing custom iterators requires boilerplate code.
> 
> A **generator** is a cleaner way to write iterators using functions and the **`yield`** keyword. When Python encounters `yield`, it pauses the function's stack frame, saves its state, and returns the yielded value. When called again, it resumes right where it left off. They are memory efficient because they compute values lazily, only when requested."*

---

## 13. Variable Scope and the LEGB Rule
> *"Python resolves variable names using the **LEGB rule**, which stands for **Local**, **Enclosing**, **Global**, and **Built-in**. When resolving a variable name, Python checks the scopes in that exact order. If you need to modify a variable in the global scope from within a function, you must declare it with the `global` keyword. If you need to modify a variable in a nested outer function, you use the `nonlocal` keyword."*

---

## 14. PEP 8, Keywords, Identifiers, and Core Data Types
> *"**PEP 8** is Python's official style guide. Adhering to it ensures code consistency and readability. Key guidelines include using 4 spaces for indentation, naming functions in `snake_case` and classes in `PascalCase`, and keeping lines under 79 characters. **Keywords** are Python's reserved syntax words, while **identifiers** are user-defined names. Most production teams enforce PEP 8 using linters and formatters like `flake8` or `black` in their CI/CD pipelines."*

---

## 15. `sort()` vs. `sorted()`; Slicing & Negative Indexing
> *"The difference between `sort` and `sorted` is that **`sort()`** modifies a list in-place and returns `None`, whereas the built-in **`sorted()`** function accepts any iterable and returns a brand-new sorted list, preserving the original data. Both use **Timsort**, which is highly efficient. 
> 
> For **slicing**, Python uses the `[start:stop:step]` syntax. **Negative indexing** allows us to access elements relative to the end of a sequence (where `-1` represents the last item), which eliminates the need to calculate the sequence's length manually."*

---

## 16. Splitting Strings, Joining, `find()` vs. `index()`, `replace()` vs. `translate()`
> *"For string operations, **`split`** breaks strings apart, while **`join`** is the standard, memory-efficient way to merge an iterable of strings. 
> 
> When searching for substrings, **`find()`** returns `-1` on failure, which is safer for conditional statements, while **`index()`** raises a `ValueError` which is useful if you want to handle failures explicitly.
> 
> Finally, **`replace`** is used for substituting substrings, whereas **`translate`** is ideal for character-by-character replacements. `translate` is much faster when doing multiple character substitutions because it performs all mappings in a single pass using a translation table."*
