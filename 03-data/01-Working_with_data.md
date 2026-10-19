# Operators in Python
## Math, Comparisons, and Logic in Python

### 1. What Are Operators?

**Operators are symbols or keywords that perform operations on values and variables.**

Think of operators as the action words of programming. They allow you to calculate numbers, compare values, make decisions, and update variables.

For example:

```python
print(10 + 5)
print(10 > 5)
print(True and False)
```

Output:

```text
15
True
False
```

Python has several categories of operators:

- **Arithmetic operators** — perform mathematical calculations.
- **Comparison operators** — compare values and return `True` or `False`.
- **Logical operators** — combine conditions or reverse Boolean values.
- **Assignment operators** — assign values to variables and update them.
- **Membership operators** — check whether a value exists in a sequence.
- **Identity operators** — check whether two references point to the same object.

Let's explore the most commonly used operators first.

### 2. Arithmetic Operators

Arithmetic operators perform mathematical calculations.

| Operator | Operation | Example | Result |
|---|---|---|---:|
| `+` | Addition | `10 + 3` | `13` |
| `-` | Subtraction | `10 - 3` | `7` |
| `*` | Multiplication | `10 * 3` | `30` |
| `/` | Division | `10 / 3` | `3.333...` |
| `//` | Floor division | `10 // 3` | `3` |
| `%` | Modulo (remainder) | `10 % 3` | `1` |
| `**` | Exponentiation (power) | `10 ** 3` | `1000` |

Example:

```python
# Arithmetic operators
print(10 + 3)   # Addition
print(10 - 3)   # Subtraction
print(10 * 3)   # Multiplication
print(10 / 3)   # Division
print(10 // 3)  # Floor division
print(10 % 3)   # Remainder
print(10 ** 3)  # Exponentiation
```

Output:

```text
13
7
30
3.3333333333333335
3
1
1000
```

**Remember:**
- `/` performs regular division and returns a float.
- `//` performs floor division, rounding down toward negative infinity.
- `%` returns the remainder.
- `**` calculates a power.

For example, `2 ** 3` means \(2 \times 2 \times 2\), which equals `8`.

### 3. Order of Operations

Python follows mathematical precedence rules when evaluating expressions. Parentheses can be used to control the order of calculations.

Consider this example:

```python
result = 2 + 3 * 4
print(result)
```

Output:

```text
14
```

Python performs multiplication before addition:

1. `3 * 4` gives `12`.
2. `2 + 12` gives `14`.

Now add parentheses:

```python
result = (2 + 3) * 4
print(result)
```

Output:

```text
20
```

Python evaluates the expression inside the parentheses first.

A simplified order of precedence is:

1. Parentheses: `()`
2. Exponentiation: `**`
3. Unary operations: `+x`, `-x`
4. Multiplication, division, floor division, modulo: `*`, `/`, `//`, `%`
5. Addition and subtraction: `+`, `-`
6. Comparisons: `==`, `!=`, `>`, `<`, `>=`, `<=`
7. Logical `not`
8. Logical `and`
9. Logical `or`

When an expression becomes complicated, use parentheses to make your intention clear.

### 4. Comparison Operators

Comparison operators compare two values and return a Boolean result: `True` or `False`.

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `==` | Equal to | `18 == 18` | `True` |
| `!=` | Not equal to | `18 != 21` | `True` |
| `>` | Greater than | `18 > 17` | `True` |
| `<` | Less than | `18 < 20` | `True` |
| `>=` | Greater than or equal to | `18 >= 18` | `True` |
| `<=` | Less than or equal to | `18 <= 18` | `True` |

Example:

```python
age = 18

print(age == 18)
print(age != 21)
print(age > 17)
print(age < 20)
print(age >= 18)
print(age <= 18)
```

Output:

```text
True
True
True
True
True
True
```

Comparison operators are useful when checking eligibility, validating input, comparing scores, or evaluating system metrics.

#### Difference between `=` and `==`

These operators have different purposes.

```python
age = 18
```

The `=` operator assigns the value `18` to `age`.

```python
print(age == 18)
```

The `==` operator checks whether `age` equals `18`.

Output:

```text
True
```

This distinction is important because using `=` where a comparison is expected can cause a syntax error.

### 5. Logical Operators

Logical operators combine conditions or reverse a Boolean value.

Python has three main logical operators: `and`, `or`, and `not`.

#### A. The `and` operator

The `and` operator returns `True` only when both conditions are true.

```python
age = 25
has_license = True

can_drive = age >= 18 and has_license

print(can_drive)
```

Output:

```text
True
```

Both conditions are true, so `can_drive` is `True`.

If either condition is false, the combined condition evaluates to `False`.

#### B. The `or` operator

The `or` operator returns `True` when at least one condition is true.

```python
day = "Saturday"

is_weekend = day == "Saturday" or day == "Sunday"

print(is_weekend)
```

Output:

```text
True
```

The first condition is true, so the overall result is `True`.

#### C. The `not` operator

The `not` operator reverses a Boolean value.

```python
age = 25

is_adult = age >= 18
is_child = not is_adult

print(is_adult)
print(is_child)
```

Output:

```text
True
False
```

Since `is_adult` is `True`, applying `not` produces `False`.

### 6. Boolean Truth Tables

Truth tables show how logical operators behave with different combinations of Boolean values.

#### AND (`and`)

| A | B | A and B |
|---|---|---|
| `True` | `True` | `True` |
| `True` | `False` | `False` |
| `False` | `True` | `False` |
| `False` | `False` | `False` |

#### OR (`or`)

| A | B | A or B |
|---|---|---|
| `True` | `True` | `True` |
| `True` | `False` | `True` |
| `False` | `True` | `True` |
| `False` | `False` | `False` |

