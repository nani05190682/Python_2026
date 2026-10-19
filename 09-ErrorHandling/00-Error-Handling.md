# Error Handling in Python
## Handle Errors Gracefully

### 1. What is error handling?

Errors are a normal part of programming. A file might not exist, an API might be unavailable, or a user might enter invalid information.

**Error handling** allows your program to respond to these problems gracefully instead of stopping unexpectedly.

Consider a Python application that reads a sales CSV file. What happens if someone deletes the file before the application starts?

Without error handling, Python raises an exception and stops the normal execution of the program. With appropriate error handling, your program can display a useful message, request another file, or use an alternative approach.

Error handling is especially important in AI engineering, where applications interact with APIs, external services, datasets, and AI models that may fail or return unexpected results.

### 2. Where do errors come from?

Errors generally arise from two broad categories.

**Programming mistakes**

- Syntax errors, such as missing colons.
- Logic errors, such as calculating an incorrect result.
- Using a variable before defining it.
- Calling a method that does not exist.
- Passing an argument of the wrong type.

**External problems**

- A file is missing or inaccessible.
- A user enters invalid input.
- An internet connection drops.
- An API returns an unsuccessful response.
- A service responds with unexpected data.
- A file contains missing or malformed values.

Even well-written programs need error handling because external systems and user inputs are not always predictable.

### 3. Understand common types of errors

Python reports different errors depending on the problem.

#### SyntaxError

A syntax error occurs when Python cannot parse your code.

Incorrect example:

```python
if x > 5
    print("Big number")
```

Output:

```text
SyntaxError: expected ':'
```

The `if` statement is missing a colon.

Correct version:

```python
x = 10

if x > 5:
    print("Big number")
```

Output:

```text
Big number
```

Syntax errors usually need to be corrected in the code itself. A `try`/`except` block around ordinary application code does not catch a syntax error in that same block because Python must parse the code before executing it.

#### ZeroDivisionError

This error occurs when you divide a number by zero.

```python
result = 10 / 0
```

Output:

```text
ZeroDivisionError: division by zero
```

Correct approach:

```python
divisor = 0

if divisor != 0:
    result = 10 / divisor
    print(result)
else:
    print("Cannot divide by zero.")
```

Output:

```text
Cannot divide by zero.
```

#### NameError

A `NameError` occurs when Python cannot find the name you are trying to use.

```python
print(score)
```

If `score` has not been defined, Python raises a `NameError`.

Correct version:

```python
score = 95
print(score)
```

#### TypeError

A `TypeError` occurs when an operation or function is used with an incompatible type.

```python
result = "hello" + 5
```

Python cannot concatenate a string and an integer directly.

Correct version:

```python
result = "hello" + str(5)
print(result)
```

Output:

```text
hello5
```

#### FileNotFoundError

A `FileNotFoundError` occurs when Python cannot find the requested file.

```python
with open("data.txt", "r", encoding="utf-8") as file:
    content = file.read()
```

If `data.txt` does not exist at the resolved path, Python raises an exception.

We will use this example to learn error handling.

### 4. Why do we need error handling?

Consider the following program:

```python
with open("data.txt", "r", encoding="utf-8") as file:
    content = file.read()

print(content)
print("Program completed.")
```

If the file does not exist, Python raises a `FileNotFoundError`. The remaining statements are not executed during that run.

We can handle this situation with `try` and `except`.

```python
try:
    with open("data.txt", "r", encoding="utf-8") as file:
        content = file.read()

    print(content)

except FileNotFoundError:
    print("Could not find data.txt")

print("Program completed.")
```

If the file is missing, the output is:

```text
Could not find data.txt
Program completed.
```

The program handles the expected problem and continues with the statements after the exception-handling block.

Notice that `content` is not assigned a default value in this version. If your application needs a fallback value, assign one explicitly inside the `except` block.

### 5. Understand `try` and `except`

Python provides a structured way to handle exceptions.

```python
try:
    # Code that might raise an exception
    result = 10 / 0

except ZeroDivisionError:
    # Code that handles the specific exception
    print("Cannot divide by zero.")
```

The flow is:

1. Python executes the statements inside `try`.
2. If an exception occurs, Python looks for a matching `except` handler.
3. If a matching handler is found, its code runs.
4. Execution continues after the exception-handling block.

Output:

```text
Cannot divide by zero.
```

If no exception occurs, the `except` block is skipped.

**Important:** Use `try` for operations that can reasonably fail, and catch exceptions you know how to handle. Avoid using exception handling to hide programming mistakes.

### 6. Handle different exceptions separately

