# Python Return Values
## Get Results Back from Your Functions

### 1. What Are Return Values?

So far, you've learned how to create functions, pass data through parameters, and display results using `print()`.

But what if you want to calculate something inside a function and use the result somewhere else in your program?

That's where **return values** become important.

A return value is the result that a function sends back to the code that called it.

Think of a calculator: you enter two numbers, perform an operation, and receive a result that you can use again.

### 2. `print()` vs. `return`

Let's compare two functions that add numbers.

#### Function that prints a result

```python
def add_print(a, b):
    print(a + b)

add_print(5, 3)
```

**Output:**

```text
8
```

This function displays the result, but it does not explicitly return it.

#### Function that returns a result

```python
def add_return(a, b):
    return a + b

result = add_return(5, 3)

print(result)
```

**Output:**

```text
8
```

Both examples display `8`, but their behavior is different.

In the second example, `add_return()` sends the value `8` back to the caller. Python assigns that value to the variable `result`.

**Remember:**

- `print()` displays information on the screen.
- `return` sends a value back to the caller so that the program can use it.

### 3. Understanding the `return` Statement

The `return` statement ends the current function call and sends a value back to the caller.

Syntax:

```python
def function_name(parameters):
    # Perform an operation
    return value
```

Let's calculate the area of a rectangle.

```python
def calculate_area(width, height):
    area = width * height
    return area

room_area = calculate_area(10, 12)

print(f"Room size: {room_area} sq ft")
```

**Output:**

```text
Room size: 120 sq ft
```

Let's understand what happens:

1. Python calls `calculate_area(10, 12)`.
2. `width` receives `10`, and `height` receives `12`.
3. Python calculates `10 * 12`, producing `120`.
4. `return area` sends `120` back to the caller.
5. The variable `room_area` receives `120`.
6. `print()` displays the result.

This is useful when the result must be stored, processed, or passed to another function.

### 4. What Happens After `return`?

When Python executes a `return` statement, the function immediately exits. Statements following that return in the same execution path are not executed.

Example:

```python
def check_number():
    print("Checking number...")
    return 100
    print("This line will not execute")

result = check_number()
print(result)
```

**Output:**

```text
Checking number...
100
```

The second `print()` inside the function is never executed because the function has already returned.

**Important:** A function can contain multiple `return` statements in different branches, but only the one reached during a particular call is executed.

### 5. Using Returned Values

Returned values can be used in many ways.

#### A. Store the result in a variable

```python
def double(number):
    return number * 2

result = double(5)

print(result)
```

**Output:**

```text
10
```

#### B. Use the result in an expression

```python
def double(number):
    return number * 2

total = double(5) + double(3)

print(total)
```

**Output:**

```text
16
```

Python calculates `10 + 6`, producing `16`.

#### C. Pass the result to another function

```python
def double(number):
    return number * 2

print(double(10))
```

**Output:**

```text
20
```

Here, the value returned by `double()` becomes the argument passed to `print()`.

#### D. Use the result in a condition

```python
def double(number):
    return number * 2

if double(7) > 10:
    print("Big number!")
else:
    print("Small number!")
```

**Output:**

```text
Big number!
```

The function returns `14`, and the condition evaluates to `True`.

### 6. Returning Multiple Values

Python allows a function to return multiple values in one statement. In practice, Python packages those values into a tuple.

Example:

```python
def get_min_max(numbers):
    return min(numbers), max(numbers)

minimum, maximum = get_min_max([5, 2, 8, 1, 9])

print(f"Min: {minimum}, Max: {maximum}")
```

**Output:**

```text
Min: 1, Max: 9
```

The statement:

```python
return min(numbers), max(numbers)
```

returns a tuple equivalent to:

```python
(1, 9)
```

You can also store the entire returned tuple in a single variable.

```python
def get_min_max(numbers):
    return min(numbers), max(numbers)

result = get_min_max([5, 2, 8, 1, 9])

print(result)
print(type(result))
```

**Output:**

```text
(1, 9)
<class 'tuple'>
```

This technique is useful when a function needs to provide several related results.

### 7. Returning Different Values with Conditions

A function can return different values depending on its input.

Example:

```python
def check_temperature(temperature):
    if temperature > 30:
        return "Hot"
    elif temperature >= 20:
        return "Pleasant"
    else:
        return "Cold"

print(check_temperature(35))
print(check_temperature(25))
print(check_temperature(15))
```

**Output:**

```text
Hot
Pleasant
Cold
```

Each call returns a string based on the temperature.

Notice that you do not need an `else` after the final `return`. Once a return statement executes, that function call ends.

### 8. Understanding `return` vs. `print()` in Detail

This is one of the most important concepts to understand when learning functions.

Consider these two functions:

```python
def get_greeting_print(name):
    print(f"Hello, {name}!")

def get_greeting_return(name):
    return f"Hello, {name}!"
```

The first function displays a greeting. The second returns a greeting as a string.

#### Using the function that prints

```python
message = get_greeting_print("Alice")

print(message)
```

**Output:**

```text
Hello, Alice!
None
```

Why does this happen?

1. `get_greeting_print("Alice")` prints `Hello, Alice!`.
2. The function does not explicitly return a value.
3. Python automatically returns `None`.
4. Therefore, `message` receives `None`.
5. `print(message)` displays `None`.

#### Using the function that returns

```python
message = get_greeting_return("Alice")

print(message)
print(message.upper())
```

**Output:**

```text
Hello, Alice!
HELLO, ALICE!
```

The function returns a string, so you can store it, transform it, or pass it to another function.

**Rule of thumb:** Use `print()` when you want to display something. Use `return` when you want to give a result back to the calling code.

### 9. Functions Without an Explicit `return`

