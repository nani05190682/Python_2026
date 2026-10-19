# Numbers in Python
## Working with Integers and Decimals

### 1. Introduction to Numbers

Numbers are one of the most commonly used data types in Python. We use them to perform calculations, count items, store measurements, and solve problems.

Python has two main numeric types for everyday calculations:

- **Integers (`int`)** — whole numbers without a decimal point.
- **Floating-point numbers (`float`)** — numbers that can represent decimal values.

Let's explore each type.

### 2. Integers (`int`)

Integers are whole numbers. They can be positive, negative, or zero.

Examples:

```python
age = 25
score = -10
students = 30
temperature = 0

print(age)
print(score)
print(students)
print(temperature)
```

Output:

```text
25
-10
30
0
```

**Common uses of integers:**
- Counting students in a classroom.
- Storing a person's age in whole years.
- Tracking the number of files on a system.
- Counting successful or failed login attempts.

### 3. Floating-Point Numbers (`float`)

Floating-point numbers represent values that include a fractional or decimal part.

Examples:

```python
price = 19.99
temperature = -5.5
pi = 3.14159
height = 5.7

print(price)
print(temperature)
print(pi)
print(height)
```

Output:

```text
19.99
-5.5
3.14159
5.7
```

**Common uses of floats:**
- Representing measurements and temperatures.
- Performing calculations involving decimal values.
- Calculating averages and percentages.
- Working with scientific data.

**Important:** Python uses a dot (`.`) as the decimal separator. Write `3.14`, not `3,14`.

For example:

```python
number = 3.14
print(number)
```

Output:

```text
3.14
```

In Python, `3,14` is not the decimal number `3.14`. It is a tuple containing two integers: `3` and `14`.

### 4. Why Are There Two Numeric Types?

Integers and floats represent numbers differently.

- Integers represent whole numbers exactly, subject to available memory.
- Floats represent many fractional values approximately because they use a finite amount of binary precision.

Python handles many operations between integers and floats automatically. You usually choose the type that makes sense for your data.

Example:

```python
students = 25
average_score = 87.5

print(type(students))
print(type(average_score))
```

Output:

```text
<class 'int'>
<class 'float'>
```

When you combine an integer and a float in an arithmetic operation, Python generally produces a float.

```python
result = 10 + 2.5
print(result)
print(type(result))
```

Output:

```text
12.5
<class 'float'>
```

### 5. Basic Mathematical Operations

Python supports the basic mathematical operations you would use on a calculator.

| Operator | Operation | Example | Result |
|---|---|---|---:|
| `+` | Addition | `10 + 5` | `15` |
| `-` | Subtraction | `20 - 7` | `13` |
| `*` | Multiplication | `6 * 4` | `24` |
| `/` | Division | `10 / 2` | `5.0` |
| `//` | Floor division | `10 // 3` | `3` |
| `%` | Modulo (remainder) | `10 % 3` | `1` |
| `**` | Exponentiation (power) | `5 ** 2` | `25` |

Let's try these operations in Python.

```python
# Addition and subtraction
total = 10 + 5
change = 20 - 7

# Multiplication and division
area = 6 * 4
half = 10 / 2

# Powers
squared = 5 ** 2
cubed = 2 ** 3

# Remainder
remainder = 10 % 3

print(total)
print(change)
print(area)
print(half)
print(squared)
print(cubed)
print(remainder)
```

Output:

```text
15
13
24
5.0
25
8
1
```

Notice that `10 / 2` returns `5.0`, even though the answer is a whole number.

### 6. Regular Division vs. Floor Division

Python provides two division operators.

#### Regular division (`/`)

The `/` operator returns a floating-point result.

```python
result = 10 / 3
print(result)
```

Output:

```text
3.3333333333333335
```

#### Floor division (`//`)

The `//` operator performs floor division. It rounds the result down to the nearest whole integer when both operands are integers.

```python
result = 10 // 3
print(result)
```

Output:

```text
3
```

**Important:** Floor division does not always mean simply removing the decimal part. It rounds toward negative infinity.

```python
print(10 // 3)
print(-10 // 3)
```

Output:

```text
3
-4
```

This happens because \(-10/3\) is approximately \(-3.33\), and the next whole number down is \(-4\).

### 7. Working with Remainders

The modulo operator (`%`) returns the remainder after division.

Example:

```python
print(10 % 3)
print(12 % 4)
print(15 % 4)
```

Output:

```text
1
0
3
```

This is useful for checking whether a number is even or odd.

```python
number = 8

if number % 2 == 0:
    print("Even number")
else:
    print("Odd number")
```

Output:

```text
Even number
```

The expression `number % 2` gives a remainder of `0` for even integers and a remainder of `1` for odd non-negative integers.

### 8. Common Mistakes to Avoid

**Mistake 1: Expecting division to return an integer**

```python
result = 10 / 2
print(result)
```

Output:

```text
5.0
```

Regular division (`/`) returns a float, even when the answer is a whole number.

**Mistake 2: Using a comma as the decimal separator**

```python
price = 3,14
print(price)
```

Output:

```text
(3, 14)
```

Use `3.14` to represent a decimal number.

**Mistake 3: Expecting all float calculations to be exact**

```python
print(0.1 + 0.2)
```

Output:

```text
0.30000000000000004
```

This happens because some decimal fractions cannot be represented exactly as binary floating-point values.

For ordinary calculations, this is usually manageable. For financial calculations requiring exact decimal arithmetic, consider Python's `decimal` module.

### 9. Practice Exercise

Create a Python file named `numbers_practice.py` and complete the following tasks.

**Task 1: Create numeric variables**

```python
age = 25
price = 199.99
students = 30
temperature = 28.5

# Print each value
# Print the data type of each value
```

**Task 2: Perform calculations**

Calculate and print:
1. The sum of `25` and `15`.
2. The difference between `100` and `35`.
3. The product of `12` and `8`.
4. The result of `25 / 4`.
5. The result of `25 // 4`.
6. The remainder of `25 % 4`.
7. The square of `6`.

**Task 3: Calculate a classroom average**

A class has five students who scored `80`, `75`, `90`, `85`, and `70`.

Write a program that calculates and prints their average score.

**Task 4: Check even or odd**

Ask the user to enter a whole number, then print whether it is even or odd.

Hint: Use `input()`, `int()`, and the modulo operator (`%`).

### 10. Sample Solution

```python
# Task 1: Numeric variables
age = 25
price = 199.99
students = 30
temperature = 28.5

print(age, type(age))
print(price, type(price))
print(students, type(students))
print(temperature, type(temperature))

# Task 2: Mathematical calculations
print(25 + 15)
print(100 - 35)
print(12 * 8)
print(25 / 4)
print(25 // 4)
print(25 % 4)
print(6 ** 2)

# Task 3: Classroom average
total = 80 + 75 + 90 + 85 + 70
average = total / 5

print("Average score:", average)

# Task 4: Even or odd
number = int(input("Enter a whole number: "))

if number % 2 == 0:
    print("Even number")
else:
    print("Odd number")
```

### Summary

In this lesson, you learned:

- `int` represents whole numbers.
- `float` represents floating-point numbers.
- Python supports addition, subtraction, multiplication, division, floor division, modulo, and exponentiation.
- `/` performs regular division, while `//` performs floor division.
- `%` returns the remainder.
- Floating-point calculations can have small precision differences.

### What's Next?

Now let's learn about **Strings in Python** — how to store text, combine words, access characters, and work with messages and user input.