A program may encounter different types of errors. You can handle each type with a separate `except` block.

```python
try:
    number = int(input("Enter a number: "))
    result = 100 / number

    print("Result:", result)

except ValueError:
    print("Invalid input. Please enter a whole number.")

except ZeroDivisionError:
    print("The number cannot be zero.")
```

Example 1:

```text
Enter a number: abc
Invalid input. Please enter a whole number.
```

Example 2:

```text
Enter a number: 0
The number cannot be zero.
```

Example 3:

```text
Enter a number: 4
Result: 25.0
```

Here:

- `ValueError` handles input that cannot be converted to an integer.
- `ZeroDivisionError` handles division by zero.

Separate handlers allow you to give users a more useful explanation of what went wrong.

### 7. Handle errors when reading files

Let's use our `sales-analysis` project.

```text
sales-analysis/
├── analyzer.py
├── helpers.py
├── data/
│   └── sales.csv
└── output/
```

Suppose `analyzer.py` needs to read `data/sales.csv`.

```python
from pathlib import Path

project_dir = Path(__file__).resolve().parent
data_path = project_dir / "data" / "sales.csv"

try:
    with open(data_path, "r", encoding="utf-8") as file:
        content = file.read()

    print(content)

except FileNotFoundError:
    print(f"File not found: {data_path}")

except PermissionError:
    print(f"Permission denied: {data_path}")
```

This code handles two common file errors:

- `FileNotFoundError` — the file does not exist at the specified location.
- `PermissionError` — the program does not have permission to access the file.

Using `pathlib` makes the path relative to the script rather than relying on the terminal's current working directory.

### 8. Use `else` and `finally`

Python also supports `else` and `finally` in exception handling.

- `else` runs when the `try` block completes without an exception.
- `finally` runs whether the `try` block succeeds or an exception occurs, subject to normal Python process termination.

Example:

```python
try:
    number = int(input("Enter a number: "))

except ValueError:
    print("Please enter a valid integer.")

else:
    print("You entered:", number)

finally:
    print("Input operation finished.")
```

If the user enters `10`, the output is:

```text
Enter a number: 10
You entered: 10
Input operation finished.
```

If the user enters `abc`, the output is:

```text
Enter a number: abc
Please enter a valid integer.
Input operation finished.
```

**When should you use them?**

- Use `else` when you want to separate successful processing from error handling.
- Use `finally` for cleanup operations that must be attempted regardless of success or failure.

For example, closing a file is normally handled automatically when you use `with open(...)`.

### 9. Understand the `raise` statement

Sometimes your program detects an invalid condition and needs to signal an error explicitly. You can use `raise` to trigger an exception.

```python
def calculate_discount(price, discount_percent):
    if price < 0:
        raise ValueError("Price cannot be negative.")

    if not 0 <= discount_percent <= 100:
        raise ValueError("Discount must be between 0 and 100.")

    return price * (1 - discount_percent / 100)


try:
    final_price = calculate_discount(1000, 10)
    print(f"Final price: ${final_price:.2f}")

except ValueError as error:
    print(f"Invalid input: {error}")
```

Output:

```text
Final price: $900.00
```

If you call `calculate_discount(1000, 150)`, the function raises a `ValueError`, which the caller can handle.

This is useful when a function must enforce rules about the values it accepts.

### 10. Handle API errors

When your Python program calls an API, the request can fail because of network problems, timeouts, or unsuccessful HTTP responses.

The `requests` package provides exception types that help you handle these failures.

```python
import requests

url = "https://api.open-meteo.com/v1/forecast"

params = {
    "latitude": 12.97,
    "longitude": 77.59,
    "current": "temperature_2m"
}

try:
    response = requests.get(
        url,
        params=params,
        timeout=10
    )

    response.raise_for_status()

    data = response.json()
    temperature = data["current"]["temperature_2m"]

    print(f"Current temperature: {temperature}°C")

except requests.exceptions.Timeout:
    print("The API request timed out.")

except requests.exceptions.HTTPError as error:
    print(f"The API returned an unsuccessful HTTP status: {error}")

except requests.exceptions.RequestException as error:
    print(f"Network or request error: {error}")

except (ValueError, KeyError, TypeError) as error:
    print(f"Unable to process the API response: {error}")
```

**Understanding the code**

- `timeout=10` limits how long the request waits for a response.
- `raise_for_status()` raises an HTTP-related exception for unsuccessful status codes.
- `response.json()` parses the response as JSON.
- The exception handlers distinguish network errors from problems processing the returned data.

A successful HTTP response does not guarantee that the returned data has every field your application expects. That is why we also handle parsing and data-access errors.

