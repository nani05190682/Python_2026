# Python Syntax: How to Write Python Code Correctly

## 1. What Is Syntax?

Every programming language has a set of rules that determines how code must be written. These rules are called **syntax**.

Think of syntax as grammar in a human language. In English, words must be arranged correctly to communicate meaning. Similarly, Python code must follow specific rules for the interpreter to understand and execute it.

For example, consider these two sentences:

- Correct: "The cat sat on the mat."
- Incorrect: "Cat the on mat sat the."

Python follows the same principle. Instructions must be written in the correct format and order.

### Example: Correct vs. Incorrect Python Syntax

**Correct Python code:**

```python
age = 25

if age > 18:
    print("Adult")
```

**Output:**

```text
Adult
```

**Incorrect Python code:**

```python
age > 18 print("Adult")
```

This code produces a `SyntaxError` because the condition and the `print()` statement are not written in a valid Python structure.

**Key takeaway:** Python syntax defines how you must write statements, expressions, and code blocks.

## 2. Why Is Syntax Important?

Correct syntax allows Python to understand your instructions.

When you write Python code, the interpreter checks whether the code follows the language's grammar. If the syntax is invalid, Python usually raises a `SyntaxError` before executing the affected code.

For example:

```python
# Correct syntax
print("Welcome to Python!")

# Incorrect syntax: missing closing parenthesis
print("Welcome to Python!"
```

The first statement runs successfully. The second statement raises a syntax error because the closing parenthesis is missing.

Learning syntax early helps you write reliable programs and identify mistakes more quickly.

## 3. Python's Unique Feature: Indentation

One of Python's most distinctive features is its use of **indentation to define code blocks**.

Many programming languages, such as JavaScript and Java, commonly use curly braces `{}` to group statements. Python uses indentation instead.

### Example: Python Indentation

```python
temperature = 35

if temperature > 30:
    print("It's hot!")
    print("Turn on the air conditioner.")

print("Program completed.")
```

**Output:**

```text
It's hot!
Turn on the air conditioner.
Program completed.
```

The two indented statements belong to the `if` block. The final `print()` statement is not indented, so it executes outside that block.

### Comparison with JavaScript

Python:

```python
if temperature > 30:
    print("It's hot!")
    print("Turn on the air conditioner.")
```

JavaScript:

```javascript
if (temperature > 30) {
    console.log("It's hot!");
    console.log("Turn on the air conditioner.");
}
```

Python uses indentation to define the block, while JavaScript uses curly braces.

## 4. Python Indentation Rules

Python uses indentation to determine which statements belong together.

Follow these guidelines:

- Use **four spaces** for each indentation level.
- Keep indentation consistent within a block.
- Indent statements that belong to an `if`, `for`, `while`, function, or other block.
- Use a colon (`:`) after statements that introduce a block, such as `if`, `for`, `while`, and `def`.
- Avoid mixing tabs and spaces.

### Correct Indentation

```python
score = 95

if score > 90:
    print("Grade A")

    if score == 100:
        print("Perfect score!")
```

**Output:**

```text
Grade A
```

The nested condition is valid, but its body does not execute because `score` is 95 rather than 100.

### Incorrect Indentation

```python
score = 95

if score > 90:
  print("Grade A")
    print("Excellent performance")
```

This example raises an `IndentationError` because the indentation is inconsistent within the block.

### Important Tip

VS Code can automatically insert indentation when you press Enter after a statement ending with a colon. However, you should still check that your code blocks are aligned correctly.

## 5. Colons and Code Blocks

In Python, a colon (`:`) introduces a block of code after statements such as `if`, `for`, `while`, and `def`.

Example:

```python
age = 22

if age >= 18:
    print("You are an adult.")
```

The colon indicates that an indented block follows.

Without the colon, Python raises a syntax error:

```python
if age >= 18
    print("You are an adult.")
```

**Remember:** A colon introduces the block, and indentation identifies which statements belong to it.

## 6. Comments in Python

Comments are notes written in source code to explain what the program does. Python ignores comments when executing ordinary code.

Use the `#` symbol to write a single-line comment.

```python
# Store the user's age
age = 25

# Display the age
print(age)
```

