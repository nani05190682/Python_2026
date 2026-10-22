# Try and Except in Python
## Catch Errors Before They Crash Your Program

### 1. What are `try` and `except`?

When you write a Python program, some operations can fail. A file may not exist, a user may enter invalid input, or a calculation may encounter an unexpected value.

Python provides `try` and `except` to handle these situations.

- **`try`** contains code that might raise an exception.
- **`except`** contains code that handles a matching exception.

Instead of allowing an expected error to interrupt your program, you can respond with a useful message or take another action.

### 2. Basic try-except structure

The basic syntax looks like this:

```python
try:
    # Code that might raise an exception
    risky_operation()

except SomeException:
    # Handle the specified exception
    print("Something went wrong.")
```

`SomeException` is a placeholder for a real exception type, such as `ValueError` or `FileNotFoundError`.

Let's start with a simple example:

```python
try:
    number = int("abc")
    print(number)

except ValueError:
    print("The text cannot be converted into an integer.")

print("Program continues.")
```

Output:

```text
The text cannot be converted into an integer.
Program continues.
```

**How does it work?**

1. Python attempts to execute the code inside `try`.
2. `int("abc")` raises a `ValueError`.
3. Python skips the remaining statements in the `try` block.
4. The matching `except` block runs.
5. The program continues after the exception-handling structure.

Notice that `print(number)` is not executed because the conversion failed before `number` was assigned.

### 3. Catch specific exceptions

Different problems require different responses. It is better to catch the exception you expect instead of catching every possible error.

Consider this example:

```python
try:
    age = int(input("Enter your age: "))
    print(f"In 10 years, you'll be {age + 10}.")

except ValueError:
    print("Please enter a valid whole number.")
```

Example 1:

```text
Enter your age: 25
In 10 years, you'll be 35.
```

Example 2:

```text
Enter your age: abc
Please enter a valid whole number.
```

The `int()` function raises `ValueError` when the input is not a valid integer representation.

This is useful when accepting user input, reading configuration values, or processing data from external systems.

### 4. Handle multiple exceptions

A program can encounter different types of errors in the same workflow. Python allows you to use multiple `except` blocks.

Imagine you need to read a number from a file and divide 100 by that number.

Create a file named `number.txt` containing:

```text
5
```

Now write the Python program:

```python
try:
    with open("number.txt", "r", encoding="utf-8") as file:
        text = file.read()

    number = int(text)
    result = 100 / number

    print(f"Result: {result}")

except FileNotFoundError:
    print("Could not find number.txt.")

except ValueError:
    print("The file does not contain a valid integer.")

except ZeroDivisionError:
    print("Cannot divide by zero.")
```

If the file contains `5`, the output is:

```text
Result: 20.0
```

If the file does not exist:

```text
Could not find number.txt.
```

If the file contains `hello`:

```text
The file does not contain a valid integer.
```

If the file contains `0`:

```text
Cannot divide by zero.
```

Each exception handler addresses a different problem, making the program easier to understand and troubleshoot.

### 5. Understand the `else` clause

Python's `else` clause runs only when the `try` block completes without raising an exception.

Consider this example:

```python
try:
    with open("data.txt", "r", encoding="utf-8") as file:
        data = file.read()

except FileNotFoundError:
    print("File not found.")

else:
    print(f"File has {len(data)} characters.")
```

If `data.txt` exists and is read successfully, the `else` block displays the character count.

If the file is missing, the `except` block handles the problem, and the `else` block is skipped.

**Why use `else`?**

It separates successful processing from error handling. This makes your code clearer when several operations depend on an earlier operation succeeding.

### 6. Understand the `finally` clause

The `finally` block runs whether the `try` block succeeds or raises an exception, provided normal Python execution reaches that point.

```python
try:
    number = int("abc")

except ValueError:
    print("Invalid number.")

finally:
    print("Operation completed.")
```

Output:

```text
Invalid number.
Operation completed.
```

The `finally` clause is commonly used for cleanup, such as releasing resources or closing manually managed connections.

For example, when you manage a file manually:

```python
file = None

try:
    file = open("data.txt", "r", encoding="utf-8")
    data = file.read()
    print(data)

except FileNotFoundError:
    print("File not found.")

finally:
    if file is not None:
        file.close()

    print("Cleanup completed.")
```