For production applications, you may also need retries, rate-limit handling, structured logging, and schema validation.

### 11. Avoid catching every exception unnecessarily

You might see code like this:

```python
try:
    result = 10 / 0

except Exception:
    print("Something went wrong.")
```

This catches many ordinary exceptions, but it also hides useful information about the problem.

Prefer a specific exception when you know what you expect:

```python
try:
    result = 10 / 0

except ZeroDivisionError:
    print("Cannot divide by zero.")
```

Catching `Exception` can be appropriate at a carefully chosen application boundary, such as a top-level task runner that logs unexpected failures. In that case, retain the error details rather than silently discarding them.

Avoid a bare `except:` unless you have a specific reason to catch exceptions outside the normal `Exception` hierarchy. It can also intercept exceptions used to interrupt a program, such as `KeyboardInterrupt`.

### 12. Common errors to remember

| Exception | Typical cause | Possible response |
|---|---|---|
| `FileNotFoundError` | A file is missing. | Check the path or request another file. |
| `PermissionError` | Access to a file or resource is denied. | Check permissions. |
| `ValueError` | A value is invalid for an operation. | Validate input or report the invalid value. |
| `TypeError` | An operation receives an incompatible type. | Check the input types and function usage. |
| `NameError` | A name has not been defined. | Correct the variable or name reference. |
| `ZeroDivisionError` | Division by zero. | Validate the divisor. |
| `KeyError` | A dictionary key is missing. | Check the available keys or use `.get()` when appropriate. |
| `IndexError` | A sequence index is outside its valid range. | Check the sequence length and index. |
| `ModuleNotFoundError` | A module cannot be found. | Check the import name, interpreter, environment, and installation. |
| `requests.exceptions.Timeout` | An API request took too long. | Retry where appropriate or report the timeout. |

A `SyntaxError` is different from most of these runtime exceptions because Python must successfully parse a script before executing it.

### 13. Best practices for error handling

1. **Handle expected failures.** Identify which operations can fail and decide what your application should do.
2. **Catch specific exceptions.** This makes the program's response more precise.
3. **Display useful messages.** Tell the user what happened and, when appropriate, how to fix it.
4. **Do not hide errors silently.** Unexpected failures should be logged or propagated.
5. **Validate inputs.** Prevent invalid data from reaching calculations or external services.
6. **Use timeouts for network requests.** Avoid waiting indefinitely.
7. **Keep cleanup reliable.** Use context managers such as `with open(...)` when working with files.
8. **Avoid exposing sensitive details.** Error messages shown to users should not reveal API keys, credentials, or confidential data.

### 14. Practice exercises

**Exercise 1: Handle division by zero**

Write a program that accepts two integers and divides the first by the second. Handle invalid input and division by zero separately.

**Exercise 2: Handle a missing file**

Attempt to read `data.txt`. If it does not exist, print a helpful message.

**Exercise 3: Validate a discount**

Write a function that raises `ValueError` when a discount percentage is outside the range of 0 to 100.

**Exercise 4: Handle API failures**

Modify the weather API example to handle a timeout and an unsuccessful HTTP response.

**Exercise 5: Use `else` and `finally`**

Write a program that asks for an integer, displays it if valid, and always prints `Operation completed` at the end.

### 15. Sample solution: Safe division

```python
def divide_numbers(a, b):
    if b == 0:
        raise ZeroDivisionError("The divisor cannot be zero.")

    return a / b


try:
    first = int(input("Enter the first number: "))
    second = int(input("Enter the second number: "))

    result = divide_numbers(first, second)

except ValueError:
    print("Invalid input. Enter whole numbers only.")

except ZeroDivisionError as error:
    print(f"Calculation error: {error}")

else:
    print(f"Result: {result}")

finally:
    print("Operation completed.")
```

This solution combines input conversion, validation, custom error messages, exception handling, and a `finally` block.

### 16. Lesson summary

In this lesson, you learned:

- Why errors occur in Python programs.
- The difference between syntax errors and runtime exceptions.
- How to use `try` and `except`.
- How to handle multiple exception types.
- How to use `else`, `finally`, and `raise`.
- How to handle file and API failures.
- Why specific exception handling is preferable to silently catching everything.
- How error handling makes applications more reliable.

**Key takeaway:** Good error handling does not prevent every failure. It helps your program recognize failures, respond appropriately, and provide enough information to diagnose problems.

These skills are essential when building reliable Python applications, data pipelines, AI agents, and cloud automation tools.

**Next lesson: Debugging Python — Find and Fix Problems in Your Code.**