If a function finishes without executing a `return` statement, Python automatically returns `None`.

Example:

```python
def greet(name):
    print(f"Hello, {name}!")

result = greet("Alice")

print(result)
```

**Output:**

```text
Hello, Alice!
None
```

Python prints the greeting and then assigns `None` to `result`.

A function can also explicitly return `None`:

```python
def do_nothing():
    return None

result = do_nothing()

print(result)
```

**Output:**

```text
None
```

This behavior is useful to understand when testing functions or working with functions that primarily perform actions rather than calculate results.

### 10. Practical DevOps Example: Calculate Disk Usage

Let's create a function that calculates the percentage of disk space used.

```python
def calculate_disk_usage(used_gb, total_gb):
    if total_gb <= 0:
        return None

    return (used_gb / total_gb) * 100

usage = calculate_disk_usage(75, 100)

if usage is not None:
    print(f"Disk usage: {usage:.1f}%")
else:
    print("Invalid disk capacity")
```

**Output:**

```text
Disk usage: 75.0%
```

The function returns `None` if the total capacity is zero or negative, preventing division by zero and indicating invalid input.

In a real monitoring application, the function could be used with disk metrics collected from a server.

### 11. Common Mistakes

#### Mistake 1: Forgetting to return a result

Incorrect:

```python
def add_numbers(a, b):
    result = a + b

total = add_numbers(10, 20)

print(total)
```

**Output:**

```text
None
```

The function calculates the result but does not return it.

Correct:

```python
def add_numbers(a, b):
    result = a + b
    return result

total = add_numbers(10, 20)

print(total)
```

**Output:**

```text
30
```

#### Mistake 2: Writing code after `return`

```python
def calculate():
    return 100
    print("Calculation complete")

calculate()
```

The message is never printed because the function exits at `return 100`.

Correct:

```python
def calculate():
    print("Calculation complete")
    return 100

result = calculate()
print(result)
```

**Output:**

```text
Calculation complete
100
```

#### Mistake 3: Confusing printing with returning

Incorrect:

```python
def square(number):
    print(number * number)

result = square(4)

print(result + 10)
```

This raises a `TypeError` because `square()` returns `None`, and Python cannot add `10` to `None`.

Correct:

```python
def square(number):
    return number * number

result = square(4)

print(result + 10)
```

**Output:**

```text
26
```

#### Mistake 4: Returning before completing a calculation

Incorrect:

```python
def calculate_total(price, tax):
    return price
    return price + tax

print(calculate_total(100, 10))
```

Output:

```text
100
```

The second `return` is never reached.

Correct:

```python
def calculate_total(price, tax):
    return price + tax

print(calculate_total(100, 10))
```

**Output:**

```text
110
```

### 12. Practice Exercises

Try these exercises before looking at the sample solutions.

**Exercise 1: Add two numbers**

Create a function called `add_numbers(a, b)` that returns the sum of two numbers. Store the returned result in a variable and print it.

**Exercise 2: Calculate the square**

Create a function called `square(number)` that returns the square of a number.

**Exercise 3: Calculate the rectangle area**

Create a function called `calculate_area(width, height)` that returns the area of a rectangle.

**Exercise 4: Check whether a number is even**

Create a function called `is_even(number)` that returns `True` if a number is even and `False` otherwise.

**Exercise 5: Return multiple values**

Create a function called `get_min_max(numbers)` that returns the minimum and maximum values from a list. Unpack the returned values into two variables.

**Exercise 6: DevOps practical exercise**

Create a function called `calculate_cpu_usage(idle_percentage)` that returns CPU usage as a percentage.

For this exercise, assume:

`CPU usage = 100 - idle percentage`

Call the function with an idle percentage of `25` and print the result.

### 13. Sample Solutions

#### Solution 1: Add two numbers

```python
def add_numbers(a, b):
    return a + b

result = add_numbers(10, 20)

print(result)
```

Output:

```text
30
```

#### Solution 2: Calculate the square

```python
def square(number):
    return number ** 2

print(square(5))
```

Output:

```text
25
```

#### Solution 3: Calculate the rectangle area

```python
def calculate_area(width, height):
    return width * height

area = calculate_area(10, 12)

print(area)
```

Output:

```text
120
```

#### Solution 4: Check whether a number is even

```python
def is_even(number):
    return number % 2 == 0

print(is_even(10))
print(is_even(7))
```

Output:

```text
True
False
```

#### Solution 5: Return multiple values

```python
def get_min_max(numbers):
    return min(numbers), max(numbers)

minimum, maximum = get_min_max([5, 2, 8, 1, 9])

print("Minimum:", minimum)
print("Maximum:", maximum)
```

Output:

```text
Minimum: 1
Maximum: 9
```

#### Solution 6: Calculate CPU usage

```python
def calculate_cpu_usage(idle_percentage):
    return 100 - idle_percentage

usage = calculate_cpu_usage(25)

print(f"CPU usage: {usage}%")
```

Output:

```text
CPU usage: 75%
```

### 14. Quick Summary

| Concept | Meaning |
|---|---|
| `return value` | Sends a result back to the caller |
| `print(value)` | Displays a value on the screen |
| `return` | Immediately ends the current function call |
| No explicit `return` | Python returns `None` |
| Multiple returned values | Commonly returned together as a tuple |
| Returned result in a variable | `result = calculate()` |
| Returned result in a condition | `if calculate() > 10:` |

**Key takeaway:** The `return` statement makes functions useful beyond displaying output. It allows you to calculate results, store them, combine them with other operations, and build larger programs from smaller reusable components.

### What's Next?

**Python Modules and Libraries — Extend Python with Reusable Code**

You'll learn how to import built-in modules, use functions written by other developers, and organize your own code into reusable Python files.
