# Common Python Errors — Understand Error Types

## 1. Introduction

When you write Python programs, you will sometimes encounter errors. These errors are a normal part of programming, and learning to understand them will save you time when debugging your code.

Python errors help you identify:
- **What went wrong** — the type of error.
- **Where it happened** — the file and line number.
- **Why it happened** — the error message.

In this lesson, you will learn six common Python errors, how to fix them, how to read error messages, and how to avoid common coding mistakes.

## 2. FileNotFoundError

### What is FileNotFoundError?

Python raises `FileNotFoundError` when you try to open a file that cannot be found at the specified path.

**Example:**

```python
with open("missing.txt", "r") as file:
    content = file.read()

print(content)
```

If `missing.txt` does not exist in the current working directory, Python raises an error similar to:

```text
FileNotFoundError: [Errno 2] No such file or directory: 'missing.txt'
```

### How to fix it

**Method 1: Check whether the file exists**

```python
from pathlib import Path

file_path = Path("data.txt")

if file_path.exists() and file_path.is_file():
    content = file_path.read_text(encoding="utf-8")
    print(content)
else:
    print("File not found")
```

**Method 2: Handle the exception**

```python
try:
    with open("data.txt", "r", encoding="utf-8") as file:
        content = file.read()
    print(content)

except FileNotFoundError:
    print("The requested file does not exist.")
```

**When to use it:** When reading configuration files, CSV datasets, log files, or other files required by your application.

## 3. ValueError

### What is ValueError?

Python raises `ValueError` when a function receives a value of an appropriate general type but cannot process that value.

**Example:**

```python
int("hello")     # Cannot convert this text to an integer
int("12.5")      # This text is not a valid integer representation
```

Both statements raise `ValueError`.

Another example:

```python
numbers = [10, 20, 30]
numbers.remove(50)
```

This raises `ValueError` because `50` is not present in the list.

### How to fix it

**Example 1: Validate user input**

```python
try:
    age = int(input("Enter your age: "))
    print(f"Your age is {age}")

except ValueError:
    print("Please enter a valid whole number.")
```

**Example 2: Convert decimal text carefully**

```python
value = "12.5"

number = float(value)

print(number)
```

Output:

```text
12.5
```

If you need an integer, you can explicitly convert the floating-point value:

```python
number = int(float("12.5"))
print(number)
```

Output:

```text
12
```

Note that this conversion truncates the decimal part; it does not round to the nearest integer.

**When to use it:** When converting user input, parsing numerical values, or validating data received from an API.

## 4. KeyError

### What is KeyError?

Python raises `KeyError` when you try to access a dictionary key that does not exist.

**Example:**

```python
user = {
    "name": "Alice",
    "age": 25
}

print(user["email"])
```

Error:

```text
KeyError: 'email'
```

The dictionary contains `name` and `age`, but it does not contain `email`.

### How to fix it

**Method 1: Check whether the key exists**

```python
if "email" in user:
    print(user["email"])
else:
    print("Email address not available.")
```

**Method 2: Use `get()` with a default value**

```python
email = user.get("email", "Not provided")

print(email)
```

Output:

```text
Not provided
```

**Method 3: Handle the exception**

```python
try:
    print(user["email"])

except KeyError:
    print("Email key not found.")
```

**When to use it:** When working with JSON responses, API data, configuration dictionaries, or records that may have missing fields.

## 5. IndexError

### What is IndexError?

Python raises `IndexError` when you try to access a sequence position that does not exist.

Sequences include lists, tuples, and strings.

**Example:**

```python
numbers = [10, 20, 30]

print(numbers[5])
```

Error:

```text
IndexError: list index out of range
```

The list has three elements, whose valid indexes are `0`, `1`, and `2`.

### How to fix it

**Method 1: Check the list length**

```python
numbers = [10, 20, 30]
index = 2

if 0 <= index < len(numbers):
    print(numbers[index])
else:
    print("Invalid index.")
```

Output:

```text
30
```

**Method 2: Access the last element safely**

```python
numbers = [10, 20, 30]

last_item = numbers[-1] if numbers else None

print(last_item)
```

Output:

```text
30
```

If the list is empty, `last_item` will be `None`.

**Method 3: Handle the exception**

```python
try:
    print(numbers[5])

except IndexError:
    print("The requested position does not exist.")
```

**When to use it:** When accessing list elements, processing datasets, or retrieving items by position.

## 6. TypeError

