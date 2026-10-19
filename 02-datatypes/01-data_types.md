# Python Data Types
## Different Kinds of Information in Python

### 1. What Are Data Types?

In everyday life, we work with different kinds of information, such as names, ages, prices, and yes-or-no answers.

Python also works with different kinds of information. A **data type** tells Python what kind of value a piece of data represents and what operations can be performed on it.

For example:
- A person's age is usually represented by a number.
- A person's name is represented by text.
- A decision can be represented by `True` or `False`.

You cannot always perform the same operations on different types of data. Python handles numbers, text, and logical values differently.

### 2. The Main Python Data Types

Python has several built-in data types. Let's start with four fundamental types.

#### A. Integers (`int`)

Integers are whole numbers without decimal points.

Examples:
```python
age = 25
students = 30
temperature = -5

print(age)
print(students)
print(temperature)
```

Output:
```text
25
30
-5
```

Common uses: counting students, storing ages, and representing quantities.

#### B. Floating-Point Numbers (`float`)

Floating-point numbers represent numbers with decimal points.

Examples:
```python
price = 99.50
height = 5.7
temperature = 36.5

print(price)
print(height)
print(temperature)
```

Output:
```text
99.5
5.7
36.5
```

Common uses: prices, measurements, and calculations involving decimal values.

#### C. Strings (`str`)

Strings represent text, such as names, messages, and sentences. You create a string by enclosing text in single or double quotation marks.

Examples:
```python
name = "Alice"
city = 'Bengaluru'
message = "Welcome to Python!"

print(name)
print(city)
print(message)
```

Output:
```text
Alice
Bengaluru
Welcome to Python!
```

You can combine strings using the `+` operator.

```python
first_name = "Alice"
last_name = "Smith"

full_name = first_name + " " + last_name

print(full_name)
```

Output:
```text
Alice Smith
```

#### D. Booleans (`bool`)

Booleans represent one of two values: `True` or `False`.

Examples:
```python
is_student = True
is_logged_in = False

print(is_student)
print(is_logged_in)
```

Output:
```text
True
False
```

Common uses: checking conditions, validating information, and making decisions in programs.

**Important:** Python uses capital letters for Boolean values: `True` and `False`, not `true` and `false`.

### 3. Why Do Data Types Matter?

Python treats different data types differently.

**Example 1: Adding numbers**

```python
total = 10 + 5
print(total)
```

Output:
```text
15
```

Python performs mathematical addition because both values are numbers.

**Example 2: Combining strings**

```python
greeting = "Hello" + " " + "World"
print(greeting)
```

Output:
```text
Hello World
```

Python combines the text because both values are strings.

**Example 3: Mixing strings and numbers**

```python
age = "25" + 5
print(age)
```

This produces a `TypeError` because Python cannot directly add a string and an integer.

To fix this, convert the string to an integer:

```python
age = int("25") + 5
print(age)
```

Output:
```text
30
```

Here, `int("25")` converts the string `"25"` into the integer `25`.

### 4. How to Check a Data Type

Python provides the built-in `type()` function to identify the data type of a value or variable.

Example:

```python
print(type(42))
print(type(3.14))
print(type("Hello"))
print(type(True))
```

Output:
```text
<class 'int'>
<class 'float'>
<class 'str'>
<class 'bool'>
```

You can also check the types of variables.

```python
age = 25
name = "Alice"
height = 5.7
is_student = True

print(type(age))
print(type(name))
print(type(height))
print(type(is_student))
```

Output:
```text
<class 'int'>
<class 'str'>
<class 'float'>
<class 'bool'>
```

### 5. Type Conversion

Type conversion means changing a value from one data type to another when appropriate.

Python provides several built-in conversion functions:

| Function | Purpose | Example | Result |
|---|---|---|---|
| `int()` | Converts to an integer | `int("25")` | `25` |
| `float()` | Converts to a float | `float("3.5")` | `3.5` |
| `str()` | Converts to a string | `str(100)` | `"100"` |
| `bool()` | Converts to a Boolean | `bool(1)` | `True` |

Example:

```python
age = "25"
height = "5.7"

age_number = int(age)
height_number = float(height)

print(age_number + 5)
print(height_number + 0.3)
```

Output:
```text
30
6.0
```

**Remember:** Not every value can be converted successfully. For example, `int("hello")` raises a `ValueError`.

### 6. Practice Exercise

Try running the following program in VS Code.

```python
name = "Vaithee"
age = 44
height = 5.7
is_learning_python = True

print("Name:", name)
print("Age:", age)
print("Height:", height)
print("Learning Python:", is_learning_python)

print(type(name))
print(type(age))
print(type(height))
print(type(is_learning_python))
```

**Your tasks:**
1. Change the name to your name.
2. Change the age to your age.
3. Add a variable called `course` containing the text `"Python for AI Engineering"`.
4. Add a variable called `completed_lessons` containing the number `5`.
5. Print the value and data type of each new variable.
6. Change the age from a number to a string and observe the difference.

### 7. Quick Knowledge Check

1. Which data type stores whole numbers?
2. Which data type stores text?
3. What are the two possible Boolean values?
4. Which function checks the type of a value?
5. What does `int("25")` return?
6. What happens when you try to add `"25" + 5`?

**Answers:**
1. `int`
2. `str`
3. `True` and `False`
4. `type()`
5. The integer `25`
6. Python raises a `TypeError` because the values have incompatible types for addition.

### Summary

In this lesson, you learned:

- **`int`** — whole numbers.
- **`float`** — decimal-point numbers.
- **`str`** — text.
- **`bool`** — `True` or `False`.
- **`type()`** — checks a value's data type.
- **Type conversion** — changes a value's type using functions such as `int()`, `float()`, and `str()`.

### What's Next?

Start with **Numbers in Python** to learn arithmetic operations, integer and floating-point numbers, and how to perform calculations in your programs.