However, Python offers a simpler and safer approach for ordinary file operations: use `with open(...)`. The file is closed automatically when the `with` block exits, even if an exception occurs.

```python
try:
    with open("data.txt", "r", encoding="utf-8") as file:
        data = file.read()

except FileNotFoundError:
    print("File not found.")

else:
    print(data)
```

Use `finally` when you need cleanup that is not already handled by a context manager.

### 7. Understand the complete structure

You can combine `try`, `except`, `else`, and `finally` in one statement.

```python
try:
    number = int(input("Enter a number: "))
    result = 100 / number

except ValueError:
    print("Please enter a valid integer.")

except ZeroDivisionError:
    print("The number cannot be zero.")

else:
    print(f"Result: {result}")

finally:
    print("Calculation attempt finished.")
```

The execution order depends on what happens:

| Situation | What runs |
|---|---|
| Valid, nonzero integer | `try`, `else`, `finally` |
| Invalid integer | `try`, matching `except`, `finally` |
| Zero | `try`, matching `except`, `finally` |

The `else` block runs only when the `try` block completes without an exception. The `finally` block runs afterward.

### 8. Avoid catching every exception

You may see this pattern:

```python
try:
    result = 10 / 0

except:
    print("Something went wrong.")
```

This is called a **bare `except`**. It catches a broad range of exceptions, including exceptions that normally should not be swallowed, such as `KeyboardInterrupt`.

It can also hide the actual cause of a programming problem.

Prefer:

```python
try:
    result = 10 / 0

except ZeroDivisionError:
    print("Cannot divide by zero.")
```

Also avoid empty exception handlers:

```python
try:
    process_data()

except Exception:
    pass
```

This silently discards the error and makes debugging difficult.

If you catch an exception, handle it meaningfully, log it, or re-raise it when the current function cannot recover.

### 9. Use `raise` when you cannot recover

Sometimes a function catches an exception only to add context before passing the problem to its caller.

```python
def load_number(filename):
    try:
        with open(filename, "r", encoding="utf-8") as file:
            return int(file.read().strip())

    except FileNotFoundError as error:
        raise FileNotFoundError(
            f"Required number file is missing: {filename}"
        ) from error
```

The `raise ... from error` syntax preserves the original exception as the cause.

You can also use `raise` by itself inside an exception handler to re-raise the original exception:

```python
try:
    result = 10 / 0

except ZeroDivisionError:
    print("Recording the calculation failure.")
    raise
```

In this example, the exception is not suppressed. It continues up the call stack after the message is printed.

### 10. Practice exercises

**Exercise 1: Convert input**

Ask the user to enter a number. Handle invalid input using `ValueError`.

**Exercise 2: Safe division**

Ask for two numbers and divide the first by the second. Handle invalid input and division by zero separately.

**Exercise 3: Read a file**

Read `data.txt`. If the file is missing, display a helpful message. If the read succeeds, print its contents in an `else` block.

**Exercise 4: Read a number from a file**

Read `number.txt`, convert its contents to an integer, and divide 100 by the result. Handle `FileNotFoundError`, `ValueError`, and `ZeroDivisionError`.

**Exercise 5: Use `finally`**

Write a program that asks the user for an integer and always displays `Operation completed` at the end.

### 11. Sample solution: Safe division

```python
try:
    first = float(input("Enter the first number: "))
    second = float(input("Enter the second number: "))

    result = first / second

except ValueError:
    print("Invalid input. Please enter numbers.")

except ZeroDivisionError:
    print("The second number cannot be zero.")

else:
    print(f"Result: {result}")

finally:
    print("Operation completed.")
```

This program handles invalid numeric input and division by zero separately. When both values are valid and the divisor is nonzero, it displays the result.

### 12. Lesson summary

In this lesson, you learned:

- How `try` and `except` work.
- Why catching specific exceptions is better than catching everything.
- How to handle multiple exceptions separately.
- How to use `else` for successful execution.
- How to use `finally` for cleanup.
- How to re-raise exceptions using `raise`.
- How to handle common file and input errors.

**Key takeaway:** Put potentially failing operations inside `try`, catch exceptions you know how to handle, and provide a useful recovery or error message. Good exception handling makes your programs more reliable without hiding real problems.

**Next lesson: Common Python Errors — Understand and Fix the Errors You Encounter Most Often.**