### What is TypeError?

Python raises `TypeError` when an operation or function is used with an inappropriate type of object.

**Examples:**

```python
"hello" + 5
```

Error: You cannot directly concatenate a string and an integer.

```python
len(42)
```

Error: An integer does not have a length.

```python
int([1, 2, 3])
```

Error: A list cannot be converted directly into a single integer using `int()`.

### How to fix it

**Method 1: Convert values to compatible types**

```python
message = "hello" + str(5)

print(message)
```

Output:

```text
hello5
```

**Method 2: Check the type**

```python
value = "Python"

if isinstance(value, str):
    print(len(value))
else:
    print("The value is not a string.")
```

Output:

```text
6
```

**Method 3: Use the correct operation**

If you want to add a number to another number:

```python
result = 10 + int("5")

print(result)
```

Output:

```text
15
```

**When to use it:** When combining data from different sources, processing API responses, or passing arguments to functions.

## 7. AttributeError

### What is AttributeError?

Python raises `AttributeError` when an object does not have the attribute or method you are trying to access.

**Example:**

```python
text = "hello"

text.append("!")
```

Error:

```text
AttributeError: 'str' object has no attribute 'append'
```

The `append()` method belongs to lists, not strings.

### How to fix it

Use an operation supported by the object's type.

**For strings:**

```python
text = "hello"

text = text + "!"

print(text)
```

Output:

```text
hello!
```

**For lists:**

```python
items = ["Python", "AI"]

items.append("DevOps")

print(items)
```

Output:

```text
['Python', 'AI', 'DevOps']
```

You can also inspect an object's type:

```python
value = ["Python", "AI"]

print(type(value))
```

Output:

```text
<class 'list'>
```

**When to use it:** When using unfamiliar objects, libraries, API clients, or methods that may not belong to the object you're working with.

---

## 8. Reading Python Error Messages

Python displays a traceback when an unhandled exception stops normal program execution.

Consider this program:

```python
result = 10 / 0
print(result)
```

The traceback looks similar to:

```text
Traceback (most recent call last):
  File "script.py", line 1, in <module>
    result = 10 / 0
ZeroDivisionError: division by zero
```

### How to understand the traceback

Read the traceback from the bottom upward to identify the final error first.

| Part | Meaning |
|---|---|
| `ZeroDivisionError` | The type of error |
| `division by zero` | The explanation |
| `script.py` | The file containing the failing code |
| `line 1` | The line where the exception occurred |
| `result = 10 / 0` | The statement that triggered the error |

**Important:** The last line usually identifies the exception. The lines above it show the execution path that led to the problem.

### How to fix the error

Check the denominator before performing the division:

```python
numerator = 10
denominator = 0

if denominator != 0:
    result = numerator / denominator
    print(result)
else:
    print("Cannot divide by zero.")
```

Output:

```text
Cannot divide by zero.
```

The key debugging habit is to read the full traceback before changing your code.

## 9. Three Common Mistake Patterns

### Mistake 1: Off-by-one errors

An off-by-one error occurs when a loop or index uses a boundary incorrectly.

**Incorrect example:**

```python
numbers = [10, 20, 30]

for index in range(len(numbers) + 1):
    print(numbers[index])
```

The loop eventually tries to access `numbers[3]`, which does not exist.

**Correct example:**

```python
numbers = [10, 20, 30]

for index in range(len(numbers)):
    print(numbers[index])
```

Output:

```text
10
20
30
```

An even simpler approach is:

```python
for number in numbers:
    print(number)
```

### Mistake 2: Modifying a list while iterating over it

Removing elements from a list while iterating over that same list can cause elements to be skipped.

**Problematic example:**

```python
numbers = [1, 2, 3, 4, 5, 6]

for number in numbers:
    if number % 2 == 0:
        numbers.remove(number)

print(numbers)
```

This can leave some even numbers behind because the list's indexes shift as elements are removed.

**Correct example: Use a list comprehension**

```python
numbers = [1, 2, 3, 4, 5, 6]

numbers = [
    number
    for number in numbers
    if number % 2 != 0
]

print(numbers)
```

Output:

```text
[1, 3, 5]
```

### Mistake 3: Mutable default arguments

A mutable default argument, such as a list, is created once when the function is defined and reused across calls.

**Incorrect example:**

```python
def add_item(item, items=[]):
    items.append(item)
    return items

print(add_item("Python"))
print(add_item("AI"))
```