**Output:**

```text
25
```

Comments help you and other developers understand your code.

A useful comment explains why something is done when the reason is not obvious. Avoid writing comments that merely repeat what the code already clearly states.

## 7. Python Naming Conventions

Python allows you to choose names for variables, functions, and other objects, subject to its naming rules.

Examples of valid variable names:

```python
user_name = "Ravi"
age = 25
total_price = 1500
server_status = "running"
```

Python developers commonly use **snake_case** for variables and function names.

### Invalid Variable Names

```python
2name = "Ravi"
user-name = "Ravi"
class = "Python"
```

These examples are invalid because:

- A variable name cannot start with a digit.
- A hyphen is interpreted as a minus operator, not as part of an identifier.
- `class` is a reserved Python keyword.

Use descriptive names such as `user_name`, `total_price`, and `server_status` to make your code easier to understand.

## 8. Python Style Guide: PEP 8

In addition to syntax rules, Python has conventions that help developers write readable and consistent code.

**PEP 8** is the widely used Python style guide. Following it makes code easier to read, review, maintain, and share with other developers.

Important recommendations include:

### Use Four Spaces for Indentation

```python
if score >= 50:
    print("Pass")
```

### Use Snake Case for Variables and Functions

```python
student_name = "Ravi"

def calculate_total():
    return 100
```

### Add Spaces Around Operators

Recommended:

```python
total = price + tax
```

Less readable:

```python
total=price+tax
```

### Use Meaningful Names

Recommended:

```python
monthly_salary = 50000
```

Less descriptive:

```python
x = 50000
```

Short names can be appropriate in some contexts, but descriptive names generally improve readability.

### Keep Lines Readable

PEP 8 traditionally recommends a maximum line length of 79 characters for code and 72 characters for comments and docstrings. Many projects adopt different limits, so follow the conventions of your project when specified.

Read the official guide: https://peps.python.org/pep-0008/

**Important:** PEP 8 is a style guide, not a collection of mandatory syntax rules. Code can run correctly even when it does not follow every PEP 8 recommendation.

## 9. Common Python Syntax Mistakes

Here are some common mistakes beginners encounter.

| Mistake | Example | Correction |
|---|---|---|
| Missing quotation mark | `print("Hello)` | `print("Hello")` |
| Missing parenthesis | `print("Hello"` | `print("Hello")` |
| Missing colon | `if age > 18` | `if age > 18:` |
| Incorrect indentation | Misaligned block statements | Use consistent indentation |
| Invalid variable name | `2name = "Ravi"` | `name2 = "Ravi"` |
| Incorrect capitalization | `Print("Hello")` | `print("Hello")` |

Python is case-sensitive, so `print`, `Print`, and `PRINT` are different identifiers. The built-in function is named `print`.

## 10. Hands-On Practice

Create a file named `syntax_practice.py` and enter the following code:

```python
# Python syntax practice

name = "Ravi"
age = 25

if age >= 18:
    print("Name:", name)
    print("You are an adult.")
else:
    print("You are under 18.")

print("Program completed successfully.")
```

**Expected output:**

```text
Name: Ravi
You are an adult.
Program completed successfully.
```

### Practice Tasks

1. Change the name to your own name.
2. Change the age to 15 and observe the output.
3. Remove the colon after the `if` statement and run the program. Observe the error.
4. Correct the colon and run the program again.
5. Adjust the indentation and observe how Python interprets the code.

These exercises will help you understand how Python syntax affects program execution.

## 11. Lesson Summary

In this lesson, you learned:

- What Python syntax is and why it matters.
- How Python uses indentation to define code blocks.
- Why colons are required after block-introducing statements.
- How to write comments and choose valid variable names.
- What PEP 8 is and how it improves code readability.
- How to identify and correct common syntax mistakes.


### Infographic for the above content

<img width="1536" height="2752" alt="Gemini_Generated_Image_82ineq82ineq82in" src="https://github.com/user-attachments/assets/c0eb1932-4801-4fda-af22-f4c5d8bab35a" />


**Next lesson: Python Errors — Understanding Syntax Errors, Runtime Errors, and Debugging.**
