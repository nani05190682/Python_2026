# Code Formatting in Python

## Keep Your Code Clean, Consistent, and Readable

### 1. What Is Code Formatting?

Code formatting is the practice of organizing Python code so that it is easy to read, understand, and maintain.

Just as proper grammar makes written communication clearer, consistent code formatting helps developers understand what a program does and how its different parts fit together.

Python programs can sometimes run even when formatting is inconsistent. However, well-formatted code is easier to debug, review, and maintain, especially when working on larger projects.

In this lesson, you will learn the basic formatting conventions commonly used in Python development.

## 2. Basic Code Formatting Principles

### Principle 1: Use Consistent Indentation

Python uses indentation to identify code blocks. The standard convention is to use **four spaces per indentation level**.

**Good formatting:**

```python
def greet(name):
    if name:
        print(f"Hello, {name}!")
    else:
        print("Hello!")
```

**Poor formatting:**

```python
def greet(name):
  if name:
      print(f"Hello, {name}!")
    else:
        print("Hello!")
```

The second example has inconsistent indentation and will raise an indentation-related error.

**Best practice:** Configure your editor to insert four spaces when you press Tab in Python files.

### Principle 2: Add Spaces Around Operators

Use spaces around assignment operators, arithmetic operators, and comparison operators to improve readability.

**Good formatting:**

```python
x = 1 + 2
price = 100
tax = 18
total = price + tax
```

**Less readable formatting:**

```python
x=1+2
price=100
tax=18
total=price+tax
```

Both styles may execute correctly, but the first is easier to read and follows PEP 8 conventions.

### Principle 3: Add Spaces After Commas

When writing lists, function arguments, or other comma-separated values, include a space after each comma.

**Good formatting:**

```python
numbers = [1, 2, 3, 4]
student = {"name": "Ravi", "age": 25}
```

**Less readable formatting:**

```python
numbers = [1,2,3,4]
student = {"name":"Ravi","age":25}
```

Consistent spacing makes values easier to distinguish.

### Principle 4: Use Blank Lines to Separate Logical Sections

Blank lines help separate functions and logical sections of code.

For example:

```python
def greet_user(name):
    print(f"Hello, {name}!")


def calculate_total(price, tax):
    return price + tax


greet_user("Ravi")
total = calculate_total(100, 18)
print("Total:", total)
```

Notice the two blank lines between the top-level function definitions. This follows the common PEP 8 convention.

Blank lines can also separate related sections inside a longer function when doing so improves readability.

### Principle 5: Keep Lines Readable

PEP 8 recommends limiting most code lines to 79 characters. Many projects use a formatter configuration with a longer limit, such as 88 or 100 characters.

The goal is to keep code readable without unnecessary horizontal scrolling.

**Good formatting:**

```python
message = (
    "Welcome to Python programming. "
    "Let's learn to write clean code."
)

print(message)
```

**Less readable formatting:**

```python
message = "Welcome to Python programming. Let's learn to write clean code."
```

The second example is not necessarily wrong, but splitting a genuinely long line can improve readability.

Python also supports implicit line continuation inside parentheses, brackets, and braces, making multiline expressions easier to format.

### Principle 6: Use Meaningful Variable Names

Choose names that clearly describe the information being stored.

**Good formatting:**

```python
student_name = "Ravi"
monthly_salary = 50000
total_price = 1200
```

**Less descriptive naming:**

```python
sn = "Ravi"
ms = 50000
tp = 1200
```

Short names are useful in certain situations, such as loop counters, but descriptive names generally make programs easier to understand.

### Principle 7: Separate Imports from Program Logic

Place import statements at the beginning of your Python file, after any module-level documentation and before other executable statements.

For example:

```python
import math
import random


radius = 5
area = math.pi * radius ** 2

print("Circle area:", area)
```

This makes dependencies easy to identify and follows standard Python style conventions.

## 3. Code Formatting in Visual Studio Code

VS Code can help you format Python code automatically.

### Basic Setup

1. Open VS Code.
2. Install the Microsoft Python extension if it is not already installed.
3. Open the Extensions panel.
4. Search for and install **Ruff** if you want to use Ruff as your formatter.
5. Open your Python file.

### Format Your Python File

With the Ruff extension installed and configured:

- **Windows/Linux:** Press `Shift + Alt + F`.
- **macOS:** Press `Shift + Option + F`.

Alternatively, right-click inside the editor and select **Format Document**.

If VS Code asks you to choose a formatter, select Ruff.

You can also enable format-on-save in VS Code settings so that your code is formatted whenever you save the file.

## 4. Automatic Formatting with Ruff

Ruff is a Python development tool that provides fast code linting and formatting.

It can help you:

- Apply consistent code formatting.
- Identify common style issues.
- Detect many common programming mistakes.
- Maintain consistent code quality across a project.

To install Ruff in your active virtual environment, run:

```bash
python -m pip install ruff
```

Format a Python file:

```bash
ruff format hello.py
```

Check a file for linting issues:

```bash
ruff check hello.py
```

Formatting and linting are different tasks. Formatting adjusts code layout, while linting identifies potential errors and style issues. Some linting issues may require you to change the code manually.

For more information, visit the official documentation:

https://docs.astral.sh/ruff/

## 5. Hands-On Practice

Create a file named `formatting_practice.py` and enter the following poorly formatted code:

```python
def calculate_total(price,tax):
    total=price+tax
    print("Total:",total)
    return total

def greet(name):
 print(f"Hello, {name}!")

greet("Ravi")
calculate_total(100,18)
```

Your task is to improve the formatting by:

1. Adding spaces after commas.
2. Adding spaces around operators.
3. Using consistent four-space indentation.
4. Adding blank lines between functions.
5. Using meaningful variable names where necessary.

### Suggested Solution

```python
def calculate_total(price, tax):
    total = price + tax
    print("Total:", total)
    return total


def greet(name):
    print(f"Hello, {name}!")


greet("Ravi")
calculate_total(100, 18)
```

**Expected output:**

```text
Hello, Ravi!
Total: 118
```

Notice that the program's behavior remains the same while the code becomes easier to read and maintain.

## 6. Lesson Summary

In this lesson, you learned:

- What code formatting is and why it matters.
- How to use consistent indentation and spacing.
- How to separate functions and logical sections with blank lines.
- How to keep lines readable and choose meaningful names.
- How to format Python code in VS Code.
- How to use Ruff for automatic formatting and linting.

**Next lesson: Python Variables — Learn How to Store and Manage Data.**
