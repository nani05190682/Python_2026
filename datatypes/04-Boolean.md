# Booleans in Python
## True and False Values for Decisions

### 1. What Are Booleans?

A **Boolean** is a data type that represents one of two possible values: `True` or `False`.

Think of Booleans as answers to yes-or-no questions.

For example:
- Is the user logged in?
- Is the server running?
- Does the user have administrator access?
- Has the student passed the exam?

Python represents these answers using Boolean values.

```python
is_logged_in = True
is_admin = False
has_permission = True

print(is_logged_in)
print(is_admin)
print(has_permission)
```

Output:

```text
True
False
True
```

The Boolean data type is called `bool`.

```python
print(type(True))
print(type(False))
```

Output:

```text
<class 'bool'>
<class 'bool'>
```

**Important:** Python is case-sensitive. Always write `True` and `False` with capital `T` and `F`. Writing `true` or `false` without defining them as variables causes a `NameError`.

### 2. Creating Boolean Values

You can create Boolean variables in two main ways.

#### A. Assigning a Boolean directly

You can assign `True` or `False` to a variable.

```python
is_ready = True
is_server_running = False
is_maintenance_mode = True

print(is_ready)
print(is_server_running)
print(is_maintenance_mode)
```

Output:

```text
True
False
True
```

#### B. Creating Booleans using comparisons

Python comparisons evaluate whether a condition is true or false.

```python
age = 18
can_vote = age >= 18

print(can_vote)
```

Output:

```text
True
```

Python checks whether `age` is greater than or equal to `18`. Since the condition is satisfied, the result is `True`.

Another example:

```python
score = 45
passed = score >= 60

print(passed)
```

Output:

```text
False
```

The score is below `60`, so the comparison returns `False`.

### 3. Comparison Operators

Comparison operators compare two values and return a Boolean result.

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `==` | Equal to | `10 == 10` | `True` |
| `!=` | Not equal to | `10 != 5` | `True` |
| `>` | Greater than | `10 > 5` | `True` |
| `<` | Less than | `5 < 10` | `True` |
| `>=` | Greater than or equal to | `10 >= 10` | `True` |
| `<=` | Less than or equal to | `5 <= 10` | `True` |

Let's explore these operators with a Python program.

```python
age = 25

print(age == 25)  # Equal to
print(age != 30)  # Not equal to
print(age > 20)   # Greater than
print(age < 30)   # Less than
print(age >= 25)  # Greater than or equal to
print(age <= 25)  # Less than or equal to
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

Try changing the value of `age` and observe how the results change.

### 4. The Difference Between `=` and `==`

This is one of the most important concepts to understand in Python.

**The `=` operator assigns a value. The `==` operator compares two values.**

Example:

```python
age = 25
```

Here, `=` assigns the value `25` to the variable `age`.

Now consider:

```python
age = 25
print(age == 25)
```

Output:

```text
True
```

Here, `==` checks whether the value of `age` is equal to `25`.

Another example:

```python
password_correct = False

print(password_correct == True)
```

Output:

```text
False
```

The variable contains `False`, so it is not equal to `True`.

A simpler and more Pythonic approach is to use the Boolean variable directly:

```python
password_correct = False

if password_correct:
    print("Access granted")
else:
    print("Access denied")
```

Output:

```text
Access denied
```

You will learn more about `if` and `else` statements in a later lesson.

### 5. Using Booleans in Real-World Applications

Booleans are essential for making decisions in programs.

#### Example 1: Checking a user's age

```python
age = 20
is_adult = age >= 18

print("Is the user an adult?", is_adult)
```

Output:

```text
Is the user an adult? True
```

#### Example 2: Checking whether a student passed

```python
score = 85
passed = score >= 60

print("Did the student pass?", passed)
```

Output:

```text
Did the student pass? True
```

#### Example 3: Checking server availability

In an SRE or DevOps environment, a Boolean can represent whether a health check succeeded.

```python
server_healthy = True

