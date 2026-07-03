# Accenture Confirmed Interview Questions

This document compiles the **most frequently asked ("confirmly asked")** coding and technical interview questions for the **Custom Software Engineering Associate / Associate Software Engineer** role at Accenture, focusing on Python.

---

## PART 1: Confirmed Online Coding Assessment Questions

In the online round, you will get **2-3 coding problems** to solve in **45-60 minutes**. The compiler verifies your code against hidden test cases (including edge cases like `None` or empty lists).

### Question 1: Rat Count House
*   **Problem Statement:** You are given the number of rats `r`, the food units each rat consumes `unit`, and an array `arr` containing the food amount available in each house (where index + 1 is the house number). Find the minimum number of houses required to provide sufficient food for all rats.
*   **Constraints/Rules:**
    *   Return `-1` if the array is null or empty.
    *   Return `0` if the total food across all houses is less than what is required.
    *   Otherwise, return the minimum count of houses needed.

```python
def solve_rat_food(r, unit, arr):
    if arr is None or len(arr) == 0:
        return -1
    
    total_food_needed = r * unit
    food_accumulated = 0
    houses_visited = 0
    
    for food in arr:
        food_accumulated += food
        houses_visited += 1
        if food_accumulated >= total_food_needed:
            return houses_visited
            
    return 0

# Test Cases:
# solve_rat_food(7, 2, [2, 8, 3, 5, 7, 4, 1, 2]) -> 4 (Total needed = 14. 2+8+3+5 = 18 >= 14)
# solve_rat_food(3, 5, [1, 2, 3]) -> 0 (Total needed = 15. Total available = 6)
```

---

### Question 2: Password Checker
*   **Problem Statement:** Write a function that checks if a string is a valid password.
*   **Validation Rules:**
    1.  At least 4 characters long.
    2.  Must contain at least 1 numeric digit (`0-9`).
    3.  Must contain at least 1 uppercase letter (`A-Z`).
    4.  Must not contain any space (` `) or slash (`/`).
    5.  The first character must not be a digit.
*   **Return:** `1` if valid, `0` otherwise.

```python
def check_password(s):
    if s is None or len(s) < 4:
        return 0
    
    # First character check
    if s[0].isdigit():
        return 0
    
    has_digit = False
    has_upper = False
    
    for char in s:
        if char == ' ' or char == '/':
            return 0  # Forbidden characters
        if char.isdigit():
            has_digit = True
        if char.isupper():
            has_upper = True
            
    return 1 if (has_digit and has_upper) else 0

# Test Cases:
# check_password("aA1_") -> 1
# check_password("1aA_") -> 0 (Starts with digit)
# check_password("aA 1") -> 0 (Contains space)
```

---

### Question 3: Move Hyphens to Front
*   **Problem Statement:** Given a string containing alphanumeric characters and hyphens (`-`), move all hyphens to the beginning of the string while maintaining the relative order of all other characters.
*   **Return:** The modified string. If the input is null, return `None`.

```python
def move_hyphen_to_front(s):
    if s is None:
        return None
        
    hyphen_count = s.count('-')
    # Filter out hyphens while maintaining original order of other characters
    non_hyphens = [char for char in s if char != '-']
    
    return ('-' * hyphen_count) + "".join(non_hyphens)

# Test Cases:
# move_hyphen_to_front("Move-Hyphens-To-Front") -> "---MoveHyphensToFront"
# move_hyphen_to_front("StringWithoutHyphens") -> "StringWithoutHyphens"
```

---

### Question 4: Autobiographical Numbers
*   **Problem Statement:** An autobiographical number is a number where each digit at index `i` counts the number of occurrences of the digit `i` within the entire number.
*   **Requirement:** Given a string representation of a number, determine if it is autobiographical. If it is, return the number of distinct digits present. If not, return `0`.

```python
def find_auto_count(s):
    if s is None or len(s) == 0:
        return 0
        
    # Check autobiographical property
    for i in range(len(s)):
        expected_count = int(s[i])
        actual_count = s.count(str(i))
        if expected_count != actual_count:
            return 0
            
    # If valid, return number of unique digits
    return len(set(s))

# Test Cases:
# find_auto_count("1210") -> 3 (Digits: '1', '2', '0'. '1' zero, '2' ones, '1' two, '0' threes)
# find_auto_count("2020") -> 2 (Digits: '2', '0'. '2' zeros, '0' ones, '2' twos, '0' threes)
# find_auto_count("1234") -> 0 (Not autobiographical)
```

---

## PART 2: Confirmed Technical Interview Questions (Q&A)

During the technical interview round, the interviewer will discuss your coding logic, check your depth of knowledge in Python, databases, and your projects.

### Q1: What is Method Resolution Order (MRO) in Python, and how does it work with Multiple Inheritance?
*   **The Answer:** MRO is the order in which Python searches for a method or attribute in a class hierarchy when multiple inheritance is involved. Python uses the **C3 Linearization Algorithm** to construct this search path.
*   **Key points to mention:**
    *   You can view a class's MRO using the `.mro()` method or the `__mro__` attribute.
    *   It prevents problems like the **Diamond Problem** (where a child inherits from two parent classes that both inherit from a single grandparent).
*   **Example:**
    ```python
    class A:
        def show(self): print("A")
    class B(A):
        def show(self): print("B")
    class C(A):
        def show(self): print("C")
    class D(B, C):
        pass

    # MRO of D will be: D -> B -> C -> A -> object
    print(D.__mro__)
    ```

---

### Q2: What is the difference between Local, Global, and Nonlocal variables in Python?
*   **Local Variables:** Defined inside a function and only accessible within that function.
*   **Global Variables:** Defined outside all functions or explicitly declared using the `global` keyword. Accessible throughout the entire file.
*   **Nonlocal Variables:** Used inside nested functions to reference variables defined in the outer (enclosing) function, using the `nonlocal` keyword.
*   **Example:**
    ```python
    def outer():
        x = "local to outer"
        def inner():
            nonlocal x
            x = "modified by inner"
        inner()
        print(x) # Prints: "modified by inner"
    ```

---

### Q3: How do you handle database transactions, and what are ACID properties?
*   **The Answer:** A transaction is a single logical unit of database work.
*   **ACID Properties:**
    *   **Atomicity:** All operations in a transaction succeed, or the entire transaction is rolled back (All-or-Nothing).
    *   **Consistency:** The database transitions from one valid state to another, maintaining all constraints.
    *   **Isolation:** Concurrent execution of transactions yields the same state as if they were executed sequentially.
    *   **Durability:** Once a transaction is committed, it remains committed even in the event of a system crash.

---

### Q4: Write an SQL query to retrieve the names of employees who earn more than their managers.
*   **Table Structure:** `Employee (Emp_ID, Name, Salary, Manager_ID)`
*   **Solution (Self-Join):**
    ```sql
    SELECT e.Name 
    FROM Employee e
    INNER JOIN Employee m ON e.Manager_ID = m.Emp_ID
    WHERE e.Salary > m.Salary;
    ```

---

### Q5: How would you explain your final-year project to a non-technical interviewer?
*   **Strategy:** Focus on the **business problem** and the **value delivered** rather than purely technical terms.
*   **Framework:**
    1.  **The Hook (Problem):** "In our daily lives, we see X problem happening, which costs businesses Y amount of time/money..."
    2.  **The Solution (Action):** "To solve this, I designed a software system using Python that automates X..."
    3.  **The Impact (Result):** "This system allowed users to do X twice as fast, reducing overall manual effort."
