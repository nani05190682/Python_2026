# Defining Functions in Python
## Create Your Own Reusable Functions

### 1. What Is a Function?

A **function** is a named, reusable block of code that performs a specific task. You define a function once and call it whenever you need that task to be performed.

Imagine you are writing a server monitoring script. Instead of writing the same health-check code several times, you can put that code inside a function and reuse it whenever required.

Functions help you write code that is organized, readable, maintainable, and reusable.

### 2. Your First Function

Let's create a simple function that displays a welcome message.

```python
def greet():
    print("Hello, world!")
    print("Welcome to Python!")

# Call the function
greet()
```

**Output:**

```text
Hello, world!
Welcome to Python!
```

Let's understand the code:

- `def` is the keyword used to define a function.
- `greet` is the function name.
- `()` contains the parameters, if any.
- `:` marks the beginning of the function body.
- The indented statements form the function body.
- `greet()` calls the function and executes its code.

**Important:** Defining a function does not execute its body. The body executes when you call the function.

### 3. Understanding Function Syntax

Every basic function follows this pattern:

```python
def function_name():
    # Function body
    statement
```

For example:

```python
def display_message():
    print("Learning Python functions!")

display_message()
```

**Output:**

```text
Learning Python functions!
```

You can also use `pass` when you want to define a function temporarily without implementing its logic.

```python
def future_task():
    pass
```

The `pass` statement does nothing. It allows Python to accept an otherwise empty function body while you develop the program.

### 4. Naming Functions

Python function names should clearly describe what the function does.

A common naming convention is **snake_case**: use lowercase letters and separate words with underscores.

#### Good function names

```python
def calculate_total():
    pass

def send_email():
    pass

def validate_password():
    pass

def check_server_status():
    pass
```

These names make the purpose of each function easy to understand.

#### Poor function names

```python
def func1():
    pass

def Calculate():
    pass

def x():
    pass
```

These names are either unclear or inconsistent with standard Python naming conventions.

**Function naming best practices:**

1. Use descriptive names.
2. Start names with a lowercase letter.
3. Separate words with underscores.
4. Prefer action-oriented names, such as `calculate_price()` or `restart_service()`.
5. Avoid Python keywords such as `if`, `for`, and `class` as function names.

### 5. Calling Functions

After defining a function, you can call it as many times as needed.

```python
def say_goodbye():
    print("Goodbye!")
    print("See you later!")

say_goodbye()
say_goodbye()
say_goodbye()
```

**Output:**

```text
Goodbye!
See you later!
Goodbye!
See you later!
Goodbye!
See you later!
```

Notice that you wrote the two `print()` statements only once but executed them three times.

This demonstrates the main benefit of functions: **write once, reuse many times.**

A function call requires parentheses:

```python
say_goodbye()
```

Writing only `say_goodbye` refers to the function object; it does not call the function.

### 6. Functions Can Contain Logic

A function can contain almost any valid Python statement, including variables, conditions, loops, and calls to other functions.

For example, let's create a function that checks the weather.

```python
def check_weather():
    temperature = 25

    if temperature > 30:
        print("It's hot!")
    else:
        print("Nice weather!")

check_weather()
```

**Output:**

```text
Nice weather!
```

The function creates a variable called `temperature`, checks its value, and prints a message based on the condition.

Let's modify the example:

```python
def check_weather():
    temperature = 35

    if temperature > 30:
        print("It's hot!")
    else:
        print("Nice weather!")

check_weather()
```

**Output:**

```text
It's hot!
```

The function's behavior changes because the temperature value changes.

In the next lesson, you'll learn how to provide such values as inputs instead of hardcoding them inside the function.

### 7. Understanding Variable Scope

**Variable scope** determines where a variable can be accessed in a Python program.

Two important concepts are local variables and global variables.

#### Local variables

A local variable is created inside a function and is normally accessible only within that function.

```python
def calculate_price():
    price = 100
    tax = price * 0.10

    print(f"Total: {price + tax}")

calculate_price()
```

**Output:**

```text
Total: 110.0
```

Here, `price` and `tax` are local variables.

If you try to access `price` outside the function, Python raises a `NameError` because no variable named `price` exists in that outer scope.

```python
def calculate_price():
    price = 100
    print(price)

calculate_price()

print(price)  # Raises NameError
```

The error occurs on the final line, not inside the function.

**Remember:** A local variable created during a function call is not automatically available outside that function.

#### Global variables

A global variable is defined outside functions, usually at the module level.

```python
discount_rate = 0.15

def apply_discount():
    price = 100
    discount = price * discount_rate
    final_price = price - discount

    print(final_price)

apply_discount()
```

**Output:**

```text
85.0
```

The function can read `discount_rate` because it is defined in the global scope.

However, using a global variable for input makes a function less flexible. A better approach is to pass the price and discount rate as parameters, which you'll learn in the next lesson.

### 8. Modifying Global Variables

If you need to reassign a global variable inside a function, Python provides the `global` keyword.

```python
counter = 0

def increment():
    global counter
    counter += 1

increment()
increment()

print(counter)
```

**Output:**

```text
2
```

The statement `global counter` tells Python that assignments to `counter` inside the function should refer to the module-level variable.

Without the `global` declaration, an assignment such as `counter += 1` would normally treat `counter` as a local variable and raise an `UnboundLocalError` because Python tries to read its local value before it has been assigned.