#### NOT (`not`)

| A | not A |
|---|---|
| `True` | `False` |
| `False` | `True` |

Try the following code:

```python
print(True and True)
print(True and False)

print(True or False)
print(False or False)

print(not True)
print(not False)
```

Output:

```text
True
False
True
False
False
True
```

**Easy way to remember:**
- `and` — both conditions must be true.
- `or` — at least one condition must be true.
- `not` — reverses the result.

### 7. Assignment Operators

Assignment operators assign values to variables or update their existing values.

The standard assignment operator is `=`.

```python
score = 10
```

Python also supports shortcuts called augmented assignment operators.

| Operator | Example | Equivalent operation |
|---|---|---|
| `+=` | `x += 5` | `x = x + 5` |
| `-=` | `x -= 5` | `x = x - 5` |
| `*=` | `x *= 2` | `x = x * 2` |
| `/=` | `x /= 2` | `x = x / 2` |
| `//=` | `x //= 2` | `x = x // 2` |
| `%=` | `x %= 3` | `x = x % 3` |
| `**=` | `x **= 2` | `x = x ** 2` |

Example:

```python
score = 10

score += 5
print(score)

score *= 2
print(score)

score -= 4
print(score)
```

Output:

```text
15
30
26
```

These shortcuts make code more concise and are frequently used when updating counters, totals, and other variables.

### 8. Membership Operators

Membership operators check whether a value exists in a sequence, such as a string, list, or tuple.

Python provides two membership operators:

- `in` — checks whether a value exists.
- `not in` — checks whether a value does not exist.

Example with strings:

```python
language = "Python"

print("Py" in language)
print("Java" in language)
print("Java" not in language)
```

Output:

```text
True
False
True
```

Example with a list:

```python
tools = ["Linux", "Docker", "Kubernetes"]

print("Docker" in tools)
print("Jenkins" not in tools)
```

Output:

```text
True
True
```

Membership operators are useful when checking whether a username, item, keyword, or tool appears in a collection.

### 9. Identity Operators

Identity operators check whether two variables refer to the same object in memory.

Python provides:
- `is`
- `is not`

For beginners, a common use is checking whether a value is `None`.

```python
result = None

print(result is None)
print(result is not None)
```

Output:

```text
True
False
```

**Important:** Use `==` to compare values for equality. Use `is` when checking object identity, especially when checking against `None`.

For example:

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a == b)
print(a is b)
```

Output:

```text
True
False
```

The lists contain equal values, but they are separate objects.

### 10. Common Mistakes to Avoid

**Mistake 1: Confusing assignment with comparison**

```python
age = 18
print(age == 18)
```

Use `=` to assign and `==` to compare.

**Mistake 2: Forgetting that division returns a float**

```python
print(10 / 2)
```

Output:

```text
5.0
```

Use `//` when floor division is what you need.

**Mistake 3: Ignoring operator precedence**

```python
print(2 + 3 * 4)
```

Output:

```text
14
```

Use parentheses when you want addition to happen first:

```python
print((2 + 3) * 4)
```

Output:

```text
20
```

**Mistake 4: Using `and` when you mean `or`**

```python
is_weekend = True
is_holiday = False

print(is_weekend and is_holiday)
print(is_weekend or is_holiday)
```

Output:

```text
False
True
```

Choose the operator based on whether both conditions must be true or just one.

### 11. Practice Exercises

Create a file named `operators_practice.py` and complete these tasks.

**Task 1: Arithmetic operators**

Calculate and print:
1. `25 + 15`
2. `100 - 45`
3. `12 * 8`
4. `50 / 4`
5. `50 // 4`
6. `50 % 4`
7. `2 ** 5`

**Task 2: Comparison operators**

Set `age = 21` and check:
1. Whether the age equals `21`.
2. Whether the age is greater than `18`.
3. Whether the age is less than `18`.
4. Whether the age is at least `21`.

**Task 3: Logical operators**

Create variables:

```python
age = 25
has_license = True
```

Create a variable named `can_drive` that is true only when the person meets your chosen minimum-age requirement and has a license.

**Task 4: Assignment shortcuts**

Start with `balance = 100`. Add `50`, subtract `20`, and then multiply the result by `2` using augmented assignment operators.

**Task 5: Membership operators**

Given the list below, check whether `"Docker"` and `"Jenkins"` are present.

```python
tools = ["Linux", "Python", "Docker", "Kubernetes"]
```

### 12. Sample Solution

```python
# Task 1: Arithmetic operators
print(25 + 15)
print(100 - 45)
print(12 * 8)
print(50 / 4)
print(50 // 4)
print(50 % 4)
print(2 ** 5)

# Task 2: Comparison operators
age = 21

print(age == 21)
print(age > 18)
print(age < 18)
print(age >= 21)

# Task 3: Logical operators
age = 25
has_license = True

can_drive = age >= 18 and has_license
print("Can drive:", can_drive)

# Task 4: Assignment shortcuts
balance = 100

balance += 50
balance -= 20
balance *= 2

print("Final balance:", balance)

# Task 5: Membership operators
tools = ["Linux", "Python", "Docker", "Kubernetes"]

print("Docker" in tools)
print("Jenkins" in tools)
```

### Summary

In this lesson, you learned:

- Arithmetic operators perform calculations.
- Comparison operators return `True` or `False`.
- Logical operators combine or reverse conditions.
- Assignment shortcuts update variable values.
- Membership operators check whether a value exists in a sequence.
- Identity operators check whether two references point to the same object.
- Operator precedence determines the order of calculations.

### What's Next?

Continue with **Working with Strings in Python** to explore text operations, string methods, formatting, and ways to manipulate text in your programs.
