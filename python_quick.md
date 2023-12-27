Certainly! Below is the consolidated Markdown content of the provided Python code:

```markdown
# Python Cheat Sheet for Coding Assessments

## Basic Syntax and Data Types

```python
# Comments
# Single line comment
""" Multi-line
    comment """

# Variables
x = 5       # Integer
y = 3.14    # Float
name = "Alice"  # String
is_valid = True  # Boolean

# Basic Operations
sum = x + y
difference = x - y
product = x * y
quotient = x / y
floor_div = x // y
remainder = x % y
power = x  y

# Strings
greeting = "Hello"
concatenated = greeting + " " + name
length = len(greeting)
sub = greeting[1:3]  # 'el'
formatted = f"{greeting}, {name}!"

# Lists
numbers = [1, 2, 3, 4, 5]
numbers.append(6)  # Add to end
numbers.insert(0, 0)  # Insert at position
first = numbers[0]  # Access element
numbers[-1]  # Last element
sliced = numbers[2:4]  # Slice list

# Dictionaries
person = {"name": "Alice", "age": 25}
person["name"]  # Access value
person["age"] = 26  # Change value
person["gender"] = "Female"  # Add key-value pair
```

## Control Structures

```python
# If-Else
if x > y:
    print("x is greater")
elif x < y:
    print("y is greater")
else:
    print("x and y are equal")

# Loops
for i in range(5):  # 0 to 4
    print(i)

for num in numbers:
    print(num)

i = 0
while i < 5:
    print(i)
    i += 1
```

## Functions

```python
def greet(name):
    return f"Hello, {name}!"

print(greet("Alice"))

# Lambda Functions
square = lambda x: x * x
print(square(4))
```

## List Comprehensions

```python
squares = [x * x for x in range(10)]
even_squares = [x * x for x in range(10) if x % 2 == 0]
```

## Error Handling

```python
try:
    result = x / 0
except ZeroDivisionError:
    print("Divided by zero!")
finally:
    print("This always executes")
```

## Modules and Imports

```python
import math
print(math.sqrt(16))

from math import sqrt
print(sqrt(16))

import math as m
print(m.sqrt(16))
```

## File I/O

```python
# Reading from a file
with open("file.txt", "r") as file:
    content = file.read()

# Writing to a file
with open("file.txt", "w") as file:
    file.write("Hello, World!")
```

## Classes and Objects

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def greet(self):
        return f"Hello, my name is {self.name}"

alice = Person("Alice", 25)
print(alice.greet())
```

## Common Standard Library Functions

```python
# Math
import math
math.ceil(3.4)  # Ceiling
math.floor(3.4) # Floor
math.sqrt(16)   # Square root

# Random
import random
random.randint(1, 10)  # Random integer between 1 and 10
```

## Advanced Python Features

### Loops

#### For Loops

- Basic For Loop: Iterates over a sequence (like a list, tuple, dictionary, set, or string).

    ```python
    for item in [1, 2, 3, 4, 5]:
        print(item)
    ```

- Range Function: Generates a sequence of numbers.

    ```python
    for i in range(5):  # 0 to 4
        print(i)
    ```

- Enumerate: For getting the index along with the value.

    ```python
    for index, value in enumerate(['a', 'b', 'c']):
        print(index, value)
    ```

- List Comprehension: A concise way to create lists.

    ```python
    squares = [x * x for x in range(10)]
    ```

- Nested Loops: Loop inside a loop.

    ```python
    for x in range(3):
        for y in range(3):
            print(x, y)
    ```

#### While Loops

- Basic While Loop: Repeats as long as a certain

 boolean condition is met.

    ```python
    i = 0
    while i < 5:
        print(i)
        i += 1
    ```

- Infinite Loop: A loop that never ends (be cautious).

    ```python
    while True:
        print("Infinite")
    ```

- Break and Continue: Control the flow of loops.

    ```python
    for i in range(10):
        if i == 5:
            break  # Exit loop
        if i < 3:
            continue  # Skip to next iteration
        print(i)
    ```

### Dictionaries

- Basic Operations: Creating, accessing, and modifying.

    ```python
    person = {"name": "Alice", "age": 25}
    print(person["name"])
    person["age"] = 26
    person["gender"] = "Female"
    ```

- Iterating: Loop through keys, values, or items.

    ```python
    for key in person:
        print(key, person[key])

    for key, value in person.items():
        print(key, value)
    ```

- Dictionary Comprehension: Similar to list comprehensions but for dictionaries.

    ```python
    squares = {x: x*x for x in range(6)}
    ```

- Nested Dictionaries: A dictionary within a dictionary.

    ```python
    family = {
        "Alice": {"age": 25, "job": "Developer"},
        "Bob": {"age": 30, "job": "Designer"}
    }
    ```

- Merging Dictionaries (Python 3.5+):

    ```python
    merged = {dict1, dict2}
    ```

- Unpacking Dictionaries:

    ```python
    def greet(name, age):
        print(f"Hello {name}, you are {age} years old.")

    person_info = {"name": "Alice", "age": 25}
    greet(person_info)
    ```

### Lists

- Basic Operations: Creating, accessing, slicing, and modifying.

    ```python
    numbers = [1, 2, 3, 4, 5]
    numbers[0] = 10
    numbers.append(6)
    numbers.insert(1, 20)
    sliced = numbers[1:4]  # Slicing
    ```

- List Comprehensions: For creating lists in a concise way.

    ```python
    squares = [x * x for x in range(10) if x % 2 == 0]
    ```

- Nested Lists: A list within a list (matrix-like structures).

    ```python
    matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    ```

- List Operations: Concatenation, repetition, and membership.

    ```python
    concatenated = [1, 2, 3] + [4, 5, 6]
    repeated = [1, 2, 3] * 3
    is_present = 1 in [1, 2, 3]  # True
    ```

- List Methods: `append()`, `extend()`, `pop()`, `remove()`, `reverse()`, `sort()`, etc.

    ```python
    numbers.sort()
    numbers.reverse()
    ```

- List Slicing: Accessing parts of the list.

    ```python
    first_three = numbers[:3]
    last_three = numbers[-3:]
    ```

- List Unpacking:

    ```python
    first, *rest = [1, 2, 3, 4, 5]
    ```

### Advanced Python Features

- Generators: Use `( )` instead of `[ ]` for memory-efficient looping.

    ```python
    squares_gen = (x * x for x in range(10))
    ```

- Lambda Functions: Anonymous functions.

    ```python
    multiply = lambda x, y: x * y
    ```

- Map and Filter:

    ```python
    doubled = map(lambda x: x * 2, [1, 2, 3])
    even = filter(lambda x: x % 2 == 0, [1, 2, 3, 4])
    ```

- Decorators: Enhance the functionality of functions.

    ```python
    def decorator(func):
        def wrapper():
            print("Something before function call")
            func()
            print("Something after function call")
        return wrapper

    @decorator
    def say_hello():
        print("Hello")
    ```

- Context Managers: Using `with` statement for resource management.

    ```python
    with open("file.txt", "r") as file:
        content = file.read()
    ```

```