Although `global` is useful in certain situations, avoid relying on it unnecessarily. Excessive use of global state makes programs harder to test, understand, and debug.

### 9. Best Practice: Use Parameters and Return Values

Instead of changing a global variable, pass the required data into a function and return the result.

#### Less flexible approach: Using a global variable

```python
total = 0

def add_to_total(amount):
    global total
    total += amount

add_to_total(10)
add_to_total(20)

print(total)
```

**Output:**

```text
30
```

This works, but the function depends on external state.

#### Better approach: Returning a result

```python
def add_amounts(current_total, amount):
    return current_total + amount

total = 0

total = add_amounts(total, 10)
total = add_amounts(total, 20)

print(total)
```

**Output:**

```text
30
```

This version is easier to reuse because the function receives its inputs and returns its result.

You'll explore the details of parameters, arguments, and `return` in upcoming lessons.

### 10. Local Variables and Global Variables with the Same Name

A local variable can have the same name as a global variable. Inside the function, the local variable takes precedence when Python resolves that name.

This is called **shadowing**.

```python
name = "Global"

def show_name():
    name = "Local"
    print(name)

show_name()
print(name)
```

**Output:**

```text
Local
Global
```

Inside `show_name()`, Python uses the local variable `name`. Outside the function, the global variable remains unchanged.

### 11. Common Mistakes

#### Mistake 1: Forgetting parentheses when calling a function

Incorrect:

```python
def greet():
    print("Hello!")

greet
```

This does not execute the function.

Correct:

```python
greet()
```

Output:

```text
Hello!
```

#### Mistake 2: Forgetting the colon

Incorrect:

```python
def greet()
    print("Hello!")
```

Python raises a `SyntaxError`.

Correct:

```python
def greet():
    print("Hello!")
```

#### Mistake 3: Incorrect indentation

Incorrect:

```python
def greet():
print("Hello!")
```

Python raises an `IndentationError`.

Correct:

```python
def greet():
    print("Hello!")
```

Python uses indentation to identify the function body. Four spaces per indentation level is the standard convention.

#### Mistake 4: Expecting a function to run when defined

```python
def greet():
    print("Hello!")
```

Nothing is printed because the function has only been defined.

To execute it, call it:

```python
greet()
```

#### Mistake 5: Accessing a local variable outside its function

```python
def show_number():
    number = 10

show_number()
print(number)
```

This raises `NameError` because `number` is local to `show_number()`.

If you need to use the value outside the function, you can return it.

```python
def show_number():
    number = 10
    return number

result = show_number()
print(result)
```

**Output:**

```text
10
```

### 12. Practice Exercises

Try these exercises before checking the solutions.

**Exercise 1: Create your first function**

Create a function called `welcome()` that prints:

```text
Welcome to Python programming!
```

Call the function twice.

**Exercise 2: Display your details**

Create a function called `display_details()` that prints your name, role, and favorite programming language.

**Exercise 3: Add conditional logic**

Create a function called `check_temperature()` that defines a temperature variable. If the temperature is greater than `30`, print `"It's hot!"`; otherwise, print `"Nice weather!"`.

**Exercise 4: Understand local scope**

Create a function called `calculate_total()` that defines `price = 500` and `tax = 50`. Print the total inside the function. Then consider what happens if you try to print `price` outside the function.

**Exercise 5: Avoid global variables**

Create a function called `add_numbers()` that accepts no inputs for now and prints the result of adding two numbers stored inside the function.

**Exercise 6: DevOps practical example**

Create a function called `check_service()` that prints:

```text
Checking service status...
Service is running.
```

Call the function three times.

### 13. Sample Solutions

#### Solution 1

```python
def welcome():
    print("Welcome to Python programming!")

welcome()
welcome()
```

#### Solution 2

```python
def display_details():
    print("Name: Ravi")
    print("Role: DevOps Engineer")
    print("Favorite language: Python")

display_details()
```

#### Solution 3

```python
def check_temperature():
    temperature = 35

    if temperature > 30:
        print("It's hot!")
    else:
        print("Nice weather!")

check_temperature()
```

Output:

```text
It's hot!
```

#### Solution 4

```python
def calculate_total():
    price = 500
    tax = 50

    print(f"Total: {price + tax}")

calculate_total()
```

Output:

```text
Total: 550
```

The local variable `price` is not available outside the function.

#### Solution 5

```python
def add_numbers():
    a = 10
    b = 20

    print(a + b)

add_numbers()
```

Output:

```text
30
```

#### Solution 6

```python
def check_service():
    print("Checking service status...")
    print("Service is running.")

check_service()
check_service()
check_service()
```

This example demonstrates code reuse. In a real monitoring system, the function would need to check the actual service rather than always print that it is running.

### 14. Quick Summary

| Concept | Meaning |
|---|---|
| `def` | Defines a function |
| `function_name()` | Calls a function |
| Indentation | Defines the function body |
| Local variable | A variable defined inside a function |
| Global variable | A variable defined outside functions |
| `global` | Declares that a function will reassign a global variable |
| `return` | Sends a result back to the caller |
| `pass` | Placeholder for a function body that is not implemented yet |

**Key takeaway:** Functions allow you to write reusable, organized code. Learn to define and call functions first, then use parameters and return values to make them flexible and easy to test.

### What's Next?

**Function Parameters and Arguments — Pass Data into Functions**

You'll learn how to provide input to a function, work with multiple parameters, and reuse the same function with different values.