print("Server healthy:", server_healthy)
```

Output:

```text
Server healthy: True
```

A monitoring application could use this value to decide whether to report a healthy or unhealthy state. In a real monitoring system, the Boolean would usually be derived from an actual health check rather than manually assigned.

### 6. Combining Boolean Conditions

Python provides logical operators that let you combine or reverse Boolean conditions.

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `and` | True when both conditions are true | `True and False` | `False` |
| `or` | True when at least one condition is true | `True or False` | `True` |
| `not` | Reverses a Boolean value | `not True` | `False` |

Example:

```python
age = 25
has_id = True

can_enter = age >= 18 and has_id

print(can_enter)
```

Output:

```text
True
```

Both conditions are true: the person is at least 18 and has identification.

Another example:

```python
is_weekend = False
is_holiday = True

day_off = is_weekend or is_holiday

print(day_off)
```

Output:

```text
True
```

At least one condition is true, so `day_off` is `True`.

To reverse a Boolean value, use `not`.

```python
server_running = True

print(not server_running)
```

Output:

```text
False
```

### 7. Common Mistakes

**Mistake 1: Incorrect capitalization**

Incorrect:

```python
is_active = true
```

Python raises a `NameError` if `true` has not been defined.

Correct:

```python
is_active = True
```

**Mistake 2: Using `=` instead of `==` in a comparison**

Incorrect:

```python
age = 18

# if age = 18:
#     print("Eligible")
```

Assignment with `=` cannot be used as the condition in an ordinary `if` statement. Uncommenting the code above causes a `SyntaxError`.

Correct:

```python
age = 18

if age == 18:
    print("The age is 18")
```

Output:

```text
The age is 18
```

**Mistake 3: Comparing a Boolean unnecessarily**

Instead of writing:

```python
is_active = True

if is_active == True:
    print("Account is active")
```

Prefer:

```python
is_active = True

if is_active:
    print("Account is active")
```

The second version is simpler and easier to read.

### 8. Practice Exercise

Create a file named `booleans_practice.py` and complete the following tasks.

**Task 1: Create Boolean variables**

Create variables representing:

- Whether a user is logged in.
- Whether a server is running.
- Whether a student has passed an exam.

Print their values and data types.

**Task 2: Use comparison operators**

Set `age = 25` and print the results of these comparisons:

- Is the age equal to `25`?
- Is the age different from `30`?
- Is the age greater than `18`?
- Is the age less than or equal to `25`?

**Task 3: Check exam results**

Set `score = 72`. Create a Boolean variable named `passed` that checks whether the score is at least `60`.

Print the result.

**Task 4: Combine conditions**

Create two variables:

```python
has_valid_credentials = True
account_enabled = True
```

Create a variable named `can_login` that is `True` only when both conditions are true.

**Task 5: Check server status**

Create a Boolean variable named `server_healthy`. Print its opposite using the `not` operator.

### 9. Sample Solution

```python
# Task 1: Boolean variables
is_logged_in = True
server_running = True
student_passed = False

print(is_logged_in, type(is_logged_in))
print(server_running, type(server_running))
print(student_passed, type(student_passed))

# Task 2: Comparison operators
age = 25

print(age == 25)
print(age != 30)
print(age > 18)
print(age <= 25)

# Task 3: Exam results
score = 72
passed = score >= 60

print("Passed:", passed)

# Task 4: Combine conditions
has_valid_credentials = True
account_enabled = True

can_login = has_valid_credentials and account_enabled

print("Can login:", can_login)

# Task 5: Reverse a Boolean
server_healthy = True

print("Server unhealthy:", not server_healthy)
```

### 10. Summary

In this lesson, you learned:

- Booleans represent `True` and `False`.
- The `bool` data type stores Boolean values.
- Comparison operators evaluate conditions and return Boolean results.
- `=` assigns a value, while `==` compares values.
- `and`, `or`, and `not` combine or reverse Boolean conditions.
- Booleans are used in applications, automation, monitoring, and decision-making.

### What's Next?

Now that you understand Python's fundamental data types, let's explore **Operators in Python** — mathematical operations, comparisons, logical operators, and how to combine them to build useful programs.