Output:

```text
['Python']
['Python', 'AI']
```

The second call unexpectedly reuses the list created during the first call.

**Correct example: Use `None` as the default**

```python
def add_item(item, items=None):
    if items is None:
        items = []

    items.append(item)
    return items

print(add_item("Python"))
print(add_item("AI"))
```

Output:

```text
['Python']
['AI']
```

Each call now creates its own list when no list is provided.

---

## 10. Quick Reference: Common Python Errors

| Error | Common cause | Typical solution |
|---|---|---|
| `FileNotFoundError` | File or path does not exist | Check the path or handle the exception |
| `ValueError` | Value cannot be processed or converted | Validate the value |
| `KeyError` | Dictionary key is missing | Use `get()` or check the key |
| `IndexError` | Sequence index is out of range | Check the index or sequence length |
| `TypeError` | Operation uses an incompatible type | Check types or convert values |
| `AttributeError` | Object lacks the requested attribute or method | Check the object's type and available methods |
| `ZeroDivisionError` | Division by zero | Validate the denominator |
| `NameError` | Variable or name is not defined | Check spelling and scope |
| `ImportError` | Requested import cannot be completed | Check the module and imported name |
| `ModuleNotFoundError` | Python cannot find the requested module | Check the environment and install the required package if needed |

## 11. Best Practices for Debugging

1. **Read the entire traceback.** Start with the final exception and message.
2. **Check the line number.** Inspect the failing statement and the values used by it.
3. **Inspect variable types.** Use `type()` and `isinstance()` when necessary.
4. **Use specific exceptions.** Catch `FileNotFoundError`, `ValueError`, or other expected exceptions rather than using a broad, unexplained `except`.
5. **Validate external data.** User input, files, and API responses may contain unexpected values.
6. **Use meaningful error messages.** Tell users what went wrong and how to recover.
7. **Avoid hiding errors.** Do not silently ignore exceptions unless that behavior is intentional.
8. **Reproduce the problem with a small example.** Smaller examples are easier to debug.

## 12. Practice Exercises

Try to solve these exercises before checking the solutions.

### Exercise 1: Fix a ValueError

The following code crashes when the user enters non-numeric text. Modify it to handle invalid input.

```python
age = int(input("Enter your age: "))
print(age)
```

### Exercise 2: Fix a KeyError

Access the `email` field safely.

```python
user = {
    "name": "Arun",
    "age": 30
}

print(user["email"])
```

### Exercise 3: Fix an IndexError

Print the last item only if the list is not empty.

```python
servers = ["web-01", "web-02", "db-01"]

print(servers[3])
```

### Exercise 4: Fix a TypeError

Correct the code so that it prints `Total: 150`.

```python
total = 100 + "50"

print(f"Total: {total}")
```

### Exercise 5: Handle a missing file

Write a program that reads `config.txt` and prints its contents. If the file does not exist, print `Configuration file not found.`

## 13. Exercise Solutions

### Solution 1

```python
try:
    age = int(input("Enter your age: "))
    print(age)
except ValueError:
    print("Please enter a valid whole number.")
```

### Solution 2

```python
user = {
    "name": "Arun",
    "age": 30
}

email = user.get("email", "Not provided")

print(email)
```

### Solution 3

```python
servers = ["web-01", "web-02", "db-01"]

if servers:
    print(servers[-1])
else:
    print("No servers available.")
```

### Solution 4

```python
total = 100 + int("50")

print(f"Total: {total}")
```

Output:

```text
Total: 150
```

### Solution 5

```python
try:
    with open("config.txt", "r", encoding="utf-8") as file:
        content = file.read()

    print(content)

except FileNotFoundError:
    print("Configuration file not found.")
```

## 14. Summary

In this lesson, you learned how to identify and fix common Python errors:

- `FileNotFoundError` — a file cannot be found.
- `ValueError` — a value cannot be processed as expected.
- `KeyError` — a dictionary key is missing.
- `IndexError` — a sequence index is invalid.
- `TypeError` — an operation uses an incompatible type.
- `AttributeError` — an object does not provide the requested attribute or method.

You also learned to read tracebacks, avoid common programming mistakes, and debug errors systematically.

**Remember:** Errors are useful feedback. Understanding the error message is usually the first step toward finding the correct solution.

## 15. What's Next?

Next, you will learn about **Python Classes and Objects** — how to organize related data and behavior together using object-oriented programming.
